---

copyright:
  years: 2010, 2021
lastupdated: "2021-10-13"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Using languages and voices
{: #voices}

The {{site.data.keyword.texttospeechfull}} service supports a variety of languages, voices, and dialects. The service offers female and male voices for different language. Each voice uses appropriate cadence and intonation for its dialect.
{: shortdesc}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only.** The list of available voices underwent many changes on 2 December 2020. To optimize the audio quality and naturalness of synthesized speech, the standard (concatenative) voices that were previously available with the service are now deprecated. {{site.data.keyword.IBM_notm}} recommends that you migrate from standard to neural voices at your earliest convenience. For more information about the changes and implications for voice synthesis, see the [2 December 2020 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-2december2020) in the release notes. For information about moving to neural voices, see [Migrating from standard to neural voices](#migrate-voice).
{: important}

## Supported languages and voices
{: #language-voices}

Table 1 lists and provides audio samples for the voices that are available for each language and dialect. All voices are generally available (GA) for production use. The default voice for speech synthesis is `en-US_MichaelV3Voice`. For more information, see [Specifying a voice for speech synthesis](#specify-voice).

All voices use [Neural voice technology](#neural-voices). Voices are classified into two types based on their quality, capabilities, and availability:

-   *Enhanced neural voices* are available for both {{site.data.keyword.cloud}} and {{site.data.keyword.icp4dfull}}.
-   *Neural voices* are available only for {{site.data.keyword.cloud_notm}}.

Unless it is labeled in the *Type / Availability* column as restricted to just one version of the service, a voice is available with both {{site.data.keyword.cloud}} and {{site.data.keyword.icp4dfull}}.

| Language | Type / Availability | Voice / Gender | Sample |
|----------|:-------------------:|:--------------:|:------:|
| Arabic | Neural<br/>{{site.data.keyword.cloud_notm}} only | `ar-MS_OmarVoice`<br/>Male | ![ar-MS_OmarVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Omar.wav){: audio controls} |
| Chinese<br/>(Mandarin) | Neural<br/>{{site.data.keyword.cloud_notm}} only | `zh-CN_LiNaVoice`<br/>Female | ![zh-CN_LiNaVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/LiNa.wav){: audio controls} |
| | Neural<br/>{{site.data.keyword.cloud_notm}} only | `zh-CN_WangWeiVoice`<br/>Male | ![zh-CN_WangWeiVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/WangWei.wav){: audio controls} |
| | Neural<br/>{{site.data.keyword.cloud_notm}} only | `zh-CN_ZhangJingVoice`<br/>Female | ![zh-CN_ZhangJingVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/ZhangJing.wav){: audio controls} |
| Dutch<br/>(Belgian) | Neural<br/>{{site.data.keyword.cloud_notm}} only | `nl-BE_AdeleVoice`<br/>Female | ![nl-BE_AdeleVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Adele.wav){: audio controls} |
| Dutch<br/>(Netherlands) | Neural<br/>{{site.data.keyword.cloud_notm}} only | `nl-NL_EmmaVoice`<br/>Female | ![nl-NL_EmmaVoive sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Emma.wav){: audio controls} |
| | Neural<br/>{{site.data.keyword.cloud_notm}} only | `nl-NL_LiamVoice`<br/>Male | ![nl-NL_LiamVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Liam.wav){: audio controls} |
| English<br/>(Australian) | Neural<br/>{{site.data.keyword.cloud_notm}} only | `en-AU_CraigVoice`<br/>Male | ![en-AU_CraigVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Craig.wav){: audio controls} |
| | Neural<br/>{{site.data.keyword.cloud_notm}} only | `en-AU_MadisonVoice`<br/>Female | ![en-AU_MadisonVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Madison.wav){: audio controls} |
| English<br/>(United Kingdom) | Enhanced neural | `en-GB_CharlotteV3Voice`<br/>Female | ![en-GB_CharlotteV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/CharlotteV3.wav){: audio controls} |
| | Enhanced neural | `en-GB_JamesV3Voice`<br/>Male | ![en-GB_JamesV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/JamesV3.wav){: audio controls} |
| | Enhanced neural | `en-GB_KateV3Voice`<br/>Female | ![en-GB_KateV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/KateV3.wav){: audio controls} |
| English<br/>(United States) | Enhanced neural | `en-US_AllisonV3Voice`<br/>Female | ![en-US_AllisonV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/AllisonV3.wav){: audio controls} |
| | Enhanced neural | `en-US_EmilyV3Voice`<br/>Female | ![en-US_EmilyV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/EmilyV3.wav){: audio controls} |
| | Enhanced neural | `en-US_HenryV3Voice`<br/>Male | ![en-US_HenryV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/HenryV3.wav){: audio controls} |
| | Enhanced neural | `en-US_KevinV3Voice`<br/>Male | ![en-US_KevinV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/KevinV3.wav){: audio controls} |
| | Enhanced neural | `en-US_LisaV3Voice`<br/>Female | ![en-US_LisaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/LisaV3.wav){: audio controls} |
| | Enhanced neural | `en-US_MichaelV3Voice`<br/>Male | ![en-US_MichaelV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/MichaelV3.wav){: audio controls} |
| | Enhanced neural | `en-US_OliviaV3Voice`<br/>Female | ![en-US_OliviaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/OliviaV3.wav){: audio controls} |
| French<br/>(Canadian) | Enhanced neural| `fr-CA_LouiseV3Voice`<br/>Female | ![fr-CA_LouiseV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/LouiseV3.wav){: audio controls} |
| French<br/>(France) | Enhanced neural | `fr-FR_NicolasV3Voice`<br/>Male | ![fr-FR_NicolasV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/NicolasV3.wav){: audio controls} |
| | Enhanced neural | `fr-FR_ReneeV3Voice`<br/>Female | ![fr-FR_ReneeV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/ReneeV3.wav){: audio controls} |
| German | Enhanced neural | `de-DE_BirgitV3Voice`<br/>Female | ![de-DE_BirgitV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/BirgitV3.wav){: audio controls} |
| | Enhanced neural | `de-DE_DieterV3Voice`<br/>Male | ![de-DE_DieterV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/DieterV3.wav){: audio controls} |
| | Enhanced neural | `de-DE_ErikaV3Voice`<br/>Female | ![de-DE_ErikaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/ErikaV3.wav){: audio controls} |
| Italian | Enhanced neural  | `it-IT_FrancescaV3Voice`<br/>Female | ![it-IT_FrancescaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/FrancescaV3.wav){: audio controls} |
| Japanese | Enhanced neural | `ja-JP_EmiV3Voice`<br/>Female | ![ja-JP_EmiV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/EmiV3.wav){: audio controls} |
| Korean | Neural<br/>{{site.data.keyword.cloud_notm}} only | `ko-KR_HyunjunVoice`<br/>Male | ![ko-KR_HyunjunVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Hyunjun.wav){: audio controls} |
| | Neural<br/>{{site.data.keyword.cloud_notm}} only | `ko-KR_SiWooVoice`<br/>Male | ![ko-KR_SiWooVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/SiWoo.wav){: audio controls} |
| | Neural<br/>{{site.data.keyword.cloud_notm}} only | `ko-KR_YoungmiVoice`<br/>Female | ![ko-KR_YoungmiVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Youngmi.wav){: audio controls} |
| | Neural<br/>{{site.data.keyword.cloud_notm}} only | `ko-KR_YunaVoice`<br/>Female | ![ko-KR_YunaVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/Yuna.wav){: audio controls} |
| Portuguese<br/>(Brazilian) | Enhanced neural | `pt-BR_IsabelaV3Voice`<br/>Female | ![pt-BR_IsabelaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/IsabelaV3.wav){: audio controls} |
| Spanish<br/>(Castilian) | Enhanced neural | `es-ES_EnriqueV3Voice`<br/>Male | ![es-ES_EnriqueV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/EnriqueV3.wav){: audio controls} |
| | Enhanced neural | `es-ES_LauraV3Voice`<br/>Female | ![es-ES_LauraV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/LauraV3.wav){: audio controls} |
| Spanish<br/>(Latin American) | Enhanced neural | `es-LA_SofiaV3Voice`<br/>Female | ![es-LA_SofiaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/SofiaV3.wav){: audio controls} |
| Spanish<br/>(North American) | Enhanced neural | `es-US_SofiaV3Voice`<br/>Female | ![es-US_SofiaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/SofiaV3.wav){: audio controls} |
{: caption="Table 1. Supported languages and voices"}

The Spanish Latin American and North American `Sofia` voices are essentially the same voice. The most significant difference concerns how the two voices interpret a $ (dollar sign). The Latin American version uses the term *pesos*; the North American version uses the term *d&oacute;lares*. Other minor differences might also exist between the two voices.
{: note}

### Neural voice technology
{: #neural-voices}

All of the service's voices are neural voices. The service's now-deprecated standard voices relied on segment selection and concatenation. Neural voice technology instead uses multiple Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech. The DNNs are trained on natural human speech and generate the resulting audio from the predicted acoustic features.

During synthesis, the DNNs predict the pitch and phoneme duration (prosody), spectral structure, and waveform of the speech. Neural voices produce speech that is crisp and clear, with a very natural-sounding, smooth, and consistent audio quality.

The service offers two types of neural voices:

-   ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only.** *Neural voices* do *not* include the string `V3` in their names. All voices for Arabic, Australian English, Chinese, Dutch, and Korean are neural voices.
-   *Enhanced neural voices* include the string `V3` in their names. All voices for Brazilian Portuguese, United Kingdom and United States English, French, German, Italian, Japanese, and Spanish (all dialects) are enhanced neural voices.

Enhanced neural voices achieve a slightly higher degree of natural-sounding speech. Enhanced neural voices support both IPA and SPR for word and phoneme customization; neural voices support only IPA.

For more information about the service's neural voice technology, see

-   The blog post [{{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}}: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   The research paper [High quality, lightweight and adaptable {{site.data.keyword.texttospeechshort}} using LPCNet](https://arxiv.org/abs/1905.00590){: external}

### Migrating from standard to neural voices
{: #migrate-voice}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only**

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only.** The list of available voices underwent many changes on 2 December 2020. To optimize the audio quality and naturalness of synthesized speech, the standard (concatenative) voices that were previously available with the service are now deprecated. {{site.data.keyword.IBM_notm}} recommends that you migrate from standard to neural voices at your earliest convenience. For more information about the changes and implications for voice synthesis, see the [2 December 2020 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-2december2020) in the release notes. For information about moving to neural voices, see [Migrating from standard to neural voices](#migrate-voice).
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

## Specifying a voice for speech synthesis
{: #specify-voice}

Both the HTTP `POST` and `GET /v1/synthesize` methods, as well as the WebSocket `/v1/synthesize` method, accept an optional `voice` query parameter. Use the `voice` parameter to indicate the voice that is to be used for speech synthesis. If you omit the parameter from a request, the service uses the US English `en-US_MichaelV3Voice` by default.

The service bases its understanding of the language for the input text on the specified voice. Be sure to specify a voice that matches the language of the input text. For example, if you specify the French voice `fr-FR_ReneeV3Voice`, the service expects to receive input text that is written in French. If you pass text that is not written in the language of the voice (for example, English text for the French voice), the service might not produce meaningful results.

-   The following example HTTP `POST` request uses the voice `en-US_AllisonV3Voice` for speech synthesis:

    ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}}**

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize?voice=en-US_AllisonV3Voice"
    ```
    {: pre}

    ![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}}**

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize?voice=en-US_AllisonV3Voice"
    ```
    {: pre}

-   The following example shows an equivalent HTTP `GET` request for speech synthesis:

    ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}}**

    ```bash
    curl -X GET -u "apikey:{apikey}" \
    --output hello_world.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hello%20world&voice=en-US_AllisonV3Voice"
    ```
    {: pre}

    ![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}}**

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --output hello_world.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hello%20world&voice=en-US_AllisonV3Voice"
    ```
    {: pre}

## Customization
{: #customize-voice}

When you synthesize text, the service applies language-dependent pronunciation rules to convert the ordinary spelling of each word to a phonetic spelling. The service's pronunciation rules work well for common words, but they can yield imperfect results for unusual words, such as terms with foreign origins, personal names, and abbreviations or acronyms. If your application's lexicon includes such words, you can use the customization interface to specify how the service pronounces them.

You create a custom model for a specific language, not for a specific voice. So a custom model can be used with any voice for its specified language. For example, a custom model that you create for the `en-US` language can be used with any US English voice. It cannot, however, be used with an `en-GB` or `en-AU` voice.

Customization is available for all languages. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

## Listing all available voices
{: #list-voices}

The `GET /v1/voices` method lists information about all available voices. It takes no arguments and returns a JSON array that is named `voices`. The array includes a separate object for each voice. The order in which the service returns voices can change from call to call. Do not rely on an alphabetized or static list of voices.

The following example lists all voices that are supported by the service:

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}}**

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/voices"
```
{: pre}

![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}}**

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/voices"
```
{: pre}

This abbreviated response shows only the first few voices of the response:

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
{: #list-voice}

The `GET /v1/voices/{voice}` method lists information about a specific voice. It accepts two parameters.

-   `voice` (path parameter, *required* string) - Identifies the voice for which information is to be returned. You specify a voice by its name (for example, `en-US_LisaV3Voice`).
-   `customization_id` (query parameter, *optional* string) - Provides the globally unique identifier (GUID) of a custom model that is defined for the language of the specified voice. If you include a customization ID, you must make the request with credentials for the instance of the service that owns the custom model.

If you omit the `customization_id` parameter, the method returns JSON output for the specified voice that is identical to the information returned for a voice by the `GET /v1/voices` method. If you specify a `customization_id`, the output includes a `customization` field that provides information about the specified custom model.

The following example returns information about the `en-US_LisaV3Voice` and the specified custom model:

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}}**

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/voices/en-US_LisaV3Voice?customization_id=64f4807f-a5f1-5867-924f-7bba1a84fe97"
```
{: pre}

![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}}**

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/voices/en-US_LisaV3Voice?customization_id=64f4807f-a5f1-5867-924f-7bba1a84fe97"
```
{: pre}

The attributes of the additional `customization` field provide metadata information such as the GUID, name, language, and description of the custom model. They also show the credentials of the model's owner, the date and time at which the model was created, and the date and time of its last modification.

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
    "name": "Customization test",
    "language": "en-US",
    "description": "Customization test",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

To see the custom words and prompts that the model includes, use the `GET /v1/customizations/{customization_id}` method. For more information, see [Querying a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery).
