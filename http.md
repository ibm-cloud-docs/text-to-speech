---

copyright:
  years: 2015, 2023
lastupdated: "2023-01-24"

subcollection: text-to-speech

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# The HTTP interface
{: #usingHTTP}

To synthesize text to speech with the HTTP REST interface of the {{site.data.keyword.texttospeechfull}} service, you call the `GET` or `POST /v1/synthesize` method. You specify the text that is to be synthesized and the voice and format for the spoken audio. You can also specify a custom model that is to be used with the request.
{: shortdesc}

For more information about the HTTP interface, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

## Synthesizing text to audio
{: #synthesize}
{: help}
{: support}

To synthesize text to audio, you call one of the two versions of the service's `/v1/synthesize` method:

-   The `GET /v1/synthesize` method accepts the text that is to be synthesized as a required `text` query parameter. The maximum size of the request is 8 KB, which includes the input text, any SSML that you specify, and the URL and headers.
-   The `POST /v1/synthesize` method accepts the text that is to be synthesized as a JSON construct in the required body of the request. The maximum size of the request is 8 KB for the URL and headers, and 5 KB for the input text that is sent in the body of the request. The 5 KB limit includes any SSML that you specify.

The two versions of the `/v1/synthesize` method have the following parameters in common:

`accept` (query parameter, *optional* string)
:   Specifies the requested audio format, or MIME type, in which the service is to return the audio. You can also specify this value with the HTTP `Accept` request header. URL-encode the argument to the `accept` query parameter. By default, the service returns the audio in the format `audio/ogg;codecs=opus`. For more information, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

    The Ogg audio format is not supported with the Safari browser. If you are using the the {{site.data.keyword.texttospeechshort}} service with the Safari browser, you must specify a different format in which you want the service to return the audio.
    {: important}

`voice` (query parameter, *optional* string
:   Specifies the voice in which the text is to be spoken in the audio. Use the `/v1/voices` method to get the current list of supported voices. Omit the parameter to use the default voice. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices) and [Using the default voice](/docs/text-to-speech?topic=text-to-speech-voices-use#specify-voice-default).

`customization_id` (query parameter, *optional* string)
:   Specifies a globally unique identifier (GUID) for a custom model that is to be used for the synthesis. A specified custom model must match the language of the voice that is used for the synthesis. If you include a customization ID, you must make the request with credentials for the instance of the service that owns the custom model. Omit the parameter to use the specified voice with no customization. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

`rate_percentage` (query parameter, *optional* integer)
:   Specifies the global speaking rate for the entire synthesis request. The speaking rate is the speed at which the service speaks the text that it synthesizes into speech. A higher rate causes the text to be spoken more quickly; a lower rate causes the text to be spoken more slowly. The parameter changes the per-voice default rate for an entire request. For more information, see [Modifying the speaking rate](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-rate-percentage).

`pitch_percentage` (query parameter, *optional* integer)
:   Specifies the global speaking pitch for the entire synthesis request. The speaking pitch represents the tone of the speech that the service synthesizes. It represents how high or low the tone of the voice is perceived by the listener. A higher pitch results in speech that is spoken at a higher tone; a lower pitch results in speech that is spoken in a lower tone. The parameter changes the per-voice default pitch for an entire request. For more information, see [Modifying the speaking pitch](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-pitch-percentage).

`spell_out_mode` (query parameter, *optional* string)
:   *For German voices,* specifies how individual characters of a string are to be spelled out. By default, the service spells out individual characters at the same rate at which it synthesizes text for a language. You can use the parameter to direct the service to spell out individual characters more slowly, in groups of one (`singles`), two (`pairs`), or three (`triples`). For more information, see [Specifying how strings are spelled out](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-spell-out-mode).

`X-Watson-Metadata` (request header, *optional* string)
:   Associates a customer ID with data that is passed with a request. For more information, see [Information security](/docs/text-to-speech?topic=text-to-speech-information-security).

`X-Watson-Learning-Opt-Out` (request header, *optional* boolean)
:   [IBM Cloud]{: tag-ibm-cloud} Indicates whether the service logs request and response data to improve the service for future users. To prevent IBM from accessing your data for general service improvements, specify `true` for the parameter. Opting out directs IBM to write to disk *no* user data (text or audio) for your request. You can also opt out at the account level. For more information, see [Request logging](/docs/text-to-speech?topic=text-to-speech-data-security#data-security-request-logging).

If you specify an invalid query parameter or JSON field as part of the input to the `/v1/synthesize` method, the service returns a `Warnings` response header that describes and lists each invalid argument. The request succeeds despite the warnings.

## Specifying input text
{: #input}
{: help}
{: support}

Both the `POST` and `GET /v1/synthesize` methods accept plain input text or text that is annotated with SSML. The two versions differ primarily in how you specify the text that is to be synthesized. The following examples both pass the plain text `Hello world`.

-   The `POST /v1/synthesize` method accepts input text in the body of the request. You specify the input with a simple JSON construct that includes plain text or SSML. You must also specify a value of `application/json` for the `Content-Type` header.

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --output hello_world.wav \
    --data "{\"text\":\"Hello world\"}" \
    "{url}/v1/synthesize?voice=en-US_MichaelV3Voice"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --output hello_world.wav \
    --data "{\"text\":\"Hello world\"}" \
    "{url}/v1/synthesize?voice=en-US_MichaelV3Voice"
    ```
    {: pre}

-   The `GET /v1/synthesize` method accepts input text that is specified by the `text` query parameter. You specify the input as plain text or SSML, both of which must be URL-encoded.

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X GET -u "apikey:{apikey}" \
    --header "Accept: audio/wav" \
    --output hello_world.wav \
    "{url}/v1/synthesize?text=Hello%20world&voice=en-US_MichaelV3Voice"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X GET \
    --header "Authorization: Bearer {token}" \
    --header "Accept: audio/wav" \
    --output hello_world.wav \
    "{url}/v1/synthesize?text=Hello%20world&voice=en-US_MichaelV3Voice"""
    ```
    {: pre}

Although the `POST` and `GET` methods offer equivalent functionality, it is always more secure to pass input text to the service with the `POST` method. A `POST` request passes input in the body of the request. A `GET` request exposes the data in the URL.

## Punctuating input text
{: #input-punctuation}

Write text for synthesis with the punctuation you would use normally. For example, include commas, periods, exclamation points, and questions marks as you would in normal writing.

The service considers punctuation when synthesizing text. For example, commas and end-of-sentence punctuation affect the audio by inserting pauses at appropriate places in the resulting synthesized speech. End-of-sentence punctuation such as periods, exclamation points, and question marks also change the intonation and inflection of the speech. You can also use SSML elements to affect these aspects of the speech.

## Specifying SSML input
{: #ssml-http}

The Speech Synthesis Markup Language (SSML) is an XML-based markup language that is designed to provide annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service. You can use SSML elements and their attributes to gain greater control over the synthesis and resulting audio output.

For more information about using SSML to annotate input text, see [Understanding SSML](/docs/text-to-speech?topic=text-to-speech-ssml). For an inventory of all supported elements and attributes, see [SSML elements](/docs/text-to-speech?topic=text-to-speech-elements).

## Escaping XML control characters
{: #escape}
{: troubleshoot}
{: support}

Because you can submit input text that includes XML-based SSML annotations, the service validates all input to ensure that any SSML is correct and well formed. Therefore, you must escape any XML control characters that are present in the input text, regardless of whether the input includes SSML. Use the equivalent escape strings or character encodings from Table 1 instead of the indicated characters.

| Character | Escape strings | Character encoding |
|:---------:|:--------------:|:------------------:|
| `"`  \n (double quotes) | `&quot;` | `&#34;` |
| `'`  \n (apostrophe or single quote) | `&apos;` | `&#39;` |
| `&`  \n (ampersand) | `&amp;` | `&#38;` |
| `<`  \n (left angle bracket) | `&lt;` | `&#60;` |
| `>`  \n (right angle bracket) | `&gt;` | `&#62;` |
| `/`  \n (forward slash) | None | `&#47;` |
{: caption="Table 1. Escaping XML control characters"}

For more information about how the service validates input text, see [SSML validation](/docs/text-to-speech?topic=text-to-speech-ssml#ssml-errors).

## Examples of input text
{: #httpExamples}

The following examples show how to specify input text with either method of the HTTP interface. They also show how to escape XML control characters. The examples include line breaks for readability. Do *not* include the line breaks in actual input.

### Example input with a GET request
{: #getExamples}

The following examples pass URL-encoded input with the `text` query parameter of the `GET /v1/synthesize` method:

-   Plain text input:

    ```text
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   SSML input:

    ```text
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3C
    break%20time=%225s%22/%3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another
    %20sentence.%3C/s%3E%3Cs%3EFinally,%20this%20is%20the%20last%20sentence.
    %3C/s%3E%3C/p%3E%22
    ```
    {: codeblock}

### Example input with a POST request
{: #postExamples}

The following examples pass input in the body of the `POST /v1/synthesize` method:

-   Plain text input:

    ```json
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   SSML input:

    ```json
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/>
        paragraph.</s><s>Here is another sentence.</s><s>Finally, this is
        the last sentence.</s></p>"
    }
    ```
    {: codeblock}

### Example input with XML control characters
{: #xmlExamples}

The following examples send two sentences to the `POST /v1/synthesize` method. The examples properly escape the embedded XML characters.

```text
"What have I learned?" he asked. "Everything!"
```
{: codeblock}

-   Plain text input:

    ```json
    {
      "text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
    }
    ```
    {: codeblock}

-   SSML input:

    ```json
    {
      "text": "<s>&quot;What have I learned?&quot; he asked.
        &quot;<prodody rate=\"50\">Everything!</prosody>&quot;</s>"
    }
    ```
    {: codeblock}
