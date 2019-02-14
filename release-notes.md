---

copyright:
  years: 2015, 2019
lastupdated: "2019-02-13"

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

# Release notes
{: #release-notes}

The following sections document the new features and changes that were included for each release and update of the {{site.data.keyword.texttospeechfull}} service. The information includes any known limitations. Unless otherwise noted, all changes are compatible with earlier releases and are automatically and transparently available to all new and existing applications.
{: shortdesc}

## Known limitations
{: #limitations}

No known limitations at this time.

## 28 January 2019
{: #January2019}

The WebSocket interface now supports token-based Identity and Access Management (IAM) authentication from browser-based JavaScript code. The limitation to the contrary has been removed. To establish an authenticated connection with the WebSocket `/v1/synthesize` method:

-   If you use IAM authentication, include the `access_token` query parameter.
-   If you use Cloud Foundry service credentials, include the `watson-token` query parameter.

For more information, see [Open a connection](/docs/services/text-to-speech/websockets.html#WSopen).

## 13 December 2018
{: #December2018}

The {{site.data.keyword.texttospeechshort}} service is now available in the {{site.data.keyword.cloud}} London location (**eu-gb**). Like all locations, London uses token-based Identity and Access Management (IAM) authentication. All new services instances that you create in this location use IAM authentication.

## 7 November 2018
{: #November2018a}

The {{site.data.keyword.texttospeechshort}} service is now available in the {{site.data.keyword.cloud}} Tokyo location (**jp-tok**). Like all locations, Tokyo uses token-based Identity and Access Management (IAM) authentication. All new services instances that you create in this location use IAM authentication.

## Older releases
{: #older}

-   [30 October 2018](#October2018)
-   [12 June 2018](#June2018)
-   [15 May 2018](#May2018)
-   [2 October 2017](#October2017)
-   [14 July 2017](#July2017)
-   [10 April 2017](#April2017)
-   [1 December 2016](#December2016)
-   [22 September 2016](/docs/services/text-to-speech/release-notes.html#September2016)
-   [23 June 2016](/docs/services/text-to-speech/release-notes.html#June2016)
-   [10 March 2016](/docs/services/text-to-speech/release-notes.html#March2016)
-   [22 February 2016](/docs/services/text-to-speech/release-notes.html#February2016)
-   [17 December 2015](/docs/services/text-to-speech/release-notes.html#December2015)
-   [21 September 2015](/docs/services/text-to-speech/release-notes.html#September2015)
-   [1 July 2015](/docs/services/text-to-speech/release-notes.html#July2015)

### 30 October 2018
{: #October2018}

The {{site.data.keyword.texttospeechshort}} service has migrated to token-based Identity and Access Management (IAM) authentication for all locations. All {{site.data.keyword.cloud_notm}} services now use IAM authentication. The {{site.data.keyword.texttospeechshort}} service migrated in each location on the following dates:

-   Dallas (**us-south**): October 30, 2018
-   Frankfurt (**eu-de**): October 30, 2018
-   Washington, DC (**us-east**): June 12, 2018
-   Sydney (**au-syd**): May 15, 2018

The migration to IAM authentication affects new and existing service instances differently:

-   *All new service instances that you create in any location* now use IAM authentication to access the service. You can pass either a bearer token or an API key: Tokens support authenticated requests without embedding service credentials in every call; API keys use HTTP basic authentication. When you use any of the {{site.data.keyword.ibmwatson}} SDKs, you can pass the API key and let the SDK manage the lifecycle of the tokens.
-   *Existing service instances that you created in a location before the indicated migration date* continue to use the `{username}` and `{password}` from their previous Cloud Foundry service credentials for authentication until you migrate them to use IAM authentication. For more information about migrating to IAM authentication, see [Migrating Cloud Foundry service instances to a resource group](https://{DomainName}/docs/resources/instance_migration.html).

For more information, see the following documentation:

-   To learn which authentication mechanism your service instance uses, view your service credentials by clicking the instance on the [{{site.data.keyword.cloud_notm}} dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/dashboard/apps){: new_window}.
-   For more information about using IAM tokens with {{site.data.keyword.watson}} services, see [Authenticating with IAM tokens](/docs/services/watson/getting-started-iam.html).
-   For more information about using IAM API keys with {{site.data.keyword.watson}} services, see [IAM service API keys](/docs/services/watson/apikey-bp.html).
-   For examples that use IAM authentication, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

### 12 June 2018
{: #June2018}

The following features are enabled for applications that are hosted in Washington, DC (**us-east**):

-   The service now supports a new API authentication process. For more information, see the [30 October 2018 service update](#October2018).
-   The service now supports the `X-Watson-Metadata` header and the `DELETE /v1/user_data` method. For more information, see [Information security](/docs/services/text-to-speech/information-security.html).

### 15 May 2018
{: #May2018}

The following features are enabled for applications that are hosted in Sydney (**au-syd**):

-   The service now supports a new API authentication process. For more information, see the [30 October 2018 service update](#October2018).
-   The service now supports the `X-Watson-Metadata` header and the `DELETE /v1/user_data` method. For more information, see [Information security](/docs/services/text-to-speech/information-security.html).

### 2 October 2017
{: #October2017}

For the `audio/l16` format, you can now optionally specify the endianness of the audio that is returned. (You must already specify the sampling rate.) Examples are `audio/l16;rate=22050;endianness=big-endian` and `audio/l16;rate=22050;endianness=little-endian`; the default is big endian. For more information, see [Audio formats](/docs/services/text-to-speech/audio-formats.html).

### 14 July 2017
{: #July2017}

The service now supports the MP3 or Motion Picture Experts Group (MPEG) audio format. For more information about supported audio formats, see [Audio formats](/docs/services/text-to-speech/audio-formats.html).

### 10 April 2017
{: #April2017}

-   The service now supports the Web Media (WebM) audio format with the Opus or Vorbis codec. The service now also supports the Ogg audio format with the Vorbis codec in addition to the Opus codec. For more information about supported audio formats, see [Audio formats](/docs/services/text-to-speech/audio-formats.html).
-   The service now supports Cross-Origin Resource Sharing (CORS) to allow browser-based clients to call the service directly. For more information, see [CORS support](/docs/services/text-to-speech/developer-overview.html#cors).
-   The HTTP response codes for successful completion of some methods of the customization interface changed:
    -   The `POST /v1/customizations` method now returns 201 (instead of 200).
    -   The `POST /v1/customizations/{customization_id}` method now returns 200 (instead of 201).
    -   The `POST /v1/customizations/{customization_id}/words` method now returns 200 (instead of 201).
    -   The `PUT /v1/customizations/{customization_id}/words/{word}` method now returns 200 (instead of 201).
-   The `POST /v1/customizations/{custom_id}/words` and `PUT /v1/customizations/{customization_id}/words/{word}` methods now return HTTP response code 400 with the error message `Part of speech is supported for ja-JP language only` if you attempt to specify a `part_of_speech` for a language other than Japanese.
-   The `POST /v1/customizations/{custom_id}/words` method now returns an empty response body (`{}`).

### 1 December 2016
{: #December2016}

-   The service includes a new voice, `es-LA_SofiaVoice`, which is the Latin American equivalent of the `es-US_SofiaVoice` voice. The most significant difference between the two voices concerns how they interpret a `$` (dollar sign): The Latin American version uses the term *pesos*, while the North American version uses the term *dolares*. Other minor differences might also exist between the two voices.
-   In addition to the `en-US_AllisonVoice`, two more voices are now transformable with SSML voice transformation: `en-US_LisaVoice` and `en-US_MichaelVoice`. For more information about voice transformation, see [Voice transformation SSML](/docs/services/text-to-speech/SSML-transformation.html).
-   When you use the customization interface with Japanese, the service now matches the longest word from the word/translation pairs that are defined for a custom voice model. For example, consider the following two entries for a custom voice:

    <pre><code data-copy="false" class="language-javascript">  {
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    If the service finds the string <code>&#65326;&#65337;&#65315;</code> in the input text, it matches that word because it is a longer match than <code>&#65326;&#65337;</code>. Previously, the service would have matched the string <code>&#65326;&#65337;</code>. For more information about working with Japanese entries for a custom voice model, see [Working with Japanese entries](/docs/services/text-to-speech/custom-rules.html#jaNotes).

### 22 September 2016
{: #September2016}

-   The customization interface, which includes the customization and `GET /v1/pronunciation` methods, is now available for all languages that are supported by the service. The interface remains a beta release. For more information, see [Understanding customization](/docs/services/text-to-speech/custom-intro.html).
-   The service now supports the Speech Synthesis Markup Language (SSML) for Japanese. For general information about SSML support, see [Using SSML](/docs/services/text-to-speech/SSML.html). For information about Japanese SPR and IPA symbols, see [Japanese symbols](/docs/services/text-to-speech/ja-JP-SPRs.html). Extra considerations and a `part_of_speech` field apply when creating entries for words in a Japanese custom voice model. For more information, see [Working with Japanese entries](/docs/services/text-to-speech/custom-rules.html#jaNotes).
-   The service now offers SSML voice transformation via the new `<voice-transformation>` element. You can expand the range of possible voices by creating custom voice transformations that modify the pitch, pitch range, glottal tension, breathiness, rate, and timbre of a voice. The service also offers two built-in virtual voices, *Young* and *Soft*. The service currently supports voice transformation only for the US English Allison voice. For more information, see [Voice transformation SSML](/docs/services/text-to-speech/SSML-transformation.html).
-   The service can now return word timing information for all strings of the input text that you pass to the WebSocket interface. To receive the start and end time of every string in the input, specify an array that includes the string `words` for the optional `timings` parameter of the JSON object that you pass to the service. The feature is not currently available for Japanese input text. For more information, see [Obtaining word timings](/docs/services/text-to-speech/word-timing.html).
-   The service now validates all SSML elements that you submit in any context. If it finds an invalid tag, the service reports an HTTP 400 response code with a descriptive message, and the method fails. In previous releases, the service handled errors inconsistently; specifying an invalid word pronunciation, for example, could lead to unpredictable or inconsistent behavior. For more information, see [SSML validation](/docs/services/text-to-speech/SSML.html#errors).
-   The use of `spr` is deprecated as an argument to the `format` option of the `GET /v1/pronunciation` method and for use with the `alphabet` attribute of an SSML `<phoneme>` element. To use {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) notation, use the `ibm` argument instead of `spr` in all cases.
-   The list of supported audio formats now includes `audio/mulaw;rate=8000`. Like `audio/basic`, this format provides single-channel audio that is encoded by using 8-bit u-law (or mu-law) data that is sampled at 8 kHz. For more information, see [Audio formats](/docs/services/text-to-speech/audio-formats.html).
-   The `GET /v1/voices` and `GET /v1/voices/{voice}` methods now return a `supported_features` object as part of their output for each voice. The object describes whether the voice supports customization and the SSML `<voice_transformation>` element. For more information, see [Languages and voices](/docs/services/text-to-speech/voices.html).

### 23 June 2016
{: #June2016}

-   The service now offers a WebSocket interface for synthesizing text to speech. The interface offers the same features as the `/v1/synthesize` method of the HTTP interface. It accepts plain text or text that is marked up with SSML. In addition, it also supports use of the SSML `<mark>` element to identify the time in the audio at which it finishes synthesizing all text that precedes the mark. For more information, see [The WebSocket interface](/docs/services/text-to-speech/websockets.html).
-   The service now offers support for text that is annotated with SSML for the languages Castilian and North American Spanish, Italian, and Brazilian Portuquese. The service already supported the use of SSML for US and British English, French, and German. As of this update, the service supports SSML for all languages but Japanese. Moreover, you can use both {{site.data.keyword.IBM_notm}} SPR and IPA notations to define word pronunciations with the SSML `<phoneme>` element. For more information, see [Using SSML](/docs/services/text-to-speech/SSML.html) and [Using IBM SPR](/docs/services/text-to-speech/SPRs.html).

    For US English, you can also use the SSML `<phoneme>` element to create word entries in a custom voice model; customization is supported only for US English. For more information, see [Understanding customization](/docs/services/text-to-speech/custom-intro.html).
-   The service features improved expressiveness and naturalness for the most frequently used voices. The improvements are based on Recursive Neural Network (RNN)-based prosody prediction from input text. They are made available as a new service engine and voice-model updates for the following languages:

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   The `GET /v1/pronunciation` method now accepts an optional `customization_id` query parameter. The parameter obtains a word translation from a specified custom voice model. If the voice model does not contain the word, the method returns the word's default pronunciation. For more information, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

    When using the `GET /v1/pronunciation` method without a customization ID and for a language other than US English, you can request a word's pronunciation only in {{site.data.keyword.IBM_notm}} SPR notation. For a language other than US English, you must specify `spr` with the method's `format` option.
    {: note}
-   The list of supported audio formats now includes `audio/basic`, which provides single-channel audio that is encoded using 8-bit u-law (or mu-law) data that is sampled at 8 kHz. For more information, see [Audio format](/docs/services/text-to-speech/audio-formats.html).
-   The HTTP and WebSocket `/v1/synthesize` methods can return a `warnings` response that includes messages about invalid query parameters or JSON fields that are included with a request. The format of the warnings changed. The following example shows the previous format:

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    The same warning now has the following format:

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

### 10 March 2016
{: #March2016}

-   The `GET` and `POST /v1/synthesize` methods can now return a `Warnings` response header that includes a list of warning messages about invalid query parameters or JSON fields that are included with the request. Each element of the list includes a string that describes the nature of the warning followed by an array of invalid argument strings; for example, `Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}'].` For more information, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/text-to-speech){: new_window}.
-   The beta *{{site.data.keyword.watson}} Speech Software Development Kit (SDK) for the Apple&reg; iOS operating system* is deprecated and replaced by the *{{site.data.keyword.watson}} Swift SDK*. The new SDK is available from the [swift-sdk repository ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} in the `watson-developer-cloud` namespace on GitHub.

### 22 February 2016
{: #February2016}

The service was updated with a new expressive SSML feature. The service extends the Speech Synthesis Markup Language (SSML) with an `<express-as>` element that you can use to indicate expressiveness in one of three speaking styles: `GoodNews`, `Apology`, or `Uncertainty`. You can apply the element to the entire body of the text, a sentence, a phrase, or a word. The service currently supports expressiveness only for the US English Allison voice (`en-US_AllisonVoice`). For more information, see [Expressive SSML](/docs/services/text-to-speech/SSML-expressive.html).

### 17 December 2015
{: #December2015}

-   The service offers a new customization interface that you can use to specify how it pronounces unusual words that occur in your input. The interface includes a number of new methods that you can use to create and manage custom voice models and the word/translation pairs that they contain. You can then use your custom models when synthesizing text to audio.

    The service supports sounds-like translations and phonetic translations. Phonetic translations can use either the standard International Phonetic Alphabet (IPA) representation or the proprietary {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). You use the Speech Synthesis Markup Language (SSML) to specify phonetic translations.

    The customization interface includes a collection of new HTTP methods that have the names `POST /v1/customizations`, `POST /v1/customizations/{customization_id}`, `POST /v1/customizations/{customization_id}/words`, and `PUT /v1/customizations/{customization_id}/words/{word}`. The service also provides a new `GET /v1/pronunciation` method that returns the pronunciation for any word and a new `GET /v1/voices/{voice}` method that returns detailed information about a specific voice. In addition, existing methods of the service's interface now accept custom voice model parameters as needed.

    For more information about customization and its interface, see [Understanding customization](/docs/services/text-to-speech/custom-intro.html) and the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

    The customization interface is a beta release that currently supports US English only. All customization methods and the `GET /v1/pronunciation` method can currently be used to create and manipulate custom voice models and word translations only in US English.
    {: note}
-   The service supports a new voice, `pt-BR_IsabelaVoice`, to synthesize audio in Brazilian Portuguese with a female voice. For more information, see [Languages and voices](/docs/services/text-to-speech/voices.html).

### 21 September 2015
{: #September2015}

-   Two new beta mobile Software Development Kits (SDKs) are available for the speech services. The SDKs enable mobile applications to interact with both the {{site.data.keyword.texttospeechshort}} and {{site.data.keyword.speechtotextshort}} services. You can use the SDKs to send text to the {{site.data.keyword.texttospeechshort}} service and receive an audio response.
    -   The *{{site.data.keyword.watson}} Swift SDK* is available from the [swift-sdk repository ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} in the `watson-developer-cloud` namespace on GitHub.
    -   The *{{site.data.keyword.watson}} Speech Android SDK* is available from the [speech-android-sdk repository ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/speech-android-sdk){: new_window} in the `watson-developer-cloud` namespace on GitHub.

    Both SDKs support authenticating with the speech services by using either your {{site.data.keyword.cloud_notm}} service credentials or an authentication token.

    Because the SDKs are beta functionality, they are subject to change in the future.
    {: note}
-   The service supports a new language, Japanese. The voice `ja-JP_EmiVoice` is a Japanese female voice.

### 1 July 2015
{: #July2015}

The service moved from beta to general availability (GA) on July 1, 2015. The following differences existed between the beta and GA versions of the {{site.data.keyword.texttospeechshort}} API. The GA release required that users upgrade to the new version of the service.

-   A new programming model supports direct interaction between a client and the service. By using this model, a client can obtain an authentication token for communicating directly with the service. By using the token, the client can bypass the need for a server-side proxy application in {{site.data.keyword.cloud_notm}} to call the service on its behalf. Tokens are the preferred means for clients to interact with the service.

    The service continues to support the old programming model that relied on a server-side proxy to relay communications and data between the client and the service. But the new model is more efficient and provides higher throughput. For more information about the new programming model, see [Programming models for {{site.data.keyword.watson}} services](/docs/services/watson/getting-started-develop.html).
-   You can now pass Speech Synthesis Markup Language (SSML) to the HTTP `GET` and `POST` versions of the `/v1/synthesize` method. SSML is an XML-based markup language that is designed to provide annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service. For more information about passing SSML input to the service, see [Specifying input text](/docs/services/text-to-speech/http.html#input).

    The service initially supports the use of SSML only for the British and US English, French, and German languages. The service does not support SSML for use with Italian and Spanish. When you use SSML, make sure that you do not select a voice for the audio in one of the unsupported languages. Results in this case are not meaningful.
-   The voices that are supported for synthesized speech changed and expanded. The service now supports a number of additional voices, languages, and dialects with the `/v1/synthesize` methods. For more information about supported voices, see [Languages and voices](/docs/services/text-to-speech/voices.html).

    The three voices that were available at beta are renamed for GA:
    -   `VoiceEnUsMichael` is now `en-US_MichaelVoice`
    -   `VoiceEnUsLisa` is now `en-US_LisaVoice`
    -   `VoiceEsEsEnrique` is now `es-ES_EnriqueVoice`

    The previous names of the voices continue to work with the beta version of the service (via `-beta` API endpoints) while that version remains available. However, you must use the new names with the GA version of the service.
-   You can now request the service to return audio in the Free Lossless Audio Codec (FLAC) format. The service can still return audio in the Ogg format with the Opus codec (the default) and in the Waveform Audio File Format (WAV). For more information about using audio formats with the `/v1/synthesize` methods, see [Audio formats](/docs/services/text-to-speech/audio-formats.html).
-   The text that you send to the `/v1/synthesize` method in the URL of an HTTP `GET` request or in the body of an HTTP `POST` request is now limited to a maximum of 5 KB. The text had a maximum size of 4 MB for the beta version.
-   The `/v1/synthesize` methods now include the header `X-WDC-PL-OPT-OUT` to control whether the service uses the text and audio results from an operation to improve future results. Specify a value of `1` for the header to prevent the service from using text and audio results. The parameter applies only to the current request. The new header replaces the `X-logging` header from the beta methods. For more information, see [Controlling request logging for {{site.data.keyword.watson}} services](/docs/services/watson/getting-started-logging.html).
-   For the `/v1/synthesize` methods, the following error codes changed:
    -   Error code 406 ("Not acceptable. Unsupported MIME type.") is removed.
    -   Error code 415 ("Unsupported Media Type") is added.
    -   Error code 503 ("Service Unavailable") is added.
-   For the `GET /v1/voices` method, the following error codes changed:
    -   Error code 406 ("Not acceptable. Unsupported MIME type.") is removed.
    -   Error code 415 ("Unsupported Media Type") is added.
