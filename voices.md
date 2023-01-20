---

copyright:
  years: 2015, 2023
lastupdated: "2023-01-16"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Languages and voices
{: #voices}

The {{site.data.keyword.texttospeechfull}} service supports a variety of languages, voices, and dialects. For different languages, the service offers female voices, male voices, or both. Each voice uses appropriate cadence and intonation for its dialect.
{: shortdesc}

All of the service's voices use neural voice technology. Neural voice technology uses multiple Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech. The DNNs are trained on natural human speech and generate the resulting audio from the predicted acoustic features. During synthesis, the DNNs predict the pitch and phoneme duration (prosody), spectral structure, and waveform of the speech. Neural voices produce speech that is crisp and clear, with a very natural-sounding, smooth, and consistent audio quality.

## Supported languages and voices
{: #language-voices}

The service offers three types of voices with different qualities and capabilities:

-   [IBM Cloud]{: tag-ibm-cloud} *Expressive neural voices*. Expressive neural voices offer natural-sounding speech that is exceptionally clear and crisp. Their pronunciation and inflections are natural and conversational, and the resulting speech offers extremely smooth transitions between words. The voices determine sentiment from context and automatically use the proper intonation to suit the text.

    Expressive neural voices support the use of both standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) phonetic symbols. They also support the use of additional features that are not available with the other types of voices. Expressive voices are available for US English only.
    -   For additional information and a complete list of all expressive voices, see [Expressive neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-expressive).
    -   For a blog that introduces the expressive voices, see [Is your conversational AI setting the right tone?](https://www.ibm.com/blogs/journey-to-ai/2022/09/is-your-conversational-ai-setting-the-right-tone/){: external}.

-   [IBM Cloud]{: tag-ibm-cloud} *Enhanced neural voices*. Enhanced neural voices achieve a slightly higher degree of natural-sounding speech and support more service features. Enhanced neural voices support both IPA and SPR symbols for word customization. For a complete list of all enhanced neural voices and their languages, see [Enhanced neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-enhanced-neural).
-   *Neural voices*. Neural voices produce natural-sounding speech but do not support all of the service's features. Neural voices support only IPA symbols for word customization. For a complete list of all neural voices and their languages, see [Neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-neural).

    Effective **31 March 2022**, all *neural voices* are deprecated. The deprecated voices remain available to existing users until 31 March 2023, when they will be removed from the service and the documentation. *No enhanced neural voices or expressive neural voices are deprecated.* For more information, see the [31 March 2022 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-31march2022) in the release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}.
    {: deprecated}

For more information about the service's neural voice technology, see [The science behind the service](/docs/text-to-speech?topic=text-to-speech-science).

### Language support by type of voice
{: #language-voices-by type}

Table 1 shows the service's support for languages by type of voice. The following topics list the available languages and voices for each voice type.

| Language | Expressive neural voices | Enhanced neural voices | Neural voices (deprecated) |
|----------|:------------------------:|:-----------------------:|:--------------------------:|
| Arabic | | | &#10004; |
| Chinese (Mandarin) | | | &#10004; |
| Czech | | | &#10004; |
| Dutch  \n (Belgian) | | | &#10004; |
| Dutch  \n (Netherlands) | | | &#10004; |
| English  \n (United Kingdom) | | &#10004; | |
| English  \n (Australian) | | | &#10004; |
| English  \n (United States) | &#10004; | &#10004; | |
| French  \n (Canadian) | | &#10004; | |
| French  \n (France) | | &#10004; | |
| German | | &#10004; | |
| Italian | | &#10004; | |
| Japanese | | &#10004; | |
| Korean | | | &#10004; |
| Portuguese  \n (Brazilian) | | &#10004; | |
| Spanish  \n (Castilian) | | &#10004; | |
| Spanish  \n (Latin American) | | &#10004; | |
| Spanish  \n (South American) | | &#10004; | |
| Swedish | | | &#10004; |
{: caption="Table 1. Language support by type of voice"}

### Expressive neural voices
{: #language-voices-expressive}

[IBM Cloud]{: tag-ibm-cloud}

Table 2 lists and provides audio samples for all available expressive neural voices. All expressive voices are generally available (GA) for production use with the *{{site.data.keyword.cloud_notm}}* version of the service only.

Expressive neural voices support additional features that are not available with other types of voices. These features include additional speaking styles, automatic emphasis of interjections, and emphasis of specified words. For more information, see [Modifying speech synthesis with expressive neural voices](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive).

To produce the most natural-sounding prosody, expressive neural voices need to consider the context of all words and phrases of a sentence. Expressive voices therefore are more compute-intensive and have slightly higher latency than other types of voices. The initial response for a synthesis request that uses an expressive voice might take a fraction of a second longer (for example, a few hundred milliseconds) to arrive. The total response time for the request to complete will also be longer.

To minimize the latency and response time for an expressive voice, use shorter sentences wherever possible.
{: tip}

| Language | Availability        | Voice / Gender | Audio sample |
|----------|:-------------------:|:--------------:|:------------:|
| English  \n (United States) | GA | `en-US_AllisonExpressive`  \n Female | ![en-US_AllisonExpressive sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_AllisonExpressive.wav){: audio controls} |
| | GA | `en-US_EmmaExpressive`  \n Female | ![en-US_EmmaExpressive sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_EmmaExpressive.wav){: audio controls} |
| | GA | `en-US_LisaExpressive`  \n Female | ![en-US_LisaExpressive sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_LisaExpressive.wav){: audio controls} |
| | GA | `en-US_MichaelExpressive`  \n Male | ![en-US_MichaelExpressive sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_MichaelExpressive.wav){: audio controls} |
{: caption="Table 2. Expressive neural languages and voices"}

When used with the SSML `<prosody>` element, expressive voices support only percentage values for the `rate` and `pitch` attributes. For more information, see [The `<prosody>` element](/docs/text-to-speech?topic=text-to-speech-elements#prosody_element).
{: note}

### Enhanced neural voices
{: #language-voices-enhanced-neural}

Table 3 lists and provides audio samples for all available enhanced neural voices. All enhanced neural voices are generally available (GA) for production use with both versions of the service, *{{site.data.keyword.cloud_notm}}* and *{{site.data.keyword.icp4dfull_notm}}*. All enhanced neural voices include the string `V3` in their names.

| Language | Availability        | Voice / Gender | Audio sample |
|----------|:-------------------:|:--------------:|:------------:|
| English  \n (United Kingdom) | GA | `en-GB_CharlotteV3Voice`  \n Female | ![en-GB_CharlotteV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-GB_CharlotteV3Voice.wav){: audio controls} |
| | GA | `en-GB_JamesV3Voice`  \n Male | ![en-GB_JamesV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-GB_JamesV3Voice.wav){: audio controls} |
| | GA | `en-GB_KateV3Voice`  \n Female | ![en-GB_KateV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-GB_KateV3Voice.wav){: audio controls} |
| English  \n (United States) | GA | `en-US_AllisonV3Voice`  \n Female | ![en-US_AllisonV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_AllisonV3Voice.wav){: audio controls} |
| | GA | `en-US_EmilyV3Voice`  \n Female | ![en-US_EmilyV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_EmilyV3Voice.wav){: audio controls} |
| | GA | `en-US_HenryV3Voice`  \n Male | ![en-US_HenryV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_HenryV3Voice.wav){: audio controls} |
| | GA | `en-US_KevinV3Voice`  \n Male | ![en-US_KevinV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_KevinV3Voice.wav){: audio controls} |
| | GA | `en-US_LisaV3Voice`  \n Female | ![en-US_LisaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_LisaV3Voice.wav){: audio controls} |
| | GA | `en-US_MichaelV3Voice`  \n Male | ![en-US_MichaelV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_MichaelV3Voice.wav){: audio controls} |
| | GA | `en-US_OliviaV3Voice`  \n Female | ![en-US_OliviaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-US_OliviaV3Voice.wav){: audio controls} |
| French  \n (Canadian) | GA | `fr-CA_LouiseV3Voice`  \n Female | ![fr-Ca_LouiseV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/fr-CA_LouiseV3Voice.wav){: audio controls} |
| French  \n (France) | GA | `fr-FR_NicolasV3Voice`  \n Male | ![fr-FR_NicolasV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/fr-FR_NicolasV3Voice.wav){: audio controls} |
| | GA | `fr-FR_ReneeV3Voice`  \n Female | ![fr-FR_ReneeV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/fr-FR_ReneeV3Voice.wav){: audio controls} |
| German | GA | `de-DE_BirgitV3Voice`  \n Female | ![de-DE_BirgitV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/de-DE_BirgitV3Voice.wav){: audio controls} |
| | GA | `de-DE_DieterV3Voice`  \n Male | ![de-DE_DieterV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/de-DE_DieterV3Voice.wav){: audio controls} |
| | GA | `de-DE_ErikaV3Voice`  \n Female | ![de-DE_ErikaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/de-DE_ErikaV3Voice.wav){: audio controls} |
| Italian | GA | `it-IT_FrancescaV3Voice`  \n Female | ![it-IT_FrancescaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/it-IT_FrancescaV3Voice.wav){: audio controls} |
| Japanese | GA | `ja-JP_EmiV3Voice`  \n Female | ![ja-JP_EmiV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/ja-JP_EmiV3Voice.wav){: audio controls} |
| Portuguese  \n (Brazilian) | GA | `pt-BR_IsabelaV3Voice`  \n Female | ![pt-BR_IsabelaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/pt-BR_IsabelaV3Voice.wav){: audio controls} |
| Spanish  \n (Castilian) | GA | `es-ES_EnriqueV3Voice`  \n Male | ![es-ES_EnriqueV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/es-ES_EnriqueV3Voice.wav){: audio controls} |
| | GA | `es-ES_LauraV3Voice`  \n Female | ![es-ES_LauraV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/es-ES_LauraV3Voice.wav){: audio controls} |
| Spanish  \n (Latin American) | GA | `es-LA_SofiaV3Voice`  \n Female | ![es-LA_SofiaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/es-LA_SofiaV3Voice.wav){: audio controls} |
| Spanish  \n (North American) | GA | `es-US_SofiaV3Voice`  \n Female | ![es-US_SofiaV3Voice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/es-US_SofiaV3Voice.wav){: audio controls} |
{: caption="Table 3. Enhanced neural languages and voices"}

The Spanish Latin American and North American `Sofia` voices are essentially the same voice. The most significant difference concerns how the two voices interpret a $ (dollar sign). The Latin American version uses the term *pesos*; the North American version uses the term *dólares*. Other minor differences might also exist between the two voices.
{: note}

### Neural voices
{: #language-voices-neural}

[IBM Cloud]{: tag-ibm-cloud}

Effective **31 March 2022**, all *neural voices* are deprecated. The deprecated voices remain available to existing users until 31 March 2023, when they will be removed from the service and the documentation. *No enhanced neural voices or expressive neural voices are deprecated.* For more information, see the [31 March 2022 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-31march2022) in the release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}.
{: deprecated}

Table 4 lists and provides audio samples for all available neural voices. All neural voices are generally available (GA) for production use with the *{{site.data.keyword.cloud_notm}}* version of the service only. (Neural voices do *not* include the string `V3` in their names.)

| Language | Availability        | Voice / Gender | Audio sample |
|----------|:-------------------:|:--------------:|:------------:|
| Arabic | GA | `ar-MS_OmarVoice`  \n Male | ![ar-MS_OmarVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/ar-MS_OmarVoice.wav){: audio controls} |
| Chinese  \n (Mandarin) | GA | `zh-CN_LiNaVoice`  \n Female | ![zh-CN_LiNaVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/zh-CN_LiNaVoice.wav){: audio controls} |
| | GA | `zh-CN_WangWeiVoice`  \n Male | ![zh-CN_WangWeiVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/zh-CN_WangWeiVoice.wav){: audio controls} |
| | GA | `zh-CN_ZhangJingVoice`  \n Female | ![zh-CN_ZhangJingVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/zh-CN_ZhangJingVoice.wav){: audio controls} |
| Czech | GA | `cs-CZ_AlenaVoice`  \n Female | ![cs-CZ_AlenaVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/cs-CZ_AlenaVoice.wav){: audio controls} |
| Dutch  \n (Belgian) | GA | `nl-BE_AdeleVoice`  \n Female | ![nl-BE_AdeleVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/nl-BE_AdeleVoice.wav){: audio controls} |
| | GA | `nl-BE_BramVoice`  \n Male | ![nl-BE_BramVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/nl-BE_BramVoice.wav){: audio controls} |
| Dutch  \n (Netherlands) | GA | `nl-NL_EmmaVoice`  \n Female | ![nl-NL_EmmaVoive sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/nl-NL_EmmaVoice.wav){: audio controls} |
| | GA | `nl-NL_LiamVoice`  \n Male | ![nl-NL_LiamVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/nl-NL_LiamVoice.wav){: audio controls} |
| English  \n (Australian) | GA | `en-AU_CraigVoice`  \n Male | ![en-AU_CraigVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-AU_CraigVoice.wav){: audio controls} |
| | GA | `en-AU_MadisonVoice`  \n Female | ![en-AU_MadisonVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-AU_MadisonVoice.wav){: audio controls} |
| | GA | `en-AU_SteveVoice`  \n Male | ![en-AU_SteveVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/en-AU_SteveVoice.wav){: audio controls} |
| Korean | GA | `ko-KR_HyunjunVoice`  \n Male | ![ko-KR_HyunjunVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/ko-KR_HyunjunVoice.wav){: audio controls} |
| | GA | `ko-KR_SiWooVoice`  \n Male | ![ko-KR_SiWooVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/ko-KR_SiWooVoice.wav){: audio controls} |
| | GA | `ko-KR_YoungmiVoice`  \n Female | ![ko-KR_YoungmiVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/ko-KR_YoungmiVoice.wav){: audio controls} |
| | GA | `ko-KR_YunaVoice`  \n Female | ![ko-KR_YunaVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/ko-KR_YunaVoice.wav){: audio controls} |
| Swedish | GA | `sv-SE_IngridVoice`  \n Female | ![sv-SE_IngridVoice sample](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-latest/sv-SE_IngridVoice.wav){: audio controls} |
{: caption="Table 4. Neural languages and voices"}

## Creating a custom model
{: #customize-model}

When you synthesize text, the service applies language-dependent pronunciation rules to convert the ordinary spelling of each word to a phonetic spelling. The service's pronunciation rules work well for common words, but they can yield imperfect results for unusual words, such as terms with foreign origins, personal names, and abbreviations or acronyms. If your application's lexicon includes such words, you can use the customization interface to specify how the service pronounces them.

A custom model is a dictionary of words and their translations. You create a custom model for a specific language, not for a specific voice. So a custom model can be used with any voice for its specified language. For example, a custom model that you create for the `en-US` language can be used with any US English voice. It cannot, however, be used with an `en-GB` or `en-AU` voice.

Customization is available for all languages. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

## Creating a custom voice
{: #customize-voice}

[IBM Cloud]{: tag-ibm-cloud}

Premium customers can work with {{site.data.keyword.IBM_notm}} to train a new custom voice for their specific use case and target market. Creating a custom voice is different from customizing one of the service's existing voices. A custom voice is a unique new voice that is based on audio training data that the customer provides. {{site.data.keyword.IBM_notm}} can train a custom voice with as little as one hour of training data.

To request a custom voice or for more information, complete and submit this [{{site.data.keyword.IBM_notm}} Request Form](https://form.asana.com/?k=CBuXK1uwlAf5ek6FwB6mcg&d=8612789739828){: external}.
