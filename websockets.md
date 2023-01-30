---

copyright:
  years: 2015, 2023
lastupdated: "2023-01-17"

subcollection: text-to-speech

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# The WebSocket interface
{: #usingWebSocket}

To synthesize text to speech with the WebSocket interface of the {{site.data.keyword.texttospeechfull}} service, you first establish a connection with the service by calling its `/v1/synthesize` method. You then send the text to be synthesized to the service as a JSON text message over the connection. The service automatically closes the WebSocket connection when it finishes processing the request.
{: shortdesc}

The synthesize request and response cycle includes the following steps:

1.  [Open a connection](#WSopen).
1.  [Send input text](#WSsend).
1.  [Receive a response](#WSreceive).

The WebSocket interface accepts identical input and produces identical results as the `GET` and `POST /v1/synthesize` methods of the HTTP interface. In addition, the WebSocket interface also supports use of the SSML `<mark>` element to identify the location of user-specified markers in the audio. It can also return timing information for all strings of the input text. (The `<mark>` element and word timings are available only with the WebSocket interface.)

-   For more information about obtaining word timings, see [Generating word timings](/docs/text-to-speech?topic=text-to-speech-timing).
-   For more information about the WebSocket interface and its parameters, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

The snippets of example code that follow are written in JavaScript and are based on the HTML5 WebSocket API. For more information about the WebSocket protocol, see the Internet Engineering Task Force (IETF) [Request for Comment (RFC) 6455](https://tools.ietf.org/html/rfc6455){: external}.
{: note}

## Open a connection
{: #WSopen}
{: help}
{: support}

You call the `/v1/synthesize` method over the WebSocket Secure (WSS) protocol to open a connection to the service. The method is available at the following endpoint:

```text
wss://api.{location}.text-to-speech.watson.cloud.ibm.com/instances/{instance_id}/v1/synthesize
```
{: codeblock}

where `{location}` indicates where your application is hosted:

-   `us-south` for Dallas
-   `us-east` for Washington, DC
-   `eu-de` for Frankfurt
-   `au-syd` for Sydney
-   `jp-tok` for Tokyo
-   `eu-gb` for London
-   `kr-seo` for Seoul

And `{instance_id}` is the unique identifier of the service instance.

The examples in the documentation abbreviate `wss://api.{location}.text-to-speech.watson.cloud.ibm.com/instances/{instance_id}` to `{ws_url}`. So all WebSocket examples call the method as `{ws_url}/v1/synthesize`.
{: note}

A WebSocket client calls the `/v1/synthesize` method with the following query parameters to establish an authenticated connection with the service:

`access_token` (*required* string)
:   Pass a valid access token to authenticate with the service. You must use the access token before it expires.

    -   [IBM Cloud]{: tag-ibm-cloud} Pass an Identity and Access Management (IAM) access token to authenticate with the service. You pass an IAM access token instead of passing an API key with the call. For more information, see [Authenticating to {{site.data.keyword.cloud_notm}}](/docs/watson?topic=watson-iam#gs-credential-cloud).
    -   [IBM Cloud Pak for Data]{: tag-cp4d} Pass an access token as you would with the `Authorization` header of an HTTP request. For more information, see [Authenticating to {{site.data.keyword.icp4dfull_notm}}](/docs/watson?topic=watson-iam#gs-credential-cpd).

`voice` (*optional* string)
:   Specifies the voice in which the text is to be spoken in the audio. Use the `/v1/voices` method to get the current list of supported voices. Omit the parameter to use the default voice. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices) and [Using the default voice](/docs/text-to-speech?topic=text-to-speech-voices-use#specify-voice-default).

`customization_id` (*optional* string)
:   Specifies the globally unique identifier (GUID) for a custom model that is to be used for the synthesis. A specified custom model must match the language of the voice that is used for the synthesis. If you include a customization ID, you must make the request with credentials for the instance of the service that owns the custom model. Omit the parameter to use the specified voice with no customization. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

`rate_percentage` (*optional* integer)
:   Specifies the global speaking rate for the entire synthesis request. The speaking rate is the speed at which the service speaks the text that it synthesizes into speech. A higher rate causes the text to be spoken more quickly; a lower rate causes the text to be spoken more slowly. The parameter changes the per-voice default rate for an entire request. For more information, see [Modifying the speaking rate](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-rate-percentage).

`pitch_percentage` (*optional* integer)
:   Specifies the global speaking pitch for the entire synthesis request. The speaking pitch represents the tone of the speech that the service synthesizes. It represents how high or low the tone of the voice is perceived by the listener. A higher pitch results in speech that is spoken at a higher tone; a lower pitch results in speech that is spoken in a lower tone. The parameter changes the per-voice default pitch for an entire request. For more information, see [Modifying the speaking pitch](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-pitch-percentage).

`spell_out_mode` (*optional* string)
:   *For German voices,* specifies how individual characters of a string are to be spelled out. By default, the service spells out individual characters at the same rate at which it synthesizes text for a language. You can use the parameter to direct the service to spell out individual characters more slowly, in groups of one (`singles`), two (`pairs`), or three (`triples`). For more information, see [Specifying how strings are spelled out](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-spell-out-mode).

`x-watson-metadata` (*optional* string)
:   Associates a customer ID with data that is passed over the connection. The parameter accepts the argument `customer_id={id}`, where `id` is a random or generic string that is to be associated with the data. You must URL-encode the argument to the parameter, for example, `customer_id%3dmy_customer_ID`. By default, no customer ID is associated with the data. For more information, see [Information security](/docs/text-to-speech?topic=text-to-speech-information-security).

`x-watson-learning-opt-out` (*optional* boolean)
:   [IBM Cloud]{: tag-ibm-cloud} Indicates whether the service logs requests and results that are sent over the connection. To prevent IBM from accessing your data for general service improvements, specify `true` for the parameter. Opting out directs IBM to write to disk *no* user data (text or audio) for your request. You can also opt out at the account level. For more information, see [Request logging](/docs/text-to-speech?topic=text-to-speech-data-security#data-security-request-logging).

The following snippet of JavaScript code opens a connection with the service. The call to the `/v1/synthesize` method passes the `voice` and `access_token` query parameters, the former to direct the service to use the US English Allison voice. Once the connection is established, the event listeners (`onOpen()`, `onClose()`, and so on) are defined to respond to events from the service.

```javascript
var access_token = '{access_token}';
var wsURI = '{ws_url}/v1/synthesize'
  + '?access_token=' + access_token
  + '&voice=en-US_AllisonV3Voice';
var websocket = new WebSocket(wsURI);

websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

## Send input text
{: #WSsend}
{: help}
{: support}

To synthesize text, the client passes a simple JSON text message to the service with the following parameters:

`text` (*required* string)
:   Provides the text that is to be synthesized. The client can pass plain text or text that is annotated with the Speech Synthesis Markup Language (SSML). The client can pass a maximum of 5 KB of input text with the request. The limit includes any SSML that you specify. For more information, see [Specifying input text](/docs/text-to-speech?topic=text-to-speech-usingHTTP#input) and the sections that follow it. (SSML input can also include the `<mark>` element. For more information, see [Specifying an SSML mark](/docs/text-to-speech?topic=text-to-speech-timing#timing-mark).)

`accept` (*required* string)
:   Specifies the requested format (MIME type) of the audio. Use `*/*` to request the default audio format, `audio/ogg;codecs=opus`. For more information, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

    The Ogg audio format is not supported with the Safari browser. If you are using the the {{site.data.keyword.texttospeechshort}} service with the Safari browser, you must specify a different format in which you want the service to return the audio.
    {: important}

`timings` (*optional* string[ ])
:   Specifies that the service is to return word timing information for all strings of the input text. The service returns the start and end time of each token of the input. Specify `words` as the lone element of the array to request word timings. Specify an empty array or omit the parameter to receive no word timings. For more information, see [Generating word timings](/docs/text-to-speech?topic=text-to-speech-timing). *Not supported for Japanese input text.*

The following snippet of JavaScript code passes a simple "Hello world" message as the input text and requests the default format for the audio. The calls are included in the `onOpen()` function that is defined for the client to ensure that they are sent only after the connection is established.

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

The service responds to this message by sending a text message that confirms the format of the audio response. The following response confirms the default audio format.

```json
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
{: help}
{: support}

After it confirms the audio format, the service sends the synthesized audio as a binary stream of data in the indicated format. For audio formats that include a header (for example, `audio/wav` and `audio/ogg`), the service returns the header before it sends the audio data. The header can span multiple binary responses. For all audio formats, the client needs to append all binary responses from the service to assemble the complete audio response.

In addition to sending a text message that confirms the requested audio format, the service can also send text messages with warnings or errors. The service also sends one or more text messages that include timing information if

-   The input text includes one or more SSML `<mark>` elements.
-   You specify the `timings` parameter with the request.

The client can handle text messages by responding to them, displaying them, or capturing them for use by the application (for example, if they contain mark locations).

When it finishes synthesizing the input text and sending all binary and text messages, the service automatically closes the WebSocket connection. The following simple `onMessage()` function appends text and binary messages that are received from the service to the appropriate variables based on their type. When the `onClose()` function executes, the entire audio stream has been received and the service sends no further binary or text messages.

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
  // The service's response is complete.
}
```
{: codeblock}

## WebSocket return codes
{: #returnCodes}
{: troubleshoot}
{: support}

The service can send the following return codes to the client over the WebSocket connection:

-   `1000` indicates normal closure of the connection, meaning that the purpose for which the connection was established has been fulfilled.
-   `1002` indicates that the service is closing the connection due to a protocol error.
-   `1006` indicates that the connection closed abnormally.
-   `1009` indicates that the frame size exceeded the 4 MB limit.
-   `1011` indicates that the service is terminating the connection because it encountered an unexpected condition that prevents it from fulfilling the request, such as an invalid argument. The return code can also indicate that the input text was too large.

If the socket closes with an error, the service sends the client an informative message of the form `{"error": "Specific error message"}` before closing. The service can also send non-fatal warning messages for unknown parameters. For more information about WebSocket return codes, see the Internet Engineering Task Force (IETF) [Request for Comments (RFC) 6455](https://tools.ietf.org/html/rfc6455){: external}.

The WebSocket implementations of the SDKs can return different or additional response codes.
{: note}

### Example error and warning messages
{: #returnErrors}
{: troubleshoot}
{: support}

The following examples show error responses. They include a JSON text message and a formatted message from the client's `onClose()` callback method. The formatted messages begin with the boolean `true` because the connection is closed. They also include the WebSocket error code that caused the closure.

-   This example shows error messages for an invalid argument for the `accept` parameter:

    ```json
    {
      "error": "Unsupported mimetype. Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   This example shows error messages for a missing `text` parameter:

    ```json
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

The following example shows a warning response, in this case for an unknown parameter named `invalid-parameter`. It does not include the second message because the connection is not closed by the warning.

```json
{
  "warnings": "Unknown arguments: invalid-parameter."
}
```
{: codeblock}
