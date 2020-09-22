---

copyright:
  years: 2020
lastupdated: "2020-09-22"

keywords: faqs,frequently asked questions,question,Text to Speech

subcollection: text-to-speech

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}

---

# Usage FAQs
{: #faq-usage}

FAQs for {{site.data.keyword.texttospeechfull}} include questions about speech synthesis, supported languages, audio formats, and other topics. To find all FAQs for {{site.data.keyword.cloud}}, see our [FAQ library](/docs/faqs){: external}.
{: shortdesc}

## What languages does the service support?
{: #faq-language-support}
{: faq}

The {{site.data.keyword.texttospeechshort}} service supports male and female voices in various spoken languages. Supported languages include Arabic (beta), Brazilian Portuguese, Chinese (Mandarin, beta), Dutch (beta), English (United Kingdom and United States), French, German, Italian, Japanese, Korean (beta), and Spanish (multiple dialects). For more information about the available voices for all languages, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## How does the service synthesize audio?
{: #faq-voices}
{: faq}

The {{site.data.keyword.texttospeechshort}} service offers voices that rely on two types of voice-synthesis technology:

-   [Neural voices](/docs/text-to-speech?topic=text-to-speech-voices#neuralVoices)
-   [Standard (concatenative) voices](/docs/text-to-speech?topic=text-to-speech-voices#standardVoices)

The topic of synthesizing text to speech is inherently complex. For more information, see [The science behind the service](/docs/text-to-speech?topic=text-to-speech-science).

## What are the output audio formats?
{: #faq-audio-types}
{: faq}

By default, the {{site.data.keyword.texttospeechshort}} service returns audio in Ogg format with the Opus codec (`audio/ogg;codecs=opus`). The service supports many other audio formats to suit your application needs. For more information, see [Supported audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats#formatsSupported).

## How do I convert my text to speech?
{: #faq-convert}
{: faq}

To submit text to the service for synthesized audio output, you make an HTTP or WebSocket request. You can use the API directly or use one of the Watson SDKs. [Getting started](/docs/text-to-speech?topic=text-to-speech-gettingStarted) offers examples of both the HTTP `POST /v1/synthesize` and `GET /v1/synthesize` methods. The [API reference](/apidocs/text-to-speech){: external} shows examples of all interfaces and methods.

There is no graphical user interface for submitting text. See the [Text to Speech Demo](https://text-to-speech-demo.ng.bluemix.net/){: external} to try an example of the service in action. The demo accepts a small amount of your text as input to generate speech with different voices.

## Can I change how the service interprets input text and produces synthesized audio?
{: #faq-change-synthesis}
{: faq}

You can use the Speech Synthesis Markup Language (SSML) to control aspects of the synthesis process such as pronunciation, volume, pitch, speed, and other attributes.

-   For general information, see [Using SSML](/docs/text-to-speech?topic=text-to-speech-ssml).
-   For information about the supported SSML elements, see [SSML elements](/docs/text-to-speech?topic=text-to-speech-elements).

## What programming languages can I use?
{: #faq-sdks}
{: faq}

The service supports SDKs in many popular programming languages and platforms.

-   For more information about the SDKs and links to them on GitHub, see [{{site.data.keyword.watson}} SDKs](/docs/text-to-speech?topic=watson-using-sdks).
-   For more information about all methods of the SDKs for the {{site.data.keyword.texttospeechshort}} service, see the [API reference](/apidocs/text-to-speech){: external}.

## How do I access my API key and URL endpoint?
{: #faq-credentials}
{: faq}

From the [{{site.data.keyword.cloud}} Resource list](https://{DomainName}/resources){: external}, click on your {{site.data.keyword.texttospeechshort}} service instance to go to the {{site.data.keyword.texttospeechshort}} service dashboard page. On the **Manage** page, click **Show Credentials** to view your API key and URL endpoint. For more information, see [Before you begin](/docs/text-to-speech?topic=text-to-speech-gettingStarted#before-you-begin).

## What is the maximum amount of text that I can submit for synthesis?
{: #faq-maximum-input}
{: faq}

You can submit the following maximum amount of text for a speech synthesis request with each of the service's method:

-   HTTP `GET /v1/synthesize` method - Maximum of 8 KB of total input, which includes the input text, SSML, and the URL and headers.
-   HTTP `POST /v1/synthesize` method - Maximum of 8 KB for the URL and headers. Maximum of 5 KB for the input text, including SSML.
-   WebSocket `/v1/synthesize` method - Maximum of 5 KB of input text, including SSML.

All characters of the input, including whitespace and those that are part of SSML elements, are counted toward the data maximum. For billing purposes, whitespace characters are not counted. For more information, see [Data limits](/docs/text-to-speech?topic=text-to-speech-overview#data-limits) in the overview for developers.

## How does voice model customization work?
{: #faq-custom-understand}
{: faq}

The customization interface of the {{site.data.keyword.texttospeechshort}} service creates a dictionary of words and their translations for a specific language. This dictionary is referred to as a custom voice model, or just a custom model. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

## How do I create a custom voice model?
{: #faq-custom-create}
{: faq}

Review the guidelines for working with the customization interface before you begin. Then, see the steps and examples for creating, querying, updating, and deleting custom models in [Creating and managing custom voice models](/docs/text-to-speech?topic=text-to-speech-customModels). Also review [Creating and managing custom entries](/docs/text-to-speech?topic=text-to-speech-customWords) for examples and guidance about adding relevant training data.

## What limits exist for a custom voice model?
{: #faq-custom-limits}
{: faq}

The following limits apply to all custom voice models and entries:

-   A custom model can include a maximum of 20,000 custom entries.
-   A word in a custom entry can contain a maximum of 49 characters.
-   A translation in a custom entry can contain a maximum of 499 characters.

For more information, see [Rules for creating custom entries](/docs/text-to-speech?topic=text-to-speech-rules).

## Where can I find plans and pricing information?
{: #faq-cost}
{: faq}

The {{site.data.keyword.texttospeechshort}} service offers multiple pricing plans. For more information about pricing, see the {{site.data.keyword.texttospeechshort}} service in the [IBM Cloud Catalog](https://cloud.ibm.com/catalog/text-to-speech).
