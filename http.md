---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-11"

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

# Using the HTTP interface
{: #using}

To synthesize text to speech with the service's HTTP REST API, you call the `GET` or `POST` version of the service's `synthesize` method. You specify the text to be synthesized and the voice for the spoken audio. You can also specify a custom voice model to be used, and you can pass text that is marked up with SSML. For detailed information about the HTTP interface, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/){: new_window}.
{: shortdesc}

## Synthesizing text to audio
{: #synthesize}

To synthesize text to audio, you call one of the two versions of the service's `synthesize` method:

-   The `GET synthesize` method accepts the text to be synthesized via its required `text` query parameter. Use this version of the method for simple text that is easily accommodated on the URL.
-   The `POST synthesize` method accepts the text to be synthesized via a JSON construct in the required body of the request. Use this version of the method for longer text or for text that you do not want to expose on the URL.

For more information, see [Specifying input text](#input). The two versions of the `synthesize` method have the following parameters in common:

<table>
  <caption>Table 1. Parameters of the <code>synthesize</code>
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
      Specifies the requested MIME type, or audio format, in which the
      service is to return the audio. You can also specify this value via
      the HTTP <code>Accept</code> request header. For complete information
      about the supported formats, see <a href="#format">Specifying an audio
        format</a>.
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
      used for the synthesis. If you include a customization ID, you must
      call the method with the service credentials of the model's owner.
      Omit the parameter to use the specified voice with no customization.
      For more information, see
      <a href="custom-intro.shtml">Understanding customization</a>.
    </td>
  </tr>
</table>

You can also use the `X-Watson-Learning-Opt-Out` header parameter available for all {{site.data.keyword.watson}} services to control the logging of requests to the service; see [Controlling request logging for {{site.data.keyword.watson}} services ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/doc/common/getting-started-logging.html){: new_window}.

> **Note:** If you specify an invalid query parameter or JSON field as part of the input to the `synthesize` method, the service returns a `Warnings` response header that describes and lists each invalid argument. The request succeeds despite the warnings.

## Specifying input text
{: #input}

The two versions of the `synthesize` method differ primarily in how you specify the text to be synthesized. Both versions accept a maximum of 5 KB of input text, but you specify the text for each in different ways:

-   The HTTP `GET` version of the method accepts input text specified by the `text` query parameter. You specify the input as plain text or as SSML, both of which must be URL-encoded.
-   The HTTP `POST` version of the method expects the text to be specified in the body of the request. You specify the input via the following simple JSON construct that encapsulates plain text or SSML:

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

    You must specify a value of `application/json` for the HTTP `content-type` header.

Although the `GET` and `POST` methods are equivalent and offer identical functionality, it is always more secure to pass input text to the service via the `POST` method. A `POST` request passes input in the body of the request, while a `GET` request exposes the data in the URL.

The following examples show equivalent text passed to each version of the `synthesize` method via different means. The text sent via the query parameter uses HTML URL-encoding to convert the characters into a format suitable for delivery over the Internet. The SSML markup includes various elements to control the synthesize operation; for more information, see [Specifying SSML input](#ssml).

-   As plain text with the `text` parameter of the `GET` version of the method:

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here&20is&20another&20sentence.
    &20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: screen}

-   As SSML input with the `text` parameter of the `GET` version of the method:

    ```
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3Cbreak%20time=%225s%22/
    %3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another%20sentence.%3C/s%3E%3Cs%3E
    Finally,%20this%20is%20the%20last%20sentence.%3C/s%3E%3C/p%3E%22
    ```
    {: screen}

-   As plain text with the JSON construct in the body of the `POST` version of the method:

    ```xml
    {
      "text": "This is the first sentence of the paragraph. Here is another sentence.
        Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   As SSML input with the JSON construct in the body of the `POST` version of the method:

    ```xml
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/> paragraph.</s><s>
        Here is another sentence.</s><s>Finally, this is the last sentence.</s></p>"
    }
    ```
    {: codeblock}

> **Note:** Line breaks are embedded in the examples for readability. Do not include them in actual input.

### Escaping XML control characters
{: #escape}

Because you can submit input text that includes XML-based SSML annotations, the service validates all input to ensure that any SSML is correct and well formed. Therefore, you must escape any XML control characters that are present in the input text, regardless of whether the input includes SSML. Use the equivalent escape strings or character encodings described in the following table instead of the indicated characters.

<table style="width:80%">
  <caption>Table 2. Escaping XML control characters</caption>
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

For example, to enter the following input with the `text` parameter of the `synthesize` method:

```
"What have I learned?" he asked. "Everything!"
```
{: screen}

specify the following plain text:

```xml
"text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
```
{: codeblock}

or the following SSML input:

```xml
"text": "<s>&quot;What have I learned?&quot; he asked. &quot;<express-as type=\"GoodNews\">
Everything!</express-as>&quot;</s>"
```
{: codeblock}

For more information about how the service validates input text, see [SSML validation](/docs/services/text-to-speech/SSML.html#errors).

## Specifying an audio format
{: #format}

Both versions of the `synthesize` method take an optional query parameter named `accept` to specify the requested MIME type of the audio. (You can specify the value with the `Accept` request header instead.) The parameter accepts the following audio formats.

<table>
  <caption>Table 3. Supported audio formats</caption>
  <tr>
    <th style="text-align:left; width:25%">Audio format</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=opus</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td>
      <em>Ogg format</em> (<code>.ogg</code>), a free, open container format
      maintained by the Xiph.org Foundation; for more information, see
      <a target="_blank" href="https://www.xiph.org/ogg/">xiph.org/ogg/ ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
      You can request audio streams compressed with the following codecs:
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; color:#404040; line-height:120%;">
          <em>Opus</em>. For more information, see
          <a target="_blank" href="https://www.opus-codec.org/">opus-codec.org ![External link icon](../../icons/launch-glyph.svg "External link icon")</a> and
          <a target="_blank" href="https://en.wikipedia.org/wiki/Opus_%28audio_format%29">en.wikipedia.org/wiki/Opus_(audio_format) ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>, especially the
          <em>Containers</em> section.
        </li>
        <li style="margin:10px 0px; color:#404040; line-height:120%;">
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
      <em>Waveform Audio File Format (WAV)</em> (<code>.wav</code>),
      a standard created by Microsoft&reg; and IBM. A WAV file is a
      container that is often used for uncompressed audio bitstreams
      but can contain compressed audio, as well. Note that due to the
      streaming nature of the returned audio, the WAV file generated
      may not work in all audio players. Specifically, the attribute
      <code>numSamples</code> in the header of the file is set to
      <code>0</code> regardless of the length of the audio. For more
      information about WAV, see
      <a target="_blank" href="https://en.wikipedia.org/wiki/WAV">en.wikipedia.org/wiki/WAV ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>Free Lossless Audio Codec (FLAC)</em> (<code>.flac</code>),
      a lossless compressed audio coding format. For more information
      about FLAC, see
      <a target="_blank" href="https://en.wikipedia.org/wiki/FLAC">en.wikipedia.org/wiki/FLAC ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
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
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code><br/>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td>
      <em>Web Media (WebM)</em> (<code>.webm</code>), an open media-file
      format that provides support for audio streams compressed with the
      Opus and Vorbis audio codecs. If you omit the codec, the service
      uses <code>audio/webm;codecs=opus</code>. For more information about
      WebM, see
      <a target="_blank" href="https://www.webmproject.org/">webmproject.org ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td>
      <em>Linear 16-bit Pulse-Code Modulation (PCM)</em>, an uncompressed
      audio data format (often <code>.raw</code> or <code>.pcm</code>).
      You must specify the sampling rate with this audio format. For
      more information, see the Internet Engineering Task Force (IETF)
      <a target="_blank" href="https://tools.ietf.org/html/rfc2586">Request
        for Comment (RFC) 2586 ![External link icon](../../icons/launch-glyph.svg "External link icon")</a> and
      <a target="_blank" href="https://en.wikipedia.org/wiki/Pulse-code_modulation">en.wikipedia.org/wiki/Pulse-code_modulation ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td>
      <em>8-bit mu-law (or u-law) audio</em>, a single-channel audio
      format encoded using 8-bit u-law (or mu-law) data. You must
      specify the sampling rate with this audio format. For more
      information, see
      <a target="_blank" href="https://en.wikipedia.org/wiki/M-law_algorithm">en.wikipedia.org/wiki/M-law_algorithm ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td>
      <em>Basic audio</em>, a single-channel audio format encoded using
      8-bit u-law (or mu-law) data sampled at 8 KHz. This format
      provides a lowest-common denominator media type. For more
      information, see the IETF
      <a target="_blank" href="https://tools.ietf.org/html/rfc2046">Request
        for Comment (RFC) 2046 ![External link icon](../../icons/launch-glyph.svg "External link icon")</a> and
      <a target="_blank" href="http://www.iana.org/assignments/media-types/audio/basic">iana.org/assignments/media-types/audio/basic ![External link icon](../../icons/launch-glyph.svg "External link icon")</a>.
    </td>
  </tr>
</table>

The audio files can be played in a web browser by an audio player such as Audacity&reg; ([audacityteam.org ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.audacityteam.org/){: new_window}) or FFmpeg ([ffmpeg.org ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ffmpeg.org){: new_window}).

### Specifying a sampling rate
{: #sampling}

The service always synthesizes audio with a sampling rate of 22,050 Hz. For most audio formats, the service returns audio with this default sampling rate. For some formats, you can specify a different sampling rate by including the `rate={rate}` parameter; for `audio/l16` and `audio/mulaw`, you *must* specify a sampling rate. The service resamples the audio and returns it at the specified rate. A specified sampling rate must lie in the range of 8 KHz to 192 KHz.

The following table shows the default sampling rate of the audio that is returned for each format and indicates those formats for which the `rate` parameter can or must be specified.

<table style="width:90%">
  <caption>Table 4. Sampling rates for audio formats</caption>
  <tr>
    <th style="text-align:left">Audio format</th>
    <th style="text-align:center">Default sampling rate</th>
    <th style="text-align:center">Use of <code>rate</code> parameter</th>
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
      <code>audio/mp3</code>
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
      <code>audio/basic</code>
    </td>
    <td style="text-align:center">
      8000 Hz
    </td>
    <td style="text-align:center">
      Not allowed
    </td>
  </tr>
</table>

The most reliable way to identify the sampling rate for any audio stream that the service returns is to extract the information from the stream itself. You can determine the rate by calling the `synthesize` method with some simple text (for example, "hello world") and specifying the format and codec that you plan to use. You can then obtain the codec and sampling rate by saving the audio stream to a file and opening it in an audio player.

> **Note:** The Opus standard requires the output sampling rate to match the capabilities of the audio player as described in Section 5.1 of the Internet Engineering Task Force (IETF) [Request for Comments (RFC) 7845 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://tools.ietf.org/html/rfc6455){: new_window}. For software audio players, the table indicates the typical output sampling rate, but the actual sampling rate of the audio varies with time within the stream. As mentioned, the service synthesizes the source audio at 22,050 Hz.

## Specifying a voice
{: #voices}

Both versions of the `synthesize` method accept an optional `voice` query parameter to specify the voice for the audio. The service offers two versions of the `GET voices` method that you can use to learn more about the available voices. The first provides information about all available voices; the second provides information about a single voice, including information about a specified custom model if requested.

When you synthesize text to audio, the service bases its understanding of the language for the input text on the specified voice. For example, if you specify the voice `fr-FR_ReneeVoice`, the service assumes that the input text is written in French. If you pass text that is not written in the language of the voice (for example, English text for the French voice), the service might not produce meaningful results. Be sure to select a voice that matches the language of the input text.

### Retrieving all available voices

The first version of the `voices` method takes no arguments. It returns a JSON array named `voices` that includes a separate element for each available voice:

```javascript
{
  "voices": [
    {
      "url": ""
      "gender": "",
      "name": "",
      "language": "",
      "description": "",
      "customizable": "",
      "supported_features": {
        "custom_pronunciation": "",
        "voice_transformation": ""
      }
    },
    . . .
  ]
}
```
{: codeblock}

The fields for each voice provide the following information:

-   `url` identifies the URL for the voice.
-   `gender` identifies the voice as `male` or `female`.
-   `name` is an identifier for the voice (for example, `en-US_LisaVoice`). This is the value you specify for the `voice` parameter of the `synthesize` method.
-   `language` specifies the language and region of the voice (for example, `en-US`).
-   `description` provides a brief description of the interface.
-   `customizable` is a Boolean value that indicates whether the voice can be customized with the service's customization interface. (Same as `custom_pronunciation`; maintained for backward compatibility.)
-   `supported_features` describes the additional service features supported with the voice:
    -   `custom_pronunciation` is a Boolean value that indicates whether the voice can be customized with the service's customization interface. (Same as `customizable`.)
    -   `voice_transformation` is a Boolean value that indicates whether the voice can be transformed by using the SSML `<voice-transformation>` element.

The following table lists the voices that are available with the service.

<table style="width:90%">
  <caption>Table 5. Supported voices</caption>
  <tr>
    <th style="text-align:left">Voice</th>
    <th style="text-align:center">Language</th>
    <th style="text-align:center">Gender</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>de-DE_BirgitVoice</code></td>
    <td style="text-align:center">German</td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>de-DE_DieterVoice</code></td>
    <td style="text-align:center">German</td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">English (British dialect)</td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>en-US_AllisonVoice</code></td>
    <td style="text-align:center">English (US dialect)</td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>en-US_LisaVoice</code></td>
    <td style="text-align:center">English (US dialect)</td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>en-US_MichaelVoice</code></td>
    <td style="text-align:center">English (US dialect) (<em>Default</em>)</td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">Spanish (Castilian dialect)</td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">Spanish (Castilian dialect)</td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">Spanish (Latin American dialect)</td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">Spanish (North American dialect)</td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">French</td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>it-IT_FrancescaVoice</code></td>
    <td style="text-align:center">Italian</td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">Japanese</td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">Brazilian Portuguese</td>
    <td style="text-align:center">Female</td>
  </tr>
</table>

> **Note:** The voices `es-LA_SofiaVoice` and `es-US_SofiaVoice` are essentially the same voice. The most significant difference concerns how the two voices interpret a `$` (dollar sign): The Latin American version uses the term *pesos*, while the North American version uses the term *dolares*. Other minor differences may also exist between the two voices.

### Retrieving a specific voice

The second version of the `voices` method accepts two parameters:

<table>
  <caption>Table 6. Parameters of the <code>voices</code> method</caption>
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
      Provides the globally unique identifier (GUID) of a custom model
      defined for the voice about which information is to be returned.
      If you include a customization ID, you must call the method with
      the service credentials of the model's owner.
    </td>
  </tr>
</table>

If you omit the `customization_id` parameter, the method returns JSON output for the specified voice that is identical to the information returned for a voice by the other version of the method. If you specify a `customization_id`, the output includes an additional `customization` field:

```javascript
{
  "url": ""
  "gender": "",
  "name": "",
  "language": "",
  "description": "",
  "customizable": "",
  "supported_features": {
    "custom_pronunciation": "",
    "voice_transformation": ""
  },
  "customization": {
    "customization_id": "",
    "owner": "",
    "created": "",
    "name": "",
    "language": "",
    "description": "",
    "last_modified": ""
  }
}
```
{: codeblock}

For information about the meaning of the attributes of the `customization` field, see [Managing custom voice models](/docs/services/text-to-speech/custom-using.html#cuModels).

## Specifying SSML input
{: #ssml}

The Speech Synthesis Markup Language (SSML) is an XML-based markup language that is designed to provide annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service. SSML lets you specify the language, voice, and text to be synthesized, as well as many of other features that control the speech that is generated, such as pronunciation, pitch, and speaking rate.

The `synthesize` methods accept input annotated with a subset of SSML. You can use SSML elements and their attributes to gain greater control over the synthesis and resulting audio output. For more information about using SSML, see the following links:

-   For general information about the W3C SSML recommendation, see [W3C Speech Synthesis Markup Language (SSML) Version 1.0 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.w3.org/TR/speech-synthesis/){: new_window}.
-   For detailed information about SSML support for the {{site.data.keyword.texttospeechshort}} service, see [Using SSML](/docs/services/text-to-speech/SSML.html). The documentation introduces the inventory of SSML elements and attributes supported by the service.
-   For information about the service's expressive SSML extension, see [Using expressive SSML](#expressive).
-   For information about the service's voice transformation SSML extension, see [Using voice transformation SSML](#transformation).

### Using expressive SSML
{: #expressive}

By default, the {{site.data.keyword.texttospeechshort}} service synthesizes text in a neutral declarative style. The service extends SSML with an `<express-as>` element that lets you indicate expressiveness by converting text to synthesized speech in a variety of speaking styles. The element is analogous to the SSML element `<say-as>`, which specifies text normalization for formatted text such as dates, times, and numbers.

You can apply the `<express-as>` tag to the entire body of the text, a sentence, or a fragment such as a phrase or word. Currently, the service supports expressiveness only for the US English Allison voice (`en-US_AllisonVoice`); using the tag with any other voice returns an error.

#### The express-as tag

The `<express-as>` element accepts one required attribute, `type`, which describes the type of expression to use for the specified text. The attribute accepts one of three values, as shown in the following examples:

-   `GoodNews` expresses a positive, upbeat message.

    ```xml
    <express-as type="GoodNews">
      I am pleased to inform you that your mortgage loan application was approved.
    </express-as>

    <express-as type="GoodNews">
      I have good news: I was able to reduce the payments on your monthly bill!
    </express-as>

    <express-as type="GoodNews">
      Congratulations on your engagement! You two are perfect for each other!
    </express-as>

    <express-as type="GoodNews">
      Wow, good job on your promotion! That&apos;s a really prestigious position!
    </express-as>
    ```
    {: codeblock}

-   `Apology` expresses a message of regret.

    ```xml
    <express-as type="Apology">
      Unfortunately, the next flight doesn&apos;t leave for another five hours.
    </express-as>

    <express-as type="Apology">
      I am terribly sorry for the quality of service you have received.
    </express-as>

    <express-as type="Apology">
      Please forgive me for deleting your files. It was an accident.
    </express-as>

    <express-as type="Apology">
      Is there any way I can make this up to you?
    </express-as>
    ```
    {: codeblock}

-   `Uncertainty` conveys an uncertain, interrogative message.

    ```xml
    <express-as type="Uncertainty">
      Could she still be in the office? She told me that she might leave early.
    </express-as>

    <express-as type="Uncertainty">
      Sorry, I think I misheard. Was that Friday or Saturday?
    </express-as>

    <express-as type="Uncertainty">
      Can you please explain it again? Im not sure I understand.
    </express-as>

    <express-as type="Uncertainty">
      I&apos;m sorry, but I didn&apos;t catch your name. Could you please repeat it?
    </express-as>
    ```
    {: codeblock}

#### Expressive examples

The following example shows the use of all three forms of expressiveness in the body of the `text` attribute of the `synthesize` method. The text to be synthesized resides within the span of the SSML root element `<speak>`.

```xml
{
  "text": "<speak>
    I have been assigned to handle your order status request.
    <express-as type=\"Apology\">
      I am sorry to inform you that the items you requested are backordered.
      We apologize for the inconvenience.
    </express-as>
    <express-as type=\"Uncertainty\">
      We don&apos;t know when the items will become available. Maybe next week,
      but we are not sure at this time.
    </express-as>
    <express-as type=\"GoodNews\">
      But because we want you to be a satisified customer, we are giving you
      a 50% discount on your order!
    </express-as>
  </speak>"
}
```
{: codeblock}

### Using voice transformation SSML
{: #transformation}

The {{site.data.keyword.texttospeechshort}} service, like most speech synthesis systems, can speak in only a limited number of voices. Moreover, some languages offer only one or two voices. To expand the range of possible voices, the service extends SSML with a `<voice-transformation>` element that lets you realize different virtual voices by controlling aspects of a default voice. Applications of the feature include

-   Giving another flavor to a voice. You want a voice to sound a bit different in general or for a specific application.
-   Voice branding. You want to use a unique voice to differentiate your applications.
-   Multi-role applications. You need multiple voices to represent different personae.

You can apply the `<voice-transformation>` element to the entire body of the text, a sentence, or a word or fragment. The element accepts one required attribute, `type`, which describes the type of voice transformation to be applied to the specified text. You can apply a built-in transformation or create a custom transformation based on different aspects of the voice.

The service currently supports voice transformation for the following US English voices only:

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

Using the tag with any other voice returns an error.

#### Built-in transformations

Built-in transformations apply pre-configured changes to the attributes of a voice. Think of them as virtual voices that are made available by the service. The service offers two built-in transformations. To use them, you specify the case-sensitive name of the built-in transformation with the `type` attribute:

-   `Young` gives the voice a more youthful sound.
-   `Soft` makes the voice sound softer.

You can apply the optional `strength` attribute to either built-in voice to control the extent to which the service applies the transformation. Think of the value as a blending factor that the service applies to the original voice. The attribute accepts a value in the range of 0% (the voice remains unaltered) to 100% (the full extent of transformation); if you omit the attribute, the default strength is `100%`.

> **Note:** The service ignores attributes for custom transformations when you use a built-in transformation.

#### Built-in transformation examples

The following examples apply the two built-in transformations to the same sentence with different strengths:

```xml
<voice-transformation type="Young" strength="80%">
  Could you provide us with new information?
</voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Could you provide us with new information?
</voice-transformation>
```
{: codeblock}

#### Custom transformations

Custom transformations give you more fine-grained control over different aspects of the voice transformation. To use a custom transformation, you specify `Custom` for the `type` attribute. You can then use one or more of the following optional attributes to control the transformation.

<table>
  <caption>Table 7. Custom transformation attributes</caption>
  <tr>
    <th style="width:15%; text-align:left">Attribute</th>
    <th style="width:25%; text-align:center">Range</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Normalized relative change of the average pitch contour
      level within safe limits. The attribute controls the perceived
      average tone level. It is borrowed from the <code>pitch</code>
      attribute of the SSML <code>&lt;prosody&gt;</code> tag. It
      contributes to changing perceived speaker identity.
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-narrow</code>, <code>narrow</code>, <code>default</code>,
      <code>wide</code>, <code>x-wide</code>]</td>
    <td>
      Normalized relative change of the pitch contour dynamic range
      within safe limits. Increasing or decreasing the pitch range
      makes the speech style more or less expressive. The attribute
      is borrowed from the <code>range</code> attribute of the SSML
      <code>&lt;prosody&gt;</code> tag.</td>
  </tr>
  <tr>
    <td><code>glottal_tension</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Normalized relative change of the glottal tension within safe
      limits. Increasing or decreasing the glottal tension is perceived
      as a more tense or lax speech quality. A positive value might
      produce buzzing sounds, which you can alleviate by increasing
      the value of the <code>breathiness</code> attribute. A negative
      value is perceived as more breathy and generally more pleasant.
    </td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Normalized relative change of the perceived level of the aspiration
      noise within safe limits. Extreme values might produce either noisy
      speech (for positive breathiness) or a buzzing sound (for negative
      breathiness). Use this attribute to compensate for buzz or extra
      noise produced as side effects of other attributes.
    </td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-slow</code>, <code>slow</code>, <code>default</code>,
      <code>fast</code>, <code>x-fast</code>]</td>
    <td>
      Normalized relative change of the speech rate within safe limits.
      Increasing or decreasing the rate makes speech faster or slower.
      A positive (faster) rate makes the perceived pitch range wider,
      and a negative (slower) rate perceptually narrows the pitch range.
      The attribute is borrowed from the <code>rate</code> attribute of
      the SSML <code>&lt;prosody&gt;</code> tag.</td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>,
      <code>Breeze</code>]</td>
    <td>
      The case-sensitive name of one of the built-in vocal-tract
      transformations: <code>Sunrise</code> or <code>Breeze</code>.
      The names are symbolic; experiment with the timbres to learn
      how they impact voice transformation. The attribute contributes
      to changing perceived speaker identity.
    </td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0%, 100%]</td>
    <td>
      The extent of the <code>timbre</code> vocal-tract transformation:
      <code>0%</code> cancels the transformation; <code>100%</code>
      represents full application of the transformation. The attribute
      quantifies the difference between the transformed and original
      voices, enabling blending of the selected timbre with that of
      the original voice. Even at moderate timbre extent values, the
      <code>timbre</code> attribute contributes to changing perceived
      speaker identity.
    </td>
  </tr>
</table>

The numeric ranges of the different attributes indicate the extent to which the attribute affects the voice. The `rate` attribute, for instance, has a range of -100% to 100%. A value of `100%` does not mean that the voice becomes 100% faster; rather, it means that the service increases the rate of the voice to the maximum that it allows for that voice. Similarly, a value of `-100%` means that the service uses the minimum rate that it allows for the voice. A value of `0%` represents the inherent level of the attribute for the voice; the voice remains unchanged.

As a convenience, many of the attributes also define literal values that you can use instead of percentages. The meanings of these values differ from those used with the SSML `<prosody>` tag; the `<voice-transformation>` tag uses a scale that is consistent across its attributes.

-   `x-low`, `x-slow`, and `x-narrow` equal a value of `-100%`.
-   `low`, `slow`, and `narrow` equal a value of `-50%`.
-   `default` equals a value of `0%`, the default value for that attribute and voice.
-   `high`, `fast`, and `wide` equal a value of `+50%`.
-   `x-high`, `x-fast`, and `x-wide` equal a value of `+100%`.

To effect voice branding or multi-role applications, use the timbre, pitch, and glottal tension attributes to change perceived speaker identity. You can use combinations of these three attributes to create virtual voices. Consider a virtual voice as a point in the multi-dimensional space realized by the two timbres, pitch, and glottal tension, with different combinations yielding different virtual voices. You can use the pitch range, breathiness, and rate attributes to add flavor to a virtual voice. (Note that other users can choose the same or very similar attribute values, so the service cannot guarantee the uniqueness of your virtual voice.)

You need to be aware of the following potential side effects of applying the attributes:

-   High glottal tension, high pitch, and low rate can each cause buzzing sounds to occur. Increase the breathiness to mitigate the effect.
-   Extremely low glottal tension can produce noisy speech. Decrease the breathiness to reduce the noise.
-   Raising or lowering pitch range and rate to extreme degrees simultaneously can make speech sound unnatural.

> **Note:** As noted, some of the attributes are borrowed from the SSML `<prosody>` element. To enable fine prosody control of a virtual voice, you can nest inner `<prosody>` tags within `<voice-transformation>` tags and vice versa; for more information about the `<prosody>` element, see [Using SSML](/docs/services/text-to-speech/SSML.html). Note that you *cannot* nest `<voice-transformation>` tags.

#### Custom transformation examples

The following examples apply different attributes to demonstrate possible applications of custom transformation. The first example lowers the glottal tension to make the voice softer and increases the pitch range and rate moderately to introduce a more dynamic speaking style.

```xml
<voice-transformation type="Custom" glottal_tension="-50%" pitch_range="30%" rate="10%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

The second example uses maximum glottal tension and pitch and minimum rate. Such combinations are generally not favorable and can produce a buzzing sound. The example mitigates this effect by increasing breathiness.

```xml
<voice-transformation type="Custom" glottal_tension="100%" pitch="100%" rate="-100%" breathiness="60%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

The next two examples change perceived speaker identity by applying timbre. The voice is altered by controlling the extent of the blending and by changing the pitch level. The first example uses the default timbre extent, 100%.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="40%">
  Do you have more information?
</voice-transformation>

<voice-transformation type="Custom" timbre="Breeze" timbre_extent="30%" pitch="-30%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

The final example uses multiple attributes to transform the voice. The example uses the default timbre extent, and it omits breathiness.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="-30%" pitch_range="80%" rate="60%" glottal_tension="-80%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}
