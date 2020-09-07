---

copyright:
  years: 2015, 2020
lastupdated: "2020-09-06"

subcollection: text-to-speech

---

{:help: data-hd-content-type='help'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:support: data-reuse='support'}
{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
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

# The HTTP interface
{: #usingHTTP}

To synthesize text to speech with the HTTP REST interface of the {{site.data.keyword.texttospeechfull}} service, you call the `GET` or `POST /v1/synthesize` method. You specify the text that is to be synthesized and the voice and format for the spoken audio. You can also specify a custom voice model that is to be used with the request.
{: shortdesc}

For more information about the HTTP interface, see the [API reference](https://{DomainName}/apidocs/text-to-speech){: external}.

## Synthesizing text to audio
{: #synthesize}
{: help}
{: support}

To synthesize text to audio, you call one of the two versions of the service's `/v1/synthesize` method:

-   The `GET /v1/synthesize` method accepts the text that is to be synthesized as a required `text` query parameter. The maximum size of the request is 8 KB, which includes the input text, any SSML that you specify, and the URL and headers.
-   The `POST /v1/synthesize` method accepts the text that is to be synthesized as a JSON construct in the required body of the request. The maximum size of the request is 8 KB for the URL and headers, and 5 KB for the input text that is sent in the body of the request. The 5 KB limit includes any SSML that you specify.

The two versions of the `/v1/synthesize` method have the following parameters in common:

-   `accept` (query parameter, *optional* string) - Specifies the requested audio format, or MIME type, in which the service is to return the audio. You can also specify this value with the HTTP `Accept` request header. URL-encode the argument to the `accept` query parameter. For more information, see [Audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats).
-   `voice` (query parameter, *optional* string) - Specifies the voice in which the text is to be spoken in the audio. Use the `/v1/voices` method to get the current list of supported voices. The default voice is `en-US_MichaelVoice`. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).
-   `customization_id` (query parameter, *optional* string) - Specifies a globally unique identifier (GUID) for a custom voice model that is to be used for the synthesis. A specified custom voice model must match the language of the voice that is used for the synthesis. If you include a customization ID, you must make the request with credentials for the instance of the service that owns the custom model. Omit the parameter to use the specified voice with no customization. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).
-   `X-Watson-Learning-Opt-Out` (request header, *optional* boolean) - Indicates whether the service logs request and response data to improve the service for future users. To prevent IBM from accessing your data for general service improvements, specify `true` for the parameter. For more information, see [Controlling request logging for {{site.data.keyword.watson}} services](/docs/watson?topic=watson-gs-logging-overview).
-   `X-Watson-Metadata` (request header, *optional* string) - Associates a customer ID with data that is passed with a request. For more information, see [Information security](/docs/text-to-speech?topic=text-to-speech-information-security).

If you specify an invalid query parameter or JSON field as part of the input to the `/v1/synthesize` method, the service returns a `Warnings` response header that describes and lists each invalid argument. The request succeeds despite the warnings.

## Specifying input text
{: #input}
{: help}
{: support}

Both the `GET` and `POST /v1/synthesize` methods accept plain input text or text that is annotated with SSML. The two versions differ primarily in how you specify the text that is to be synthesized:

-   The `GET /v1/synthesize` method accepts input text that is specified by the `text` query parameter. You specify the input as plain text or as SSML, both of which must be URL-encoded.
-   The `POST /v1/synthesize` method accepts input text in the body of the request. You specify the input with the following simple JSON construct that encapsulates plain text or SSML. You must also specify a value of `application/json` for the `Content-Type` header.

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

Although the `GET` and `POST` methods offer equivalent functionality, it is always more secure to pass input text to the service with the `POST` method. A `POST` request passes input in the body of the request, while a `GET` request exposes the data in the URL.

## Specifying SSML input
{: #ssml-http}

The Speech Synthesis Markup Language (SSML) is an XML-based markup language that is designed to provide annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service. You can use SSML elements and their attributes to gain greater control over the synthesis and resulting audio output.

For more information about using SSML to annotate input text, see [Using SSML](/docs/text-to-speech?topic=text-to-speech-ssml). The documentation inventories the SSML elements and attributes that are supported by the service. It also documents the service's expressive and voice-transformation extensions.

## Escaping XML control characters
{: #escape}
{: troubleshoot}
{: support}

Because you can submit input text that includes XML-based SSML annotations, the service validates all input to ensure that any SSML is correct and well formed. Therefore, you must escape any XML control characters that are present in the input text, regardless of whether the input includes SSML. Use the equivalent escape strings or character encodings from Table 2 instead of the indicated characters.

| Character | Escape strings | Character encoding |
|:---------:|:--------------:|:------------------:|
| `"`<br/>(double quotes) | `&quot;` | `&#34;` |
| `'`<br/>(apostrophe or single quote) | `&apos;` | `&#39;` |
| `&`<br/>(ampersand) | `&amp;` | `&#38;` |
| `<`<br/>(left angle bracket) | `&lt;` | `&#60;` |
| `>`<br/>(right angle bracket) | `&gt;` | `&#62;` |
{: caption="Table 1. Escaping XML control characters"}

For more information about how the service validates input text, see [SSML validation](/docs/text-to-speech?topic=text-to-speech-ssml#errors).

## Examples of input text
{: #httpExamples}

The following examples show how to specify input text with either method of the HTTP interface. They also show how to escape XML control characters. The examples include line breaks for readability. Do *not* include the line breaks in actual input.

### Example input with a GET request
{: #getExamples}

The following examples pass URL-encoded input with the `text` query parameter of the `GET /v1/synthesize` method:

-   Plain text input:

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   SSML input:

    ```
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

    ```javascript
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   SSML input:

    ```javascript
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

```
"What have I learned?" he asked. "Everything!"
```
{: codeblock}

-   Plain text input:

    ```javascript
    {
      "text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
    }
    ```
    {: codeblock}

-   SSML input:

    ```javascript
    {
      "text": "<s>&quot;What have I learned?&quot; he asked.
        &quot;<express-as type=\"GoodNews\">Everything!</express-as>&quot;</s>"
    }
    ```
    {: codeblock}
