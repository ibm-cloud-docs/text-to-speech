---

copyright:
  years: 2015, 2021
lastupdated: "2021-07-08"

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

The {{site.data.keyword.texttospeechfull}} service provides APIs that use {{site.data.keyword.IBM_notm}}'s speech-synthesis capabilities to convert written text to natural-sounding speech. The service streams the synthesized audio back to the client with minimal delay. The audio uses appropriate cadence and intonation for its language and dialect to provide voices that are smooth and natural.

The service can be used in applications such as voice-automated chatbots, as well as a variety of voice-driven and screenless applications, such as tools for the disabled or visually impaired, video narration and voice over, and educational and home-automation solutions. It is appropriate for any application where audio is the preferred method of output.

This documentation describes managed instances of {{site.data.keyword.texttospeechfull}} that are offered in {{site.data.keyword.cloud_notm}} or in {{site.data.keyword.icp4dfull_notm}} as a Service. If you are interested in on-premises or installed deployments of the service, see [About {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}](https://{DomainName}/docs/text-to-speech-data?topic=text-to-speech-data-about#about){: external}.
{: note}

## Speech synthesis
{: #about-synthesis}

The {{site.data.keyword.texttospeechshort}} service supports both HTTP and WebSocket interfaces for speech synthesis. Both interfaces accept plain text and text that is marked up with the XML-based Speech Synthesis Markup Language (SSML). The WebSocket interface can also produce timing information about the words of the audio. For more information, see [Synthesizing speech with the service](/docs/text-to-speech?topic=text-to-speech-service-features#features-synthesis-interfaces) in the service features.

## Customization
{: #about-customization}

The service provides a customization interface that you can use to specify how the service pronounces unusual words that occur in your input text. You can define custom models to include dictionaries of words for your application's lexicon. With the Tune by Example feature, you can also add custom prompts to your custom models. Custom prompts let you dictate the prosody with which the service speaks user-specified prompts. For more information about the customization interface and Tune by Example, see [Customizing the service](/docs/text-to-speech?topic=text-to-speech-service-features#features-customization) in the service features.

## Language and voice support
{: #about-languages}
{: help}
{: support}

The service synthesizes text to speech in many languages and dialects:

-   Arabic
-   Brazilian Portuguese
-   Chinese (Mandarin)
-   Dutch (Belgian and Netherlands dialects)
-   English (Australian, United Kingdom, and United States dialects)
-   French (Canadian and France dialects)
-   German
-   Italian
-   Japanese
-   Korean
-   Spanish (Castilian, Latin American, and North American dialects)

The service offers female and male voices for different languages. All voices are neural voices. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## Audio format support
{: #about-formats}
{: help}
{: support}

The service produces audio in many popular formats:

-   Ogg or Web Media (WebM) audio with the Opus or Vorbis codec
-   MP3 (or MPEG)
-   Waveform Audio File Format (WAV)
-   Free Lossless Audio Codec (FLAC)
-   Linear 16-bit Pulse-Code Modulation (PCM)
-   Mu-law (or u-law)
-   Basic audio

Different formats support different sampling rates and other characteristics. For more information, see [Audio formats](/docs/text-to-speech?topic=text-to-speech-audioFormats).

## Pricing
{: #about-pricing}

The service offers multiple pricing plans to suit your usage and application needs. For more information about the pricing plans or to purchase a plan, see the {{site.data.keyword.texttospeechshort}} service in the [{{site.data.keyword.cloud}} Catalog](https://{DomainName}/catalog/text-to-speech){: external}.
