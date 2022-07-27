---

copyright:
  years: 2015, 2022
lastupdated: "2022-07-11"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Generating word timings
{: #timing}

You can use the WebSocket interface of the {{site.data.keyword.texttospeechfull}} service to obtain timing information for user-specified locations such as word boundaries or for all words of the input text:
{: shortdesc}

-   Include the SSML `<mark>` element in input text to identify the time at which the marker occurs in the audio.
-   Specify the `timings` parameter of a JSON text message to obtain timing information for all strings of the input text.

Timing information is useful for synchronizing the audio and the input text. For example, you can coordinate an avatar's or robot's gestures with the content of the synthesized speech.

The `<mark>` element and the `timings` parameter are available only with the WebSocket interface, not with the HTTP interface. Also, the `timings` parameter is not supported for Japanese input text.
{: note}

## How the service returns word timings
{: #timing-how}

To return mark or word timing information, the service multiplexes independent binary and text streams to construct its response:

-   For each `<mark`> element, the service returns a JSON text message. Each message indicates the exact time from the beginning of the synthesized audio at which the mark occurs.
-   For word timings for all strings, the service returns one or more JSON text messages. Each message contains an array of words and their start and end times from the beginning of the synthesized audio.

The binary and text streams that the service sends are independent. So the service has little control over the number of audio chunks that it delivers and when the user receives the text and audio messages. For example, if the audio is synthesized more quickly than it is compressed, all text messages might arrive before any of the audio arrives.

In practical terms, the service can send an arbitrary number of audio chunks, including multiple chunks of audio before and after each text message. It is also possible for a single binary chunk to contain audio data that both precede and follow the timing information for a mark or word.

However, the text message that contains the timing information always arrives before the binary chunk that contains the corresponding audio. Moreover, the audio messages always arrive in order so that you can construct complete and accurate audio of the synthesized text from the binary results.

## Specifying an SSML mark
{: #timing-mark}

The optional SSML `<mark>` element is an empty tag that places a marker into the text to be synthesized. The client is notified when all of the text that precedes the `<mark>` element has been synthesized.

The element accepts a single `name` attribute that specifies a string that uniquely identifies the mark. The name must begin with an alphanumeric character. The service returns the name along with the time at which the mark occurs from the beginning of the synthesized audio. You can include any number of marks in the input text.

The following snippet of JavaScript code includes an instance of the `<mark>` element with the name `here`:

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

When it finishes synthesizing the text that precedes the mark, the service sends a text message that identifies the name of the mark and the time in seconds at which the mark occurs in the audio:

```json
{
  "marks": [
    ["here", 0.501]
  ]
}
```
{: codeblock}

The text message that contains the timing information always arrives before the audio chunk that contains the mark's location.

## Requesting word timings for all words
{: #timing-request}

The optional `timings` parameter of the JSON object that you pass to the service for a request returns timing information for all strings of the input text. This convenience eliminates the need to specify the SSML `<mark>` element for each word of the input. Pass an array that includes the string `words` to request word timings. Pass an empty array or omit the parameter to receive no timing information.

The service returns word timings over the WebSocket connection in the same way that it returns timing information for individual `<mark>` elements. It returns one or more JSON text messages. Each message contains an array of words and their start and end times in seconds from the beginning of the synthesized audio. For example, the following example requests word timing information:

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

```json
{
  "words": [
    [
      "I", 0.0, 0.157
    ],
    [
      "have", 0.157, 0.321
    ],
    [
      "a", 0.321, 0.406
    ]
  ]
}
{
  "words": [
    [
      "pet", 0.406, 0.731
    ],
    [
      "bird.", 0.731, 1.049
    ]
  ]
}
```
{: codeblock}

The response is just an example. The service can return one or more text messages with timing information for the input. It can also return a separate text message for each word of the input. Moreover, the messages can be interspersed with responses that contain binary chunks of audio. But the text message that contains the timing information for a word always arrives before the audio chunk that contains that word.

### Timings for plain text
{: #timing-text}

The service's synthesis process involves a text normalization step that spells out numbers, dates, times, monetary amounts, acronyms, and abbreviations. The results correspond to how such strings are spoken. For example, the string *$200* is spoken as three words: *two*, *hundred*, and *dollars*. Because word timing information is used to synchronize the audio with the input text, the service returns timing information that corresponds to the non-normalized spelling of the input.

For example, consider the following input text:

```text
The coldest recorded temperature is -89.2 degrees Celsius in Antarctica on July 21, 1983!
```
{: codeblock}

The service returns audio timings for the following strings:

"*The*", "*coldest*", "*recorded*", "*temperature*", "*is*", "*-89.2*", "*degrees*", "*Celsius*", "*in*", "*Antarctica*", "*on*", "*July*", "*21,*", "*1983!*"

Although "*-89.2*" is spoken in the audio as five separate words (*minus*, *eighty*, *nine*, *point*, *two*), the text message provides timing information for the string as a single unit with the start time of *minus* and the end time of *two*.

As in the previous example, non-normalized strings can also contain punctuation. The service includes the punctuation that precedes or follows a word in the text message that it returns with the timings. For instance, the strings "*21,*" and "*1983!*" include punctuation that the service returns in its text message. Although the punctuation results in silence, the audio timing for the word does *not* include that silence.

For example, consider input text that contains the following conditional statement:

```text
If it is sunny, I will go to the beach.
```
{: codeblock}

The service returns timing information for all strings of the input, including "*sunny,*" and "*beach.*", both of which end in punctuation that produces silence. But the timing information for "*sunny,*" does not include the silence that is produced by the comma, and the timing information for "*beach.*" does not include the silence for the period. The information reflects only the timing of the spoken strings.

### Timings for SSML text
{: #timing-ssml}

When the service synthesizes plain text, it returns all input characters except for blank spaces as part of the strings in its word timing response. The same is not true of SSML, since some SSML elements do not generate audio. The following list summarizes the SSML elements that can impact word timing information:

-   `<say-as>` indicates how the text that is enclosed between the opening and closing `<say-as>` tags is to be handled in the normalization step. Attributes specify how the embedded text is to be spoken. The following example indicates how the date is to be spoken:

    ```xml
    The baby was born on <say-as interpret-as="date" format="mdy">3/4/2016</say-as>.
    ```
    {: codeblock}

    The service returns timing information for the following strings: "*The*", "*baby*", "*was*", "*born*", "*on*", "*3/4/2016.*" The service normalizes the string "*3/4/2016*" as "*march fourth two thousand sixteen*". The word timing information for the string reflects the start time of "*march*" and the end time of "*sixteen*".

    The following example indicates that the word `Hello` is to be spelled out:

    ```xml
    <say-as interpret-as="letters">Hello</say-as>.
    ```
    {: codeblock}

    The service returns timing information for the string "*Hello.*". The service spells the word letter-by-letter during the normalization step. The word timing information in the response reflects the start time of the letter "*h*" and the end time of the letter "*o*".
-   `<phoneme>` provides a pronunciation for the text that is enclosed in the opening and closing `<phoneme>` tags. But both the text and the closing tag are optional. The following example includes embedded text and a closing tag:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme> was ripe.
    ```
    {: codeblock}

    The service returns timing information for the following strings: "*The*", "*tomato*", "*was*", "*ripe.*"

    Conversely, the following example provides a unary `<phoneme>` element with no embedded text and no closing tag:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo"/> was ripe.
    ```
    {: codeblock}

    In this case, the service returns timing information for the following strings: "*The*", "*\<phoneme\>*", "*was*", "*ripe.*"
-   `<sub>` substitutes the text that is included in the element's `alias` attribute for the text that is enclosed between the opening and closing `<sub>` tags in the spoken audio. For example, the following input includes a single `<sub>` tag:

    ```xml
    I work at <sub alias="International Business Machines">IBM</sub>.
    ```
    {: codeblock}

    The service produces timing information for the following strings: "*I*", "*work*", "*at*", "*{{site.data.keyword.IBM_notm}}.*". The service normalizes the string "*{{site.data.keyword.IBM_notm}}*" as "*International Business Machines*". The timing information for the string reflects the start time of "*International*" and the end time of "*Machines*".
-   `<break>` inserts a pause in the spoken text. The service reflects the resulting silence in the word timings as a gap between the end time of the word that precedes the `<break>` element and the start time of the word that follows the element.
- `<paragraph>` (or `<p>`) can add silence to the audio. The service does not return timing information for the silence.
- `<sentence>` (or `<s>`) can add silence to the audio. The service does not return timing information for the silence.

SSML elements that are not mentioned in the list do not impact word timing information. For more information about the service's support for SSML, see [Understanding SSML](/docs/text-to-speech?topic=text-to-speech-ssml).

## Examples with mark elements
{: #timing-examples}

The following examples show a simple WebSocket session between a client and the service. The examples focus on the exchange of data, not on opening the connection. The client sends a text message that includes two `<mark>` elements, named `SIMPLE` and `EXAMPLE`, and it requests the audio to be returned in WAV format:

```json
{
  "text": "This is a <mark name=\"SIMPLE\"/>simple <mark name=\"EXAMPLE\"/> example.",
  "accept": "audio/wav"
}
```
{: codeblock}

The service first sends a message to confirm the audio format. It then sends multiple messages with the results. The service cannot guarantee the number of audio chunks that it sends to the client or the order in which the text and audio messages are delivered.

Both of the following responses are possible. In each case, the service sends two text messages that identify the locations of the marks in the binary stream. But it sends an arbitrary number of binary messages that contain the audio. The timing information for a mark always arrives before the audio chunk that contains the location of the mark.

-   *In the first example response,* the text messages are interspersed with multiple audio messages:

    ```json
    {
      "binary_streams": [
        {
          "content_type": "audio/wav"
        }
      ]
    }
    ... One or more chunks of binary audio.
        All audio precedes the SIMPLE mark....
    {
      "marks": [
        [
          "SIMPLE", 0.784
        ]
      ]
    }
    ... One or more chunks of binary audio audio can precede
        and follow the SIMPLE mark.
        All audio precedes the EXAMPLE mark....
    {
      "marks": [
        [
          "EXAMPLE", 1.003
        ]
      ]
    }
    ... One or more chunks of binary audio.
        Audio can precede and follow the EXAMPLE mark....
    ```
    {: codeblock}

-   *In the second example response,* the text messages arrive before any of the audio messages:

    ```json
    {
      "binary_streams": [
        "content_type": "audio/wav"}
      ]
    }
    {
      "marks": [
        [
          "SIMPLE", 0.784
        ]
      ]
    }
    {
      "marks": [
        [
          "EXAMPLE", 1.003
        ]
      ]
    }
    ... One or more chunks of binary audio....
    ```
    {: codeblock}
