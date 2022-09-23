---

copyright:
  years: 2015, 2022
lastupdated: "2022-09-08"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Using audio formats
{: #audio-formats}

The {{site.data.keyword.texttospeechfull}} service can return synthesized audio in a number of popular audio formats (or MIME types). For information about all supported formats, see [Supported audio formats](#formats-supported).
{: shortdesc}

To make the best use of the service, you need to understand the sampling rate of the audio that the service returns and how to specify a different rate if you need to. For more information, see [Sampling rate](#formats-rate). The service always returns single-channel audio for all formats.

## Sampling rate
{: #formats-rate}

The sampling rate (or sampling frequency) is the number of samples that are generated per second for the audio. Sampling rate is measured in Hertz (Hz) or kilohertz (kHz). For example, a rate of 16,000 samples per second is equal to 16,000 Hz (or 16 kHz). For more information about sampling rates, see [Sampling (signal processing)](https://wikipedia.org/wiki/Sampling_%28signal_processing%29){: external}.

Internally, the service always synthesizes audio with a sampling rate of 22,050 Hz. For many formats, the service also returns audio with this sampling rate. For other formats, the service returns audio with a different sampling rate.

For most formats, you can specify a different sampling rate for the audio. For the `audio/alaw`, `audio/l16`, and `audio/mulaw` formats, you must specify a sampling rate. You specify a sampling rate by including the `rate={integer}` parameter with the audio format specification. For more information, see [Specifying an audio format](#formats-specify).

When you specify a sampling rate, the service resamples the audio from 22,050 Hz to the specified rate before it returns the audio. A specified sampling rate must lie in the range of 8 kHz to 192 kHz. Some audio formats restrict the rate to specific values; the descriptions of the formats identify such restrictions.

### Determining the sampling rate
{: #formats-rate-find}

The most reliable way to identify the sampling rate for any audio that the service returns is to extract the information from the audio stream itself. To determine the rate, call the `/v1/synthesize` method with some simple text (for example, "hello world") and specify the format and codec that you plan to use. You can then obtain the sampling rate by saving the audio stream to a file and opening it in an audio player such as one of those listed in [Playing an audio file](#formats-play).

## Supported audio formats
{: #formats-supported}

Table 1 lists the audio formats in which you can request synthesized audio. By default, the service returns the audio in the Ogg format with the Opus codec (`audio/ogg;codecs=opus`).

The Ogg audio format is not supported with the Safari browser. If you are using the the {{site.data.keyword.texttospeechshort}} service with the Safari browser, you must specify a different format in which you want the service to return the audio. For more information, see [Specifying an audio format](#formats-specify).
{: important}

The service provides the following information for each format:

-   *Default sampling rate* shows the sampling rate for audio in the indicated format if you do not specify an alternative rate.
-   *Required parameters* indicates those formats for which you must specify a sampling rate for the returned audio.
-   *Optional parameters* identifies formats for which you can optionally specify a sampling rate or other characteristics of the returned audio.

As shown in the *Audio formats* column for those formats that accept a `codecs` parameter, you separate all parameters of the format specification with a `;` (semicolon). For more information about the different formats, see the sections that follow the table.

| Audio formats | Default sampling rate | Required parameters | Optional parameters |
|---------------|:---------------------:|:-------------------:|:-------------------:|
| [audio/alaw](#audio-alaw) | None | `rate={integer}` | None |
| [audio/basic](#audio-basic) | 8000 Hz | None | None |
| [audio/flac](#audio-flac) | 22,050 Hz | None | `rate={integer}` |
| [audio/l16](#audio-l16) | None | `rate={integer}` | `endianness=big-endian`  \n `endianness=little-endian` |
| [audio/mp3](#audio-mp3)  \n [audio/mpeg](#audio-mp3) | 22,050 Hz | None | `rate={integer}` |
| [audio/mulaw](#audio-mulaw) | None | `rate={integer}` | None |
| [audio/ogg](#audio-ogg)  \n [audio/ogg;codecs=vorbis](#audio-ogg) | 22,050 Hz | None | `rate={integer}` |
| [audio/ogg;codecs=opus](#audio-ogg) | 48,000 Hz | None | `rate={integer}` |
| [audio/wav](#audio-wav) | 22,050 Hz | None | `rate={integer}` |
| [audio/webm](#audio-webm)  \n [audio/webm;codecs=opus](#audio-webm) | 48,000 Hz | None | None |
| [audio/webm;codecs=vorbis](#audio-webm) | 22,050 Hz | None | `rate={integer}` |
{: caption="Table 1. Summary of supported audio formats"}

### audio/alaw format
{: #audio-alaw}

*A-law* (`audio/alaw`) is a single-channel, lossy audio format that is encoded by using u-law (or mu-law) data that is similar to the `audio/basic` and `audio/mulaw` formats, though the A-law algorithm produces different signal characteristics. You must specify the sampling rate with this format. For example, specify `audio/alaw;rate=8000` for audio that is sampled at 8 kHz.

Due to the streaming nature of the returned audio, the A-law audio that is generated might not work in all audio players. Specifically, the attribute `numSamples` in the header of the audio stream is set to `0` regardless of the length of the audio.
{: note}

For more information, see [A-law algorithm](https://wikipedia.org/wiki/A-law_algorithm){: external}.

### audio/basic format
{: #audio-basic}

*Basic audio* is a single-channel, lossy audio format that is encoded by using 8-bit u-law (or mu-law) data that is sampled at 8 kHz. This format provides a lowest-common denominator media type. Audio in this format always has a sampling rate of 8 kHz.

For more information, see

-   Internet Engineering Task Force (IETF) [Request for Comment (RFC) 2046](https://tools.ietf.org/html/rfc2046){: external}
-   [iana.org/assignments/media-types/audio/basic](https://www.iana.org/assignments/media-types/audio/basic){: external}

### audio/flac format
{: #audio-flac}

*Free Lossless Audio Codec (FLAC)* (`.flac`) is a lossless compressed audio coding format. You can optionally specify a sampling rate other than the default 22,050 Hz.

For more information, see [FLAC](https://wikipedia.org/wiki/FLAC){: external}.

### audio/l16 format
{: #audio-l16}

*Linear 16-bit Pulse-Code Modulation (PCM)* is an uncompressed audio data format (often `.raw` or `.pcm`). You must specify the sampling rate with this audio format. For example, specify `audio/l16;rate=16000` for audio that is sampled at 16 kHz.

You can optionally specify the endianness for the audio by using the `endianness` parameter. Endianness indicates how bytes of data are ordered by the underlying computer architecture:

-   Big-endian (`endianness=big-endian`) orders data by most-significant bit.
-   Little-endian (`endianness=little-endian`) orders data by least-significant bit.

For example, specify `audio/l16;rate=16000;endianness=big-endian` to obtain audio that is sampled at 16 kHz and returned in big-endian order. If you omit the endianness, the default is little-endian. (Specifying the endianness is an issue only for the `audio/l16` format, which does not include a header. Endianness is not a concern for the other formats.)

For more information, see

-   IETF [Request for Comment (RFC) 2586](https://tools.ietf.org/html/rfc2586){: external}
-   [Pulse-code modulation](https://wikipedia.org/wiki/Pulse-code_modulation){: external}
-   [Endianness](https://wikipedia.org/wiki/Endianness){: external}

### audio/mp3 and audio/mpeg formats
{: #audio-mp3}

*MP3* or *Motion Picture Experts Group (MPEG)* is a lossy data compression format (MP3 and MPEG refer to the same format). You can optionally specify a sampling rate other than the default 22,050 Hz.

For more information, see [MP3](https://wikipedia.org/wiki/MP3){: external}.

### audio/mulaw format
{: #audio-mulaw}

*8-bit mu-law (or u-law) audio* is a single-channel, lossy audio format that is encoded by using 8-bit mu-law data. You must specify the sampling rate with this audio format. For example, specify `audio/mulaw;rate=16000` for audio that is sampled at 16 kHz.

For more information, see [M-law algorithm](https://wikipedia.org/wiki/M-law_algorithm){: external}.

### audio/ogg format
{: #audio-ogg}

*Ogg format* (`.ogg`) is a free, open container format that is maintained by the Xiph.org Foundation. You can specify the `codecs` parameter with the format to request an audio stream that is compressed with one of the following codecs:

-   The *Opus* codec by specifying `audio/ogg;codecs=opus`. You can optionally specify a sampling rate other than the default 48,000 Hz. Only the following values are valid sampling rates: `48000`, `24000`, `16000`, `12000`, or `8000`. If you specify a value other than one of these, the service returns an error.

    A current limitation causes the service to disregard a valid sampling rate. The service always returns the audio with a sampling rate of 48 kHz.
    {: important}

-   The *Vorbis* codec by specifying `audio/ogg;codecs=vorbis` or simply `audio/ogg`. You can optionally specify a sampling rate other than the default 22,050 Hz.

Both codecs are free, open, lossy audio-compression formats. Opus is the preferred codec, but per the Ogg specification, the service returns the audio in Vorbis format if you omit the codec. If you omit an audio format altogether, the service returns the audio in Ogg format with the Opus codec by default.

For more information, see

-   [xiph.org/ogg](https://www.xiph.org/ogg/){: external}
-   [xiph.org/vorbis](https://xiph.org/vorbis/){: external}
-   [Vorbis](https://wikipedia.org/wiki/Vorbis){: external}
-   [opus-codec.org](https://www.opus-codec.org/){: external}
-   IETF [Request for Comments (RFC) 7845](https://tools.ietf.org/html/rfc7845){: external}
-   [Opus (audio format)](https://wikipedia.org/wiki/Opus_%28audio_format%29){: external} (look especially at the *Containers* section)

### audio/wav format
{: #audio-wav}

*Waveform Audio File Format (WAV)* (`.wav`) is a standard container format that is often used for uncompressed audio bitstreams but can contain compressed audio, as well. You can optionally specify a sampling rate other than the default 22,050 Hz.

Due to the streaming nature of the returned audio, the WAV audio that is generated might not work in all audio players. Specifically, the attribute `numSamples` in the header of the audio stream is set to `0` regardless of the length of the audio.
{: note}

For more information, see [WAV](https://wikipedia.org/wiki/WAV){: external}.

### audio/webm format
{: #audio-webm}

*Web Media (WebM)* (`.webm`) is an open media-file format. You can specify the `codecs` parameter with the format to request an audio stream that is compressed with one of the following codecs:

-   The *Opus* codec by specifying `audio/webm;codecs=opus` or simply `audio/webm`. Audio in this format always has a sampling rate of 48 kHz.
-   The *Vorbis* codec by specifying `audio/webm;codecs=vorbis`. You can optionally specify a sampling rate other than the default 22,050 Hz.

Both codecs are free, open, lossy audio-compression formats. Opus is the preferred codec.

For more information, see

-   [webmproject.org](https://www.webmproject.org/){: external}
-   [opus-codec.org](https://www.opus-codec.org/){: external}
-   [Opus (audio format)](https://wikipedia.org/wiki/Opus_%28audio_format%29){: external} (look especially at the *Containers* section)
-   [Vorbis](https://wikipedia.org/wiki/Vorbis){: external}

## Specifying an audio format
{: #formats-specify}

By default, the service returns audio in the format `audio/ogg;codecs=opus`. You can specify a different audio format with either the HTTP or the WebSocket interface.

-   With the HTTP `GET` and `POST /v1/synthesize` methods, you can specify a format by using the `Accept` request header or the `accept` query parameter.
    -   If you use the `Accept` request header, you specify the format and any additional parameters as shown in the following example. The example specifies the `audio/l16` format and a sampling rate of 16,000 Hz.

        ```text
        audio/l16;rate=16000
        ```
        {: codeblock}

    -   If you use the `accept` query parameter, you must URL-encode the format and any additional parameters as shown in the following example. The example specifies the same format and sampling rate as the previous example.

        ```text
        audio%2Fl16%3Brate%3D16000
        ```
        {: codeblock}

    To receive audio in the default format, omit both the header and the query parameter. For more information, see [Synthesizing text to audio](/docs/text-to-speech?topic=text-to-speech-usingHTTP#synthesize).
-   With the WebSocket `/v1/synthesize` method, you must specify a format by using the required `accept` parameter of the text message that you pass to initiate synthesis. To receive audio in the default format, specify the value `*/*` for the parameter. For more information, see [Send input text](/docs/text-to-speech?topic=text-to-speech-usingWebSocket#WSsend).

## Playing an audio file
{: #formats-play}

To play an audio file that the service generates, use one of the following tools:

-   A web browser such as Google Chrome™, Firefox®, or Microsoft® Internet Explorer®
-   An audio player such as Audacity® ([audacityteam.org](https://www.audacityteam.org/){: external}) or FFmpeg ([ffmpeg.org](https://www.ffmpeg.org){: external})
