---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-06"

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

# Audio formats
{: #audioFormats}

The {{site.data.keyword.texttospeechfull}} service can return synthesized audio in a number of formats. For most formats, the service returns audio with a default sampling rate of 22,050 Hz. For some formats, you can or must specify the sampling rate of the audio. The service always returns single-channel audio for all formats.
{: shortdesc}

## Supported audio formats
{: #formatsSupported}

Table 1 lists the audio formats (MIME types) in which you can request synthesized audio. By default, the service returns the audio in Ogg format with the Opus codec (`audio/ogg;codecs=opus`).

<table>
  <caption>Table 1. Supported audio formats</caption>
  <tr>
    <th style="text-align:left; width:25%">Audio format</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td>
      <em>Basic audio</em>, a single-channel, lossy audio format that is
      encoded by using 8-bit u-law (or mu-law) data that is sampled at 8 kHz.
      This format provides a lowest-common denominator media type. For more
      information, see the IETF
      [Request for Comment (RFC) 2046](https://tools.ietf.org/html/rfc2046) and
      [iana.org/assignments/media-types/audio/basic](http://www.iana.org/assignments/media-types/audio/basic).
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>Free Lossless Audio Codec (FLAC)</em> (<code>.flac</code>),
      a lossless compressed audio coding format. For more information,
      see [FLAC](https://wikipedia.org/wiki/FLAC).
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td>
      <em>Linear 16-bit Pulse-Code Modulation (PCM)</em>, an uncompressed
      audio data format (often <code>.raw</code> or <code>.pcm</code>). For
      more information, see the Internet Engineering Task Force (IETF)
      [Request for Comment (RFC) 2586](https://tools.ietf.org/html/rfc2586) and
      [Pulse-code modulation](https://wikipedia.org/wiki/Pulse-code_modulation).<br/><br/>
      You must specify the sampling rate with this audio format. For example,
      specify <code>audio/l16;rate=16000</code> for audio that is sampled at
      16 kHz. You can also optionally specify the endianness as either
      <code>audio/l16;rate={rate};endianness=big-endian</code> or
      <code>audio/l16;rate={rate};endianness=little-endian</code>.
      The default is little endian.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td>
      <em>MP3</em> or <em>Motion Picture Experts Group (MPEG)</em>, a lossy
      data compression format (MP3 and MPEG refer to the same format).
      For more information, see [MP3](https://wikipedia.org/wiki/MP3).
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td>
      <em>8-bit mu-law (or u-law) audio</em>, a single-channel, lossy audio
      format that is encoded by using 8-bit u-law (or mu-law) data. You must
      specify the sampling rate with this audio format. For more information,
      see [M-law algorithm](https://wikipedia.org/wiki/M-law_algorithm).
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=opus</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td>
      <em>Ogg format</em> (<code>.ogg</code>), a free, open container format
      that is maintained by the Xiph.org Foundation. For more information, see
      [xiph.org/ogg/](https://www.xiph.org/ogg/).
      You can request audio streams that are compressed with the following
      codecs:
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <em>Opus</em>. For more information, see
	  [opus-codec.org](https://www.opus-codec.org/) and
	  [Opus (audio format)](https://wikipedia.org/wiki/Opus_%28audio_format%29).
          Look especially at the <em>Containers</em> section.
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <em>Vorbis</em>. For more information, see
	  [xiph.org/vorbis](https://xiph.org/vorbis/) and
	  [Vorbis](https://wikipedia.org/wiki/Vorbis).
        </li>
      </ul>
      Both codecs are free, open, lossy audio-compression formats. Opus
      is the preferred codec, but per the Ogg specification, the service
      returns the audio in Vorbis format if you omit the codec. If you
      omit an audio format altogether, the service returns the audio in
      Ogg format with the Opus codec by default.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td>
      <em>Waveform Audio File Format (WAV)</em> (<code>.wav</code>) is
      a standard container format that is often used for uncompressed
      audio bitstreams but can contain compressed audio, as well. Due to
      the streaming nature of the returned audio, the WAV file that is
      generated might not work in all audio players. Specifically,
      the attribute <code>numSamples</code> in the header of the file
      is set to <code>0</code> regardless of the length of the audio.
      For more information, see [WAV](https://wikipedia.org/wiki/WAV).
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code><br/>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td>
      <em>Web Media (WebM)</em> (<code>.webm</code>), an open media-file
      format that provides support for audio streams that are compressed
      with the Opus and Vorbis audio codecs. If you omit the codec, the
      service returns the audio in Opus format. For more information, see
      [webmproject.org](https://www.webmproject.org/).
    </td>
  </tr>
</table>

## Specifying an audio format
{: #formatSpecify}

Specifying an audio format is optional. By default, the service returns audio in the format `audio/ogg;codecs=opus`. But you can specify a format for either the HTTP or the WebSocket interface:

-   With the HTTP `GET` and `POST /v1/synthesize` methods, you specify a format by using the `Accept` request header or the `accept` query parameter. To receive audio in the default format, omit both the header and the query parameter. For more information, see [Synthesizing text to audio](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#synthesize).

    If you use the `accept` query parameter, URL-encode the argument to the parameter. For example, URL-encode the following argument

    ```
    audio/l16;rate=16000;endianness=little-endian
    ```
    {: codeblock}

    as

    ```
    audio%2Fl16%3Brate%3D16000%3Bendianness%3Dlittle-endian
    ```
    {: codeblock}

-   With the WebSocket interface, you specify a format by using the `accept` parameter of the text message that you pass to initiate synthesis. To receive audio in the default format, specify the value `*/*` for the parameter. For more information, see [Send input text](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket#WSsend).

## Specifying a sampling rate
{: #formatRate}

The service always synthesizes audio with a sampling rate of 22,050 Hz. For most audio formats, the service returns audio with this default sampling rate. For some formats, you can specify a different sampling rate by including the `rate={rate}` parameter. For the `audio/l16` and `audio/mulaw` formats, you *must* specify a sampling rate.

When you specify a sampling rate, the service resamples the audio and returns it at the specified rate. A specified sampling rate must lie in the range of 8 kHz to 192 kHz.

Table 2 shows the default sampling rate of the audio that is returned for each format and indicates those formats for which you can or must specify a sampling rate.

<table style="width:90%">
  <caption>Table 2. Sampling rates for audio formats</caption>
  <tr>
    <th style="text-align:left">Audio format</th>
    <th style="text-align:center">Default sampling rate</th>
    <th style="text-align:center">Use of <code>rate</code> parameter</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td style="text-align:center">
      8000 Hz
    </td>
    <td style="text-align:center">
      Not allowed
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td style="text-align:center">
      22,050 Hz
    </td>
    <td style="text-align:center">
      Optional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td style="text-align:center">
      None
    </td>
    <td style="text-align:center">
      Required; for example<br />
      <code>audio/l16;rate=22050</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td style="text-align:center">
      22,050 Hz
    </td>
    <td style="text-align:center">
      Optional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td style="text-align:center">
      None
    </td>
    <td style="text-align:center">
      Required; for example<br />
      <code>audio/mulaw;rate=8000</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td style="text-align:center">
      22,050 Hz
    </td>
    <td style="text-align:center">
      Optional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg;codecs=opus</code>
    </td>
    <td style="text-align:center">
      22,050 Hz [see <strong>Note</strong>]
    </td>
    <td style="text-align:center">
      Optional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td style="text-align:center">
      22,050 Hz
    </td>
    <td style="text-align:center">
      Optional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code>
    </td>
    <td style="text-align:center">
      48,000 Hz [see <strong>Note</strong>]
    </td>
    <td style="text-align:center">
      Not allowed
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td style="text-align:center">
      22,050 Hz
    </td>
    <td style="text-align:center">
      Optional
    </td>
  </tr>
</table>

The most reliable way to identify the sampling rate for any audio stream that the service returns is to extract the information from the stream itself. You can determine the rate by calling the `/v1/synthesize` method with some simple text (for example, "hello world") and specifying the format and codec that you plan to use. You can then obtain the codec and sampling rate by saving the audio stream to a file and opening it in an audio player.

The Opus standard requires the output sampling rate to match the capabilities of the audio player. For more information, see Section 5.1 of the Internet Engineering Task Force (IETF) [Request for Comments (RFC) 7845](http://tools.ietf.org/html/rfc6455){: external}. For software audio players, the table indicates the typical output sampling rate, but the actual sampling rate of the audio varies with time within the stream. As mentioned, the service synthesizes the source audio at 22,050 Hz.
{: note}

## Playing an audio file
{: #formatsPlay}

To play an audio file that the service generates, use one of the following tools:

-   A web browser such as Google Chrome&trade;, Firefox&reg; or Microsoft&reg; Internet Explorer&reg;.
-   An audio player such as Audacity&reg; ([audacityteam.org](http://www.audacityteam.org/){: external}) or FFmpeg ([ffmpeg.org](https://www.ffmpeg.org){: external}).
