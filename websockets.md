---

copyright:
  years: 2015, 2017
lastupdated: "2017-09-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Using the WebSocket interface
{: #using}

To synthesize text to speech with the service's WebSocket interface, you first establish a connection with the service by calling its `synthesize` method. You then send the text to be synthesized to the service as a JSON text message over the connection.
{: shortdesc}

The WebSocket interface accepts identical input and produces identical results as the `synthesize` method of the HTTP interface. However, the WebSocket interface supports use of the SSML `<mark>` element to identify the location of user-specified markers in the audio, and it allows you to obtain word timing information in the audio for all strings in the input text.

## Synthesizing text to audio
{: #synthesize}

The synthesize request and response cycle includes the following steps:

1.  [Opening a connection](#WSopen)
1.  [Sending text](#WSsend)
1.  [Receiving a response](#WSreceive)

### Opening a connection
{: #WSopen}

The service makes the `synthesize` method for the WebSocket Secure (WSS) protocol available at the following endpoint:

```
wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize
```
{: screen}

A WebSocket client calls this method with the following query parameters to establish an authenticated connection with the service.

<table>
  <caption>Table 1. Parameters of the <code>synthesize</code>
    method</caption>
  <tr>
    <th style="text-align:left; width:23%">Parameter</th>
    <th style="text-align:center; width:12%">Data type</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>watson-token</code><br/><em>Optional</em></td>
    <td style="text-align:center">String</td>
    <td>
      Passes a valid authentication token instead of passing the service
      credentials with the call. You can instead use the
      <code>X-Watson-Authorization-Token</code> header to pass the token,
      but you must pass a token in one of these two ways. For more
      information, see
      <a href="/docs/services/watson/getting-started-tokens.html">Tokens
        for authentication</a>.
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Optional</em></td>
    <td style="text-align:center">String</td>
    <td>
      Specifies the voice in which the text is to be spoken in the audio.
      Omit the parameter to use the default voice. For more information,
      see <a href="http.html#voices">Specifying a voice</a>.
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Optional</em></td>
    <td style="text-align:center">String</td>
    <td>
      Specifies the globally unique identifier (GUID) for a custom voice
      model that is to be used for the synthesis. A custom voice model is
      guaranteed to work only if it matches the language of the voice used
      for the synthesis. If you include a customization ID, you must call
      the method with the service credentials of the model's owner. Omit
      the parameter to use the specified voice with no customization. For
      more information, see <a herf="custom-intro.shtml">Understanding
        customization</a>.
    </td>
  </tr>
  <tr>
    <td><code>x-watson-learning-opt-out</code><br/><em>Optional</em></td>
    <td style="text-align:center">Boolean</td>
    <td>
      Specifies whether the service logs the request and results sent over
      the connection, which it does by default to improve the service for
      future users. Specify <code>true</code> or <code>1</code> to prevent
      the service from logging the data. You can also opt out of request
      logging by passing a value of <code>true</code> with the
      <code>X-Watson-Learning-Opt-Out</code> request header; for more
      information, see
      <a href="/docs/services/watson/getting-started-logging.html">Controlling
        request logging for Watson services</a>.
    </td>
  </tr>
</table>

The following snippet of JavaScript code opens a connection with the service. The call to the `synthesize` method passes the `voice` and `watson-token` query parameters, the former to direct the service to use the US English Allison voice. Once the connection is established, the event listeners (`onOpen`, `onClose`, and so on) are defined to respond to events from the service.

```javascript
var voice = 'en-US_AllisonVoice';
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?voice=' +
  voice + '&watson-token=' + token;
var websocket = new WebSocket(wsURI);
websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

### Sending text
{: #WSsend}

To synthesize text, the client passes a simple JSON text message to the service with the following parameters.

<table>
  <caption>Table 2. Parameters of the JSON text message</caption>
  <tr>
    <th style="text-align:left; width:23%">Parameter</th>
    <th style="text-align:center; width:12%">Data type</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>text</code><br/><em>Required</em></td>
    <td style="text-align:center">String</td>
    <td>
      Provides the text that is to be synthesized. The client can pass
      plain text or text that is annotated with the Speech Synthesis
      Markup Language (SSML), including the service-specific
      <code>&lt;express-as&gt;</code> and
      <code>&lt;voice-transformation&gt;</code> elements; for more
      information, see <a href="http.html#input">Specifying input
        text</a>. SSML input can also include the <code>&lt;mark&gt;</code>
      element; for more information, see <a href="#mark">Specifying
        an SSML mark</a>. The client can pass a maximum of 5 KB of
      data with the request.
    </td>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>Required</em></td>
    <td style="text-align:center">String</td>
    <td>
      Specifies the requested format (MIME type) of the audio. For
      detailed information about the available audio formats, see
      <a href="http.shtml">Specifying an audio format</a>. In addition
      to the supported specifications, the WebSocket interface lets you
      specify <code>*/*</code> to use the default audio format,
      <code>audio/ogg;codecs=opus</code>.
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>Optional</em></td>
    <td style="text-align:center">String[ ]</td>
    <td>
      A list that specifies whether the service is to return word
      timing information for all strings of the input text. Specify
      <code>words</code> to request word timing information; the start
      and end time of each word of the input is returned. Specify an
      empty list or omit the parameter to receive no word timing
      information. For more information, see
      <a href="#timing">Requesting word timings</a>. <em>Not supported
        for Japanese input text.</em>
    </td>
  </tr>
</table>

The following snippet of JavaScript code passes a simple "Hello world" message as the input text and requests the default MIME type for the audio. The calls are included in the `onOpen` function defined for the client to ensure that they are sent only after the connection is established.

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

The service responds to this message by sending a text message that confirms the MIME type of the audio response:

```javascript
{
  'binary_streams': [ { 'content_type': 'audio/ogg;codecs=opus' } ]
}
```
{: codeblock}

### Receiving a response
{: #WSreceive}

After it confirms the MIME type, the server sends the synthesized audio as a binary stream of data in the indicated format. If the input text includes one or more SSML `<mark>` tags, the service sends the location in the audio of each mark as a text message. The service can also send text messages with warnings or errors. When it finishes synthesizing the input text, the service automatically closes the WebSocket connection.

The client should append binary responses from the service to the audio results received over the connection. It can handle text messages by responding to them, displaying them, or capturing them for use by the application (for example, if they contain mark locations). The following simple example of an `onMessage` function appends text and binary messages received from the service to the appropriate variable depending on their type. When the `onClose()` function executes, the entire audio stream has been received.

```javascript
var messages;
var audioStream;

function onMessage(evt) {
  if (typeof evt.data === string) {
    messages += evt.data;
  } else {
    console.log('Received ' + evt.data.size() + ' binary bytes');
    audioStream += evt.data;
  }
}

function onClose(evt) {
  // The audio stream is complete.
}
```
{: codeblock}

## Specifying an SSML mark
{: #mark}

The WebSocket interface supports the optional SSML `<mark>` element. The element is an empty tag that places a marker into the text to be synthesized. The client is notified when all of the text that precedes the `<mark>` element has been synthesized. The tag is useful for synchronizing the audio and the input text, for example, to coordinate a robot's gestures with the content of the synthesized speech.

The element accepts a single `name` attribute that specifies a string that uniquely identifies the mark. The name must begin with an alphanumeric character. The service returns the name along with the time at which the mark occurs in the synthesized audio. The client can include any number of marks in the input text.

The following snippet of JavaScript code is the same as the earlier example but includes an instance of the `<mark>` tag with the name `here`:

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello <mark name="here"/> world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

When it has synthesized the text that precedes the mark, the service sends a text message that identifies the name of the mark and the time in seconds at which it occurs in the audio:

```javascript
{
  "marks": [
    ["here", 0.4019387755102041]
  ]
}
```
{: codeblock}

Note that the service multiplexes independent binary and text streams to construct its response. As a result, the service has very little control over the number of audio chunks it delivers and when the user receives the text and audio messages. For example, if the synthesis is quick but the compression of the audio takes longer, all text messages may arrive before any of the audio.

In practical terms, this means that the service can send an arbitrary number of audio chunks, including multiple chunks of audio before and after each mark. It is also possible for a single chunk to contain audio data that both precedes and follows a mark. However, the text message that contains the timing information for a mark always arrives before the audio chunk that contains the mark's location; the timing information for the mark indicates precisely where the mark occurs in the audio stream. Note also that the audio messages always arrive in order so that the user can construct an accurate audio synthesis of the text from the binary results.

## Requesting word timings
{: #timing}

You can use the `timings` parameter of the JSON object that you pass to the service to request word timing information for all strings of the input text. This convenience eliminates the need to specify the SSML `<mark>` element for each word of the input. Pass an array that includes the string `words` to request word timings; pass an empty array or omit the parameter to receive no timing information.

> **Note:** The `timings` field is not supported for use with Japanese input text.

The service returns word timings over the WebSocket connection in the same way that it returns timing information for individual words with `<mark>` element. It returns one or more JSON text messages, each of which contains an array of words and their start and end times in seconds from the beginning of the synthesized audio. For example, the following example requests word timing information:

```javascript
function onOpen(evt) {
  var message = {
    text: 'I have a pet bird.',
    accept: '*/*',
    timings: ['words']
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

In response, the service can return the following text messages:

```javascript
{
  "words": [
    ["I", [0.0690258394023930, 0.1655782733012873]]
    ["have", [0.1655789302434486, 0.3722901056092351]]
    ["a", [0.3722906798320199, 0.4012192331086645]]
  ]
}
{
  "words": [
    ["pet", [0.4012195492838347, 0.5798213856109801]]
    ["bird.", [0.5798218710823425, 0.7440360383928273]]
  ]
}
```
{: codeblock}

As described for the `<mark>` tag, because the service multiplexes independent binary and text streams to create its response, it has little control over the number of audio chunks it delivers and when the user receives text and audio messages. As a result, the service can send an arbitrary number of audio chunks and text messages. But the text message that contains the timing information for a word always arrives before the audio chunk that contains that word, and the audio messages always arrive in order.

### Timings for plain text
{: #timingText}

The service's synthesis process involves a text normalization step that spells out numbers, dates, times, monetary amounts, acronyms, and abbreviations. The results correspond to how such strings are spoken. For example, the string *$200* is spoken as three words: *two*, *hundred*, and *dollars*. Because word timing information is used to synchronize the audio with the input text, the service returns timing information that corresponds to the unnormalized spelling of the input.

For example, consider the following input text:

```
The coldest recorded temperature is -89.2 degrees Celsius in Antarctica on July 21, 1983!
```
{: screen}

The service returns audio timings for the following strings: "*The*", "*coldest*", "*recorded*", "*temperature*", "*is*", "*-89.2*", "*degrees*", "*Celsius*", "*in*", "*Antarctica*", "*on*", "*July*", "*21,*", "*1983!*" Although "*-89.2*" is spoken in the audio as five separate words (*minus*, *eighty*, *nine*, *point*, *two*), the text message provides timing information for the string as a single unit with the start time of *minus* and the end time of *two*.

As in the previous example, unnormalized strings can also contain punctuation. The service includes the punctuation that precedes or follows a word in the text message that it returns with the timings. For instance, the strings "*21,*" and "*1983!*" include punctuation that the service returns in its text message. Although the punctuation results in silence, the audio timing for the word does *not* include that silence.

For example, consider the following conditional statement as input text:

```
If it is sunny, I will go to the beach.
```
{: screen}

The service returns timing information for "*sunny,*" and for "*beach.*", both of which end in punctuation that produces silence. But the word timing information for "*sunny,*" does not include the silence that is produced by the comma, and the word timings for "*beach.*" do not include the silence for the period. The information reflects only the timing of the spoken strings.

### Timings for SSML text
{: #timingSSML}

When the service synthesizes plain text, it returns all input characters except for blankspaces as part of the word strings in its word timing response. The same is not true of SSML, however, since some SSML tags do not generate audio. The following list summarizes the SSML tags that can impact word timing information:

-   `<say-as>`: Indicates how the text that is enclosed between the opening and closing `<say-as>` tags is to be handled in the normalization step, with additional attributes specifying how the embedded text is to be spoken. The following example indicates how the date is to be spoken:

    ```xml
    The baby was born on <say-as interpret-as="date" format="mdy">3/4/2016</say-as>.
    ```
    {: codeblock}

    The service returns word timing information for the following strings: "*The*", "*baby*", "*was*", "*born*", "*on*", "*3/4/2016.*" The service normalizes the string "*3/4/2016*" as "*march fourth two thousand sixteen*", and the word timing information for the string reflects the start time of "*march*" and the end time of "*sixteen*".

    The following example indicates that the word `Hello` is to be spelled out:

    ```xml
    <say-as intepret-as="letters">Hello</say-as>.
    ```
    {: codeblock}

    The service returns word timing information for the string "*Hello*". The service spells the word letter-by-letter during the normalization step, and the word timing information in the response reflects the start time of the letter "*h*" and the end time of the letter "*o*".
-   `<phoneme>`: Provides a pronunciation for the text enclosed in the opening and closing `<phoneme>` tags, though both the text and the closing tag are optional. The following example includes embedded text and a closing tag:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme> was ripe.
    ```
    {: codeblock}

    The service returns word timing information for the following strings: "*The*", "*tomato*", "*was*", "*ripe.*"

    Conversely, the following example provides a unary `<phoneme>` tag with no embedded text and no closing tag:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo"/> was ripe.
    ```
    {: codeblock}

    In this case, the service returns word timings for the following strings: "*The*", "*&lt;phoneme&gt;*", "*was*", "*ripe.*"
-   `<sub>`: Substitutes the text included in the tag's `alias` attribute for the text enclosed between the opening and closing `<sub>` tags in the spoken audio. For example, the input text

    ```xml
    I work at <sub alias="International Business Machines">IBM</sub>.
    ```
    {: codeblock}

    produces word timing information for the following strings: "*I*", "*work*", "*at*", "*{{site.data.keyword.IBM_notm}}.*". The service normalizes the string "*{{site.data.keyword.IBM_notm}}*" as "*International Business Machines*", and the word timing information for the string reflects the start time of "*International*" and the end time of "*Machines*".
-   `<break>`: Inserts a pause in the spoken text. The service reflects the resulting silence in the word timings as a gap between the end time of the word that precedes the `<break>` tag and the word that follows the tag.
- `<paragraph>`: Can add silence to the audio. The service does not return word timing information for the silence.
- `<sentence>`: Can add silence to the audio. The service does not return word timing information for the silence.

SSML elements not mentioned in the list do not impact word timing information. For more information about the service's support for SSML, see [Using SSML](/docs/services/text-to-speech/SSML.html).

## WebSocket return codes
{: #returnCodes}

The service can send the following return codes to the client over the WebSocket connection:

-   `1000` indicates normal closure of the connection, meaning that the purpose for which the connection was established has been fulfilled.
-   `1002` indicates that the service is closing the connection due to a protocol error.
-   `1006` indicates that the connection was closed abnormally.
-   `1009` indicates that the frame size exceeded the 4 MB limit.
-   `1011` indicates that the service is terminating the connection because it encountered an unexpected condition that prevents it from fulfilling the request, such as an invalid argument. The return code can also indicate that the input text was too large; the text cannot exceed 5 KB in size.

If the socket closes with an error, the service sends the client an informative message of the form `{"error": "Specific error message"}` before closing. The service can also send warning messages for unknown parameters.

In the following examples, the first response is a JSON text message from the service and, where included, the second message is a formatted message from the client's `onClose` callback method. In the first two examples, the second message begins with the boolean `true` because the connection is closed, followed by the WebSocket error code that caused the closure. The third example does not include the second message because the connection is not closed by the warning.

-   *Example 1* shows the error messages for an invalid argument for the `accept` parameter:

    ```javascript
    {
      "error": "Unsupported mimetype.  Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   *Example 2* shows the error messages for a missing `text` parameter:

    ```javascript
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   *Example 3* shows a warning message for an unknown parameter named `invalid-parameter`:

    ```javascript
    {
      "warnings": "Unknown arguments: invalid-parameter."
    }
    ```
    {: codeblock}

For more information about WebSocket return codes, see the Internet Engineering Task Force (IETF) [Request for Comments (RFC) 6455 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://tools.ietf.org/html/rfc6455){: new_window}.

## Example Python code
{: #python}

The following brief example Python code defines a class that sends a simple message with a single `<mark>` tag to the service over a WebSocket connection. The code defines callback methods to handle state changes and responses in the connection; the Python callback methods differ slightly from the JavaScript event handlers shown previously. All methods log suitable messages to the console.

-   The `onConnect` method fires when the service accepts the connection but before the handshake is completed.
-   The `onOpen` method fires when the handshake between the client and service is complete and the connection is fully established. The method sends a JSON text message that specifies the text to be synthesized and the requested MIME type of the response.
-   The `onMessage` method fires when the service sends a response. The method appends a binary response to the audio received from the service and a text message to the list of messages received from the service.
-   The `onClose` method fires when the connection is closed. It reports the closing of the socket. The `wasClean` argument is a boolean that indicates whether the connection was closed as a result of the service sending a close frame, as opposed to a network or protocol error. The `code` and `reason` arguments provide the WebSocket return code and its accompanying message. For example return codes and messages, see [WebSocket return codes](#returnCodes).

```python
class TTSWSClientProtocol(WebSocketClientProtocol):

  def __init__(self):
    WebSocketClientProtocol.__init__(self)
    self.msgs = []
    self.binaryBytesReceived = 0

  def onConnect(self, response):
    logging.info('onConnect')

  def onOpen(self):
    logging.info('onOpen')
    self.sendMessage(json.dumps({'text': 'Hello <mark name="here"/> world',
                                 'accept': 'audio/ogg;codecs=opus'}))

  def onMessage(self, msg, binary):
    if binary:
      logging.info('binary message: %s bytes received', len(msg))
      self.binaryBytesReceived += len(msg)
    else:
      logging.info(msg)
      self.msgs.append(json.loads(msg))

  def onClose(self, wasClean, code, reason):
    logging.info((wasClean, code, reason))
```
{: codeblock}

## Example WebSocket session
{: #example}

The following example shows a simple WebSocket session between a client and the {{site.data.keyword.texttospeechshort}} service. Each line indicates whether the message is sent from the *Client* or returned by the *Server*. The example focuses on the exchange of data, not on opening the connection.

In the example, the client sends a text message that includes two `<mark>` tags. The client requests that audio be returned in WAV format. The server confirms the audio format and then sends multiple messages with the results. As noted previously, the service can guarantee neither the number of audio chunks it sends to the client nor the order in which it delivers text and audio messages.

Both of the following response scenarios are possible. In both cases, the service can send an arbitrary number of binary messages that contain the audio data and two text messages that identify the locations of the marks in the binary stream. But in both cases, the timing information for the marks arrives before the audio chunk that contains the locations of the marks.

In the first example, the text messages are interspersed with the multiple audio messages.

```
Client>> { "text": "This is a <mark name=\"simple\"/> simple
           <mark name=\"example\"/> example.", "accept": "audio/wav" };
Server<< { "binary_streams": [ { "content_type": "audio/wav" } ] }
Server<< <one or more chunks of binary audio>
         <all audio precedes the simple mark>
Server<< { "marks": [ ["simple", 0.7848991042702103] ] }
Server<< <one or more chunks of binary audio>
         <audio can precede and follow the simple mark>
         <all audio precedes the example mark>
Server<< { "marks": [ ["example", 1.0034702987337102] ] }
Server<< <one or more chunks of binary audio>
         <audio can precede and follow the example mark>
```
{: screen}

In the second example, the text messages arrive before any of the audio.

```
Client>> { "text": "This is a <mark name=\"simple\"/>
           simple <mark name=\"example\"/> example.", "accept": "audio/wav" };
Server<< { "binary_streams": [ { "content_type": "audio/wav" } ] }
Server<< { "marks": [ ["simple", 0.7848991042702103] ] }
Server<< { "marks": [ ["example", 1.0034702987337102] ] }
Server<< <one or more chunks of binary audio>
```
{: screen}
