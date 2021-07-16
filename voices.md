---

copyright:
  years: 2015, 2021
lastupdated: "2021-07-08"

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

The {{site.data.keyword.texttospeechfull}} service supports a variety of languages, voices, and dialects. The service offers female and male voices for different language. Each voice uses appropriate cadence and intonation for its dialect.
{: shortdesc}

## Supported languages and voices
{: #languageVoices}

The list of available voices underwent many changes on 2 December 2020. For example, to optimize the audio quality and naturalness of synthesized speech, the standard (concatenative) voices that were previously available with the service are now deprecated. For more information about the changes and the implications for voice availability and usage, see the [2 December 2020 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#December2020) in the release notes.
{: important}

Table 1 lists and provides audio samples for the voices that are available for each language and dialect.

-   All voices use [Neural voice technology](#neuralVoices). Voices are classified into two types based on their quality and functionality: neural voices and enhanced neural voices.
-   All voices are generally available (GA) for production use.

If you omit the optional `voice` parameter from a synthesis request, the service uses `en-US_MichaelV3Voice` by default.

| Language | Gender / Type | Voice | Sample |
|----------|:-------------:|:-----:|:------:|
| Arabic | Male<br/>Neural | `ar-MS_OmarVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Omar.wav" type="audio/wav"></audio> |
| Brazilian<br/>Portuguese | Female<br/>Enhanced neural | `pt-BR_IsabelaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/IsabelaV3.wav" type="audio/wav"></audio> |
| Chinese<br/>(Mandarin) | Female<br/>Neural | `zh-CN_LiNaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/LiNa.wav" type="audio/wav"></audio> |
| | Male<br/>Neural | `zh-CN_WangWeiVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/WangWei.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `zh-CN_ZhangJingVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/ZhangJing.wav" type="audio/wav"></audio> |
| Dutch<br/>(Belgian) | Neural | `nl-BE_AdeleVoice`<br/>Female | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Adele.wav" type="audio/wav"></audio> |
| Dutch<br/>(Netherlands) | Female<br/>Neural | `nl-NL_EmmaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Emma.wav" type="audio/wav"></audio> |
| | Male<br/>Neural | `nl-NL_LiamVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Liam.wav" type="audio/wav"></audio> |
| English<br/>(Australian) | Male<br/>Neural | `en-AU_CraigVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Craig.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `en-AU_MadisonVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Madison.wav" type="audio/wav"></audio> |
| English<br/>(United Kingdom) | Female<br/>Enhanced neural | `en-GB_CharlotteV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/CharlotteV3.wav" type="audio/wav"></audio> |
| | Male<br/>Enhanced neural | `en-GB_JamesV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/JamesV3.wav" type="audio/wav"></audio> |
| | Female<br/>Enhanced neural | `en-GB_KateV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/KateV3.wav" type="audio/wav"></audio> |
| English<br/>(United States) | Female<br/>Enhanced neural | `en-US_AllisonV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/AllisonV3.wav" type="audio/wav"></audio> |
| | Female<br/>Enhanced neural | `en-US_EmilyV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/EmilyV3.wav" type="audio/wav"></audio> |
| | Male<br/>Enhanced neural | `en-US_HenryV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/HenryV3.wav" type="audio/wav"></audio> |
| | Male<br/>Enhanced neural | `en-US_KevinV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/KevinV3.wav" type="audio/wav"></audio> |
| | Female<br/>Enhanced neural | `en-US_LisaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/LisaV3.wav" type="audio/wav"></audio> |
| | Male<br/>Enhanced neural | `en-US_MichaelV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/MichaelV3.wav" type="audio/wav"></audio> |
| | Female<br/>Enhanced neural | `en-US_OliviaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/OliviaV3.wav" type="audio/wav"></audio> |
| French | Male<br/>Enhanced neural | `fr-FR_NicolasV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/NicolasV3.wav" type="audio/wav"></audio> |
| | Female<br/>Enhanced neural | `fr-FR_ReneeV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/ReneeV3.wav" type="audio/wav"></audio> |
| French<br/>(Canadian) | Female<br/>Enhanced neural | `fr-FR_LouiseV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/LouiseV3.wav" type="audio/wav"></audio> |
| German | Female<br/>Enhanced neural | `de-DE_BirgitV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/BirgitV3.wav" type="audio/wav"></audio> |
| | Male<br/>Enhanced neural | `de-DE_DieterV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/DieterV3.wav" type="audio/wav"></audio> |
| | Female<br/>Enhanced neural | `de-DE_ErikaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/ErikaV3.wav" type="audio/wav"></audio> |
| Italian | Female<br/>Enhanced neural | `it-IT_FrancescaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/FrancescaV3.wav" type="audio/wav"></audio> |
| Japanese | Female<br/>Enhanced neural | `ja-JP_EmiV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/EmiV3.wav" type="audio/wav"></audio> |
| Korean | Male<br/>Neural | `ko-KR_HyunjunVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Hyunjun.wav" type="audio/wav"></audio> |
| | Male<br/>Neural | `ko-KR_SiWooVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/SiWoo.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `ko-KR_YoungmiVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Youngmi.wav" type="audio/wav"></audio> |
| | Female<br/>Neural | `ko-KR_YunaVoice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Yuna.wav" type="audio/wav"></audio> |
| Spanish<br/>(Castilian) | Male<br/>Enhanced neural | `es-ES_EnriqueV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/EnriqueV3.wav" type="audio/wav"></audio> |
| | Female<br/>Enhanced neural | `es-ES_LauraV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/LauraV3.wav" type="audio/wav"></audio> |
| Spanish<br/>(Latin American) | Female<br/>Enhanced neural | `es-LA_SofiaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/SofiaV3.wav" type="audio/wav"></audio> |
| Spanish<br/>(North American) | Female<br/>Enhanced neural | `es-US_SofiaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/SofiaV3.wav" type="audio/wav"></audio> |
{: caption="Table 1. Supported languages and voices"}

The Spanish Latin American and North American `Sofia` voices are essentially the same voice. The most significant difference concerns how the two voices interpret a $ (dollar sign). The Latin American version uses the term *pesos*; the North American version uses the term *d&oacute;lares*. Other minor differences might also exist between the two voices.
{: note}

### Neural voice technology
{: #neuralVoices}

All of the service's voices are neural voices. The service's now-deprecated standard voices relied on segment selection and concatenation. Neural voice technology instead uses multiple Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech. The DNNs are trained on natural human speech and generate the resulting audio from the predicted acoustic features.

During synthesis, the DNNs predict the pitch and phoneme duration (prosody), spectral structure, and waveform of the speech. Neural voices produce speech that is crisp and clear, with a very natural-sounding, smooth, and consistent audio quality.

The service offers two types of neural voices:

-   *Neural voices* do *not* include the string `V3` in their names. All voices for Arabic, Australian English, Chinese, Dutch, and Korean are neural voices.
-   *Enhanced neural voices* include the string `V3` in their names. All voices for Brazilian Portuguese, United Kingdom and United States English, French, German, Italian, Japanese, and Spanish (all dialects) are enhanced neural voices.

Enhanced neural voices achieve a slightly higher degree of natural-sounding speech. Enhanced neural voices support both IPA and SPR for word and phoneme customization; neural voices support only IPA. Further customization capabilities will be exposed for enhanced neural voices in the coming months.

For more information about the service's neural voice technology, see

-   The blog post [{{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}}: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   The research paper [High quality, lightweight and adaptable {{site.data.keyword.texttospeechshort}} using LPCNet](https://arxiv.org/abs/1905.00590){: external}

### Customization
{: #customizeVoice}

When you synthesize text, the service applies language-dependent pronunciation rules to convert the ordinary spelling of each word to a phonetic spelling. The service's pronunciation rules work well for common words, but they can yield imperfect results for unusual words, such as terms with foreign origins, personal names, and abbreviations or acronyms. If your application's lexicon includes such words, you can use the customization interface to specify how the service pronounces them.

You create a custom model for a specific language, not for a specific voice. So a custom model can be used with any voice for its specified language. For example, a custom model that you create for the `en-US` language can be used with any US English voice. It cannot, however, be used with an `en-GB` or `en-AU` voice.

Customization is available for all languages. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

## Migrating from standard to neural voices
{: #migrateVoice}

To optimize the audio quality and naturalness of synthesized speech, the standard (concatenative) voices that were previously available with the service are deprecated as of 2 December 2020. {{site.data.keyword.IBM_notm}} recommends that you migrate from standard to neural voices at your earliest convenience. For more information about the changes and the implications for voice synthesis, see the [2 December 2020 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#December2020) in the release notes.
{: important}

If you previously used any of the now-deprecated standard voices, you might have used the following features:

-   The `<express-as>` element. This feature was available only for the standard US English voice `en-US_AllisonVoice`.
-   The `<voice-transformation>` element. This feature was available only for the standard US English voices `en-US_AllisonVoice`, `en-US_LisaVoice`, and `US_MichaelVoice`.
-   The `volume` attribute of the `<prosody>` element. This attribute was available for all standard voices.

These SSML features are not available for neural voices. However, you might find that these features are no longer needed when using neural voices. Also, you can make pitch and rate modifications to neural voices by using the `<prosody>` element in place of the `<voice-transformation>` element. For more information, see [The prosody element](/docs/text-to-speech?topic=text-to-speech-elements#prosody_element).

To migrate from a standard voice to a neural voice, complete these steps:

1.  Modify calls to the `/v1/synthesize` method. Change the `voice` query parameter of the `/v1/synthesize` method to specify the neural voice instead of the standard voice. For example, change

    ```sh
    voice=en-US_AllisonVoice
    ```
    {: codeblock}

    to

    ```sh
    voice=en-US_AllisonV3Voice
    ```
    {: codeblock}

1.  Eliminate the use of *Expressive SSML*. The `<express-as>` SSML element was supported only with the standard `en-US_AllisonVoice` voice. You must remove any instances of the element from input text when using neural voices. For example, change

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

1.  Eliminate the use of *Voice transformation SSML*. The `<voice-transformation>` SSML element was supported only for the standard `en-US_AllisonVoice`, `en-US_LisaVoice`, and `en-US_MichaelVoice` voices. You must remove all instances of the element from input text when using neural voices.

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

1.  Eliminate the use of the `volume` attribute of the SSML `<prosody>` element. The `volume` attribute was supported only for standard voices. For example, change

    ```xml
    <prosody rate="50%" volume="75">
      Let me say that again.
    </prosody>
    ```
    {: codeblock}

    to

    ```xml
    <prosody rate="50%">
      Let me say that again.
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
    -   `voice_transformation` is a boolean value that indicates whether the voice can be transformed by using the SSML `<voice-transformation>` element. The feature was available only for now-deprecated standard US English voices. You cannot use voice transformation with neural voices.
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

The attributes of the additional `customization` field provide metadata information such as the GUID, name, language, and description of the custom model. They also show the credentials of the model's owner, the date and time at which the model was created, and the date and time of its last modification. To see the custom words and prompts that the model includes, use the `GET /v1/customizations/{customization_id}` method. For more information, see [Querying a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery).
