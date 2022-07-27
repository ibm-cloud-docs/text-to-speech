---

copyright:
  years: 2015, 2022
lastupdated: "2022-07-15"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Service features
{: #service-features}

You can access the speech synthesis capabilities of the {{site.data.keyword.texttospeechfull}} service via an HTTP or WebSocket interface. Both interfaces provide features that let you submit and receive different information from the service. And as with all {{site.data.keyword.watson}} services, SDKs are available to simplify application development in many programming languages.
{: shortdesc}

## Using languages and voices
{: #features-languages-voices}

The service supports speech synthesis with voices for the many languages listed in [Language support](/docs/speech-to-text?topic=speech-to-text-about#about-languages). For different languages, the service offers female voices, male voices, or both. Some languages and voices are supported for {{site.data.keyword.cloud}} only. For information about the supported languages and voices, see [Using languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

Effective **31 March 2022**, all neural voices are deprecated. The deprecated voices remain available to existing users until 31 March 2023, when they will be removed from the service and the documentation. The neural voices are supported only for IBM Cloud; they are not available for IBM Cloud Pak for Data. New voices for Australian English, Dutch, and Korean will be released by 15 February 2023. If you are using Australian English, Dutch, or Korean voices, your API calls will automatically redirect to the new voices in that language. Voices in Arabic, Chinese, Czech, Swedish, and Flemish will be removed from service. All enhanced neural voices remain available to all users. For more information, see the [31 March 2022 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-31march2022) in the release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}.
{: deprecated}

## Using audio formats
{: #features-audio-formats}

The service can return synthesized audio in the many formats listed in [Audio support](/docs/text-to-speech?topic=text-to-speech-about#about-formats). For information about the supported audio formats, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

## Synthesizing speech with the service
{: #features-synthesis-interfaces}

The {{site.data.keyword.texttospeechshort}} service offers an HTTP Representational State Transfer (REST) interface and a WebSocket interface:

-   [The HTTP interface](/docs/text-to-speech?topic=text-to-speech-usingHTTP) provides both `GET` and `POST` versions of the service's `/v1/synthesize` method. The two versions of the method offer generally equivalent functionality. You pass the text that is to be synthesized as a query parameter with the `GET` method and as the body of the request with the `POST` method.
-   [The WebSocket interface](/docs/text-to-speech?topic=text-to-speech-usingWebSocket) provides a `/v1/synthesize` method. You pass the text that is to be synthesized over an established WebSocket connection.

With both the HTTP and WebSocket interfaces, you specify the language and voice that are to be used, and the format for the audio that is to be returned.

-   For an overview of the features that are available for speech synthesis, see [Using speech synthesis features](#features-synthesis).
-   For detailed descriptions and examples of the speech synthesis methods, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

### Data limits
{: #features-data-limits}

The interfaces accept the following maximum amounts of text with a single request:

-   The HTTP `GET /v1/synthesize` method accepts a maximum of 8 KB of input, which includes the input text and the URL and headers.
-   The HTTP `POST /v1/synthesize` method accepts a maximum of 8 KB for the URL and headers, and a maximum of 5 KB for the input text that is sent in the body of the request.
-   The WebSocket `/v1/synthesize` method accepts a maximum of 5 KB of input text.

These limits include all characters of the input, including whitespace.

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only.** For billing purposes, whitespace characters are not counted. However, all other characters are counted, including those that are part of SSML elements.

## Using speech synthesis features
{: #features-synthesis}

The service supports additional features that you can use to tailor the text that you send and the audio that you receive.

### SSML
{: #features-ssml}

You can pass the service plain text or text that is annotated with the Speech Synthesis Markup Language (SSML). SSML is an XML-based markup language that provides annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service.

-   For more information about specifying input text, see [Specifying input text](/docs/text-to-speech?topic=text-to-speech-usingHTTP#input).
-   For more information about using SSML, see [Understanding SSML](/docs/text-to-speech?topic=text-to-speech-ssml).

### Spelling out strings
{: #features-spell-out}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only**

To indicate how individual characters of a string (alphabetic, numeric, or alphanumeric) are to be spelled out, you can include the `spell_out_mode` query parameter with a request. By default, the service spells out individual characters at the same rate at which it synthesizes text for a language. You can use the parameter to direct the service to spell out individual characters more slowly, in groups of one, two, or three characters. Use the parameter with the SSML `<say-as>` element to control how the characters of a string are synthesized. For more information, see [Specifying how strings are spelled out](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-spell-out-mode).

The `spell_out_mode` parameter is beta functionality that is supported only for German voices.
{: beta}

### Word timings
{: #features-timings}

With the WebSocket interface, you can obtain timing information about the location of words in the audio that the service returns. Timing information is useful for synchronizing the input text and the audio.

You can use the SSML `<mark>` element to identify specific locations, such as word boundaries, in the audio. For languages other than Japanese, you can also request word timing information for all words of the input text. For more information, see [Generating word timings](/docs/text-to-speech?topic=text-to-speech-timing).

## Customizing the service
{: #features-customization}

The service includes a customization interface that you can use to create custom models for use during speech synthesis. A custom model is a dictionary of words and their translations for a specific language. Each word/translation pair in a model tells the service how to pronounce a word when it occurs in input text.

You can use custom models to create application-specific translations for unusual words for which the service's regular pronunciation rules might yield imperfect pronunciations. For example, your application might routinely encounter domain-specific terms, special terms with foreign origins, personal or geographic names, or abbreviations and acronyms. By using customization, you can define translations that tell the service how you want such terms to be pronounced.

You can define the custom entry for a word/translation pair based on other words, or you can create pronunciations based on phoneme symbols in the standard International Phonetic Alphabet (IPA) or the proprietary {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). Customization is available for all languages.

-   For more information about customization, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).
-   For more information about using phonetic IPA and SPR symbols, see [Understanding phonetic symbols](/docs/text-to-speech?topic=text-to-speech-symbols).

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only.** You must have the Standard or Premium pricing plan to use customization. Users of the Lite plan cannot use the customization interface. For more information about pricing plans, see the {{site.data.keyword.texttospeechshort}} service in the [{{site.data.keyword.cloud}} Catalog](https://{DomainName}/catalog/text-to-speech){: external}.

### Creating a custom voice
{: #features-customization-voice}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only**

Premium customers can work with {{site.data.keyword.IBM_notm}} to train a new custom voice for their specific application needs. A custom voice is a unique voice that is based on audio training data that the customer provides. {{site.data.keyword.IBM_notm}} can train a custom voice with as little as one hour of training data. For more information, see [Creating a custom voice](/docs/text-to-speech?topic=text-to-speech-voices#customize-voice) or contact your {{site.data.keyword.IBM_notm}} Sales Representative.

## Using Tune by Example
{: #features-tune-by-example}

The Tune by Example feature lets you control how specified text is spoken by the service. The feature lets you dictate the intonation, cadence, and stress of the synthesized text. You create a custom prompt by providing a sample recording that speaks the text as you want to hear it. The service then duplicates the qualities of the recorded speech with its voices when you synthesize the prompt.

The feature provides a simpler mechanism than standard SSML for modifying how speech is synthesized. Tune by Example eliminates the need for complex SSML by letting you record text as you want it to be spoken rather than requiring you to emulate the intended prosody with SSML.

You can increase the quality of custom prompts by associating speaker models with those users who speak the prompts. You create a speaker model by providing an audio sample of a user's voice. The service trains itself on the voice to help it produce higher-quality prompts for that speaker.

For more information about Tune by Example, custom prompts, and speaker models, see [Understanding Tune by Example](/docs/text-to-speech?topic=text-to-speech-tbe-intro).

The Tune by Example feature is beta functionality that is supported only for US English custom models and voices.
{: beta}

## Using software development kits
{: #features-sdks}

SDKs are available for the {{site.data.keyword.texttospeechshort}} service to simplify the development of speech applications. The SDKs support many popular programming languages and platforms.

-   For a complete list of SDKs and links to the SDKs on GitHub, see [{{site.data.keyword.watson}} SDKs](/docs/text-to-speech?topic=watson-using-sdks).
-   For more information about all methods of the SDKs for the {{site.data.keyword.texttospeechshort}} service, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

## Learning more about application development
{: #features-learn}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only**

For more information about working with {{site.data.keyword.watson}} services and {{site.data.keyword.cloud_notm}}:

-   For an introduction, see [Getting started with {{site.data.keyword.watson}} and {{site.data.keyword.cloud_notm}}](/docs/watson?topic=watson-about).
-   For information about using {{site.data.keyword.cloud_notm}} Identity and Access Management, see [Authenticating to {{site.data.keyword.watson}} services](/docs/watson?topic=watson-iam).

## Next steps
{: #features-next-steps}

Explore the features introduced in this topic to gain a more in-depth understanding of the service's capabilities. Each feature includes links to topics that describe it in much greater detail.

-   [Using languages and voices](#features-languages-voices) and [Using audio formats](#features-audio-formats) describe the basic underpinnings of the service's capabilities. You must choose a language and voice that are suitable for your text and application, and you must understand the characteristics of the audio the service returns.
-   [Synthesizing speech with the service](#features-synthesis-interfaces) provides links to detailed presentations of each of the service's interfaces. Experiment with the interfaces to determine which is best suited to your application needs.
-   [Using speech synthesis features](#features-synthesis) briefly describes the features that are available for speech synthesis and provides links for more information. Use the features to tailor the text that you send and the audio that you receive.
-   [Customizing the service](#features-customization) describes the more advanced topic of customization, which you can use to create custom models that contain dictionaries of words and their translations for specific languages.
-   [Using Tune by Example](#features-tune-by-example) introduces the Tune by Example feature that lets you create custom prompts. You can control the intonation, cadence, and stress of the synthesized text for your prompts.
-   [Using software development kits](#features-sdks) provide links to the SDKs that are available to simplify application development in many programming languages.
-   ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only.** [Learning more about application development](#features-learn) provides links to help you get started with {{site.data.keyword.watson}} services and understand authentication.
