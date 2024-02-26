---

copyright:
  years: 2015, 2023
lastupdated: "2023-03-30"

---

{{site.data.keyword.attribute-definition-list}}

# Known limitations
{: #known-limitations}

The {{site.data.keyword.texttospeechshort}} service has the following known limitations. These issues apply to service functionality that spans releases on all platforms. For information about known limitations specific to {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.6.x, see [Limitations and known issues in Watson Speech services](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=issues-watson-speech-services){: external}.
{: shortdesc}

## Issue: The Ogg audio format is not supported with the Safari browser
{: #limitation-ogg-safari}

**9 September 2022:** By default, the service returns audio in the Ogg audio format with the Opus codec (`audio/ogg;codecs=opus`). However, the Ogg audio format is not supported with the Safari browser. If you are using the {{site.data.keyword.texttospeechshort}} service with the Safari browser, you must specify a different format in which you want the service to return the audio.

-   For more information about the available formats, see [Supported audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats#formats-supported).
-   For more information about specifying a format, see [Specifying an audio format](/docs/text-to-speech?topic=text-to-speech-audio-formats#formats-specify).

## Issue: Sampling rate for ogg format with opus codec is always 48 kHz
{: #limitation-opus-rate}

**22 August 2019:** When you specify the `audio/ogg;codecs=opus` audio format, you can optionally specify a sampling rate other than the default 48,000 Hz. However, although the service accepts `48000`, `24000`, `16000`, `12000`, or `8000` as a valid sampling rate, it currently disregards a specified value and always returns the audio with a sampling rate of 48 kHz.
