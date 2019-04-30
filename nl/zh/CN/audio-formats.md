---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-09"

subcollection: text-to-speech

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# 音频格式
{: #audioFormats}

{{site.data.keyword.texttospeechfull}} 服务可以返回多种格式的合成音频。对于大多数格式，服务会返回缺省采样率为 22,050 赫兹的音频。对于某些格式，可以或者必须指定音频的采样率。对于所有格式，服务始终返回单声道音频。
{: shortdesc}

## 支持的音频格式
{: #formatsSupported}

表 1 列出了可以请求合成音频的音频格式（MIME 类型）。缺省情况下，服务使用 Opus 编码解码器 (`audio/ogg;codecs=opus`) 返回 Ogg 格式的音频。

<table>
  <caption>表 1. 支持的音频格式</caption>
  <tr>
    <th style="text-align:left; width:25%">音频格式</th>
    <th style="text-align:left">描述</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td>
      <em>基本音频</em>，一种单声道有损音频格式，使用 8 位 u-law（或 mu-law）数据进行编码，采样率为 8 千赫兹。此格式提供了最大众化的媒体类型。有关更多信息，请参阅 IETF 的 <a target="_blank" href="https://tools.ietf.org/html/rfc2046">Request for Comments (RFC) 2046 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a> 和 <a target="_blank" href="http://www.iana.org/assignments/media-types/audio/basic">iana.org/assignments/media-types/audio/basic ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a>。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>自由无损音频编码解码器 (FLAC)</em> (<code>.flac</code>)，一种无损压缩音频编码格式。有关更多信息，请参阅 <a target="_blank" href="https://en.wikipedia.org/wiki/FLAC">en.wikipedia.org/wiki/FLAC ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a>。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td>
      <em>线性 16 位脉冲编码调制 (PCM)</em>，一种未压缩的音频数据格式（通常为 <code>.raw</code> 或 <code>.pcm</code>）。有关更多信息，请参阅因特网工程任务组织 (IETF) 的 <a target="_blank" href="https://tools.ietf.org/html/rfc2586">Request for Comments (RFC) 2586 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a> 和 <a target="_blank" href="https://en.wikipedia.org/wiki/Pulse-code_modulation">en.wikipedia.org/wiki/Pulse-code_modulation ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a>。<br/><br/>
      对于此音频格式，必须指定采样率。例如，指定 <code>audio/l16;rate=16000</code> 表示采样率为 16 千赫兹的音频。还可以选择将字节序指定为 <code>audio/l16;rate={rate};endianness=big-endian</code> 或 <code>audio/l16;rate={rate};endianness=little-endian</code>。
      缺省值为小尾数法。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td>
      <em>MP3</em> 或<em>运动图像专家组 (MPEG)</em>，一种有损数据压缩格式（MP3 和 MPEG 指的是同一格式）。有关更多信息，请参阅 <a target="_blank" href="https://en.wikipedia.org/wiki/MP3">en.wikipedia.org/wiki/MP3 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a>。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td>
      <em>8 位 u-law（或 mu-law）音频</em>，一种单声道有损音频格式，使用 8 位 u-law（或 mu-law）数据进行编码。对于此音频格式，必须指定采样率。有关更多信息，请参阅 <a target="_blank" href="https://en.wikipedia.org/wiki/M-law_algorithm">en.wikipedia.org/wiki/M-law_algorithm ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a>。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=opus</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td>
      <em>Ogg 格式</em> (<code>.ogg</code>)，这是由 Xiph.org Foundation 维护的免费开放式容器格式。有关更多信息，请参阅 <a target="_blank" href="https://www.xiph.org/ogg/">xiph.org/ogg/ ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a>。您可以请求使用以下编码解码器压缩的音频流：
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <em>Opus</em>。有关更多信息，请参阅 <a target="_blank" href="https://www.opus-codec.org/">opus-codec.org ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a> 和 <a target="_blank" href="https://en.wikipedia.org/wiki/Opus">en.wikipedia.org/wiki/Opus (audio format) ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a>。在 <em>Opus (audio format)</em> 页面上，请特别查看 <em>Containers</em> 部分。
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <em>Vorbis</em>。有关更多信息，请参阅 <a target="_blank" href="https://xiph.org/vorbis/">xiph.org/vorbis ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a> 和 <a target="_blank" href="https://en.wikipedia.org/wiki/Vorbis">en.wikipedia.org/wiki/Vorbis ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a>。
        </li>
      </ul>
      这两种编码解码器都是免费开放式有损音频压缩格式。Opus 是首选编码解码器，但根据 Ogg 规范，如果省略编码解码器，服务将返回 Vorbis 格式的音频。如果完全省略音频格式，那么缺省情况下，服务会返回使用 Opus 编码解码器的 Ogg 格式音频。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td>
      <em>波形音频文件格式 (WAV)</em> (<code>.wav</code>) 是一种标准容器格式，通常用于未压缩的音频位流，但也可以包含压缩音频。由于所返回音频的流式性质，生成的 WAV 文件可能无法在所有音频播放器中正常使用。具体来说，文件头中的 <code>numSamples</code> 属性会设置为 <code>0</code>，而不考虑音频的长度。有关更多信息，请参阅 <a target="_blank" href="https://en.wikipedia.org/wiki/WAV">en.wikipedia.org/wiki/WAV ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a>。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code><br/>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td>
      <em>Web 媒体 (WebM)</em> (<code>.webm</code>)，一种开放式媒体文件格式，用于支持使用 Opus 和 Vorbis 音频编码解码器压缩的音频流。如果省略编码解码器，那么服务会返回 Opus 格式的音频。有关更多信息，请参阅 <a target="_blank" href="https://www.webmproject.org/">webmproject.org ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")</a>。
    </td>
  </tr>
</table>

## 指定音频格式
{: #formatSpecify}

指定音频格式是可选的。缺省情况下，服务会返回 `audio/ogg;codecs=opus` 格式的音频。但是，您可以为 HTTP 或 WebSocket 接口指定格式：

-   采用 HTTP `GET` 和 `POST /v1/synthesize` 方法时，可使用 `Accept` 请求头或 `accept` 查询参数来指定格式。要接收缺省格式的音频，请省略该头和查询参数。有关更多信息，请参阅[将文本合成为音频](/docs/services/text-to-speech/http.html#synthesize)。

    如果使用 `accept` 查询参数，请对自变量进行 URL 编码，使其成为参数。例如，对以下自变量进行 URL 编码：

    ```
    audio/l16;rate=16000;endianness=little-endian
    ```
    {: codeblock}

    使其成为：

    ```
    audio%2Fl16%3Brate%3D16000%3Bendianness%3Dlittle-endian
    ```
    {: codeblock}

-   通过 WebSocket 接口，可以使用传递的文本消息中的 `accept` 参数来指定格式以启动合成。要接收缺省格式的音频，请将该参数的值指定为 `*/*`。有关更多信息，请参阅[发送输入文本](/docs/services/text-to-speech/websockets.html#WSsend)。

## 指定采样率
{: #formatRate}

服务始终会合成采样率为 22,050 赫兹的音频。对于大多数音频格式，服务会返回具有此缺省采样率的音频。对于某些格式，可以通过包含 `rate={rate}` 参数来指定其他采样率。对于 `audio/l16` 和 `audio/mulaw` 格式，*必须*指定采样率。

指定采样率时，服务会对音频重新采样，并返回指定采样率的音频。指定的采样率必须在 8 千赫兹到 192 千赫兹范围内。

表 2 显示了针对每种格式返回的音频缺省采样率，并指示可以或必须对哪些格式指定采样率。

<table style="width:90%">
  <caption>表 2. 音频格式的采样率</caption>
  <tr>
    <th style="text-align:left">音频格式</th>
    <th style="text-align:center">缺省采样率</th>
    <th style="text-align:center">使用 <code>rate</code> 参数</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td style="text-align:center">
      8000 赫兹
    </td>
    <td style="text-align:center">
      不允许
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td style="text-align:center">
      22,050 赫兹
    </td>
    <td style="text-align:center">
      可选
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td style="text-align:center">
      无
    </td>
    <td style="text-align:center">
      必需；例如：<br />
      <code>audio/l16;rate=22050</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td style="text-align:center">
      22,050 赫兹
    </td>
    <td style="text-align:center">
      可选
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td style="text-align:center">
      无
    </td>
    <td style="text-align:center">
      必需；例如：<br />
      <code>audio/mulaw;rate=8000</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td style="text-align:center">
      22,050 赫兹
    </td>
    <td style="text-align:center">
      可选
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg;codecs=opus</code>
    </td>
    <td style="text-align:center">
      22,050 赫兹 [请参阅<strong>注</strong>]
    </td>
    <td style="text-align:center">
      可选
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td style="text-align:center">
      22,050 赫兹
    </td>
    <td style="text-align:center">
      可选
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code>
    </td>
    <td style="text-align:center">
      48,000 赫兹 [请参阅<strong>注</strong>]
    </td>
    <td style="text-align:center">
      不允许
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td style="text-align:center">
      22,050 赫兹
    </td>
    <td style="text-align:center">
      可选
    </td>
  </tr>
</table>

要确定服务返回的任何音频流的采样率，最可靠方法是从流本身中抽取信息。可以通过调用带有一些简单文本（例如，“hello world”）的 `/v1/synthesize` 方法，并指定计划使用的格式和编码解码器来确定采样率。然后，可以通过将音频流保存到文件并在音频播放器中打开，获取编码解码器和采样率。

Opus 标准需要输出采样率与音频播放器能力相匹配。有关更多信息，请参阅因特网工程任务组织 (IETF) 的 [Request for Comments (RFC) 7845 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://tools.ietf.org/html/rfc6455){: new_window} 的第 5.1 部分。对于软件音频播放器，该表指示的是典型输出采样率，但音频的实际采样率在流中随时间而变化。如上所述，服务会合成 22,050 赫兹的源音频。
{: note}

## 播放音频文件
{: #formatsPlay}

要播放服务生成的音频文件，请使用下列其中一个工具：

-   Web 浏览器，例如 Google Chrome&trade;、Firefox&reg; 或 Microsoft&reg; Internet Explorer&reg;。
-   音频播放器，例如 Audacity&reg; ([audacityteam.org ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.audacityteam.org/){: new_window}) 或 FFmpeg ([ffmpeg.org ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ffmpeg.org){: new_window})。
