---

copyright:
  years: 2015, 2022
lastupdated: "2022-08-14"

---

{{site.data.keyword.attribute-definition-list}}

# Known limitations
{: #known-limitations}

The {{site.data.keyword.texttospeechshort}} service has the following known limitations.
{: shortdesc}

## Issue: CORS is not supported for neural voices in the Firefox browser
{: #limitation-cors}

**2 December 2020:** Cross-Origin Resource Sharing (CORS) support is not available from the Mozilla Firefox™ browser for neural voices in the following languages: Arabic, Australian English, Chinese, Dutch (Belgian and Netherlands), Korean, and Swedish.

## Issue: Sampling rate for ogg format with opus codec is always 48 kHz
{: #limitation-opus-rate}

**22 August 2019:** When you specify the `audio/ogg;codecs=opus` audio format, you can optionally specify a sampling rate other than the default 48,000 Hz. However, although the service accepts `48000`, `24000`, `16000`, `12000`, or `8000` as a valid sampling rate, it currently disregards a specified value and always returns the audio with a sampling rate of 48 kHz.
