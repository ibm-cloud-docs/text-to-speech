---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# The HTTP REST interface
{: #usingHTTP}

To synthesize text to speech with the service's HTTP REST API, you call the `GET` or `POST` version of the service's `/v1/synthesize` method. You specify the text to be synthesized, the voice for the spoken audio, and the format for the audio. You can also specify a custom voice model to be used with the request. For more information about the HTTP interface, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/){: new_window}.
{: shortdesc}

## Synthesizing text to audio
{: #synthesize}

To synthesize text to audio, you call one of the two versions of the service's `/v1/synthesize` method:

-   The `GET /v1/synthesize` method accepts the text to be synthesized via its required `text` query parameter.
-   The `POST /v1/synthesize` method accepts the text to be synthesized via a JSON construct in the required body of the request.

Both versions of the method accept a maximum of 5 KB of input text. For more information, see [Specifying input text](#input). The two versions of the `/v1/synthesize` method have the following parameters in common:

<table>
  <caption>Table 1. Parameters of the <code>/v1/synthesize</code>
    methods</caption>
  <tr>
    <th style="text-align:left; width:18%">Parameter</th>
    <th style="text-align:center; width:12%">Type</th>
    <th style="text-align:center; width:12%">Data type</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>Optional</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      Specifies the requested audio format, or MIME type, in which the
      service is to return the audio. You can also specify this value with
      the HTTP <code>Accept</code> request header. For more information,
      see <a href="#format">Specifying an audio format</a>.
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Optional</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      Specifies the voice in which the text is to be spoken in
      the audio. Use the <code>voices</code> method to get the current
      list of supported voices. The default voice is
      <code>en-US_MichaelVoice</code>. For more information, see
      <a href="#voices">Specifying a voice</a>.
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Optional</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      Specifies a globally unique identifier (GUID) for a custom voice
      model to be used for the synthesis. A specified custom voice model
      is guaranteed to work only if it matches the language of the voice
      that is used for the synthesis. If you include a customization ID,
      you must call the method with the service credentials of the model's
      owner. Omit the parameter to use the specified voice with no
      customization. For more information, see
      <a href="/docs/services/text-to-speech/custom-intro.html">Understanding
        customization</a>.
    </td>
  </tr>
</table>

You can also use the following request headers, which are available for all {{site.data.keyword.watson}} service, with a synthesize request:

-   `X-Watson-Learning-Opt-Out` controls the logging of requests to the service; see [Controlling request logging for {{site.data.keyword.watson}} services](/docs/services/watson/getting-started-logging.html).
-   `X-Watson-Metadata` associates a customer ID with data that is passed with a request; see [Information security](/docs/services/text-to-speech/information-security.html).

> **Note:** If you specify an invalid query parameter or JSON field as part of the input to the `/v1/synthesize` method, the service returns a `Warnings` response header that describes and lists each invalid argument. The request succeeds despite the warnings.

## Specifying an audio format
{: #format}

Both versions of the `/v1/synthesize` method take an optional `accept` query parameter to specify the requested audio format (MIME type) of the audio. (You can also specify the value with the `Accept` request header.) The parameter accepts the following audio formats. If you omit the parameter, the service returns the audio in Ogg format with the Opus codec (`audio/ogg;codecs=opus`) by default.

<table>
  <caption>Table 2. Supported audio formats</caption>
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
      <a target="_blank" href="https://tools.ietf.org/html/rfc2046">Request
        for Comment (RFC) 2046 ![External link icon](../../icons/launch-glyph.svg "External link icon")</a> and
      <a target="_blank" href="http://www.iana.org/assignments/media-types/audio/basic">iana.org/assignments/media-types/audio/basic ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>Free Lossless Audio Codec (FLAC)</em> (<code>.flac</code>),
      a lossless compressed audio coding format. For more information, see
      <a target="_blank" href="https://en.wikipedia.org/wiki/FLAC">en.wikipedia.org/wiki/FLAC ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
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
      <a target="_blank" href="https://tools.ietf.org/html/rfc2586">Request
        for Comment (RFC) 2586 ![External link icon](../../icons/launch-glyph.svg "External link icon")</a> and
      <a target="_blank" href="https://en.wikipedia.org/wiki/Pulse-code_modulation">en.wikipedia.org/wiki/Pulse-code_modulation ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.<br/><br/>
      You must specify the sampling rate with this audio format. For example,
      specify <code>audio/l16;rate=16000</code> for audio that is sampled at
      16 kHz. You can also optionally specify the endianness as either
      <code>audio/l16;rate={rate};endianness=big-endian</code> or
      <code>audio/l16;rate={rate};endianness=little-endian</code>; the
      default is little endian.
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
      For more information, see
      <a target="_blank" href="https://en.wikipedia.org/wiki/MP3">en.wikipedia.org/wiki/MP3 ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
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
      see
      <a target="_blank" href="https://en.wikipedia.org/wiki/M-law_algorithm">en.wikipedia.org/wiki/M-law_algorithm ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
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
      <a target="_blank" href="https://www.xiph.org/ogg/">xiph.org/ogg/ ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
      You can request audio streams that are compressed with the following
      codecs:
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <em>Opus</em>. For more information, see
          <a target="_blank" href="https://www.opus-codec.org/">opus-codec.org ![External link icon](../../icons/launch-glyph.svg "External link icon")</a> and
          <a target="_blank" href="https://en.wikipedia.org/wiki/Opus">en.wikipedia.org/wiki/Opus (audio format) ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
          On the <em>Opus (audio format)</em> page, look especially at the
          <em>Containers</em> section.
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <em>Vorbis</em>. For more information, see
          <a target="_blank" href="https://xiph.org/vorbis/">xiph.org/vorbis ![External link icon](../../icons/launch-glyph.svg "External link icon")</a> and
          <a target="_blank" href="https://en.wikipedia.org/wiki/Vorbis">en.wikipedia.org/wiki/Vorbis ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
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
      For more information, see
      <a target="_blank" href="https://en.wikipedia.org/wiki/WAV">en.wikipedia.org/wiki/WAV ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
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
      <a target="_blank" href="https://www.webmproject.org/">webmproject.org ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
    </td>
  </tr>
</table>

The audio files can be played in a web browser by an audio player such as Audacity&reg; ([audacityteam.org ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.audacityteam.org/){: new_window}) or FFmpeg ([ffmpeg.org ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ffmpeg.org){: new_window}).

### Specifying a sampling rate
{: #sampling}

The service always synthesizes audio with a sampling rate of 22,050 Hz. For most audio formats, the service returns audio with this default sampling rate. For some formats, you can specify a different sampling rate by including the `rate={rate}` parameter. For `audio/l16` and `audio/mulaw`, you *must* specify a sampling rate. The service resamples the audio and returns it at the specified rate. A specified sampling rate must lie in the range of 8 kHz to 192 kHz.

The following table shows the default sampling rate of the audio that is returned for each format and indicates those formats for which the `rate` parameter can or must be specified.

<table style="width:90%">
  <caption>Table 3. Sampling rates for audio formats</caption>
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

> **Note:** The Opus standard requires the output sampling rate to match the capabilities of the audio player. For more information, see Section 5.1 of the Internet Engineering Task Force (IETF) [Request for Comments (RFC) 7845 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://tools.ietf.org/html/rfc6455){: new_window}. For software audio players, the table indicates the typical output sampling rate, but the actual sampling rate of the audio varies with time within the stream. As mentioned, the service synthesizes the source audio at 22,050 Hz.

## Specifying a voice
{: #voices}

Both versions of the `/v1/synthesize` method accept an optional `voice` query parameter to specify the voice for the audio. The service bases its understanding of the language for the input text on the specified voice. Be sure to specify a voice that matches the language of the input text.

For example, if you specify the voice `fr-FR_ReneeVoice`, the service assumes that the input text is written in French. If you pass text that is not written in the language of the voice (for example, English text for the French voice), the service might not produce meaningful results.

The service offers methods for [Listing all available voices](#listVoices) and for [Listing a specific voice](#listVoice).

### Languages and voices
{: #languageVoices}

The following table lists the voices that are available for each language and dialect, including their gender. Each voice uses appropriate cadence and intonation for its dialect. If you omit the voice from any request, the service uses the `en-US_MichaelVoice` voice by default.

<table style="width:90%">
  <caption>Table 4. Supported languages and voices</caption>
  <tr>
    <th style="text-align:left">Languages</th>
    <th style="text-align:center">Voice</th>
    <th style="text-align:center">Gender</th>
  </tr>
  <tr>
    <td style="text-align:left">Brazilian Portuguese</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">Castilian Spanish</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">French</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">German</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td style="text-align:left">Italian</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">Japanese</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">Latin American Spanish</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">North American Spanish</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">UK English</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">US English</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
</table>

> **Note:** The voices `es-LA_SofiaVoice` and `es-US_SofiaVoice` are essentially the same voice. The most significant difference concerns how the two voices interpret a `$` (dollar sign): The Latin American version uses the term *pesos*, while the North American version uses the term *dolares*. Other minor differences might exist between the two voices.

### Listing all available voices
{: #listVoices}

The `GET /v1/voices` method lists information about all available voices. It takes no arguments and returns a JSON array that is named `voices`. The array includes a separate object for each voice.

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaVoice",
      "language": "en-US",
      "gender": "female",
      "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
      "description": "Lisa: American English female voice.",
      "customizable": true,
      "supported_features": {
        "voice_transformation": true,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

The fields of the voice objects provide the following information:

-   `name` is an identifier for the voice (for example, `en-US_LisaVoice`). Specify this value for the `voice` parameter of the `/v1/synthesize` method.
-   `language` specifies the language and region of the voice (for example, `en-US`).
-   `gender` identifies the voice as `male` or `female`.
-   `url` identifies the URL for the voice.
-   `description` provides a brief description of the voice.
-   `customizable` is a boolean value that indicates whether the voice can be customized with the service's customization interface. (Same as `custom_pronunciation`; maintained for backward compatibility.)
-   `supported_features` describes the additional service features that are supported by the voice:
    -   `voice_transformation` is a boolean value that indicates whether the voice can be transformed by using the SSML `<voice-transformation>` element.
    -   `custom_pronunciation` is a boolean value that indicates whether the voice can be customized with the service's customization interface. (Same as `customizable`.)

### Listing a specific voice
{: #listVoice}

The `GET /v1/voices/{voice}` method lists information about a specific voice. It accepts two parameters:

<table>
  <caption>Table 5. Parameters of the <code>voices</code> method</caption>
  <tr>
    <th style="text-align:left; width:18%">Parameter</th>
    <th style="text-align:center; width:12%">Type</th>
    <th style="text-align:center; width:12%">Data type</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Required</em></td>
    <td style="text-align:center">Path</td>
    <td style="text-align:center">String</td>
    <td>
      Identifies the voice for which information is to be returned.
      You specify a voice by its name (for example,
      <code>en-US_LisaVoice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Optional</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      Provides the globally unique identifier (GUID) of a custom voice
      model that is defined for the specified voice. If you include a
      customization ID, you must call the method with the service
      credentials of the custom model's owner.
    </td>
  </tr>
</table>

If you omit the `customization_id` parameter, the method returns JSON output for the specified voice that is identical to the information returned for a voice by the `GET /v1/voices` method. If you specify a `customization_id`, the output includes a `customization` field that provides information about the specified custom voice model.

```javascript
{
  "name": "en-US_LisaVoice",
  "language": "en-US",
  "gender": "female",
  "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
  "description": "Lisa: American English female voice.",
  "customizable": true,
  "supported_features": {
    "voice_transformation": true,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

The attributes of the additional `customization` field provide information such as the GUID, name, language, and description of the custom voice model. They also show the service credentials of the model's owner, the date and time at which the model was created, and the date and time of its last modification.

## Specifying input text
{: #input}

Both the `GET` and `POST` versions of the `/v1/synthesize` method accept a maximum of 5 KB of input text, and both accept input that is annotated with SSML. The two versions differ primarily in how you specify the text to be synthesized:

-   The `GET /v1/synthesize` method accepts input text that is specified by the `text` query parameter. You specify the input as plain text or as SSML, both of which must be URL-encoded.
-   The `POST /v1/synthesize` method accepts input text in the body of the request. You specify the input with the following simple JSON construct that encapsulates plain text or SSML. You must also specify a value of `application/json` for the `Content-Type` header.

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

Although the `GET` and `POST` methods offer equivalent functionality, it is always more secure to pass input text to the service with the `POST` method. A `POST` request passes input in the body of the request, while a `GET` request exposes the data in the URL.

> **Note:** The examples that follow include line breaks for readability; do *not* include them in actual input.

### Specifying SSML input
{: #ssml}

The Speech Synthesis Markup Language (SSML) is an XML-based markup language that is designed to provide annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service. You can use SSML elements and their attributes to gain greater control over the synthesis and resulting audio output.

For more information about using SSML to annotate input text, see [Using SSML](/docs/services/text-to-speech/SSML.html). The documentation introduces the inventory of SSML elements and attributes that are supported by the service. It also documents the service's expressive and voice-transformation extensions.

### Escaping XML control characters
{: #escape}

Because you can submit input text that includes XML-based SSML annotations, the service validates all input to ensure that any SSML is correct and well formed. Therefore, you must escape any XML control characters that are present in the input text, regardless of whether the input includes SSML. Use the equivalent escape strings or character encodings from the following table instead of the indicated characters.

<table style="width:80%">
  <caption>Table 6. Escaping XML control characters</caption>
  <tr>
    <th style="text-align:center; vertical-align:bottom; width:40%">Character</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">Escape strings</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">Character encoding</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>&quot;</code><br/>(double quotes)</td>
    <td style="text-align:center"><code>&amp;quot;</code></td>
    <td style="text-align:center"><code>&amp;#34;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>'</code><br/>(apostrophe or single quote)</td>
    <td style="text-align:center"><code>&amp;apos;</code></td>
    <td style="text-align:center"><code>&amp;#39;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&amp;</code><br/>(ampersand)</td>
    <td style="text-align:center"><code>&amp;amp;</code></td>
    <td style="text-align:center"><code>&amp;#38;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&lt;</code><br/>(left angle bracket)</td>
    <td style="text-align:center"><code>&amp;lt;</code></td>
    <td style="text-align:center"><code>&amp;#60;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&gt;</code><br/>(right angle bracket)</td>
    <td style="text-align:center"><code>&amp;gt;</code></td>
    <td style="text-align:center"><code>&amp;#62;</code></td>
  </tr>
</table>

For more information about how the service validates input text, see [SSML validation](/docs/services/text-to-speech/SSML.html#errors).

### Example input with a GET request
{: #getExamples}

The following examples pass URL-encoded input with the `text` query parameter of the `GET /v1/synthesize` method:

-   Plain text input:

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   SSML input:

    ```
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3C
    break%20time=%225s%22/%3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another
    %20sentence.%3C/s%3E%3Cs%3EFinally,%20this%20is%20the%20last%20sentence.
    %3C/s%3E%3C/p%3E%22
    ```
    {: codeblock}

### Example input with a POST request
{: #postExamples}

The following examples pass input in the body of the `POST /v1/synthesize` method:

-   Plain text input:

    ```javascript
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   SSML input:

    ```javascript
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/>
        paragraph.</s><s>Here is another sentence.</s><s>Finally, this is
        the last sentence.</s></p>"
    }
    ```
    {: codeblock}

### Example input with XML control characters
{: #xmlExamples}

The following examples send two sentences to the `POST /v1/synthesize` method. The examples properly escape the embedded XML characters.

```
"What have I learned?" he asked. "Everything!"
```
{: codeblock}

-   Plain text input:

    ```javascript
    {
      "text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
    }
    ```
    {: codeblock}

-   SSML input:

    ```javascript
    {
      "text": "<s>&quot;What have I learned?&quot; he asked.
        &quot;<express-as type=\"GoodNews\">Everything!</express-as>&quot;</s>"
    }
    ```
    {: codeblock}
