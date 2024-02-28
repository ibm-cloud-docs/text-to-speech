---

copyright:
  years: 2015, 2023
lastupdated: "2023-03-30"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Service features
{: #service-features}

You can access the speech synthesis capabilities of the {{site.data.keyword.texttospeechfull}} service via an HTTP or WebSocket interface. Both interfaces provide features that let you submit and receive different information from the service. And as with all {{site.data.keyword.watson}} services, SDKs are available to simplify application development in many programming languages.
{: shortdesc}

## Using languages and voices
{: #features-languages-voices}

The service supports speech synthesis with voices for the languages listed in [Language support](/docs/speech-to-text?topic=speech-to-text-about#about-languages). For different languages, the service offers female voices, male voices, or both. Some languages and voices might be supported for {{site.data.keyword.cloud}} only.

All of the service's voices use neural voice technology, which produces more natural-sounding speech. The service offers two types of voices, *expressive neural* and *enhanced neural*, which have different qualities and features. For information about the types of voices and about the supported languages and voices for each type, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

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

[IBM Cloud]{: tag-ibm-cloud} For billing purposes, whitespace characters are not counted. However, all other characters are counted, including those that are part of SSML elements.

## Using speech synthesis features
{: #features-synthesis}

The service supports additional features that you can use to tailor the text that you send and the audio that you receive.

### SSML
{: #features-ssml}

You can pass the service plain text or text that is annotated with the Speech Synthesis Markup Language (SSML). SSML is an XML-based markup language that provides annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service.

-   For more information about specifying input text, see [Specifying input text](/docs/text-to-speech?topic=text-to-speech-usingHTTP#input).
-   For more information about using SSML, see [Understanding SSML](/docs/text-to-speech?topic=text-to-speech-ssml).

### Modifying the speaking rate
{: #features-rate}

To modify the global rate of speech synthesis for a request, you can use the `rate_percentage` query parameter. The speaking rate is the speed at which the service speaks the text that it synthesizes into speech. A higher rate causes the text to be spoken more quickly; a lower rate causes the text to be spoken more slowly. The parameter changes the per-voice default rate for an entire request. For more information, see [Modifying the speaking rate](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-rate-percentage).

The `rate_percentage` parameter is beta functionality.
{: beta}

### Modifying the speaking pitch
{: #features-pitch}

To modify the global pitch of speech synthesis for a request, you can use the `rate_pitch` query parameter. The speaking pitch represents the tone of the speech that the service synthesizes. It represents how high or low the tone of the voice is perceived by the listener. A higher pitch results in speech that is spoken at a higher tone and is perceived as a higher voice; a lower pitch results in speech that is spoken in a lower tone and is perceived as a lower voice. The parameter changes the per-voice default pitch for an entire request. For more information, see [Modifying the speaking pitch](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-pitch-percentage).

The `pitch_percentage` parameter is beta functionality.
{: beta}

### Spelling out strings
{: #features-spell-out}

To indicate how individual characters of a string (alphabetic, numeric, or alphanumeric) are to be spelled out, you can include the `spell_out_mode` query parameter with a request. By default, the service spells out individual characters at the same rate at which it synthesizes text for a language. You can use the parameter to direct the service to spell out individual characters more slowly, in groups of one, two, or three characters. Use the parameter with the SSML `<say-as>` element to control how the characters of a string are synthesized. For more information, see [Specifying how strings are spelled out](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-spell-out-mode).

The `spell_out_mode` parameter is beta functionality that is supported only for German voices.
{: beta}

### Word timings
{: #features-timings}

With the WebSocket interface, you can obtain timing information about the location of words in the audio that the service returns. Timing information is useful for synchronizing the input text and the audio.

You can use the SSML `<mark>` element to identify specific locations, such as word boundaries, in the audio. For languages other than Japanese, you can also request word timing information for all words of the input text. For more information, see [Generating word timings](/docs/text-to-speech?topic=text-to-speech-timing).

## Using speech synthesis features with expressive neural voice
{: #features-synthesis-expressive}

With expressive neural voices, the service supports additional features that modify how the text that you pass is synthesized into audio.

### Using speaking styles
{: #features-synthesis-expressive-styles}

The expressive neural voices determine the sentiment of the text from the context of its words and phrases. The speech that they produce, in addition to having a very conversational style, reflects the mood of the text. You can embellish the voices' natural tendencies by indicating that all or some of the text is to emphasize a specific style: cheerful, empathetic, neutral, or uncertain. You use SSML to indicate the style and the text to which it is to be applied. For more information, see [Using speaking styles](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#syntheses-expressive-styles).

### Emphasizing interjections
{: #features-synthesis-expressive-interjections}

When you use expressive neural voices, the service automatically detects a collection of common interjections based on context. When it synthesizes these interjections, it gives them the natural emphasis that a human would use in normal conversation. For some of the interjections, you can use SSML to enable or disable their emphasis. For more information, see [Emphasizing interjections](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#emphasizing-interjections).

### Emphasizing words
{: #features-synthesis-expressive-words}

The expressive voices use a conversational style that naturally applies the correct intonation from context. But you can indicate that one or more words are to be given more or less emphasis. The change in stress can be indicated by an increase or decrease in pitch, timing, volume, or other acoustic attributes. For more information, see [Emphasizing words](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#emphasizing-words).

## Customizing the service
{: #features-customization}

The service includes a customization interface that you can use to create custom models for use during speech synthesis. A custom model is a dictionary of words and their translations for a specific language. Each word/translation pair in a model tells the service how to pronounce a word when it occurs in input text.

You can use custom models to create application-specific translations for unusual words for which the service's regular pronunciation rules might yield imperfect pronunciations. For example, your application might routinely encounter domain-specific terms, special terms with foreign origins, personal or geographic names, or abbreviations and acronyms. By using customization, you can define translations that tell the service how you want such terms to be pronounced.

You can define the custom entry for a word/translation pair based on other words, or you can create pronunciations based on phoneme symbols in the standard International Phonetic Alphabet (IPA) or the proprietary {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). Customization is available for all languages.

-   For more information about customization, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).
-   For more information about using phonetic IPA and SPR symbols, see [Understanding phonetic symbols](/docs/text-to-speech?topic=text-to-speech-symbols).

[IBM Cloud]{: tag-ibm-cloud} You must have the Standard or Premium pricing plan to use customization. Users of the Lite plan cannot use the customization interface. For more information about pricing plans, see the {{site.data.keyword.texttospeechshort}} service in the [{{site.data.keyword.cloud}} Catalog](https://{DomainName}/catalog/text-to-speech){: external}.
{: note}

### Creating a custom voice
{: #features-customization-voice}

[IBM Cloud]{: tag-ibm-cloud}

Premium customers can work with {{site.data.keyword.IBM_notm}} to train a new custom voice for their specific application needs. A custom voice is a unique voice that is based on audio training data that the customer provides. {{site.data.keyword.IBM_notm}} can train a custom voice with as little as one hour of training data.

To request a custom voice or for more information, complete and submit this [{{site.data.keyword.IBM_notm}} Request Form](https://forms.monday.com/forms/5fd92c54536a18f9afab8a47404bf828?r=use1){: external}.

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

For more information about working with {{site.data.keyword.watson}} services and {{site.data.keyword.cloud_notm}}:

-   For an introduction, see [Getting started with {{site.data.keyword.watson}} and {{site.data.keyword.cloud_notm}}](/docs/watson?topic=watson-about).
-   For information about using {{site.data.keyword.cloud_notm}} Identity and Access Management, see [Authenticating to {{site.data.keyword.watson}} services](/docs/watson?topic=watson-iam).

## Next steps
{: #features-next-steps}

Explore the features introduced in this topic to gain a more in-depth understanding of the service's capabilities. Each feature includes links to topics that describe it in much greater detail.

-   [Using languages and voices](#features-languages-voices) and [Using audio formats](#features-audio-formats) describe the basic underpinnings of the service's capabilities. You must choose a language and voice that are suitable for your text and application, and you must understand the characteristics of the audio the service returns.
-   [Synthesizing speech with the service](#features-synthesis-interfaces) provides links to detailed presentations of each of the service's interfaces. Experiment with the interfaces to determine which is best suited to your application needs.
-   [Using speech synthesis features](#features-synthesis) briefly describes the features that are available for speech synthesis and provides links for more information. Use the features to tailor the text that you send and the audio that you receive.
-   [Using speech synthesis features with expressive neural voice](#features-synthesis-expressive) introduces three additional features that are available for speech synthesis with expressive neural voices.
-   [Customizing the service](#features-customization) describes the more advanced topic of customization, which you can use to create custom models that contain dictionaries of words and their translations for specific languages.
-   [Using Tune by Example](#features-tune-by-example) introduces the Tune by Example feature that lets you create custom prompts. You can control the intonation, cadence, and stress of the synthesized text for your prompts.
-   [Using software development kits](#features-sdks) provide links to the SDKs that are available to simplify application development in many programming languages.
-   [Learning more about application development](#features-learn) provides links to help you get started with {{site.data.keyword.watson}} services and understand authentication.
