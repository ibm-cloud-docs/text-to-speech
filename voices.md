---

copyright:
  years: 2015, 2022
lastupdated: "2022-08-01"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Using languages and voices
{: #voices}

The {{site.data.keyword.texttospeechfull}} service supports a variety of languages, voices, and dialects. For different languages, the service offers female voices, male voices, or both. Each voice uses appropriate cadence and intonation for its dialect.
{: shortdesc}

## Supported languages and voices
{: #language-voices}

Table 1 lists and provides audio samples for the voices that are available for each language and dialect. All voices are generally available (GA) for production use. For more information about specifying a voice for speech synthesis and about the default voice, see [Specifying a voice for speech synthesis](#specify-voice).

All voices use neural voice technology. The service offers two types of voices with different quality, capabilities, and availability: *enhanced neural voices* and *neural voices*. For more information, see [Neural voice technology](#neural-voices).

Effective **31 March 2022**, all *neural voices* are deprecated. The deprecated voices remain available to existing users until 31 March 2023, when they will be removed from the service and the documentation. The neural voices are supported only for IBM Cloud; they are not available for IBM Cloud Pak for Data. New voices for Australian English, Dutch, and Korean will be released by 15 February 2023. If you are using Australian English, Dutch, or Korean voices, your API calls will automatically redirect to the new voices in that language. Voices in Arabic, Chinese, Czech, Swedish, and Flemish will be removed from service. All *enhanced neural voices* remain available to all users. For more information, see the [31 March 2022 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-31march2022) in the release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}.
{: deprecated}

If a voice is labeled in the **Type / Availability** column with just one version of the service, *{{site.data.keyword.cloud_notm}} only* or *{{site.data.keyword.icp4dfull_notm}} only*, it is restricted to that version. Otherwise, the voice is available with both versions of the service. Only enhanced neural voices are available for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}.

| Language | Type / Availability | Voice / Gender | Sample |
|----------|:-------------------:|:--------------:|:------:|
| Arabic | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `ar-MS_OmarVoice`  \n Male | ![ar-MS_OmarVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/ar-MS_OmarVoice.wav){: audio controls} |
| Chinese  \n (Mandarin) | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `zh-CN_LiNaVoice`  \n Female | ![zh-CN_LiNaVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/zh-CN_LiNaVoice.wav){: audio controls} |
| | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `zh-CN_WangWeiVoice`  \n Male | ![zh-CN_WangWeiVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/zh-CN_WangWeiVoice.wav){: audio controls} |
| | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `zh-CN_ZhangJingVoice`  \n Female | ![zh-CN_ZhangJingVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/zh-CN_ZhangJingVoice.wav){: audio controls} |
| Czech | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `cs-CZ_AlenaVoice`  \n Female | ![cs-CZ_AlenaVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/cs-CZ_AlenaVoice.wav){: audio controls} |
| Dutch  \n (Belgian) | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `nl-BE_AdeleVoice`  \n Female | ![nl-BE_AdeleVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/nl-BE_AdeleVoice.wav){: audio controls} |
| | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `nl-BE_BramVoice`  \n Male | ![nl-BE_BramVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/nl-BE_BramVoice.wav){: audio controls} |
| Dutch  \n (Netherlands) | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `nl-NL_EmmaVoice`  \n Female | ![nl-NL_EmmaVoive sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/nl-NL_EmmaVoice.wav){: audio controls} |
| | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `nl-NL_LiamVoice`  \n Male | ![nl-NL_LiamVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/nl-NL_LiamVoice.wav){: audio controls} |
| English  \n (Australian) | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `en-AU_CraigVoice`  \n Male | ![en-AU_CraigVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-AU_CraigVoice.wav){: audio controls} |
| | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `en-AU_MadisonVoice`  \n Female | ![en-AU_MadisonVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-AU_MadisonVoice.wav){: audio controls} |
| | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `en-AU_SteveVoice`  \n Male | ![en-AU_SteveVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-AU_SteveVoice.wav){: audio controls} |
| English  \n (United Kingdom) | Enhanced neural | `en-GB_CharlotteV3Voice`  \n Female | ![en-GB_CharlotteV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-GB_CharlotteV3Voice.wav){: audio controls} |
| | Enhanced neural | `en-GB_JamesV3Voice`  \n Male | ![en-GB_JamesV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-GB_JamesV3Voice.wav){: audio controls} |
| | Enhanced neural | `en-GB_KateV3Voice`  \n Female | ![en-GB_KateV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-GB_KateV3Voice.wav){: audio controls} |
| English  \n (United States) | Enhanced neural | `en-US_AllisonV3Voice`  \n Female | ![en-US_AllisonV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-US_AllisonV3Voice.wav){: audio controls} |
| | Enhanced neural | `en-US_EmilyV3Voice`  \n Female | ![en-US_EmilyV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-US_EmilyV3Voice.wav){: audio controls} |
| | Enhanced neural | `en-US_HenryV3Voice`  \n Male | ![en-US_HenryV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-US_HenryV3Voice.wav){: audio controls} |
| | Enhanced neural | `en-US_KevinV3Voice`  \n Male | ![en-US_KevinV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-US_KevinV3Voice.wav){: audio controls} |
| | Enhanced neural | `en-US_LisaV3Voice`  \n Female | ![en-US_LisaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-US_LisaV3Voice.wav){: audio controls} |
| | Enhanced neural | `en-US_MichaelV3Voice`  \n Male | ![en-US_MichaelV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-US_MichaelV3Voice.wav){: audio controls} |
| | Enhanced neural | `en-US_OliviaV3Voice`  \n Female | ![en-US_OliviaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/en-US_OliviaV3Voice.wav){: audio controls} |
| French  \n (Canadian) | Enhanced neural| `fr-CA_LouiseV3Voice`  \n Female | ![fr-Ca_LouiseV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/fr-CA_LouiseV3Voice.wav){: audio controls} |
| French  \n (France) | Enhanced neural | `fr-FR_NicolasV3Voice`  \n Male | ![fr-FR_NicolasV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/fr-FR_NicolasV3Voice.wav){: audio controls} |
| | Enhanced neural | `fr-FR_ReneeV3Voice`  \n Female | ![fr-FR_ReneeV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/fr-FR_ReneeV3Voice.wav){: audio controls} |
| German | Enhanced neural | `de-DE_BirgitV3Voice`  \n Female | ![de-DE_BirgitV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/de-DE_BirgitV3Voice.wav){: audio controls} |
| | Enhanced neural | `de-DE_DieterV3Voice`  \n Male | ![de-DE_DieterV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/de-DE_DieterV3Voice.wav){: audio controls} |
| | Enhanced neural | `de-DE_ErikaV3Voice`  \n Female | ![de-DE_ErikaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/de-DE_ErikaV3Voice.wav){: audio controls} |
| Italian | Enhanced neural  | `it-IT_FrancescaV3Voice`  \n Female | ![it-IT_FrancescaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/it-IT_FrancescaV3Voice.wav){: audio controls} |
| Japanese | Enhanced neural | `ja-JP_EmiV3Voice`  \n Female | ![ja-JP_EmiV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/ja-JP_EmiV3Voice.wav){: audio controls} |
| Korean | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `ko-KR_HyunjunVoice`  \n Male | ![ko-KR_HyunjunVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/ko-KR_HyunjunVoice.wav){: audio controls} |
| | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `ko-KR_SiWooVoice`  \n Male | ![ko-KR_SiWooVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/ko-KR_SiWooVoice.wav){: audio controls} |
| | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `ko-KR_YoungmiVoice`  \n Female | ![ko-KR_YoungmiVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/ko-KR_YoungmiVoice.wav){: audio controls} |
| | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `ko-KR_YunaVoice`  \n Female | ![ko-KR_YunaVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/ko-KR_YunaVoice.wav){: audio controls} |
| Portuguese  \n (Brazilian) | Enhanced neural | `pt-BR_IsabelaV3Voice`  \n Female | ![pt-BR_IsabelaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/pt-BR_IsabelaV3Voice.wav){: audio controls} |
| Spanish  \n (Castilian) | Enhanced neural | `es-ES_EnriqueV3Voice`  \n Male | ![es-ES_EnriqueV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/es-ES_EnriqueV3Voice.wav){: audio controls} |
| | Enhanced neural | `es-ES_LauraV3Voice`  \n Female | ![es-ES_LauraV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/es-ES_LauraV3Voice.wav){: audio controls} |
| Spanish  \n (Latin American) | Enhanced neural | `es-LA_SofiaV3Voice`  \n Female | ![es-LA_SofiaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/es-LA_SofiaV3Voice.wav){: audio controls} |
| Spanish  \n (North American) | Enhanced neural | `es-US_SofiaV3Voice`  \n Female | ![es-US_SofiaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/es-US_SofiaV3Voice.wav){: audio controls} |
| Swedish | Neural  \n {{site.data.keyword.cloud_notm}} only  \n Deprecated | `sv-SE_IngridVoice`  \n Female | ![sv-SE_IngridVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-2112/sv-SE_IngridVoice.wav){: audio controls} |
{: caption="Table 1. Supported languages and voices"}

The Spanish Latin American and North American `Sofia` voices are essentially the same voice. The most significant difference concerns how the two voices interpret a $ (dollar sign). The Latin American version uses the term *pesos*; the North American version uses the term *dólares*. Other minor differences might also exist between the two voices.p
{: note}

### Neural voice technology
{: #neural-voices}

All of the service's voices are neural voices. Neural voice technology uses multiple Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech. The DNNs are trained on natural human speech and generate the resulting audio from the predicted acoustic features. (The service's now-deprecated standard voices relied on segment selection and concatenation.)

During synthesis, the DNNs predict the pitch and phoneme duration (prosody), spectral structure, and waveform of the speech. Neural voices produce speech that is crisp and clear, with a very natural-sounding, smooth, and consistent audio quality.

The service offers two types of neural voices:

-   *Neural voices* do *not* include the string `V3` in their names. All voices for Arabic, Australian English, Chinese, Dutch, Korean, and Swedish are neural voices.

    Effective **31 March 2022**, all *neural voices* are deprecated. The deprecated voices remain available to existing users until 31 March 2023, when they will be removed from the service and the documentation. The neural voices are supported only for IBM Cloud; they are not available for IBM Cloud Pak for Data. New voices for Australian English, Dutch, and Korean will be released by 15 February 2023. If you are using Australian English, Dutch, or Korean voices, your API calls will automatically redirect to the new voices in that language. Voices in Arabic, Chinese, Czech, Swedish, and Flemish will be removed from service. All *enhanced neural voices* remain available to all users. For more information, see the [31 March 2022 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-31march2022) in the release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}.
    {: deprecated}

-   *Enhanced neural voices* include the string `V3` in their names. All voices for Brazilian Portuguese, United Kingdom and United States English, French (both dialects), German, Italian, Japanese, and Spanish (all dialects) are enhanced neural voices.

Enhanced neural voices achieve a slightly higher degree of natural-sounding speech. Enhanced neural voices support both IPA and SPR for word and phoneme customization; neural voices support only IPA.

For more information about the service's neural voice technology, see the research paper [High quality, lightweight and adaptable {{site.data.keyword.texttospeechshort}} using LPCNet](https://arxiv.org/abs/1905.00590){: external}.

## Specifying a voice for speech synthesis
{: #specify-voice}

Both the HTTP `POST` and `GET /v1/synthesize` methods, as well as the WebSocket `/v1/synthesize` method, accept an optional `voice` query parameter. You use the `voice` parameter to indicate the voice and language that are to be used for speech synthesis. The service bases its understanding of the language for the input text on the language of the specified voice.

Be sure to specify a voice that matches the language of the input text. For example, if you specify the French voice `fr-FR_ReneeV3Voice`, the service expects to receive input text that is written in French. If you pass text that is not written in the language of the voice (for example, English text for the French voice), the service might not produce meaningful results.

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

### The default voice
{: #specify-voice-default}

If you omit the `voice` parameter from a request, the service uses the US English `en-US_MichaelV3Voice` by default. This default applies to all speech synthesis requests and to the  `GET /v1/pronunciation` method.

![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}} only** If you do not install the `en-US_MichaelV3Voice`, it cannot serve as the default voice. In this case, you must either

-   Use the `voice` parameter to pass the voice that is to be used with each request.
-   Specify a new default voice for your installation of {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} by using the `defaultTTSVoice` property in the Speech services custom resource. For more information, see  [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

## Multilingual speech synthesis
{: #synthesis-multilingual}

The service does not support multilingual speech synthesis at this time. All synthesis is based on the language of the voice that is specified by the `voice` parameter. Depending on the language and the word in question, you might be able to use customization to approximate the pronunciation of a word in a language that is different from the voice of the request. For more information, see [Creating a custom model](#customize-model).

If you decide to use customization to emulate pronunciation in a different language, use the HTTP `GET /v1/pronunciation` method to see the pronunciation of the word in the other language. The method returns the phonemes that the service uses to pronounce the word in that language. For more information, see [Phonetic translation](/docs/text-to-speech?topic=text-to-speech-customIntro#phonetic).

You can adjust the phonemes that the method returns to match as closely as possible the phonemes that are available in your language. You can then create a custom model that includes a custom word with that translation and use that model with your synthesis request. Becuase two different languages might not support the same phonemes, it might not be possible to match exactly the sounds and pronunciation of one language with the phonetic symbols of another language.

The Speech Synthesis Markup Language (SSML) `<speak>` element includes an `xml:lang` element, but that element applies to the entire request, and the service does not support its use as a way of specifying a different language for speech synthesis.
{: note}

## Creating a custom model
{: #customize-model}

When you synthesize text, the service applies language-dependent pronunciation rules to convert the ordinary spelling of each word to a phonetic spelling. The service's pronunciation rules work well for common words, but they can yield imperfect results for unusual words, such as terms with foreign origins, personal names, and abbreviations or acronyms. If your application's lexicon includes such words, you can use the customization interface to specify how the service pronounces them.

You create a custom model for a specific language, not for a specific voice. So a custom model can be used with any voice for its specified language. For example, a custom model that you create for the `en-US` language can be used with any US English voice. It cannot, however, be used with an `en-GB` or `en-AU` voice.

Customization is available for all languages. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

## Creating a custom voice
{: #customize-voice}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only**

Premium customers can work with {{site.data.keyword.IBM_notm}} to train a new custom voice for their specific use case and target market. Creating a custom voice is different from customizing one of the service's existing voices. A custom voice is a unique new voice that is based on audio training data that the customer provides. {{site.data.keyword.IBM_notm}} can train a custom voice with as little as one hour of training data.

For more information, contact your {{site.data.keyword.IBM_notm}} Sales Representative.

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
