---

copyright:
  years: 2015, 2023
lastupdated: "2023-12-13"

keywords: text to speech release notes,text to speech for IBM cloud release notes

subcollection: text-to-speech

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}
{: #release-notes}

[IBM Cloud]{: tag-ibm-cloud}

The following features and changes were included for each release and update of managed instances of {{site.data.keyword.texttospeechfull}} that are hosted on {{site.data.keyword.cloud_notm}} or for instances that are hosted on [IBM Cloud Pak for Data as a Service](https://dataplatform.cloud.ibm.com/docs/content/wsj/landings/wtts.html){: external}. Unless otherwise noted, all changes are compatible with earlier releases and are automatically and transparently available to all new and existing applications.
{: shortdesc}

For information about known limitations of the service, see [Known limitations](/docs/text-to-speech?topic=text-to-speech-known-limitations).

For information about releases and updates of the service for {{site.data.keyword.icp4dfull_notm}}, see [Release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}](/docs/text-to-speech?topic=text-to-speech-release-notes-data).
{: note}

## 15 May 2024
{: #text-to-speech-15may2024}
{: release-note}

Supporting Latin American Spanish female expressive neural voices
:   The service now supports a new female expressive neural voice for Latin American Spanish
    - es-LA_DanielaExpressive.

    Expressive neural voices offer natural-sounding speech that is clear, crisp, and fluid. The new voice is generally available (GA) for production use. It supports the use of both the standard International Phonetic Alphabet (IPA) and IBM Symbolic Phonetic Representation (SPR) phonetic symbols. For more information, see
    - [Expressive neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-expressive).
    - [Spanish expressive voices](/docs/text-to-speech?topic=text-to-speech-expressive-spanish).
    - [Spanish symbols](/docs/text-to-speech?topic=text-to-speech-esSymbols).

## 16 Jan 2024
{: #text-to-speech-16jan2024}
{: release-note}

Text to Speech improvements for US English Expressive voices 
:   When you use US English Expressive voices, the synthesis is faster with lower latency.

Defect fix: Inflection issue when using the question mark (?) in short utterance
:   **Defect fix:** When some short utterances were ended with a question mark (?), the inflection was ignored. This issue is now fixed.

## 30 Nov 2023
{: #text-to-speech-30nov2023}
{: release-note}

Improved Text to Speech synthesis engine for version 3 voices 
:   The Text to Speech engine is improved for delivering faster synthesis with lower latency for version 3 voices.

Improved Text to Speech voice en-AU_HeidiExpressive
:   The Text to Speech voice en-AU_HeidiExpressive is improved that can adjust the pitch and synthesis.  

## 9 June 2023
{: #text-to-speech-19may2023}
{: release-note}

Defect fix: TTS no longer fails due to error message “[Errno 2] No such file or directory“
:   **Defect fix:** When using TTS with websockets, it no longer fails due to error message “[Errno 2] No such file or directory“.

## 18 May 2023
{: #text-to-speech-18may2023}
{: release-note}

Defect fix: Added support for missing SSML features on the Dutch voice
:   **Defect fix:** When using the Dutch voice, all supported SSML features now work as designed. Previously, when using the Dutch voice, some SSML features were not working.

Defect fix: Commas are now respected when using phoneme tags
:   **Defect fix:** When using phoneme tags in SSML, commas (pauses) are now working as expected. Previously, when commas were preceding or following text with phoneme tags, the pause was ignored.

## 6 April 2023
{: #text-to-speech-6april2023}
{: release-note}

Updates to beta Netherlands Dutch enhanced neural voice
:   **Defect fix:** The beta Netherlands Dutch `nl-NL_MerelV3Voice` was updated for internal fixes and improvements. The limitations described for the initial release of the voice in the [31 March 2023 service update](#text-to-speech-31march2023) still apply.

## 31 March 2023
{: #text-to-speech-31march2023}
{: release-note}

Important: End of service for all neural voices
:   **Important:** All neural voices have reached their end of service date and have been removed from the service and the documentation. *No enhanced neural or expressive neural voices are effected.* For complete list of all obsolete neural voices, see the [1 March 2023 service updates](#text-to-speech-1march2023). An attempt to use an obsolete voice returns the HTTP response code 404 with the message `Model '{voice}' not found`.

    New enhanced neural and expressive neural voices are available for the Australian English, Korean, and Netherlands Dutch languages. *You must migrate to one of the new voices for Australian English, Korean, or Netherlands Dutch to continue using the obsolete languages.*

    For more information, see
    -   [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices)
    -   [Migrating from neural voices](/docs/text-to-speech?topic=text-to-speech-voices-migrate)

## 22 March 2023
{: #text-to-speech-22march2023}
{: release-note}

New beta Netherlands Dutch enhanced neural voice
:   The service now supports a new enhanced neural female voice for Netherlands Dutch: `nl-NL_MerelV3Voice`. It supports the use of both standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) phonetic symbols.

    The new voice is beta functionality pending completion of support for SSML. At its initial release, the voice does not support use of the following SSML-related functionality:
    -   The `<prosody>` element with any speech synthesis request
    -   The `rate_percentage` and `pitch_percentage` parameters with any speech synthesis request
    -   The `<mark>` element with a WebSocket speech synthesis request
    -   The `timings` parameter of the JSON text message with a WebSocket speech synthesis request

    For more information about the new voice, its support for IPA and SPR symbols, and migrating to the new voice from the deprecated Netherlands Dutch neural voices, see
    -   [Enhanced neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-enhanced-neural)
    -   [Dutch (Netherlands) symbols](/docs/text-to-speech?topic=text-to-speech-nlSymbols-new)
    -   [Migrating from neural voices](/docs/text-to-speech?topic=text-to-speech-voices-migrate)

Defect fix: Update Korean phonetic symbols in documentation
:   **Defect fix:** In the documentation for Korean SPR symbols, two-character symbols for consonants are now enclosed in single quotes, making them a single symbol. Previously, they were shown as two separate symbols, without enclosing quotes. For more information, see [Consonants (Korean)](/docs/text-to-speech?topic=text-to-speech-koSymbols-new#koConsonants-new).

Documentation updates for IBM SPR symbols
:   The overview documentation for IBM SPR symbols has been updated to clarify the use of multi-character symbols. For more information, see [Speech sound symbols](/docs/text-to-speech?topic=text-to-speech-symbols#intro-SPRs-symbols)).

## 1 March 2023
{: #text-to-speech-1march2023}
{: release-note}

Important: Pending end of service for all neural voices
:   **Important:** Effective **31 March 2023**, all neural voices reach their end of service date and will be removed from the service and the documentation. The neural voices have been deprecated since 31 March 2022. *No enhanced neural or expressive neural voices are effected.*

    The following neural voices will be removed:
    -   Arabic: `ar-MS_OmarVoice`
    -   Chinese (Mandarin): `zh-CN_LiNaVoice`, `zh-CN_WangWeiVoice`, and `zh-CN_ZhangJingVoice`
    -   Czech: `cs-CZ_AlenaVoice`
    -   Dutch (Belgian): `nl-BE_AdeleVoice` and `nl-BE_BramVoice`
    -   Dutch (Netherlands): `nl-NL_EmmaVoice` and `nl-NL_LiamVoice`
    -   English (Australian): `en-AU_CraigVoice`, `en-AU_MadisonVoice`, and `en-AU_SteveVoice`
    -   Korean: `ko-KR_HyunjunVoice`, `ko-KR_SiWooVoice`, `ko-KR_YoungmiVoice`, and `ko-KR_YunaVoice`
    -   Swedish: `sv-SE_IngridVoice`

    New enhanced neural and expressive neural voices are already available for the Australian English and Korean languages. In the coming weeks, a new enhanced neural voice will be available for the Netherlands Dutch language. *You must migrate to one of the new voices for Australian English, Korean, or Netherlands Dutch before 31 March 2023.*

    For more information, see
    -   [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices)
    -   [Migrating from neural voices](/docs/text-to-speech?topic=text-to-speech-voices-migrate)

## 27 February 2023
{: #text-to-speech-27february2023}
{: release-note}

New Australian English expressive neural voices
:   The service now supports two new expressive neural voices, male and female, for Australian English:
    -   `en-AU_HeidiExpressive`
    -   `en-AU_JackExpressive`

    Expressive neural voices offer natural-sounding speech that is exceptionally clear, crisp, and fluid. The new voices are generally available (GA) for production use. They support the use of both standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) phonetic symbols. For more information, see
    -   [Expressive neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-expressive)
    -   [English (Australian) symbols](/docs/text-to-speech?topic=text-to-speech-auSymbols-new)

    You can migrate from Australian English neural voices that are deprecated to the new expressive neural voices. For more information, see
    -   [Migrating from neural voices](/docs/text-to-speech?topic=text-to-speech-voices-migrate)

New Korean enhanced neural voice
:   The service now supports a new enhanced neural female voice for Korean: `ko-KR_JinV3Voice`. The new voice is generally available (GA) for production use. It supports the use of both standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) phonetic symbols. For more information, see
    -   [Enhanced neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-enhanced-neural)
    -   [Korean symbols](/docs/text-to-speech?topic=text-to-speech-koSymbols-new)

    You can migrate from Korean neural voices that are deprecated to the new enhanced neural voice. For more information, see
    -   [Migrating from neural voices](/docs/text-to-speech?topic=text-to-speech-voices-migrate)

Defect fix: French Canadian voice now handles numeric times properly
:   **Defect fix:** The French Canadian voices now pronounce times like `19:41` correctly. Previously, the voices were omitting elements of the time in the synthesized audio.

Defect fix: Japanese voice no longer inserts unexpected audio
:   **Defect fix:** The Japanese voice no longer inserts unexpected audio in speech synthesis results. Previously, additional audio was inserted in certain cases.

## 20 January 2023
{: #text-to-speech-20january2023}
{: release-note}

Cloud Foundry deprecation and migration to resource groups
:   {{site.data.keyword.IBM_notm}} announced the deprecation of IBM Cloud Foundry on 31 May 2022. As of 30 November 2022, new {{site.data.keyword.IBM_notm}} Cloud Foundry applications cannot be created and only existing users are able to deploy applications. {{site.data.keyword.IBM_notm}} Cloud Foundry reaches end of support on 1 June 2023. At that time, any {{site.data.keyword.IBM_notm}} Cloud Foundry application runtime instances running {{site.data.keyword.IBM_notm}} Cloud Foundry applications will be permanently disabled, deprovisioned, and deleted. For more information about the deprecation, see [Deprecation of {{site.data.keyword.IBM_notm}} Cloud Foundry](/docs/cloud-foundry-public?topic=cloud-foundry-public-deprecation).

    To continue to use your {{site.data.keyword.cloud_notm}} applications beyond 1 June 2023, you must migrate to resource groups before that date. Resource groups are conceptually similar to Cloud Foundry spaces. They include several extra benefits, such as finer-grained access control by using IBM Cloud Identity and Access Management (IAM), the ability to connect service instances to apps and service across different regions, and an easy way to view usage per group. For more information about migration, see [Migrating Cloud Foundry service instances and apps to a resource group](/docs/account?topic=account-migrate).

Defect fix: Specifying large cardinal numbers with the `<say-as>` element no longer causes errors for English voices
:   **Defect fix:** You can now use the `<say-as>` element to pronounce large numbers as cardinal numbers. Previously, enclosing a large number in the `<say-as>` element with the attribute `interpret-as="cardinal"` could cause speech synthesis to fail for English voices. For example, `<say-as interpret-as="cardinal">3,200</say-as>` could cause the service to generate an error. For more information, see [cardinal](/docs/text-to-speech?topic=text-to-speech-elements#say-as-cardinal) in the topic *SSML elements*.

Defect fix: Homonyms and other words are now pronounced correctly by English voices
:   **Defect fix:** The service now pronounces homonyms and other words correctly based on their context in English text that is to be synthesized. Previously, words such as `advocate` and `wifi` could be pronounced incorrectly by English voices.

## 30 November 2022
{: #text-to-speech-30november2022}
{: release-note}

Defect fix: Add rules for custom model naming documentation
:   **Defect fix:** The documentation now provides detailed rules for naming custom models. For more information, see
    -   [Creating a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsCreate)
    -   [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}

## 7 October 2022
{: #text-to-speech-7october2022}
{: release-note}

The service now enforces stricter SSML validation
:   The service now enforces stricter validation of input text that includes Speech Synthesis Markup Language (SSML) elements. Required elements of attributes must be specified with valid values. Otherwise, the request fails with a 400 error code. For more information about SSML validation and the requirements that marked-up text must meet, see [SSML validation](/docs/text-to-speech?topic=text-to-speech-ssml#ssml-errors).

Defect fix: The gender listed for the `en-US_MichaelExpressive` voice is now correct
:   **Defect fix:** When you list information about the available voices, the `gender` of the `en-US_MichaelExpressive` voice is now `male`. Previously, the voice's gender was mistakenly described as `female`. For more information, see [Listing information about voices](/docs/text-to-speech?topic=text-to-speech-voices-list).

## 23 September 2022
{: #text-to-speech-23september2022}
{: release-note}

New US English expressive neural voices
:   The service offers four new expressive neural voices for US English:
    -   `en-US_AllisonExpressive`
    -   `en-US_EmmaExpressive`
    -   `en-US_LisaExpressive`
    -   `en-US_MichaelExpressive`

    Expressive neural voices offer natural-sounding speech that is exceptionally clear, crisp, and fluid. The new voices are generally available (GA) for production use. They support the use of both standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) phonetic symbols. For more information, see
    -   [Expressive neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-expressive)
    -   [English (United States) symbols](/docs/text-to-speech?topic=text-to-speech-usSymbols)

New speaking styles for expressive neural voices
:   The expressive neural voices determine the sentiment of the text from the context of its words and phrases. The speech that they produce, in addition to having a very conversational style, reflects the mood of the text. But you can embellish the voices' natural tendencies by indicating that all or some of the text is to emphasize one of the following speaking styles:
    -   **Cheerful** - Expresses happiness and good news.
    -   **Empathetic** - Expresses empathy or sympathy.
    -   **Neutral** - Expresses objectivity and evenness.
    -   **Uncertain** - Expresses confusion or uncertainty.

    For more information, see [Using speaking styles](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#syntheses-expressive-styles).

New interjection emphasis with expressive neural voices
:   With expressive neural voices, the service automatically detects a set of common interjections based on context. When it synthesizes these interjections, it gives them the natural emphasis that a human would use in normal conversation. For some of the interjections, you can use SSML to enable or disable their emphasis. For more information, see [Emphasizing interjections](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#emphasizing-interjections).

New word emphais with expressive neural voices
:   The expressive voices use a conversational style that naturally applies the correct intonation from context. But you can indicate that one or more words are to be given more or less emphasis. The change in stress can be indicated by an increase or decrease in pitch, timing, volume, or other acoustic attributes. For more information, see [Emphasizing words](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#emphasizing-words).

## 21 September 2022
{: #text-to-speech-21september2022}
{: release-note}

New Activity Tracker event for GDPR deletion of user information
:   The service now returns an Activity Tracker event when you use the `DELETE /v1/user_data` method to delete all information about a user. The event is named `text-to-speech.gdpr-user-data.delete`. For more information, see [Activity Tracker events](/docs/text-to-speech?topic=text-to-speech-at-events).

Defect fix: Custom word translations now accept commas in all cases
:   **Defect fix:** Word translations added to custom models now accept commas in all cases. Previously, a comma in a translation could occasionally cause the translation to fail to generate valid audio when used for speech syntheses. This problem was identified in US English custom models.

Defect fix: French synthesis of dates is now consistent
:   **Defect fix:** French synthesis no longer includes the article "le" before dates of the form "the *ordinal* of *month*." Previously, the article was included only for the first day of the month for French (for example, "the first of September," "le premier septembre").

Known limitation with using the Ogg audio format with the Safari browser
:   By default, the service returns audio in the Ogg audio format with the Opus codec (`audio/ogg;codecs=opus`). However, the Ogg audio format is not supported with the Safari browser. If you are using the the {{site.data.keyword.texttospeechshort}} service with the Safari browser, you must specify a different format in which you want the service to return the audio.
    -   For more information about the available formats, see [Supported audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats#formats-supported).
    -   For more information about specifying a format, see [Specifying an audio format](/docs/text-to-speech?topic=text-to-speech-audio-formats#formats-specify).

## 31 August 2022
{: #text-to-speech-31august2022}
{: release-note}

New beta `rate_percentage` query parameter for controlling the global speaking rate
:   The service offers a new `rate_percentage` query parameter to modify the speaking rate for a speech synthesis request. The speaking rate is the speed at which the service speaks the text that it synthesizes into speech. A higher rate causes the text to be spoken more quickly; a lower rate causes the text to be spoken more slowly. The parameter changes the per-voice default rate for an entire request. For more information, see [Modifying the speaking rate](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-rate-percentage).

New beta `pitch_percentage` query parameter for controlling the global speaking pitch
:   The service offers a new `pitch_percentage` query parameter to modify the speaking pitch for a synthesis request. The speaking pitch represents the tone of the speech that the service synthesizes. It represents how high or low the tone of the voice is perceived by the listener. A higher pitch results in speech that is spoken at a higher tone and is perceived as a higher voice; a lower pitch results in speech that is spoken in a lower tone and is perceived as a lower voice. The parameter changes the per-voice default pitch for an entire request. For more information, see [Modifying the speaking pitch](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-pitch-percentage).

Defect fix: Japanese synthesis is improved to handle long strings of input text
:   **Defect fix:** The service now correctly synthesizes Japanese requests that include long strings of characters. Previously, the service failed to properly synthesize very long strings of Japanese text.

Documentation updates for the SSML `<prosody>` element
:   The documentation for the SSML `<prosody>` element and its `pitch` and `rate` parameters has been improved and clarified. It also now includes a description of the differences between the service and the latest version of the SSML specification. For more information, see [The `<prosody>` element](/docs/text-to-speech?topic=text-to-speech-elements#prosody_element).

## 3 August 2022
{: #text-to-speech-3august2022}
{: release-note}

The service does not support multilingual speech synthesis
:   The service does not support multilingual speech synthesis at this time. However, you can use customization to approximate the pronunciation of words from other languages. For more information, see [Multilingual speech synthesis](/docs/text-to-speech?topic=text-to-speech-voices-use#synthesis-multilingual).

## 27 July 2022
{: #text-to-speech-27july2022}
{: release-note}

New beta `spell_out_mode` parameter for German voices
:   To indicate how individual characters of a string are to be spelled out, you can now include the beta `spell_out_mode` query parameter with a synthesis request for a German voice. By default, the service spells out individual characters at the same rate at which it synthesizes text for a language. You can use the parameter to direct the service to spell out individual characters more slowly, in groups of one, two, or three characters. Use the parameter with the SSML `<say-as>` element to control how the characters of a string are synthesized. For more information, see [Specifying how strings are spelled out](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-spell-out-mode).

## 25 May 2022
{: #text-to-speech-25may2022}
{: release-note}

New support for `audio/alaw` audio format
:   The list of supported audio formats now includes `audio/alaw;rate={rate}`. Like `audio/basic` and `audio/mulaw`, this format provides single-channel audio that is encoded by using 8-bit u-law (or mu-law) data that is sampled at 8 kHz. For more information, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

## 19 May 2022
{: #text-to-speech-19may2022}
{: release-note}

Defect fix: Multiple consecutive SSML `<phoneme>` tags are now parsed correctly
:   **Defect fix:** The service now correctly synthesizes text that contains consecutive `<phoneme>` tags. Previously, if the text contained two or more consecutive `<phoneme>` tags, the service synthesized only the first tag, ignoring the others.

## 31 March 2022
{: #text-to-speech-31march2022}
{: release-note}

Important: Deprecation of all neural voices
:   **Important:** Effective **31 March 2022**, all neural voices are deprecated. The deprecated voices remain available to existing users until **31 March 2023**, when they will be removed from the service and the documentation. *No enhanced neural voices or expressive voices are deprecated.*

    The following neural voices are now deprecated:
    -   Arabic: `ar-MS_OmarVoice`
    -   Chinese (Mandarin): `zh-CN_LiNaVoice`, `zh-CN_WangWeiVoice`, and `zh-CN_ZhangJingVoice`
    -   Czech: `cs-CZ_AlenaVoice`
    -   Dutch (Belgian): `nl-BE_AdeleVoice` and `nl-BE_BramVoice`
    -   Dutch (Netherlands): `nl-NL_EmmaVoice` and `nl-NL_LiamVoice`
    -   English (Australian): `en-AU_CraigVoice`, `en-AU_MadisonVoice`, and `en-AU_SteveVoice`
    -   Korean: `ko-KR_HyunjunVoice`, `ko-KR_SiWooVoice`, `ko-KR_YoungmiVoice`, and `ko-KR_YunaVoice`
    -   Swedish: `sv-SE_IngridVoice`

    The deprecated neural voices continue to be available to existing users but are no longer available to new users:
    -   *Existing users:* Instances of the service created before *31 March 2022* can continue to use the deprecated voices for speech synthesis. The instances can also be used create and work with custom models that are based on the deprecated voices. And they can continue to list and query the voices with the `GET /v1/voices` and `GET /v1/voices/{voice}` methods.
    -   *New users:* Instances of the service created on or after *31 March 2022* cannot use the deprecated voices for speech synthesis. The instances also cannot be used create custom models that are based on the deprecated voices. And they cannot list or query the voices with the `GET /v1/voices` and `GET /v1/voices/{voice}` methods. Any API call that includes one of the deprecated voices returns an HTTP error code of 400 or 404, depending on the call.

    New voices for Australian English, Dutch, and Korean will be released by 15 February 2023. If you are using Australian English, Dutch, or Korean voices, your API calls will automatically redirect to the new voices in that language. Voices in Arabic, Chinese, Czech, Swedish, and Flemish will be removed from service.

    For more information about all available languages and voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

Deprecated standard voices are removed from the documentation
:   The standard concatenative voices were deprecated on [2 December 2020](#text-to-speech-2december2020). These standard voices have now been removed from the API reference. The topic *Migrating from standard to neural voices* has also been removed from the page [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

    Similarly, the former name of the Arabic voice, `ar-AR_OmarVoice`, was deprecated at the same time. It too has been removed from the documentation. Use the voice `ar-MS_OmarVoice` instead.

## 28 February 2022
{: #text-to-speech-28february2022}
{: release-note}

Change to word timing response for WebSocket interface
:   The response object that the service sends when you request word timings with the WebSocket interface has changed. The service now sends word timing results in a single array that includes a string followed by two floats:

    ```json
    {
      "words": [
        ["Hello", 0.0, 0.259],
        ["world", 0.259, 0.532]
      ]
    }
    ```
    {: codeblock}

    The service previously sent timing results as an array that included a string following by an array of two floats:

    ```json
    {
      "words": [
        ["Hello", [0.0629826778195474, 0.2590192737303819]],
        ["world", [0.2598829173456253, 0.5322130804452672]]
      ]
    }
    ```
    {: codeblock}

    Also, the level of precision for word timings and marks is now reduced to three decimal places. For more information about the new responses, see [Generating word timings](/docs/text-to-speech?topic=text-to-speech-timing).

    **Note:** Results for enhanced neural and neural voices were different previously. These inconsistencies could cause errors for the {{site.data.keyword.watson}} SDKs. The results for all voices are now consistent.

## 26 January 2022
{: #text-to-speech-26january2022}
{: release-note}

Defect fix: Improve SSML documentation
:   **Defect fix:** The SSML documentation was updated to correct the following errors:
    -   The examples of the `<break>` element are now correct. The element is unary, as now shown in the examples. The previous examples included open and close tags with embedded text. The embedded text was not spoken by the service. For more information, see [The `<break>` element](/docs/text-to-speech?topic=text-to-speech-elements#break_element).
    -   The service supports SSML version 1.1. All references and examples now use the correct version. The documentation previously referred to version 1.0.

## 3 December 2021
{: #text-to-speech-3december2021}
{: release-note}

New Czech neural voice: `cs-CZ_AlenaVoice`
:   A new language, Czech, with a new female voice, `cs-CZ_AlenaVoice`, is now available. The voice is a neural voice.

New Belgian Dutch neural voice: `nl-BE_BramVoice`
:   A new male Belgian Dutch (Flemish) voice, `nl-BE_BramVoice`, is now available. The voice is a neural voice.

Defect fix: Improve SSML and speech synthesis
:   **Defect fix:**  The following defects for the Speech Synthesis Markup Language (SSML) and speech synthesis were fixed with this release:

    -   The `pitch` attribute of the `<prosody>` element is now applied to all specified text. Previously, the pitch change was not always applied to the first word of the affected text. Also, the documentation now includes additional guidance about specifying a `pitch` value. For more information, see [The `pitch` attribute](/docs/text-to-speech?topic=text-to-speech-elements#prosody-pitch).
    -   Speech synthesis of Japanese text now speaks the audio more slowly. Previously, the synthesized speech was being spoken too quickly. If you find that synthesis of Japanese text is still spoken too quickly for your application, use the `rate` attribute of the SSML `<prosody>` element to control the rate of speech. For more information, see [The `rate` attribute](/docs/text-to-speech?topic=text-to-speech-elements#prosody-rate).
    -   Neural voices now parse the escaped apostrophe character (`&apos;`) properly. Previously, some neural voices were not interpreting the character properly.

## 22 October 2021
{: #text-to-speech-22october2021}
{: release-note}

Multiple neural voice improvements
:   The existing neural voices for Chinese, Dutch (Belgian and Netherlands), Australian English, and Korean have been updated for improved speech synthesis and enhanced audio results. For more information about all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

New Australian English neural voice: `en-AU_SteveVoice`
:   A new male Australian English voice, `en-AU_SteveVoice`, is now available. The voice is a neural voice.

New Swedish neural voice: `sv-SE_IngridVoice`
:   A new language, Swedish, with a new female voice, `sv-SE_IngridVoice`, is now available. The voice is a neural voice.

## 6 October 2021
{: #text-to-speech-6october2021}
{: release-note}

New US HIPAA support for Premium plans in Dallas location
:   US Health Insurance Portability and Accountability Act (HIPAA) support is now available for Premium plans that are hosted in the Dallas (`us-south`) location. For more information, see [Health Insurance Portability and Accountability Act (HIPAA)](/docs/text-to-speech?topic=text-to-speech-information-security#hipaa).

Defect fix: Improve Latin American Spanish enhanced neural voice
:   **Defect fix:** For the Latin American Spanish voice (`es-LA_SofiaV3Voice`), questions of all types now use the correct intonation.

## 16 September 2021
{: #text-to-speech-16september2021}
{: release-note}

Defect fix: Improve Castilian Spanish and North American Spanish enhanced neural voices
:   **Defect fix:** For the Castilian Spanish (`es-ES_EnriqueV3Voice` and `es-ES_LauraV3Voice`) and North American Spanish (`es-US_SofiaV3Voice`) voices, questions of all types now use the correct intonation. For the Latin American Spanish voice (`es-LA_SofiaV3Voice`), some questions do not use the correct intonation and sound instead like statements. The Latin American Spanish voice will be fixed soon.

## 16 July 2021
{: #text-to-speech-16july2021}
{: release-note}

New Belgian Dutch neural voice: `nl-BE_AdeleVoice`
:   The service now supports Belgian Dutch (Flemish) with the neural voice `nl-BE_AdeleVoice`. The Belgian Dutch voice supports customization and is generally available (GA) for production use.

## 12 April 2021
{: #text-to-speech-12april2021}
{: release-note}

New Canadian French enhanced neural voice: `fr-CA_LouiseV3Voice`
:   The service now supports Canadian French with the enhanced neural voice `fr-CA_LouiseV3Voice`. The Canadian French voice supports customization and is generally available (GA) for production use.
    -   To hear a sample of the new voice, see [Supported languages and voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices).
    -   For more information about the phonetic symbols and Unicode values that are available for the Canadian French language, see [French (Canadian) symbols](/docs/text-to-speech?topic=text-to-speech-caSymbols).

New Tune by Example feature
:   The new Tune by Example feature lets you control how specified text is spoken by the service. The feature is beta functionality that is supported only for US English custom models and voices. It has two components:
    -   *Custom prompts* include the written text that is to be spoken and recorded audio that speaks the text as you want to hear it. The audio specifies the intonation, cadence, and stress of the synthesized text. The prompt can emphasize different syllables or words, introduce pauses, and generally make the synthesized audio sound more natural and appropriate for its context.
    -   *Speaker models* provide enrollment audio for a user who speaks one or more prompts. A speaker model provides an audio sample of a user's voice. The service trains itself on the voice, which can help it to produce higher-quality prompts for that speaker.

    You specify a custom prompt with a speech synthesis request to indicate how the service's voice is to pronounce the text. To specify a prompt, you use the SSML extension `<ibm:prompt id="{prompt_id}"/>`. The synthesized audio duplicates the prosody of the prompt.

    For more information about using the Tune by Example feature, see the following topics:

    -   [Understanding Tune by Example](/docs/text-to-speech?topic=text-to-speech-tbe-intro)
    -   [Rules for creating custom prompts and speaker models](/docs/text-to-speech?topic=text-to-speech-tbe-rules)
    -   [Creating a custom prompt](/docs/text-to-speech?topic=text-to-speech-tbe-create)
    -   [Using a custom prompt for speech synthesis](/docs/text-to-speech?topic=text-to-speech-tbe-use)
    -   [Managing custom prompts](/docs/text-to-speech?topic=text-to-speech-tbe-custom-prompts)
    -   [Managing speaker models](/docs/text-to-speech?topic=text-to-speech-tbe-speaker-models)

New Tune be Example methods
:   The service includes eight new methods for working with the Tune by Example feature. The descriptions of the new methods that follow provide links to their entries in the API & SDK reference. You might need to select the `Curl` tab of the reference to see the new methods.

    -   The service includes four methods for working with custom prompts:

        -   [Add a custom prompt](https://{DomainName}/apidocs/text-to-speech/text-to-speech#addcustomprompt){: external}: `POST /v1/customizations/{customization_id}/prompts/{prompt_id}`
        -   [List custom prompts](https://{DomainName}/apidocs/text-to-speech/text-to-speech#listcustomprompts){: external}: `GET /v1/customizations/{customization_id}/prompts`
        -   [Get a custom prompt](https://{DomainName}/apidocs/text-to-speech/text-to-speech#getcustomprompt){: external}: `GET /v1/customizations/{customization_id}/prompts/{prompt_id}`
        -   [Delete a custom prompt](https://{DomainName}/apidocs/text-to-speech/text-to-speech#deletecustomprompt){: external}: `DELETE /v1/customizations/{customization_id}/prompts/{prompt_id}`

    -   The service includes four methods for working with speaker models:

        -   [Create a speaker model](https://{DomainName}/apidocs/text-to-speech/text-to-speech#createspeakermodel){: external}: `POST /v1/speakers`
        -   [List speaker models](https://{DomainName}/apidocs/text-to-speech/text-to-speech#listspeakermodels){: external}: `GET /v1/speakers`
        -   [Get a speaker model](https://{DomainName}/apidocs/text-to-speech/text-to-speech#getspeakermodel){: external}: `GET /v1/speakers/{speaker_id}`
        -   [Delete a speaker model](https://{DomainName}/apidocs/text-to-speech/text-to-speech#deletespeakermodel){: external}: `DELETE /v1/speakers/{speaker_id}`

    Activity Tracker actions are available for all new Tune by Example events. For more information, see [Tune by Example events](/docs/text-to-speech?topic=text-to-speech-at-events#at-events-tbe).

Updates to Activity Tracker actions for customization
:   The names of the actions for the Activity Tracker events for the customization methods have changed. The actions now include the string `custom-model` instead of `custom-voice`. The old names of the actions are deprecated. The old names are still available for use but will be removed at a future date. Migrate to the new names that are listed in [Customization events](/docs/text-to-speech?topic=text-to-speech-at-events#at-events-custom) at your earliest convenience.

    **Create events** *Deprecated action name* -> *New action name*
    -   `text-to-speech.custom-voice.create` -> `text-to-speech.custom-model.create`
    -   `text-to-speech.custom-voice-word-list.create` -> `text-to-speech.custom-model-word-list.create`
    -   `text-to-speech.custom-voice-word.create` -> `text-to-speech.custom-model-word.create`

    **Read events** *Deprecated action name* -> *New action name*
    -   `text-to-speech.custom-voice-list.read` -> `text-to-speech.custom-model-list.read`
    -   `text-to-speech.custom-voice.read` -> `text-to-speech.custom-model.read`
    -   `text-to-speech.custom-voice-word-list.read` -> `text-to-speech.custom-model-word-list.read`
    -   `text-to-speech.custom-voice-word.read` -> `text-to-speech.custom-model-word.read`

    **Update event** *Deprecated action name* -> *New action name*
    -   `text-to-speech.custom-voice.update` -> `text-to-speech.custom-model.update`

    **Delete events** *Deprecated action name* -> *New action name*
    -   `text-to-speech.custom-voice.delete` -> `text-to-speech.custom-model.delete`
    -   `text-to-speech.custom-voice-word.delete` -> `text-to-speech.custom-model-word.delete`

## 2 December 2020
{: #text-to-speech-2december2020}
{: release-note}

Multiple voice improvements
:   The voices offered by the service have undergone significant change. The service supports new languages and voices, has improved the quality of many voices, and has deprecated many older voices. In addition, all of the service's voices are now customizable and generally available (GA) for production use.

New neural and enhanced neural voices
:   To optimize the overall quality of voice synthesis, all available voices are now based on neural technology. The service offers two types of voices that are based on neural technology:

    -   *Neural voices*, which do *not* include the string `V3` in their names, are now available for Arabic, Australian English, Chinese, Netherlands Dutch, and Korean. Neural voices support the use of the International Phonetic Alphabet (IPA) with the Speech Synthesis Markup Language (SSML) `<phoneme>` element.
    -   *Enhanced neural voices*, which include the string `V3` in their names, are now available for Brazilian Portuguese, United Kingdom and United States English, French, German, Italian, Japanese, and Spanish (all dialects). Enhanced neural voices support the use of both IPA and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) with the SSML `<phoneme>` element. Enhanced neural voices also achieve a slightly higher degree of natural-sounding speech. And further customization capabilities will be exposed for enhanced neural voices in the coming months.

    The service no longer offers standard voices for any language. Standard voices used concatenative synthesis to assemble segments of recorded speech to generate the requested audio.

    For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

New Australian English and Korean neural voices
:   The following Australian English and Korean voices are new:

    -   The service now supports Australian English with the following two neural voices: `en-AU_CraigVoice` and `en-AU_MadisonVoice`.
    -   The service now supports two new Korean neural voices: `ko-KR_HyunjunVoice` and `ko-KR_SiWooVoice`.

Improved neural voices
:   The voices for the existing Arabic, Chinese, Netherlands Dutch, and Korean languages, all of which were concatenative, are now neural:

    -   `ar-MS_OmarVoice`
    -   `ko-KR_YoungmiVoice`
    -   `ko-KR_YunaVoice`
    -   `nl-NL_EmmaVoice`
    -   `nl-NL_LiamVoice`
    -   `zh-CN_LiNaVoice`
    -   `zh-CN_WangWeiVoice`
    -   `zh-CN_ZhangJingVoice`

    The following additional changes have also been made:

    -   The Arabic voice is now named `ar-MS_OmarVoice`. The former name, `ar-AR_OmarVoice`, is deprecated. It will continue to function for at least one year but might be removed at a future date. You are encouraged to migrate to the new name at your earliest convenience.
    -   The Arabic language now supports the use of IPA symbols and Unicode values with the SSML `<phoneme>` element. To create a custom model for Arabic, you must use the language identifier `ar-MS`. The identifier `ar-AR` is not supported for customization.
    -   The IPA symbols for the Arabic language are new. The previously documented symbols have been completely replaced.
    -   The IPA symbols for the Netherlands Dutch language have been changed as follows:
        -   Netherlands Dutch no longer supports the following IPA symbols: `tʲ` (`0074+02B2`), `ɲ` (`0272`), `ʦ` (`02A6`), and `ʔ` (`0294`).
        -   Netherlands Dutch now supports the following IPA symbol: `ɣ` (`0263`).

Deprecated standard voices
:   The following standard concatenative voices are now deprecated:

    -   `de-DE_BirgitVoice`
    -   `de-DE_DieterVoice`
    -   `en-GB_KateVoice`
    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `es-ES_LauraVoice`
    -   `es-LA_SofiaVoice`
    -   `es-US_SofiaVoice`
    -   `fr-FR_ReneeVoice`
    -   `it-IT_FrancescaVoice`
    -   `ja-JP_EmiVoice`
    -   `pt-BR_IsabelaVoice`

    All of the standard voices that have been deprecated have equivalent neural counterparts, so no voice is being taken away. Rather, you can change to the equivalent neural version of the voice (for example, from `de-DE_BirgitVoice` to `de-DE_BirgitV3Voice`) for better speech-synthesis results.

    These deprecated voices are removed from the published documentation. They will continue to function for at least one year but might be removed at a future date. You are encouraged to migrate to the equivalent neural voices at your earliest convenience.

    If you omit the optional `voice` parameter from a speech synthesis request, the service uses `en-US_MichaelV3Voice` by default. This neural voice replaces the now-deprecated `en-US_MichaelVoice` standard voice that was the previous default.

Deprecated features
:   The following features were available only for standard concatenative voices. They are deprecated and have been removed from the published documentation. They will continue to function for at least one year but might be removed at a future date. You are encouraged to remove these features from your applications and to migrate to neural voices at your earliest convenience.

    -   *Expressive SSML.* This was an IBM extension to SSML that was supported only for the `en-US_AllisonVoice` voice.
    -   *Voice transformation SSML.* This was an IBM extension to SSML that was supported only for the `en-US_AllisonVoice`, `en-US_LisaVoice`, and `en-US_MichaelVoice` voices.
    -   *The `volume` attribute of the `<prosody>` element.* This attribute was available for all standard voices.

    Including these SSML elements with a synthesis request for a neural voice generates an HTTP 400 response code because the request fails SSML validation. For more information about SSML validation, see [SSML validation](/docs/text-to-speech?topic=text-to-speech-ssml#ssml-errors).

New support for Cross-Origin Resource Sharing
:   Cross-Origin Resource Sharing (CORS) support is now available for all voices from the Google Chrome™ and Apple® Safari browsers. It is *not* available from the Mozilla Firefox™ browser for voices in the following languages: Arabic, Australian English, Chinese, Netherlands Dutch, and Korean. For more information, see [Leveraging CORS support](/docs/text-to-speech?topic=text-to-speech-service-features#features-cors).

## 10 September 2020
{: #text-to-speech-10september2020}
{: release-note}

Defect fix: Improve Japanese voice
:   **Defect fix:** For the `ja-JP_EmiV3Voice` voice, the service now correctly parses SSML input text that includes a prosody rate specification. Previously, the following use of the `<prosody>` element worked properly:

    ```xml
    <speak>成功する/繁栄する</speak>
    ```
    {: codeblock}

    But the following use of the `rate` attribute with the `<prosody>` element caused the service to read and speak the embedded SSML notation:

    ```xml
    <speak>
      <prosody rate="fast">成功する/繁栄する</prosody>
    </speak>
    ```
    {: codeblock}

    The service now correctly parses and applies the `rate` attribute of the `<prosody>` element for Japanese input.

## 4 September 2020
{: #text-to-speech-4september2020}
{: release-note}

Customization interface is now generally available
:   The customization interface is now generally available (GA). Customization is no longer beta functionality. You can use the customization interface to specify how the service pronounces unusual words that occur in your input text by creating language-specific custom dictionaries. It can be used with all generally available and beta voices. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

## 24 June 2020
{: #text-to-speech-24june2020}
{: release-note}

New UK English and French neural voices
:   The service now offers three new neural voices:
    -   UK English: `en-GB_CharlotteV3Voice` and `en-GB_JamesV3Voice`
    -   French: `fr-FR_NicolasV3Voice`

    It also offers an improved version of the existing UK neural voice, `en-GB_KateV3Voice`. For more information about all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

Support for SSML `digits` attribute of `<say-as>` element for Japanese
:   The service now supports the `digits` attribute of the SSML `<say-as>` element with its Japanese voice. For more information, see [The say-as element](/docs/text-to-speech?topic=text-to-speech-elements#say-as_element).

## 1 April 2020
{: #text-to-speech-1april2020}
{: release-note}

New Korean standard voices: `ko-KR_YoungmiVoice` and `ko-KR_YunaVoice`
:   The service now supports two standard female Korean voices: `ko-KR_YoungmiVoice` and `ko-KR_YunaVoice`. The following information applies to both Korean voices:
    -   The voices are beta functionality. They might not be ready for production use and are subject to change. They are initial offerings that are expected to improve in quality with time and usage.
    -   The voices support customization and the `/v1/pronunciation` method.
    -   The voices support the `<mark>` element and the `timings` parameter that are available with the WebSocket interface.
    -   The voices support all Speech Synthesis Markup Language (SSML) elements except for expressive SSML and voice transformation SSML.
    -   The voices support only the International Phonetic Alphabet (IPA), not {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR), with the `<phoneme>` element.

New feature support for Arabic, Chinese, and Netherlands Dutch voices
:   The beta Arabic, Chinese, and Netherlands Dutch voices now support the following features:
    -   Customization and the `/v1/pronunciation` method.
    -   The `<mark>` element and the `timings` parameter that are available with the WebSocket interface.

    See the following sections for additional information:

    -   For more information about all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).
    -   For more information about using the WebSocket interface to obtain word timings, see [Generating word timings](/docs/text-to-speech?topic=text-to-speech-timing).
    -   For more information about customization, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).
    -   For more information about the use of IPA and SPR with customization, see [Understanding phonetic symbols](/docs/text-to-speech?topic=text-to-speech-symbols). (The IPA symbols for the Arabic, Chinese, Netherlands Dutch, and Korean languages are not yet documented. This documentation will be made available soon.)

## 24 February 2020
{: #text-to-speech-24february2020}
{: release-note}

New US English and German neural voices
:   The service now supports five new neural voices:

    -   US English: `en-US_EmilyV3Voice`, `en-US_HenryV3Voice`, `en-US_KevinV3Voice`, and `en-US_OliviaV3Voice`
    -   German: `de-DE_ErikaV3Voice`

    The new voices do not support the following SSML elements:

    -   Expressive SSML with the `<express-as>` element
    -   Voice Transformation with the `<voice-transformation>` element
    -   The `volume` attribute of the `<prosody>` element

    For more information about these and all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

New support for Activity Tracker
:   The service now supports the use of Activity Tracker events for all customization operations. {{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. For more information, see [Activity Tracker events](/docs/text-to-speech?topic=text-to-speech-at-events).

## 18 December 2019
{: #text-to-speech-18december2019}
{: release-note}

New standard Arabic, Chinese, and Netherlands Dutch voices
:   The service now supports six new standard voices in three new languages:

    -   *Arabic:* `ar-AR_OmarVoice`
    -   *Chinese (Mandarin):* `zh-CN_LiNaVoice`, `zh-CN_WangWeiVoice`, and `zh-CN_ZhangJingVoice`
    -   *Netherlands Dutch:* `nl-NL_EmmaVoice` and `nl-NL_LiamVoice`

    The following information applies to these new standard voices:

    -   The new voices are beta functionality. The voices might not be ready for production use and are subject to change. They are initial offerings that are expected to improve in quality with time and usage.
    -   The voices do not support the `<mark>` element and `timings` parameter that are available with the WebSocket interface.
    -   The voices do not support customization or the `/v1/pronunciation` method.
    -   The voices do not support expressive SSML or voice transformation SSML.
    -   The voices do support all other SSML elements. However, they support only the International Phonetic Alphabet (IPA), not {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR), with the `<phoneme>` element.

    For more information about these and all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## 12 December 2019
{: #text-to-speech-12december2019}
{: release-note}

Full support for {{site.data.keyword.cloud_notm}} IAM
:   The {{site.data.keyword.texttospeechshort}} service now supports the full implementation of {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). API keys for {{site.data.keyword.watson}} services are no longer limited to a single service instance. You can create access policies and API keys that apply to more than one service, and you can grant access between services. For more information about IAM, see [Authenticating to {{site.data.keyword.watson}} services](/docs/watson?topic=watson-iam).

    To support this change, the API service endpoints use a different domain and include the service instance ID. The pattern is `api.{location}.text-to-speech.watson.cloud.ibm.com/instances/{instance_id}`.

    -   Example HTTP URL for an instance hosted in the Dallas location:

        `https://api.us-south.text-to-speech.watson.cloud.ibm.com/instances/6bbda3b3-d572-45e1-8c54-22d6ed9e52c2`

    -   Example WebSocket URL for an instance hosted in the Dallas location:

        `wss://api.us-south.text-to-speech.watson.cloud.ibm.com/instances/6bbda3b3-d572-45e1-8c54-22d6ed9e52c2`

    For more information about the URLs, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech/text-to-speech#service-endpoint){: external}.

    These URLs do not constitute a breaking change. The new URLs work for both your existing service instances and for new instances. The original URLs continue to work on your existing service instances for at least one year, until December 2020.

New network and data security features
:   Support for the following new network and data security features is now available:
    -   *Support for private network endpoints*

        Users of Premium plans can create private network endpoints to connect to the {{site.data.keyword.texttospeechshort}} service over a private network. Connections to private network endpoints do not require public internet access. For more information, see [Public and private network endpoints](/docs/text-to-speech/?topic=watson-public-private-endpoints).
    -   *Support for data encryption with customer-managed keys*

        Users of new Premium and Dedicated instances can integrate {{site.data.keyword.keymanagementservicefull}} with the {{site.data.keyword.texttospeechshort}} service to encrypt your data and manage encryption keys. For more information, see [Protecting sensitive information in your {{site.data.keyword.watson}} service](/docs/watson?topic=watson-keyservice).

## 12 November 2019
{: #text-to-speech-12november2019}
{: release-note}

New Seoul location now available
:   The {{site.data.keyword.texttospeechshort}} service is now available in the {{site.data.keyword.cloud_notm}} Seoul location (**kr-seo**). As with other locations, the {{site.data.keyword.cloud_notm}} location uses token-based IAM authentication. All new service instances that you create in this location use IAM authentication.

## 1 October 2019
{: #text-to-speech-1october2019}
{: release-note}

New US HIPAA support for Premium plans in Washington, DC, location
:   US HIPAA support is available for Premium plans that are hosted in the Washington, DC, location and are created on or after 1 April 2019. For more information, see [US Health Insurance Portability and Accountability Act (HIPAA)](/docs/text-to-speech?topic=text-to-speech-information-security#hipaa).

## 22 August 2019
{: #text-to-speech-22august2019}
{: release-note}

Defect fix: Multiple small improvements
:   **Defect fix:** The service was updated for small defect fixes and improvements.

## 30 July 2019
{: #text-to-speech-30july2019}
{: release-note}

New Japanese neural voice: `ja-JP_EmiV3Voice`
:   The service now offers a neural voice in Japanese: `ja-JP_EmiV3Voice`. Both standard and neural versions of all available voices in all supported languages are now available. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## 24 June 2019
{: #text-to-speech-24june2019}
{: release-note}

New support for standard and neural voices
:   The service now offers two versions of most of its available voices:
    -   *Standard voices* that use concatenative synthesis to assemble segments of recorded speech to generate audio. Standard voices do not include a version string in their name (for example, `en-US_AllisonVoice`).
    -   *Neural voices* that use Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech. Neural voices include a version string (`V3`) in their name (for example, `en-US_AllisonV3Voice`).

    Neural versions are available for all standard voices except for the `ja-JP_EmiVoice` voice, which is pending and will be available soon. You cannot use the SSML `<express-as>` and `<voice-transformation>` elements with the neural voices, and you cannot use the `volume` attribute of the `<prosody>` element with the neural voices. For more information about all available voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

V2 neural voices withdrawn from service
:   The service no longer includes the `V2` DNN voices that were previously available. If you use a `V2` voice in your application, the service automatically uses the equivalent `V3` voice instead.

## 24 March 2019
{: #text-to-speech-24march2019}
{: release-note}

New V2 neural German voices
:   The service now offers `V2` Deep Neural Network (DNN) versions of its German voices:
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

    For more information about DNN-based voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

New support for `pitch` and `rate` attributes of the SSML `<prosody>` element
:   All of the service's DNN-based voices now support the `pitch` and `rate` attributes of the SSML `<prosody>` element. The DNN-based voices do not support the `volume` attribute of the `<prosody>` element. For more information, see [The prosody element](/docs/text-to-speech?topic=text-to-speech-elements#prosody_element).

## 21 March 2019
{: #text-to-speech-21march2019}
{: release-note}

Visibility of service credentials now restricted by role
:   Users can now see only service credential information that is associated with the role that has been assigned to their {{site.data.keyword.cloud_notm}} account. For example, if you are assigned a `reader` role, any `writer` or higher levels of service credentials are no longer visible.

    This change does not affect API access for users or applications with existing service credentials. The change affects only the viewing of credentials within {{site.data.keyword.cloud_notm}}.

## 4 March 2019
{: #text-to-speech-4march2019}
{: release-note}

New V2 neural English and Italian voices
:   The service now offers four new `V2` voices that use deep-learning synthesis to generate audio:

    -   `en-US_AllisonV2Voice`
    -   `en-US_LisaV2Voice`
    -   `en-US_MichaelV2Voice`
    -   `it-IT_FrancescaV2Voice`

    These new voices use machine learning and a DNN to synthesize text to speech. Deep-learning, or Deep Neural Network (DNN)-based, synthesis produces audio with a more natural prosody and a more consistent overall quality.

    But the new voices also produce audio with different signal qualities from the existing voices, so they might not be appropriate for all applications. Also, the new voices do not support the SSML elements `<prosody>`, `<express-as>`, and `<voice-transformation>`.

    For more information about these DNN-based voices and how they differ from the existing voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## 28 January 2019
{: #text-to-speech-28january2019}
{: release-note}

New support for {{site.data.keyword.cloud_notm}} IAM by WebSocket interface
:   The WebSocket interface now supports token-based Identity and Access Management (IAM) authentication from browser-based JavaScript code. The limitation to the contrary has been removed. To establish an authenticated connection with the WebSocket `/v1/synthesize` method:

    -   If you use IAM authentication, include the `access_token` query parameter.
    -   If you use Cloud Foundry service credentials, include the `watson-token` query parameter.

    For more information, see [Open a connection](/docs/text-to-speech?topic=text-to-speech-usingWebSocket#WSopen).

## 13 December 2018
{: #text-to-speech-13december2018}
{: release-note}

New London location now available
:   The {{site.data.keyword.texttospeechshort}} service is now available in the {{site.data.keyword.cloud}} London location (**eu-gb**). Like all locations, London uses token-based Identity and Access Management (IAM) authentication. All new service instances that you create in this location use IAM authentication.

## 7 November 2018
{: #text-to-speech-7november2018}
{: release-note}

New Tokyo location now available
:   The {{site.data.keyword.texttospeechshort}} service is now available in the {{site.data.keyword.cloud}} Tokyo location (**jp-tok**). Like all locations, Tokyo uses token-based Identity and Access Management (IAM) authentication. All new service instances that you create in this location use IAM authentication.

## 30 October 2018
{: #text-to-speech-30october2018}
{: release-note}

New support for token-based {{site.data.keyword.cloud_notm}} IAM
:   The {{site.data.keyword.texttospeechshort}} service has migrated to token-based Identity and Access Management (IAM) authentication for all locations. All {{site.data.keyword.cloud_notm}} services now use IAM authentication. The {{site.data.keyword.texttospeechshort}} service migrated in each location on the following dates:

    -   Dallas (**us-south**): October 30, 2018
    -   Frankfurt (**eu-de**): October 30, 2018
    -   Washington, DC (**us-east**): June 12, 2018
    -   Sydney (**au-syd**): May 15, 2018

    The migration to IAM authentication affects new and existing service instances differently:

    -   *All new service instances that you create in any location* now use IAM authentication to access the service. You can pass either a bearer token or an API key: Tokens support authenticated requests without embedding service credentials in every call; API keys use HTTP basic authentication. When you use any of the {{site.data.keyword.watson}} SDKs, you can pass the API key and let the SDK manage the lifecycle of the tokens.
    -   *Existing service instances that you created in a location before the indicated migration date* continue to use the `{username}` and `{password}` from their previous Cloud Foundry service credentials for authentication until you migrate them to use IAM authentication.

    For more information, see the following documentation:

    -   To learn which authentication mechanism your service instance uses, view your service credentials by clicking the instance on the [{{site.data.keyword.cloud_notm}} dashboard](https://{DomainName}/dashboard/apps){: external}.
    -   For more information about using IAM tokens with {{site.data.keyword.watson}} services, see [Authenticating to {{site.data.keyword.watson}} services](/docs/watson?topic=watson-iam).
    -   For examples that use IAM authentication, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

## 12 June 2018
{: #text-to-speech-12june2018}
{: release-note}

New features for applications hosted in Washington, DC, location
:   The following features are enabled for applications that are hosted in Washington, DC (**us-east**):

    -   The service now supports a new API authentication process. For more information, see the [30 October 2018 service update](#text-to-speech-30october2018).
    -   The service now supports the `X-Watson-Metadata` header and the `DELETE /v1/user_data` method. For more information, see [Information security](/docs/text-to-speech?topic=text-to-speech-information-security).

## 15 May 2018
{: #text-to-speech-15may2018}
{: release-note}

New features for applications hosted in Sydney location
:   The following features are enabled for applications that are hosted in Sydney (**au-syd**):

    -   The service now supports a new API authentication process. For more information, see the [30 October 2018 service update](#text-to-speech-30october2018).
    -   The service now supports the `X-Watson-Metadata` header and the `DELETE /v1/user_data` method. For more information, see [Information security](/docs/text-to-speech?topic=text-to-speech-information-security).

## 2 October 2017
{: #text-to-speech-2october2017}
{: release-note}

Changes to `audio/l16` audio format
:   For the `audio/l16` format, you can now optionally specify the endianness of the audio that is returned. (You must already specify the sampling rate.) Examples are `audio/l16;rate=22050;endianness=big-endian` and `audio/l16;rate=22050;endianness=little-endian`; the default is big endian. For more information, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

## 14 July 2017
{: #text-to-speech-14july2017}
{: release-note}

New support for MP3 (MPEG) audio format
:   The service now supports the MP3 or Motion Picture Experts Group (MPEG) audio format. For more information about supported audio formats, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

## 10 April 2017
{: #text-to-speech-10april2017}
{: release-note}

New support for Web Media (WebM) audio format
:   The service now supports the Web Media (WebM) audio format with the Opus or Vorbis codec. The service now also supports the Ogg audio format with the Vorbis codec in addition to the Opus codec. For more information about supported audio formats, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

New support for Cross-Origin Resource Sharing
:   The service now supports Cross-Origin Resource Sharing (CORS) to allow browser-based clients to call the service directly. For more information, see [Leveraging CORS support](/docs/text-to-speech?topic=text-to-speech-service-features#features-cors).

Changes to successful HTTP response codes
:   The HTTP response codes for successful completion of some methods of the customization interface changed:
    -   The `POST /v1/customizations` method now returns 201 (instead of 200).
    -   The `POST /v1/customizations/{customization_id}` method now returns 200 (instead of 201).
    -   The `POST /v1/customizations/{customization_id}/words` method now returns 200 (instead of 201).
    -   The `PUT /v1/customizations/{customization_id}/words/{word}` method now returns 200 (instead of 201).

New errors for misuse of Japanese `part_of_speech` parameter
:   The `POST /v1/customizations/{custom_id}/words` and `PUT /v1/customizations/{customization_id}/words/{word}` methods now return HTTP response code 400 with the error message `Part of speech is supported for ja-JP language only` if you attempt to specify a `part_of_speech` for a language other than Japanese.

Changes to response body for adding words method
:   The `POST /v1/customizations/{custom_id}/words` method now returns an empty response body (`{}`).

## 1 December 2016
{: #text-to-speech-1december2016}
{: release-note}

New Latin American Spanish voice: `es-LA_SofiaVoice`
:   The service includes a new voice, `es-LA_SofiaVoice`, which is the Latin American equivalent of the `es-US_SofiaVoice` voice. The most significant difference between the two voices concerns how they interpret a `$` (dollar sign): The Latin American version uses the term *pesos*; the North American version uses the term *dolares*. Other minor differences might also exist between the two voices.

New US English voices: `en-US_LisaVoice` and `en-US_MichaelVoice`
:   In addition to the `en-US_AllisonVoice`, two more voices are now transformable with SSML voice transformation: `en-US_LisaVoice` and `en-US_MichaelVoice`.

Changes to customization for Japanese
:   When you use the customization interface with Japanese, the service now matches the longest word from the word/translation pairs that are defined for a custom model. For example, consider the following two entries for a custom model:

    ```json
    {
      "words": [
        {"word":"ＮＹ", "translation":"ニューヨーク", "part_of_speech":"Mesi"},
        {"word":"ＮＹＣ", "translation":"ニューヨークシティ", "part_of_speech":"Mesi"}
      ]
    }
    ```
    {: codeblock}

    If the service finds the string `ＮＹＣ` in the input text, it matches that word because it is a longer match than `ＮＹ`. Previously, the service would have matched the string `ＮＹ`. For more information about working with Japanese entries for a custom model, see [Working with Japanese entries](/docs/text-to-speech?topic=text-to-speech-rules#jaNotes).

## 22 September 2016
{: #text-to-speech-22september2016}
{: release-note}

Customization now available for all languages
:   The customization interface, which includes the customization and `GET /v1/pronunciation` methods, is now available for all languages that are supported by the service. The interface remains a beta release. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

New Japanese support for SSML
:   The service now supports SSML for Japanese. For general information about SSML support, see [Understanding SSML](/docs/text-to-speech?topic=text-to-speech-ssml). For information about Japanese SPR and IPA symbols, see [Japanese symbols](/docs/text-to-speech?topic=text-to-speech-jaSymbols). Extra considerations and a `part_of_speech` field apply when creating entries for words in a Japanese custom model. For more information, see [Working with Japanese entries](/docs/text-to-speech?topic=text-to-speech-rules#jaNotes).

New voice transformation SSML feature
:   The service now offers SSML voice transformation via the new `<voice-transformation>` element. You can expand the range of possible voices by creating custom transformations that modify the pitch, pitch range, glottal tension, breathiness, rate, and timbre of a voice. The service also offers two built-in virtual voices, *Young* and *Soft*. The service currently supports voice transformation only for the US English Allison voice.

Word timings now available with WebSocket interface
:   The service can now return word timing information for all strings of the input text that you pass to the WebSocket interface. To receive the start and end time of every string in the input, specify an array that includes the string `words` for the optional `timings` parameter of the JSON object that you pass to the service. The feature is not currently available for Japanese input text. For more information, see [Generating word timings](/docs/text-to-speech?topic=text-to-speech-timing).

New support for SSML validation
:   The service now validates all SSML elements that you submit in any context. If it finds an invalid tag, the service reports an HTTP 400 response code with a descriptive message, and the method fails. In previous releases, the service handled errors inconsistently; specifying an invalid word pronunciation, for example, could lead to unpredictable or inconsistent behavior. For more information, see [SSML validation](/docs/text-to-speech?topic=text-to-speech-ssml#ssml-errors).

IBM SPR format now specified with `ibm` instead of `spr`
:   The use of `spr` is deprecated as an argument to the `format` option of the `GET /v1/pronunciation` method and for use with the `alphabet` attribute of an SSML `<phoneme>` element. To use {{site.data.keyword.IBM_notm}} SPR notation, use the `ibm` argument instead of `spr` in all cases.

New support for `audio/mulaw` audio format
:   The list of supported audio formats now includes `audio/mulaw;rate={rate}`. Like `audio/basic`, this format provides single-channel audio that is encoded by using 8-bit u-law (or mu-law) data that is sampled at 8 kHz. For more information, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

New supported features identified when listing voices
:   The `GET /v1/voices` and `GET /v1/voices/{voice}` methods now return a `supported_features` object as part of their output for each voice. The object describes whether the voice supports customization and the SSML `<voice_transformation>` element. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## 23 June 2016
{: #text-to-speech-23june2016}
{: release-note}

New WebSocket interface for speech synthesis
:   The service now offers a WebSocket interface for synthesizing text to speech. The interface offers the same features as the `/v1/synthesize` method of the HTTP interface. It accepts plain text or text that is marked up with SSML. In addition, it also supports use of the SSML `<mark>` element to identify the time in the audio at which it finishes synthesizing all text that precedes the mark. For more information, see [The WebSocket interface](/docs/text-to-speech?topic=text-to-speech-usingWebSocket).

Expanded language support for SSML
:   The service now offers support for text that is annotated with SSML for the languages Castilian and North American Spanish, Italian, and Brazilian Portuguese. The service already supported the use of SSML for US and UK English, French, and German. As of this update, the service supports SSML for all languages but Japanese. Moreover, you can use both {{site.data.keyword.IBM_notm}} SPR and IPA notations to define word pronunciations with the SSML `<phoneme>` element. For more information, see [Understanding SSML](/docs/text-to-speech?topic=text-to-speech-ssml) and [Understanding phonetic symbols](/docs/text-to-speech?topic=text-to-speech-symbols).

    For US English, you can also use the SSML `<phoneme>` element to create word entries in a custom model; customization is supported only for US English. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

Voices updated for improved speech synthesis
:   The service features improved expressiveness and naturalness for the most frequently used voices. The improvements are based on Recursive Neural Network (RNN)-based prosody prediction from input text. They are made available as a new service engine and voice-model updates for the following languages:

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`

New customization ID parameter for word pronunciation
:   The `GET /v1/pronunciation` method now accepts an optional `customization_id` query parameter. The parameter obtains a word translation from a specified custom model. If the custom model does not contain the word, the method returns the word's default pronunciation. For more information, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

    When using the `GET /v1/pronunciation` method without a customization ID and for a language other than US English, you can request a word's pronunciation only in {{site.data.keyword.IBM_notm}} SPR notation. For a language other than US English, you must specify `spr` with the method's `format` option.

New support for `audio/basic` audio format
:   The list of supported audio formats now includes `audio/basic`, which provides single-channel audio that is encoded using 8-bit u-law (or mu-law) data that is sampled at 8 kHz. For more information, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

HTTP and WebSocket interfaces can now return warnings
:   The HTTP and WebSocket `/v1/synthesize` methods can return a `warnings` response that includes messages about invalid query parameters or JSON fields that are included with a request. The format of the warnings changed. The following example shows the previous format:

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    The same warning now has the following format:

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

## 10 March 2016
{: #text-to-speech-10march2016}
{: release-note}

Synthesis methods can now return warnings
:   The `GET` and `POST /v1/synthesize` methods can now return a `Warnings` response header that includes a list of warning messages about invalid query parameters or JSON fields that are included with the request. Each element of the list includes a string that describes the nature of the warning followed by an array of invalid argument strings; for example, `Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}'].` For more information, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

Beta Apple iOS SDK is deprecated
:   The beta *{{site.data.keyword.watson}} Speech Software Development Kit (SDK) for the Apple® iOS operating system* is deprecated and replaced by the *{{site.data.keyword.watson}} Swift SDK*. The new SDK is available from the [swift-sdk repository](https://github.com/watson-developer-cloud/swift-sdk){: external} in the `watson-developer-cloud` namespace on GitHub.

## 22 February 2016
{: #text-to-speech-22february2016}
{: release-note}

New expressive SSML feature
:   The service was updated with a new expressive SSML feature. The service extends SSML with an `<express-as>` element that you can use to indicate expressiveness in one of three speaking styles: `GoodNews`, `Apology`, or `Uncertainty`. You can apply the element to the entire body of the text, a sentence, a phrase, or a word. The service currently supports expressiveness only for the US English Allison voice (`en-US_AllisonVoice`).

## 17 December 2015
{: #text-to-speech-17december2015}
{: release-note}

New beta customization interface
:   The service offers a new customization interface that you can use to specify how it pronounces unusual words that occur in your input. The interface includes a number of new methods that you can use to create and manage custom models and the word/translation pairs that they contain. You can then use your custom models when synthesizing text to audio.

    The service supports sounds-like translations and phonetic translations. Phonetic translations can use either the standard International Phonetic Alphabet (IPA) representation or the proprietary {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). You use SSML to specify phonetic translations.

    The customization interface includes a collection of new HTTP methods that have the names `POST /v1/customizations`, `POST /v1/customizations/{customization_id}`, `POST /v1/customizations/{customization_id}/words`, and `PUT /v1/customizations/{customization_id}/words/{word}`. The service also provides a new `GET /v1/pronunciation` method that returns the pronunciation for any word and a new `GET /v1/voices/{voice}` method that returns detailed information about a specific voice. In addition, existing methods of the service's interface now accept custom model parameters as needed.

    For more information about customization and its interface, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro) and the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

    The customization interface is a beta release that currently supports US English only. All customization methods and the `GET /v1/pronunciation` method can currently be used to create and manipulate custom models and word translations only in US English.

New Brazilian Portuguese voice: `pt-BR_IsabelaVoice`
:   The service supports a new voice, `pt-BR_IsabelaVoice`, to synthesize audio in Brazilian Portuguese with a female voice. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## 21 September 2015
{: #text-to-speech-21september2015}
{: release-note}

New mobile SDKs available
:   Two new beta mobile Software Development Kits (SDKs) are available for the speech services. The SDKs enable mobile applications to interact with both the {{site.data.keyword.texttospeechshort}} and {{site.data.keyword.speechtotextshort}} services. You can use the SDKs to send text to the {{site.data.keyword.texttospeechshort}} service and receive an audio response.
    -   The *{{site.data.keyword.watson}} Swift SDK* is available from the [swift-sdk repository](https://github.com/watson-developer-cloud/swift-sdk){: external} in the `watson-developer-cloud` namespace on GitHub.
    -   The *{{site.data.keyword.watson}} Speech Android™ SDK* is available from the [speech-android-sdk repository](https://github.com/watson-developer-cloud/speech-android-sdk){: external} in the `watson-developer-cloud` namespace on GitHub.

    Both SDKs support authenticating with the speech services by using either your {{site.data.keyword.cloud_notm}} service credentials or an authentication token. Because the SDKs are beta functionality, they are subject to change in the future.

New Japanese voice: `ja-JP_EmiVoice`
:   The service supports a new language, Japanese. The voice `ja-JP_EmiVoice` is a Japanese female voice.

## 1 July 2015
{: #text-to-speech-1july2015}
{: release-note}

The {{site.data.keyword.texttospeechshort}} service is now generally available
:   The service moved from beta to general availability (GA) on 1 July 2015. The following differences existed between the beta and GA versions of the {{site.data.keyword.texttospeechshort}} API. The GA release requires that users upgrade to the new version of the service.

New token-based programming model
:   A new programming model supports direct interaction between a client and the service. By using this model, a client can obtain an authentication token for communicating directly with the service. By using the token, the client can bypass the need for a server-side proxy application in {{site.data.keyword.cloud_notm}} to call the service on its behalf. Tokens are the preferred means for clients to interact with the service.

    The service continues to support the old programming model that relied on a server-side proxy to relay communications and data between the client and the service. But the new model is more efficient and provides higher throughput.

New support for the Speech Synthesis Markup Language
:   You can now pass Speech Synthesis Markup Language (SSML) to the HTTP `GET` and `POST` versions of the `/v1/synthesize` method. SSML is an XML-based markup language that is designed to provide annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service. For more information about passing SSML input to the service, see [Specifying input text](/docs/text-to-speech?topic=text-to-speech-usingHTTP#input).

    The service initially supports the use of SSML only for the UK and US English, French, and German languages. The service does not support SSML for use with Italian and Spanish. When you use SSML, make sure that you do not select a voice for the audio in one of the unsupported languages. Results in this case are not meaningful.

Changes to available voices
:   The voices that are supported for synthesized speech changed and expanded. The service now supports a number of additional voices, languages, and dialects with the `/v1/synthesize` methods. For more information about supported voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

    The three voices that were available at beta are renamed for GA:
    -   `VoiceEnUsMichael` is now `en-US_MichaelVoice`
    -   `VoiceEnUsLisa` is now `en-US_LisaVoice`
    -   `VoiceEsEsEnrique` is now `es-ES_EnriqueVoice`

    The previous names of the voices continue to work with the beta version of the service (via `-beta` API endpoints) while that version remains available. However, you must use the new names with the GA version of the service.

New support for Free Lossless Audio Codec (FLAC) audio format
:   You can now request the service to return audio in the Free Lossless Audio Codec (FLAC) format. The service can still return audio in the Ogg format with the Opus codec (the default) and in the Waveform Audio File Format (WAV). For more information about using audio formats with the `/v1/synthesize` methods, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

New limits on maximum amount of synthesized text
:   The text that you send to the `/v1/synthesize` method in the URL of an HTTP `GET` request or in the body of an HTTP `POST` request is now limited to a maximum of 5 KB. The text had a maximum size of 4 MB for the beta version.

New header to opt out of contributing to service improvements
:   The `/v1/synthesize` methods now include the header `X-WDC-PL-OPT-OUT` to control whether the service uses the text and audio results from an operation to improve future results. Specify a value of `1` for the header to prevent the service from using text and audio results. The parameter applies only to the current request. The new header replaces the `X-logging` header from the beta methods. For more information, see [Controlling request logging for {{site.data.keyword.watson}} services](/docs/watson?topic=watson-gs-logging-overview).

Changes to HTTP error codes for speech synthesis
:   For the `/v1/synthesize` methods, the following error codes changed:
    -   Error code 406 ("Not acceptable. Unsupported MIME type.") is removed.
    -   Error code 415 ("Unsupported Media Type") is added.
    -   Error code 503 ("Service Unavailable") is added.

Changes to HTTP error codes for listing voices
:   For the `GET /v1/voices` method, the following error codes changed:
    -   Error code 406 ("Not acceptable. Unsupported MIME type.") is removed.
    -   Error code 415 ("Unsupported Media Type") is added.
