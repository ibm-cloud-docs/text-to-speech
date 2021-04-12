---

copyright:
  years: 2020, 2021
lastupdated: "2021-03-19"

keywords: faqs,frequently asked questions,question,Text to Speech

subcollection: text-to-speech

content-type: faq

---

{:faq: data-hd-content-type='faq'}
{:support: data-reuse='support'}
{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}

# Usage FAQs
{: #faq-usage}

FAQs for {{site.data.keyword.texttospeechfull}} include questions about speech synthesis, supported languages, audio formats, and other topics. To find all FAQs for {{site.data.keyword.cloud}}, see our [FAQ library](/docs/faqs){: external}.
{: shortdesc}

## What languages does the service support?
{: #faq-language-support}
{: faq}
{: support}

The {{site.data.keyword.texttospeechshort}} service supports male and female voices in various spoken languages. Supported languages include Arabic, Brazilian Portuguese, Chinese (Mandarin), Dutch, English (Australian, United Kingdom, and United States), French, German, Italian, Japanese, Korean, and Spanish (multiple dialects). For more information about the available voices for all languages, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## How does the service synthesize audio?
{: #faq-voices}
{: faq}
{: support}

The {{site.data.keyword.texttospeechshort}} service offers voices that rely on neural technology to synthesize text to speech. The topic of synthesizing text to speech is inherently complex. For more information, see

-   [Neural voice technology](/docs/text-to-speech?topic=text-to-speech-voices#neuralVoices)
-   [The science behind the service](/docs/text-to-speech?topic=text-to-speech-science)

## What are the output audio formats?
{: #faq-audio-types}
{: faq}
{: support}

By default, the {{site.data.keyword.texttospeechshort}} service returns audio in Ogg format with the Opus codec (`audio/ogg;codecs=opus`). The service supports many other audio formats to suit your application needs. For more information, see [Supported audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats#formatsSupported).

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

You can use the Speech Synthesis Markup Language (SSML) to control aspects of the synthesis process such as pronunciation, volume, pitch, speed, and other attributes.

-   For general information, see [Using SSML](/docs/text-to-speech?topic=text-to-speech-ssml).
-   For information about the supported SSML elements, see [SSML elements](/docs/text-to-speech?topic=text-to-speech-elements).

## What programming languages can I use?
{: #faq-sdks}
{: faq}
{: support}

The service supports SDKs in many popular programming languages and platforms.

-   For more information about the SDKs and links to them on GitHub, see [{{site.data.keyword.watson}} SDKs](/docs/text-to-speech?topic=watson-using-sdks).
-   For more information about all methods of the SDKs for the {{site.data.keyword.texttospeechshort}} service, see the [API & SDK reference](/apidocs/text-to-speech){: external}.

## How do I access my API key and URL endpoint?
{: #faq-credentials}
{: faq}
{: support}

From the [{{site.data.keyword.cloud}} Resource list](https://{DomainName}/resources){: external}, click on your {{site.data.keyword.texttospeechshort}} service instance to go to the {{site.data.keyword.texttospeechshort}} service dashboard page. On the **Manage** page, click **Show Credentials** to view your API key and URL endpoint. For more information, see [Before you begin](/docs/text-to-speech?topic=text-to-speech-gettingStarted#before-you-begin).

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

The {{site.data.keyword.texttospeechshort}} service offers multiple pricing plans. For more information about pricing, see the {{site.data.keyword.texttospeechshort}} service in the [IBM Cloud Catalog](https://cloud.ibm.com/catalog/text-to-speech).
