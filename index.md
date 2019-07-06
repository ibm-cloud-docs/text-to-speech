---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-06"

subcollection: text-to-speech

---

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

> ** Service update:** *The {{site.data.keyword.texttospeechshort}} service was updated on June 24, 2019. The service now offers enhanced neural versions of most voices. The neural voices include the string `V3` in their names. The new voices replace the previous `V2` voices, which are no longer available. For more information, see the [24 June 2019 service update](/docs/services/text-to-speech?topic=text-to-speech-release-notes#June2019) in the release notes*.

The {{site.data.keyword.texttospeechfull}} service provides an application programming interface (API) that uses {{site.data.keyword.IBM_notm}}'s speech-synthesis capabilities to convert written text to natural-sounding speech. The service streams the results back to the client with minimal delay. The service offers both [HTTP](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) and [WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket) interfaces.

## Features and capabilities

The {{site.data.keyword.texttospeechshort}} service offers the following features and capabilities:

-   **Audio formats** - Produces audio in Ogg or WebM with the Opus or Vorbis codec, WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw, or basic format. For more information, see [Audio formats](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   **Voices** - Synthesizes text to audio in various languages, voices, and dialects. The service offers both standard (concatenative) and neural versions of most voices. For more information, see [Languages and voices](/docs/services/text-to-speech?topic=text-to-speech-voices).
-   **SSML** - Accepts plain text or text that is marked up with the XML-based Speech Synthesis Markup Language (SSML). For more information, see [Using SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml).
-   **Expressiveness** - Extends SSML with an expressive element that you can use to indicate a speaking style of *GoodNews*, *Apology*, or *Uncertainty*. Available only for the standard US English Allison voice. For more information, see [Expressive SSML](/docs/services/text-to-speech?topic=text-to-speech-expressive).
-   **Voice transformation** - Extends SSML by adding a voice transformation element. You can use the element to expand the range of possible voices by controlling aspects such as pitch, rate, and timbre. Also offers two built-in virtual voices, *Young* and *Soft*. Available only for standard US English voices. For more information, see [Voice transformation SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   **Word timings** - With the WebSocket interface, supports the SSML `<mark>` element and optional word timing information for all strings of the input text. Timing information synchronizes the input text and the resulting audio. For more information, see [Obtaining word timings](/docs/services/text-to-speech?topic=text-to-speech-timing).
-   **Customization** - Provides a customization interface that you can use to specify how the service pronounces unusual words that occur in your input. You can define pronunciations with the International Phonetic Alphabet (IPA) or {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). For more information, see [Understanding customization](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

For more information about the pricing plans for the service, see the {{site.data.keyword.texttospeechshort}} service in the [{{site.data.keyword.cloud_notm}} Catalog](https://{DomainName}/catalog/services/text-to-speech){: external}.

## Language support
{: #languages-index}

The service supports voices in the following languages: Brazilian Portuguese, English (UK and US dialects), French, German, Italian, Japanese, and Spanish (Castilian, Latin American, and North American dialects).

The service offers at least one female voice for each language. For some languages the service offers multiple voices, including both male and female voices. Each voice uses appropriate cadence and intonation for its dialect. The service offers both standard and neural versions of most voices.

For more information about the voices that are available for each language, see [Languages and voices](/docs/services/text-to-speech?topic=text-to-speech-voices).

## Use cases
{: #usecases}

The service is appropriate for voice-driven and screenless applications, where audio is the preferred method of output:

-   Interfaces for the disabled, such as assistance tools for the vision-impaired
-   Reading text and email messages aloud to drivers
-   Video-script narration and video voice over
-   Reading-based educational tools
-   Home-automation solutions

## Try out the service

For examples of the service in action, see

-   A [quick demo](https://text-to-speech-demo.ng.bluemix.net/){: external} of the {{site.data.keyword.texttospeechshort}} service that accepts text and generates speech with different voices. It offers expressiveness and transformation where supported.
-   Applications in {{site.data.keyword.ibmwatson}} [Starter Kits](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} that demonstrate the {{site.data.keyword.texttospeechshort}} service.
