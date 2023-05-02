---

copyright:
  years: 2015, 2023
lastupdated: "2023-05-02"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# About {{site.data.keyword.texttospeechshort}}
{: #about}

The {{site.data.keyword.texttospeechfull}} service provides APIs that use {{site.data.keyword.IBM_notm}}'s speech-synthesis capabilities to convert written text to natural-sounding speech. The service streams the synthesized audio back to the client with minimal delay.  The audio uses appropriate cadence and intonation for its language and dialect to provide voices that are smooth and natural.

The service can be used in applications such as voice-automated chatbots, as well as a variety of voice-driven and screenless applications, such as tools for the disabled or visually impaired, video narration and voice over, and educational and home-automation solutions. It is appropriate for any application where audio is the preferred method of output.

## Product versions
{: #about-version}

{{site.data.keyword.texttospeechshort}} can be deployed as a managed cloud service or can be installed on premises. This documentation describes how to use both versions of the product. Information such as topics, paragraphs, and examples that applies exclusively to one version is clearly denoted:

-   [IBM Cloud]{: tag-ibm-cloud} for managed instances of {{site.data.keyword.texttospeechshort}} that are hosted on {{site.data.keyword.cloud_notm}} or for instances that are hosted on [IBM Cloud Pak for Data as a Service](https://dataplatform.cloud.ibm.com/docs/content/wsj/landings/wtts.html){: external}.
    -   For information about all service updates, see the [Release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}](/docs/text-to-speech?topic=text-to-speech-release-notes).
    -   For information about the latest service update, see the [6 April 2023](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-6april2023) service update in the release notes.
-   [IBM Cloud Pak for Data]{: tag-cp4d} for installed or on-premises instances of {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}. For links to information about installing and managing {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}, see [Installing {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}](/docs/text-to-speech?topic=text-to-speech-speech-install-data).
    -   For information about all service updates, see the [Release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}](/docs/text-to-speech?topic=text-to-speech-release-notes-data).
    -   For information about the latest service update, see the [2 May 2023 (Version 4.6.5)](/docs/text-to-speech?topic=text-to-speech-release-notes-data#text-to-speech-data-2may2023) service update in the release notes.

## Speech synthesis
{: #about-synthesis}

The {{site.data.keyword.texttospeechshort}} service supports both HTTP and WebSocket interfaces for speech synthesis. Both interfaces accept plain text and text that is marked up with the XML-based Speech Synthesis Markup Language (SSML). The WebSocket interface can also produce timing information about the words of the audio. For more information, see the following service features:

-   [Synthesizing speech with the service](/docs/text-to-speech?topic=text-to-speech-service-features#features-synthesis-interfaces)
-   [Using speech synthesis features](/docs/text-to-speech?topic=text-to-speech-service-features#features-synthesis)

## Customization
{: #about-customization}

The service provides a customization interface that you can use to specify how the service pronounces unusual words that occur in your input text. You can define custom models to include dictionaries of words for your application's lexicon. For more information, see [Customizing the service](/docs/text-to-speech?topic=text-to-speech-service-features#features-customization) in the service features.

With the Tune by Example feature, you can also add custom prompts to your custom models. Custom prompts let you dictate the prosody with which the service speaks user-specified prompts. For more information, see [Using Tune by Example](/docs/text-to-speech?topic=text-to-speech-service-features#features-tune-by-example) in the service features.

## Language support
{: #about-languages}
{: help}
{: support}

The service offers neural voices to synthesize text to speech in many languages and dialects:

-   Dutch (Netherlands)
-   English (Australian, United Kingdom, and United States dialects)
-   French (Canadian and France dialects)
-   German
-   Italian
-   Japanese
-   Korean
-   Portuguese (Brazilian)
-   Spanish (Castilian, Latin American, and North American dialects)

For different languages, the service offers female voices, male voices, or both. For more information about the supported languages and voices, the types of voices that the service provides for each language, and their status for both versions of the service, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## Audio support
{: #about-formats}
{: help}
{: support}

The service produces audio in many popular formats:

-   A-law
-   Basic audio
-   Free Lossless Audio Codec (FLAC)
-   Linear 16-bit Pulse-Code Modulation (PCM)
-   MP3 (or MPEG)
-   Mu-law (or u-law)
-   Ogg or Web Media (WebM) audio with the Opus or Vorbis codec
-   Waveform Audio File Format (WAV)

Different formats support different sampling rates and other characteristics. For more information, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

## Beta features
{: #about-beta-features}

{{site.data.keyword.IBM_notm}} occasionally releases features and language support that are classified as beta. Such features are provided so that you can evaluate their functionality. They might be unstable and are subject to change or removal with short notice. They are not intended for use in a production environment.

Beta features might not provide the same level of performance or compatibility as generally available features. Generally available features are ready for use in a production environment.

## Pricing
{: #about-pricing}

[IBM Cloud]{: tag-ibm-cloud}

The service offers multiple pricing plans to suit your usage and application needs. For more information about the pricing plans or to purchase a plan, see the {{site.data.keyword.texttospeechshort}} service in the [{{site.data.keyword.cloud}} Catalog](https://{DomainName}/catalog/text-to-speech){: external}.
