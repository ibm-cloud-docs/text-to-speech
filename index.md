---

copyright:
  years: 2015, 2021
lastupdated: "2021-11-23"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# About {{site.data.keyword.texttospeechshort}}
{: #about}

The {{site.data.keyword.texttospeechfull}} service provides APIs that use {{site.data.keyword.IBM_notm}}'s speech-synthesis capabilities to convert written text to natural-sounding speech. The service streams the synthesized audio back to the client with minimal delay.  The audio uses appropriate cadence and intonation for its language and dialect to provide voices that are smooth and natural.

The service can be used in applications such as voice-automated chatbots, as well as a variety of voice-driven and screenless applications, such as tools for the disabled or visually impaired, video narration and voice over, and educational and home-automation solutions. It is appropriate for any application where audio is the preferred method of output.

## Product versions
{: #about-version}

{{site.data.keyword.texttospeechshort}} can be deployed as a managed cloud service or can be installed on premises. This documentation describes how to use both versions of the product. Information that applies exclusively to one version is denoted by the appropriate icon:

-   ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}}** for managed instances of {{site.data.keyword.texttospeechshort}} that are hosted on {{site.data.keyword.cloud_notm}} or for instances that are hosted on [IBM Cloud Pak for Data as a Service](https://dataplatform.cloud.ibm.com/docs/content/wsj/landings/wtts.html){: external}.
    -   For information about all service updates and known limitations, see the [Release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}](/docs/text-to-speech?topic=text-to-speech-release-notes).
    -   For information about the latest service update, see [22 October 2021](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-22october2021) in the release notes.
-   ![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}}** for installed or on-premises instances of {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}. For links to information about installing and managing {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}, see [Installing {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}](/docs/text-to-speech?topic=text-to-speech-speech-install-data).
    -   For information about all service updates and known limitations, see the [Release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}](/docs/text-to-speech?topic=text-to-speech-release-notes-data).
    -   For information about the latest service update, see [30 November 2021 (Version 4.0.3)](/docs/text-to-speech?topic=text-to-speech-release-notes-data#text-to-speech-data-30november2021) in the release notes.

## Speech synthesis
{: #about-synthesis}

The {{site.data.keyword.texttospeechshort}} service supports both HTTP and WebSocket interfaces for speech synthesis. Both interfaces accept plain text and text that is marked up with the XML-based Speech Synthesis Markup Language (SSML). The WebSocket interface can also produce timing information about the words of the audio. For more information, see [Synthesizing speech with the service](/docs/text-to-speech?topic=text-to-speech-service-features#features-synthesis-interfaces) in the service features.

## Customization
{: #about-customization}

The service provides a customization interface that you can use to specify how the service pronounces unusual words that occur in your input text. You can define custom models to include dictionaries of words for your application's lexicon. For more information, see [Customizing the service](/docs/text-to-speech?topic=text-to-speech-service-features#features-customization) in the service features.

With the Tune by Example feature, you can also add custom prompts to your custom models. Custom prompts let you dictate the prosody with which the service speaks user-specified prompts. For more information, see [Using Tune by Example](/docs/text-to-speech?topic=text-to-speech-service-features#features-tune-by-example) in the service features.

## Language support
{: #about-languages}
{: help}
{: support}

The service synthesizes text to speech in many languages and dialects:

-   Arabic
-   Chinese (Mandarin)
-   Dutch (Belgian and Netherlands dialects)
-   English (Australian, United Kingdom, and United States dialects)
-   French (Canadian and France dialects)
-   German
-   Italian
-   Japanese
-   Korean
-   Portuguese (Brazilian)
-   Spanish (Castilian, Latin American, and North American dialects)
-   Swedish

For different languages, the service offers female voices, male voices, or both. For more information, see [Using languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

## Audio support
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

Different formats support different sampling rates and other characteristics. For more information, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

## Beta features
{: #about-beta-features}

{{site.data.keyword.IBM_notm}} occasionally releases features and language support that are classified as beta. Such features are provided so that you can evaluate their functionality. They might be unstable and are subject to change or removal with short notice. They are not intended for use in a production environment.

Beta features might not provide the same level of performance or compatibility as generally available features. Generally available features are ready for use in a production environment.

## Pricing
{: #about-pricing}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only**

The service offers multiple pricing plans to suit your usage and application needs. For more information about the pricing plans or to purchase a plan, see the {{site.data.keyword.texttospeechshort}} service in the [{{site.data.keyword.cloud}} Catalog](https://{DomainName}/catalog/text-to-speech){: external}.
