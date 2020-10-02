---

copyright:
  years: 2015, 2020
lastupdated: "2020-10-01"

subcollection: text-to-speech

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:beta: .beta}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Languages and voices
{: #voices}

The {{site.data.keyword.texttospeechfull}} service supports a variety of languages, voices, and dialects. The service offers at least one female voice for each language. For some languages the service offers multiple voices, including both male and female voices. Each voice uses appropriate cadence and intonation for its dialect.
{: shortdesc}

The `V2` voices that were previously available with the service have been discontinued. If you use a `V2` voice in your application, the service automatically uses the equivalent `V3` voice instead.
{: note}

## Supported languages and voices
{: #languageVoices}

Table 1 lists and provides audio samples for the voices that are available for each language and dialect. Voices are available as [Standard voices](#standardVoices), [Neural voices](#neuralVoices), or both. If you omit the optional `voice` parameter from a synthesis request, the service uses the standard `en-US_MichaelVoice` by default.

Voices labeled *Beta* are currently beta functionality. Beta voices might not be ready for production use and are subject to change. They are initial offerings that are expected to improve in quality with time and usage. All other voices are generally available (GA) for production use.
{: beta}

| Language | Gender / Type | Voice | Sample |
|----------|:-------------:|:-----:|:------:|
| Arabic<br/>(Beta) | Male<br/>Standard | `ar-AR_OmarVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Omar.wav" type="audio/wav"></audio> |
| Brazilian<br/>Portuguese | Female<br/>Standard | `pt-BR_IsabelaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Isabela.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `pt-BR_IsabelaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/IsabelaV3.wav" type="audio/wav"></audio> |
| Chinese<br/>(Mandarin, Beta) | Female<br/>Standard | `zh-CN_LiNaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/LiNa.wav" type="audio/wav"></audio> |
| | Male<br/>Standard | `zh-CN_WangWeiVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/WangWei.wav" type="audio/wav"></audio> |
| | Female<br/>Standard | `zh-CN_ZhangJingVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/ZhangJing.wav" type="audio/wav"></audio> |
| Dutch<br/>(Beta) | Female<br/>Standard | `nl-NL_EmmaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Emma.wav" type="audio/wav"></audio> |
| | Male<br/>Standard | `nl-NL_LiamVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Liam.wav" type="audio/wav"></audio> |
| English<br/>(United Kingdom) | Female<br/>Neural | `en-GB_CharlotteV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/CharlotteV3.wav" type="audio/wav"></audio> |
| | Male<br/>Neural | `en-GB_JamesV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/JamesV3.wav" type="audio/wav"></audio> |
| | Female<br/>Standard | `en-GB_KateVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Kate.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `en-GB_KateV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/KateV3.wav" type="audio/wav"></audio> |
| English<br/>(United States) | Female<br/>Standard | `en-US_AllisonVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Allison.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `en-US_AllisonV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/AllisonV3.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `en-US_EmilyV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/EmilyV3.wav" type="audio/wav"></audio> |
| | Male<br/>Neural | `en-US_HenryV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/HenryV3.wav" type="audio/wav"></audio> |
| | Male<br/>Neural | `en-US_KevinV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/KevinV3.wav" type="audio/wav"></audio> |
| | Female<br/>Standard | `en-US_LisaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Lisa.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `en-US_LisaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/LisaV3.wav" type="audio/wav"></audio> |
| | Male<br/>Standard | `en-US_MichaelVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Michael.wav" type="audio/wav"></audio> |
| | Male<br/>Neural | `en-US_MichaelV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/MichaelV3.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `en-US_OliviaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/OliviaV3.wav" type="audio/wav"></audio> |
| French | Male<br/>Neural | `fr-FR_NicolasV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/NicolasV3.wav" type="audio/wav"></audio> |
| | Female<br/>Standard | `fr-FR_ReneeVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Renee.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `fr-FR_ReneeV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/ReneeV3.wav" type="audio/wav"></audio> |
| German | Female<br/>Standard | `de-DE_BirgitVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Birgit.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `de-DE_BirgitV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/BirgitV3.wav" type="audio/wav"></audio> |
| | Male<br/>Standard | `de-DE_DieterVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Dieter.wav" type="audio/wav"></audio> |
| | Male<br/>Neural | `de-DE_DieterV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/DieterV3.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `de-DE_ErikaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/ErikaV3.wav" type="audio/wav"></audio> |
| Italian | Female<br/>Standard | `it-IT_FrancescaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Francesca.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `it-IT_FrancescaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/FrancescaV3.wav" type="audio/wav"></audio> |
| Japanese | Female<br/>Standard | `ja-JP_EmiVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Emi.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `ja-JP_EmiV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/EmiV3.wav" type="audio/wav"></audio> |
| Korean<br/>(Beta) | Female<br/>Standard | `ko-KR_YoungmiVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Youngmi.wav" type="audio/wav"></audio> |
| | Female<br/>Standard | `ko-KR_YunaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Yuna.wav" type="audio/wav"></audio> |
| Spanish<br/>(Castilian) | Male<br/>Standard | `es-ES_EnriqueVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Enrique.wav" type="audio/wav"></audio> |
| | Male<br/>Neural | `es-ES_EnriqueV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/EnriqueV3.wav" type="audio/wav"></audio> |
| | Female<br/>Standard | `es-ES_LauraVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Laura.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `es-ES_LauraV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/LauraV3.wav" type="audio/wav"></audio> |
| Spanish<br/>(Latin American) | Female<br/>Standard | `es-LA_SofiaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Sofia.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `es-LA_SofiaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/SofiaV3.wav" type="audio/wav"></audio> |
| Spanish<br/>(North American) | Female<br/>Standard | `es-US_SofiaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/Sofia.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `es-US_SofiaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples/SofiaV3.wav" type="audio/wav"></audio> |
{: caption="Table 1. Supported languages and voices"}

The Spanish Latin American and North American `Sofia` voices are essentially the same voice. The most significant difference concerns how the two voices interpret a $ (dollar sign). The Latin American version uses the term *pesos*, while the North American version uses the term *d&oacute;lares*. Other minor differences might also exist between the two voices.
{: note}

### Standard voices
{: #standardVoices}

Standard voices do not include a version string (`V3`) in their name (for example, `pt-BR_IsabelaVoice` and `en-US_AllisonVoice`). Standard voices use concatenative synthesis to assemble segments (or units) of recorded speech to generate the requested audio. The concatenation points of the recorded segments sometimes result in speech discontinuities that can degrade the quality and naturalness of the resulting speech.

### Neural voices
{: #neuralVoices}

Neural voices include a version string (`V3`) in their name (for example, `pt-BR_IsabelaV3Voice` and `en-US_AllisonV3Voice`). Instead of relying on segment selection and concatenation, neural voice technology uses multiple Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech. The DNNs are trained on natural human speech and generate the resulting audio from the predicted acoustic features.

During synthesis, the DNNs predict the pitch and phoneme duration (prosody), spectral structure, and waveform of the speech. Neural voices produce speech that is crisp and clear, with a very natural-sounding and smooth audio quality. Thus, neural voices have greater consistency in overall quality than standard voices.

For more information about the service's neural voice technology, see

-   The blog post [{{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}}: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   The research paper [High quality, lightweight and adaptable {{site.data.keyword.texttospeechshort}} using LPCNet](https://arxiv.org/abs/1905.00590){: external}

The neural voices do not support the following SSML elements or attributes:

-   The `volume` attribute of the `<prosody>` element
-   The `<express-as>` element
-   The `<voice-transformation>` element

However, you might find that these SSML features are no longer needed when using the neural voices. Also, you can make pitch and rate modifications to neural voices by using the `<prosody>` element in place of the `<voice-transformation>` element. For more information, see [The prosody element](/docs/text-to-speech?topic=text-to-speech-elements#prosody_element).

### Customization
{: #customizeVoice}

When you synthesize text, the service applies language-dependent pronunciation rules to convert the ordinary spelling of each word to a phonetic spelling. The service's pronunciation rules work well for common words, but they can yield imperfect results for unusual words, such as terms with foreign origins, personal names, and abbreviations or acronyms.

If your application's lexicon includes such words, you can use the customization interface to specify how the service pronounces them. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

You create a custom model for a specific language, not for a specific voice. So a custom model can be used with any voice, standard or neural, for its specified language. For example, a custom model that you create for the `en-US` language can be used with any US English voice. It cannot, however, be used with an `en-GB` voice.

## Migrating from standard to neural voices
{: #migrateVoice}

Many voices are available as both standard and neural voices. To optimize the audio quality and naturalness of synthesized speech, {{site.data.keyword.IBM_notm}} recommends that you migrate from standard to neural voices whenever possible.

To migrate from a standard voice to a neural voice, complete these steps:

1.  Modify calls to the `/v1/synthesize` method.

    Change the `voice` query parameter of the `/v1/synthesize` method to specify the neural voice instead of the standard voice. For example, change

    ```xml
    voice=en-US_AllisonVoice
    ```
    {: codeblock}

    to

    ```xml
    voice=en-US_AllisonV3Voice
    ```
    {: codeblock}

1.  Eliminate the use of [Expressive SSML](/docs/services/text-to-speech?topic=text-to-speech-expressive).

    The `<express-as>` SSML element is supported only with the standard `en-US_AllisonVoice` voice. You must remove any instances of the element from input text when using neural voices. For example, change

    ```xml
    <express-as type="GoodNews">
      I have your results!
    </express-as>
    ```
    {: codeblock}

    to

    ```xml
    I have your results.
    ```
    {: codeblock}

    Because neural voices are more natural sounding, you might find that you no longer need this SSML extension.

1.  Eliminate the use of [Voice transformation SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation).

    The `<voice-transformation>` SSML element is supported only for the standard `en-US_AllisonVoice`, `en-US_LisaVoice`, and `en-US_MichaelVoice` voices. You must remove all instances of the element from input text when using neural voices.

    -  *For built-in transformations* of `type` equals `Young` or `Soft`, with or without the optional `strength` attribute, remove the `<voice-transformation>` element from the input text. For example, change

        ```xml
        <voice-transformation type="Young" strength="80%">
          Could you provide us with new information?
        </voice-transformation>
        ```
        {: codeblock}

        to

        ```xml
        Could you provide us with new information?
        ```
        {: codeblock}

    -   *For custom transformations* of `type` equals `Custom`:

        -   Remove instances of the `<voice-transformation>` element that use the `glottal_tension`, `breathiness`, `timbre`, or `timbre_extent` attributes.

        -   Change instances of the `<voice-transformation>` element that use the `pitch`, `pitch_rate`, or `rate` attributes to use the SSML `<prosody>` element instead. For more information, see [The prosody element](/docs/text-to-speech?topic=text-to-speech-elements#prosody_element).

        For example, change

        ```xml
        <voice-transformation type="Custom" glottal_tension="-50%" rate="10%">
          Do you have more information?
        </voice-transformation>
        ```
        {: codeblock}

        to

        ```xml
        <prosody rate="10%">
          Do you have more information?
        </prosody>
        ```
        {: codeblock}

## Specifying a voice
{: #specifyVoice}

Both the HTTP `GET` and `POST /v1/synthesize` methods, as well as the WebSocket `/v1/synthesize` method, accept an optional `voice` query parameter to specify the voice for the synthesized audio. For more information, see [The HTTP interface](/docs/text-to-speech?topic=text-to-speech-usingHTTP) and [The WebSocket interface](/docs/text-to-speech?topic=text-to-speech-usingWebSocket).

The service bases its understanding of the language for the input text on the specified voice. Be sure to specify a voice that matches the language of the input text. For example, if you specify the French voice `fr-FR_ReneeV3Voice`, the service expects to receive input text that is written in French. If you pass text that is not written in the language of the voice (for example, English text for the French voice), the service might not produce meaningful results.

## Listing all available voices
{: #listVoices}

The `GET /v1/voices` method lists information about all available voices. It takes no arguments and returns a JSON array that is named `voices`. The array includes a separate object for each voice.

The order in which the service returns voices can change from call to call. Do not rely on an alphabetized or static list of voices. Because the voices are returned as an array of JSON objects, the order has no bearing on programmatic uses of the response.

The following example lists all voices that are supported by the service:

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/voices"
```
{: pre}

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaV3Voice",
      "language": "en-US",
      "gender": "female",
      "url": "{url}/v1/voices/en-US_LisaV3Voice",
      "customizable": true,
      "supported_features": {
        "voice_transformation": false,
        "custom_pronunciation": true
      },
      "description": "Lisa: American English female voice.",
    },
    {
      "name": "es-LA_SofiaV3Voice",
      "language": "es-LA",
      "customizable": true,
      "gender": "female",
      "url": "{url}/v1/voices/es-LA_SofiaV3Voice",
      "supported_features": {
        "voice_transformation": false,
        "custom_pronunciation": true
      },
      "description": "Sofia: Latin American Spanish (español latinoamericano) female voice."
    },
    {
      "name": "pt-BR_IsabelaV3Voice",
      "language": "pt-BR",
      "customizable": true,
      "gender": "female",
      "url": "{url}/v1/voices/pt-BR_IsabelaV3Voice",
      "supported_features": {
        "voice_transformation": false,
        "custom_pronunciation": true
      },
      "description": "Isabela: Brazilian Portuguese (português brasileiro) female voice."
    },
    . . .
  ]
}
```
{: codeblock}

The fields of the voice objects provide the following information:

-   `name` is an identifier for the voice (for example, `en-US_LisaV3Voice`). Specify this value for the `voice` parameter of the `/v1/synthesize` method.
-   `language` specifies the language and region of the voice (for example, `en-US`).
-   `gender` identifies the voice as `male` or `female`.
-   `url` identifies the URL for the voice.
-   `description` provides a brief description of the voice.
-   `customizable` is a boolean value that indicates whether the voice can be customized with the service's customization interface. (This field, which provides the same information as the `custom_pronunciation` field, is maintained for backward compatibility.)
-   `supported_features` describes the additional service features that are supported by the voice:
    -   `voice_transformation` is a boolean value that indicates whether the voice can be transformed by using the SSML `<voice-transformation>` element.
    -   `custom_pronunciation` is a boolean value that indicates whether the voice can be customized with the service's customization interface.

## Listing a specific voice
{: #listVoice}

The `GET /v1/voices/{voice}` method lists information about a specific voice. It accepts two parameters.

-   `voice` (path parameter, *required* string) - Identifies the voice for which information is to be returned. You specify a voice by its name (for example, `en-US_LisaV3Voice`).
-   `customization_id` (query parameter, *optional* string) - Provides the globally unique identifier (GUID) of a custom model that is defined for the language of the specified voice. If you include a customization ID, you must make the request with credentials for the instance of the service that owns the custom model.

If you omit the `customization_id` parameter, the method returns JSON output for the specified voice that is identical to the information returned for a voice by the `GET /v1/voices` method. If you specify a `customization_id`, the output includes a `customization` field that provides information about the specified custom model.

The following example returns information about the `en-US_LisaV3Voice` and the specified custom model:

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/voices/en-US_LisaV3Voice?customization_id=64f4807f-a5f1-5867-924f-7bba1a84fe97"
```
{: pre}

```javascript
{
  "name": "en-US_LisaV3Voice",
  "language": "en-US",
  "gender": "female",
  "url": "{url}/v1/voices/en-US_LisaV3Voice",
  "description": "Lisa: American English female voice.",
  "customizable": true,
  "supported_features": {
    "voice_transformation": false,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

The attributes of the additional `customization` field provide information such as the GUID, name, language, and description of the custom model. They also show the credentials of the model's owner, the date and time at which the model was created, and the date and time of its last modification.
