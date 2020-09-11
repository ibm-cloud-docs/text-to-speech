---

copyright:
  years: 2015, 2020
lastupdated: "2020-09-11"

subcollection: text-to-speech

---

{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}
{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# About
{: #about}

**Service update:** *As of 4 September 2020, the customization interface of the {{site.data.keyword.texttospeechshort}} service is generally available. Customization is no longer beta functionality. Also, the service was updated on 10 September 2020 to address a defect with Japanese SSML. For more information, see the [10 September 2020 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#September2020b) in the release notes.*

The {{site.data.keyword.texttospeechfull}} service provides application programming interfaces (APIs) that use {{site.data.keyword.IBM_notm}}'s speech-synthesis capabilities to convert written text to natural-sounding speech. The service streams the synthesized audio back to the client with minimal delay. The audio uses appropriate cadence and intonation for its language and dialect to provide voices that are smooth and natural.

The service can be used in applications such as voice-automated chatbots, as well as a variety of voice-driven and screenless applications, such as tools for the disabled or visually impaired, video narration and voice over, and educational and home-automation solutions. It is appropriate for any application where audio is the preferred method of output.

This documentation describes managed instances of {{site.data.keyword.texttospeechfull}} that are offered in {{site.data.keyword.cloud_notm}} or in {{site.data.keyword.icp4dfull_notm}} as a Service. If you are interested in on-premises or installed deployments of the service, see [About {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}](https://{DomainName}/docs/text-to-speech-data?topic=text-to-speech-data-about#about){: external}.
{: note}

## Features and capabilities
{: #features-index}

The {{site.data.keyword.texttospeechshort}} service supports both [HTTP](/docs/text-to-speech?topic=text-to-speech-usingHTTP) and [WebSocket](/docs/text-to-speech?topic=text-to-speech-usingWebSocket) interfaces for speech synthesis. It offers the following features and capabilities:

-   [Audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats) - Produces audio in Ogg or WebM with the Opus or Vorbis codec, WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw, or basic format.
-   [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices) - Synthesizes text to audio in many different languages, voices, and dialects. The service offers both standard (concatenative) and neural versions of most voices.
-   [Obtaining word timings](/docs/text-to-speech?topic=text-to-speech-timing) - With the WebSocket interface, supports the SSML `<mark>` element and optional word timing information for all strings of the input text. Timing information synchronizes the input text and the resulting audio.
-   [Voice customization](/docs/text-to-speech?topic=text-to-speech-customIntro) - Provides a customization interface that you can use to specify how the service pronounces unusual words that occur in your input text. You can define custom dictionaries for domain-specific terms, words with foreign origins, personal or geographic names, and abbreviations or acronyms in your application's lexicon. You can create pronunciations based on other words, on the International Phonetic Alphabet (IPA), or on the {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR).
-   [SSML](/docs/text-to-speech?topic=text-to-speech-ssml) - Accepts plain text or text that is marked up with the XML-based Speech Synthesis Markup Language (SSML).
-   [Expressive SSML](/docs/text-to-speech?topic=text-to-speech-expressive) - Extends SSML with an expressive element that you can use to indicate a speaking style of *GoodNews*, *Apology*, or *Uncertainty*. Available only for the standard US English Allison voice.
-   [Voice transformation SSML](/docs/text-to-speech?topic=text-to-speech-transformation) - Extends SSML by adding a voice transformation element. You can use the element to expand the range of possible voices by controlling aspects such as pitch, rate, and timbre. Also offers two built-in virtual voices, *Young* and *Soft*. Available only for standard US English voices.

For more information about the pricing plans for the service, see the {{site.data.keyword.texttospeechshort}} service in the [{{site.data.keyword.cloud_notm}} Catalog](https://{DomainName}/catalog/text-to-speech){: external}.

## Language support
{: #languages-index}
{: help}
{: support}

The service supports voices in the following languages:

-   Arabic (beta)
-   Brazilian Portuguese
-   Chinese (Mandarin, beta)
-   Dutch (beta)
-   English (United Kingdom and United States dialects)
-   French
-   German
-   Italian
-   Japanese
-   Korean (beta)
-   Spanish (Castilian, Latin American, and North American dialects)

The service offers neural, standard, or both versions of each voice. The service offers at least one female voice for each language. For many languages the service offers multiple voices, including both male and female voices. Each voice uses appropriate cadence and intonation for its dialect.

For more information about the voices that are available for each language, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## Try out the service

For examples of the service in action, see

-   A [quick demo](https://text-to-speech-demo.ng.bluemix.net/){: external} of the {{site.data.keyword.texttospeechshort}} service that accepts text and generates speech with different voices. It offers expressiveness and transformation where supported.
-   Applications in {{site.data.keyword.ibmwatson}} [Starter Kits](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} that demonstrate the {{site.data.keyword.texttospeechshort}} service.
