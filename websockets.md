---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# The WebSocket interface
{: #usingWebSocket}

**Important:** You cannot use JavaScript to call the WebSocket interface from a browser. The `watson-token` parameter that is available with the `/v1/synthesize` method does not accept IAM tokens or API keys, and you cannot pass request headers from JavaScript. For more information about working around this limitation, see the [Known limitations](/docs/services/text-to-speech/release-notes.html#limitations) in the release notes.

To synthesize text to speech with the service's WebSocket interface, you first establish a connection with the service by calling its `/v1/synthesize` method. You then send the text to be synthesized to the service as a JSON text message over the connection. The service automatically closes the WebSocket connection when it finishes processing the request.
{: shortdesc}

The synthesize request and response cycle includes the following steps:

1.  [Open a connection](#WSopen).
1.  [Send input text](#WSsend).
1.  [Receive a response](#WSreceive).

The WebSocket interface accepts identical input and produces identical results as the `GET` and `POST /v1/synthesize` methods of the HTTP interface. However, the WebSocket interface supports use of the SSML `<mark>` element to identify the location of user-specified markers in the audio. It can also return timing information for all strings of the input text. For more information, see [Obtaining word timings](/docs/services/text-to-speech/word-timing.html).

> **Note:** The snippets of example code that follow are written in JavaScript and are based on the HTML5 WebSocket API. For more information about the WebSocket protocol, see the Internet Engineering Task Force (IETF) [Request for Comment (RFC) 6455 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://tools.ietf.org/html/rfc6455){: new_window}.

## Open a connection
{: #WSopen}

You call the `/v1/synthesize` method over the WebSocket Secure (WSS) protocol to open a connection to the service. The method is available at the following endpoint:

```
wss://{host_name}/text-to-speech/api/v1/synthesize
```
{: codeblock}

where `{host_name}` is the location in which your application is hosted:

-   `stream.watsonplatform.net` for Dallas (the following examples use this host name)
-   `stream-fra.watsonplatform.net` for Frankfurt
-   `gateway-syd.watsonplatform.net` for Sydney
-   `gateway-wdc.watsonplatform.net` for Washington, DC
-   `gateway-tok.watsonplatform.net` for Tokyo

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
      credentials with the call. Watson authentication tokens are an
      alternative to service credentials. They are based on Cloud Foundry
      service credentials that use a `{username}` and `{password}` for
      authentication.
      <br/><br/>
      **Note:** You cannot use JavaScript to call the WebSocket interface from
      a browser if your service credentials are based on IAM authentication.
      The `watson-token` parameter does not accept IAM tokens or API keys.
      For more information about working around this limitation, see the
      [Known limitations](/docs/services/text-to-speech/release-notes.html#limitations)
      in the release notes.
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
      guaranteed to work only if it matches the language of the voice that
      is used for the synthesis. If you include a customization ID, you must
      call the method with the service credentials of the custom model's owner.
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
      Indicates whether the service logs requests and results that are sent
      over the connection. To prevent IBM from accessing your data for general
      service improvements, specify <code>true</code> for the parameter. For
      more information, see
      <a href="/docs/services/watson/getting-started-logging.html">Controlling
        request logging for Watson services</a>.
    </td>
  <tr>
    <td style="text-align:left"><code>x-watson-metadata</code>
      <br/><em>Optional</em></td>
    <td style="text-align:center">String</td>
    <td style="text-align:left">
      Associates a customer ID with data that is passed over the
      connection. The parameter accepts the argument
      <code>customer_id={id}</code>, where <code>id</code> is a random
      or generic string that is to be associated with the data. You must
      URL-encode the argument to the parameter, for example,
      `customer_id%3dmy_ID`. By default, no customer ID is associated
      with the data. For more information, see
      <a href="/docs/services/text-to-speech/information-security.html">Information
      security</a>.
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
      an SSML mark</a>. The client can pass a maximum of 5 KB of text with
      the request.
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
      you can use `*/*` to specify the default audio format,
      <code>audio/ogg;codecs=opus</code>.
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>Optional</em></td>
    <td style="text-align:center">String[ ]</td>
    <td>
      Specifies that the service is to return word timing information
      for all strings of the input text. The service returns the start
      and end time of each string of the input. Specify <code>words</code>
      as the lone element of the array to request word timings. Specify
      an empty array or omit the parameter to receive no word timings.
      For more information, see
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
      content_type: 'audio/ogg;codecs=opus'
    }
  ]
}
```
{: codeblock}

## Receive a response
{: #WSreceive}

After it confirms the audio format, the service sends the synthesized audio as a binary stream of data in the indicated format. The service sends timing information as one or more text messages if

-   The input text includes one or more SSML `<mark>` elements.
-   You specify the `timings` parameter with the request.

The service can also send text messages with warnings or errors. When it finishes synthesizing the input text, the service automatically closes the WebSocket connection.

The client needs to append binary responses from the service to the audio results received over the connection. It can handle text messages by responding to them, displaying them, or capturing them for use by the application (for example, if they contain mark locations). The following simple example of an `onMessage` function appends text and binary messages that are received from the service to the appropriate variable based on their type. When the `onClose()` function executes, the entire audio stream has been received.

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
-   `1011` indicates that the service is terminating the connection because it encountered an unexpected condition that prevents it from fulfilling the request, such as an invalid argument. The return code can also indicate that the input text was too large; the text cannot exceed 5 KB.

If the socket closes with an error, the service sends the client an informative message of the form `{"error": "Specific error message"}` before closing. The service can also send warning messages for unknown parameters.

### Example error and warning messages
{: #returnErrors}

The first two examples show error responses. They include a JSON text message and a formatted message from the client's `onClose` callback method. The formatted messages begin with the boolean `true` because the connection is closed. They also include the WebSocket error code that caused the closure. The third example shows a warning response. It does not include the second message because the connection is not closed by the warning.

-   The first example shows error messages for an invalid argument for the `accept` parameter:

    ```javascript
    {
      "error": "Unsupported mimetype. Supported mimetypes are: ['application/json', 'audio/flac', ...]"
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
