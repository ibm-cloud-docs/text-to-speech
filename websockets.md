---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-20"

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

# The WebSocket interface
{: #usingWebSocket}

To synthesize text to speech with the service's WebSocket interface, you first establish a connection with the service by calling its `/v1/synthesize` method. You then send the text to be synthesized to the service as a JSON text message over the connection. The service automatically closes the WebSocket connection when it finishes processing the request.
{: shortdesc}

The synthesize request and response cycle includes the following steps;

1.  [Open a connection](#WSopen).
1.  [Send input text](#WSsend).
1.  [Receive a response](#WSreceive).

The WebSocket interface accepts identical input and produces identical results as the `GET` and `POST /v1/synthesize` methods of the HTTP interface. However, the WebSocket interface supports use of the SSML `<mark>` element to identify the location of user-specified markers in the audio, and it allows you to obtain word timing information in the audio for all strings of the input text. For more information, see [Obtaining word timings](/docs/services/text-to-speech/word-timing.html).

## Open a connection
{: #WSopen}

You call the `/v1/synthesize` method over the WebSocket Secure (WSS) protocol to open a connection to the service. The method is available at the following endpoint:

```
wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize
```
{: codeblock}

A WebSocket client calls this method with the following query parameters to establish an authenticated connection with the service.

<table>
  <caption>Table 1. Parameters of the <code>/v1/synthesize</code>
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
      Omit the parameter to use the default voice, `en-US_MichaelVoice`.
      For more information, see
      <a href="/docs/services/text-to-speech/http.html#voices">Specifying
        a voice</a>.
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
      the method with the service credentials of the custom model's owner.
      Omit the parameter to use the specified voice with no customization.
      For more information, see
      <a href="/docs/services/text-to-speech/custom-intro.html">Understanding
         customization</a>.
    </td>
  </tr>
  <tr>
    <td><code>x-watson-learning-opt-out</code><br/><em>Optional</em></td>
    <td style="text-align:center">Boolean</td>
    <td>
      Specifies whether the service logs the request and results sent over
      the connection, which it does by default to improve the service for
      future users. Specify <code>true</code> to prevent the service from
      logging the data. You can also opt out of request logging by passing
      a value of <code>true</code> with the
      <code>X-Watson-Learning-Opt-Out</code> request header; for more
      information, see
      <a href="/docs/services/watson/getting-started-logging.html">Controlling
        request logging for Watson services</a>.
    </td>
  </tr>
</table>

The following snippet of JavaScript code opens a connection with the service. The call to the `/v1/synthesize` method passes the `voice` and `watson-token` query parameters, the former to direct the service to use the US English Allison voice. Once the connection is established, the event listeners (`onOpen`, `onClose`, and so on) are defined to respond to events from the service.

```javascript
var voice = 'en-US_AllisonVoice';
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?voice=' + voice
  + '&watson-token=' + token;
var websocket = new WebSocket(wsURI);
websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

## Send input text
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
      Markup Language (SSML). For more information, see
      <a href="/docs/services/text-to-speech/http.html#input">Specifying
      input text</a>. SSML input can also include the
      <code>&lt;mark&gt;</code> element; see
      <a href="/docs/services/text-to-speech/word-timing.html#mark">Specifying
      an SSML mark</a>. The client can pass a maximum of 5 KB of data
      with the request.
    </td>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>Required</em></td>
    <td style="text-align:center">String</td>
    <td>
      Specifies the requested format (MIME type) of the audio. For
      more information, see
      <a href="/docs/services/text-to-speech/http.html#format">Specifying
      an audio format</a>. In addition to the supported specifications,
      the WebSocket interface lets you specify `*/*` to use the default
      audio format, <code>audio/ogg;codecs=opus</code>.
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>Optional</em></td>
    <td style="text-align:center">String[ ]</td>
    <td>
      Specifies that the service is to return word timing information
      for all strings of the input text. The service returns the start
      and end time of each string of the input. Specify <code>words</code>
      as the sole element of the array to request word timings; specify
      an empty list or omit the parameter to receive no word timings. For
      more information, see
      <a href="/docs/services/text-to-speech/word-timing.html#timing">Obtaining
      word timings</a>. <em>Not supported for Japanese input text.</em>
    </td>
  </tr>
</table>

The following snippet of JavaScript code passes a simple *Hello world* message as the input text and requests the default format for the audio. The calls are included in the `onOpen` function that is defined for the client to ensure that they are sent only after the connection is established.

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

The service responds to this message by sending a text message that confirms the format of the audio response:

```javascript
{
  'binary_streams': [
    {
      'content_type': 'audio/ogg;codecs=opus'
    }
  ]
}
```
{: codeblock}

## Receive a response
{: #WSreceive}

After it confirms the audio format, the service sends the synthesized audio as a binary stream of data in the indicated format. If the input text includes one or more SSML `<mark>` elements or if you specified the `timings` parameter with the request, the service sends timing information as one or more text messages. The service can also send text messages with warnings or errors. When it finishes synthesizing the input text, the service automatically closes the WebSocket connection.

The client needs to append binary responses from the service to the audio results received over the connection. It can handle text messages by responding to them, displaying them, or capturing them for use by the application (for example, if they contain mark locations). The following simple example of an `onMessage` function appends text and binary messages received from the service to the appropriate variable depending on their type. When the `onClose()` function executes, the entire audio stream has been received.

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

## WebSocket return codes
{: #returnCodes}

The service can send the following return codes to the client over the WebSocket connection:

-   `1000` indicates normal closure of the connection, meaning that the purpose for which the connection was established has been fulfilled.
-   `1002` indicates that the service is closing the connection due to a protocol error.
-   `1006` indicates that the connection closed abnormally.
-   `1009` indicates that the frame size exceeded the 4 MB limit.
-   `1011` indicates that the service is terminating the connection because it encountered an unexpected condition that prevents it from fulfilling the request, such as an invalid argument. The return code can also indicate that the input text was too large; the text cannot exceed 5 KB in size.

If the socket closes with an error, the service sends the client an informative message of the form `{"error": "Specific error message"}` before closing. The service can also send warning messages for unknown parameters.

### Example error and warning messages
{: #returnErrors}

The first two examples show error responses. They include a JSON text message and a formatted message from the client's `onClose` callback method. The formatted messages begin with the boolean `true` because the connection is closed; they also include the WebSocket error code that caused the closure. The third example shows a warning response. It does not include the second message because the connection is not closed by the warning.

-   The first example shows error messages for an invalid argument for the `accept` parameter:

    ```javascript
    {
      "error": "Unsupported mimetype.  Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   The second example shows error messages for a missing `text` parameter:

    ```javascript
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   The third example shows a warning message for an unknown parameter named `invalid-parameter`:

    ```javascript
    {
      "warnings": "Unknown arguments: invalid-parameter."
    }
    ```
    {: codeblock}

For more information about WebSocket return codes, see the Internet Engineering Task Force (IETF) [Request for Comments (RFC) 6455 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://tools.ietf.org/html/rfc6455){: new_window}.

## Example Python code
{: #python}

The following brief example Python code defines a class that sends a simple message with a single `<mark>` element to the service over a WebSocket connection. The code works equally well for text that does not include a `<mark>` element.

The code defines callback methods to handle state changes and responses in the connection. The Python callback methods differ slightly from the JavaScript event handlers shown previously. All methods log suitable messages to the console.

-   The `onConnect` method fires when the service accepts the connection but before the handshake is completed.
-   The `onOpen` method fires when the handshake between the client and service is complete and the connection is fully established. The method sends a JSON text message that specifies the text to be synthesized and the requested format of the audio.
-   The `onMessage` method fires when the service sends a response. The method appends a binary response to the audio received from the service and a text message to the list of messages received from the service.
-   The `onClose` method fires when the connection is closed. The `wasClean` argument is a boolean that indicates whether the connection was closed as a result of the service sending a close frame, as opposed to a network or protocol error. The `code` and `reason` arguments provide the WebSocket return code and its accompanying message.

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
