---

copyright:
  years: 2020, 2023
lastupdated: "2023-03-30"

keywords: faqs,frequently asked questions,question,Text to Speech

subcollection: text-to-speech

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# Usage FAQs
{: #faq-usage}

FAQs for {{site.data.keyword.texttospeechfull}} include questions about speech synthesis, supported languages, audio formats, and other topics. To find all FAQs for {{site.data.keyword.cloud}}, see the [FAQ library](/docs/faqs){: external}.
{: shortdesc}

## How do I access my service credentials?
{: #faq-credentials}
{: faq}
{: support}

How you access your service credentials depends on whether you are using {{site.data.keyword.texttospeechshort}} with {{site.data.keyword.cloud}} or {{site.data.keyword.icp4dfull}}. For more information about obtaining your credentials for both versions, see [Before you begin](/docs/text-to-speech?topic=text-to-speech-gettingStarted#getting-started-before-you-begin) in the getting started tutorial.

Once you have your service credentials, see the following topics for information about authenticating to the service:
-   [Authenticating to {{site.data.keyword.cloud_notm}}](/docs/watson?topic=watson-iam#gs-credential-cloud)
-   [Authenticating to {{site.data.keyword.icp4dfull_notm}}](/docs/watson?topic=watson-iam#gs-credential-cpd)

## What languages does the service support?
{: #faq-language-support}
{: faq}
{: support}

The {{site.data.keyword.texttospeechshort}} service supports male and female voices in various spoken languages:
-   The service offers *expressive neural voices* for English (Australian and United States).
-   The services offers *enhanced neural voices* for Dutch Netherlands, English (United Kingdom and United States), French (Canadian and France), German, Italian, Japanese, Korean, Portuguese (Brazilian), and Spanish (Castilian, Latin American, and North American).

Some languages and voices are available only for {{site.data.keyword.cloud}}, not for {{site.data.keyword.icp4dfull}}. For more information about the available voices for all languages, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## How does the service synthesize audio?
{: #faq-voices}
{: faq}
{: support}

The {{site.data.keyword.texttospeechshort}} service offers voices that rely on neural technology to synthesize text to speech. The topic of synthesizing text to speech is inherently complex. For more information, see

-   [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices)
-   [The science behind the service](/docs/text-to-speech?topic=text-to-speech-science)

## What are the output audio formats?
{: #faq-audio-types}
{: faq}
{: support}

By default, the {{site.data.keyword.texttospeechshort}} service returns audio in Ogg format with the Opus codec (`audio/ogg;codecs=opus`). The service supports many other audio formats to suit your application needs. For more information, see [Supported audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats#formats-supported).

## How do I convert my text to speech?
{: #faq-convert}
{: faq}
{: support}

To submit text to the service for synthesized audio output, you make an HTTP or WebSocket request. You can use the API directly or use one of the Watson SDKs. [Getting started](/docs/text-to-speech?topic=text-to-speech-gettingStarted) offers examples of both the HTTP `POST /v1/synthesize` and `GET /v1/synthesize` methods. The [API & SDK reference](/apidocs/text-to-speech){: external} shows examples of all interfaces and methods.

There is no graphical user interface for submitting text. See the [Text to Speech demo](https://www.ibm.com/demos/live/tts-demo/self-service/home){: external} to try an example of the service in action. The demo accepts a small amount of your text as input to generate speech with different voices.

## Can I change how the service interprets input text and produces synthesized audio?
{: #faq-change-synthesis}
{: faq}
{: support}

You can use the Speech Synthesis Markup Language (SSML) to control aspects of the synthesis process such as pronunciation, volume, pitch, speed, and other attributes. You can also use the Tune by Example feature to tailor the prosody, intonation, and cadence of custom prompts to better suit your application needs.

-   For general information about SSML, see [Understanding SSML](/docs/text-to-speech?topic=text-to-speech-ssml).
-   For information about the supported SSML elements, see [SSML elements](/docs/text-to-speech?topic=text-to-speech-elements).
-   For information about the Tune by Example feature, see [Understanding Tune by Example](/docs/text-to-speech?topic=text-to-speech-tbe-intro).

## What programming languages can I use?
{: #faq-sdks}
{: faq}
{: support}

The service supports SDKs in many popular programming languages and platforms.

-   For more information about the SDKs and links to them on GitHub, see [{{site.data.keyword.watson}} SDKs](/docs/text-to-speech?topic=watson-using-sdks).
-   For more information about all methods of the SDKs for the {{site.data.keyword.texttospeechshort}} service, see the [API & SDK reference](/apidocs/text-to-speech){: external}.

## What is the maximum amount of text that I can submit for synthesis?
{: #faq-maximum-input}
{: faq}
{: support}

You can submit the following maximum amount of text for a speech synthesis request with each of the service's method:

-   HTTP `GET /v1/synthesize` method - Maximum of 8 KB of total input, which includes the input text, SSML, and the URL and headers.
-   HTTP `POST /v1/synthesize` method - Maximum of 8 KB for the URL and headers. Maximum of 5 KB for the input text, including SSML.
-   WebSocket `/v1/synthesize` method - Maximum of 5 KB of input text, including SSML.

All characters of the input, including whitespace and those that are part of SSML elements, are counted toward the data maximum. For billing purposes, whitespace characters are not counted. For more information, see [Data limits](/docs/text-to-speech?topic=text-to-speech-service-features#features-data-limits).

## How does customization work?
{: #faq-custom-understand}
{: faq}

The customization interface of the {{site.data.keyword.texttospeechshort}} service creates a dictionary of words and their translations for a specific language. This dictionary is referred to as a custom model. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

## How do I create a custom model?
{: #faq-custom-create}
{: faq}

Review the guidelines for working with the customization interface before you begin. Then, see the steps and examples for creating, querying, updating, and deleting custom models in [Creating and managing custom models](/docs/text-to-speech?topic=text-to-speech-customModels). Also review [Creating and managing custom entries](/docs/text-to-speech?topic=text-to-speech-customWords) for examples and guidance about adding relevant training data.

## Can I create a custom voice?
{: #faq-custom-create-voice}
{: faq}

[IBM Cloud]{: tag-ibm-cloud}

As a premium customer, you can work with {{site.data.keyword.IBM_notm}} to train a new custom voice for your specific use case and target market. Creating a custom voice is different from customizing one of the service's existing voices. A custom voice is a unique new voice that is based on audio training data that the customer provides. {{site.data.keyword.IBM_notm}} can train a custom voice with as little as one hour of training data.

To request a custom voice or for more information, complete and submit this [{{site.data.keyword.IBM_notm}} Request Form](https://forms.monday.com/forms/5fd92c54536a18f9afab8a47404bf828?r=use1){: external}.

## How do I use the Tune by Example feature?
{: #faq-tune-by-example}
{: faq}

Tune by Example lets you control exactly how specified text is spoken by the service. You provide text and spoken audio to add a custom prompt to a custom model. The spoken audio can stress different syllables or words, introduce pauses, and generally make the synthesized audio sound more natural and appropriate for its context. When you synthesize the prompt, the service duplicates the qualities of the recorded speech with its voices.

You can further enhance the quality of a prompt by creating an optional speaker model that contains a sample of a speaker's voice. The service leverages the sample audio to train itself on the voice, which can help it produce higher-quality prompts for that speaker.

For more information, see [Understanding Tune by Example](/docs/text-to-speech?topic=text-to-speech-tbe-intro).

## What limits exist for a custom model?
{: #faq-custom-limits}
{: faq}

The following limits apply to all custom models:

-   A word in a custom entry can contain a maximum of 49 characters.
-   A translation in a custom entry can contain a maximum of 499 characters.
-   A custom model can include a maximum of 20,000 custom entries.
-   A custom model can include a maximum of 1000 custom prompts.

For more information, see [Rules for creating custom entries](/docs/text-to-speech?topic=text-to-speech-rules).

## Where can I find plans and pricing information?
{: #faq-cost}
{: faq}

[IBM Cloud]{: tag-ibm-cloud}

The {{site.data.keyword.texttospeechshort}} service offers multiple pricing plans. For more information about pricing, see the {{site.data.keyword.texttospeechshort}} service in the [IBM Cloud Catalog](https://cloud.ibm.com/catalog/text-to-speech).
