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

# 音訊格式
{: #audioFormats}

{{site.data.keyword.texttospeechfull}} 服務可用若干種格式傳回合成音訊。對於大部分格式，服務會傳回預設取樣率為 22,050 Hz 的音訊。對於部分格式，您可以或必須指定音訊的取樣率。服務一律針對所有格式傳回單一頻道音訊。
{: shortdesc}

## 支援的音訊格式
{: #formatsSupported}

表 1 列出您可以在其中要求合成音訊的音訊格式（MIME 類型）。依預設，服務會以 Ogg 格式傳回音訊，並搭配使用 Opus 轉碼器 (`audio/ogg;codecs=opus`)。

<table>
  <caption>表 1. 支援的音訊格式</caption>
  <tr>
    <th style="text-align:left; width:25%">音訊格式</th>
    <th style="text-align:left">說明</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td>
      <em>基本音訊</em> 是一種單一頻道的有損音訊格式，它是使用取樣率為 8 kHz 的 8 位元 u-law（或 mu-law）資料進行編碼的。
      此格式提供最低共同分母媒體類型。如需相關資訊，請參閱 IETF
      [Request for Comment (RFC) 2046](https://tools.ietf.org/html/rfc2046) 和
      [iana.org/assignments/media-types/audio/basic](http://www.iana.org/assignments/media-types/audio/basic)。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>自由無損音訊轉碼器 (FLAC)</em> (<code>.flac</code>)，這是一種無損壓縮音訊編碼格式。如需相關資訊，請參閱
      [FLAC](https://wikipedia.org/wiki/FLAC)。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td>
      <em>線性 16 位元脈衝編碼調變 (PCM)</em>，這是一種未經壓縮的音訊資料格式（通常指的是 <code>.raw</code> 或 <code>.pcm</code>）。如需相關資訊，請參閱網際網路工程工作小組 (IETF) 的
      [Request for Comment (RFC) 2586](https://tools.ietf.org/html/rfc2586) 和
      [Pulse-code modulation](https://wikipedia.org/wiki/Pulse-code_modulation)。<br/><br/>
      您必須使用此音訊格式來指定取樣率。例如，對於取樣率為 16 kHz 的音訊指定 <code>audio/l16;rate=16000</code>。您也可以選擇性地將排列法指定為 <code>audio/l16;rate={rate};endianness=big-endian</code> 或 <code>audio/l16;rate={rate};endianness=little-endian</code>。
      預設值為小序排列法。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td>
      <em>MP3</em> 或 <em>Motion Picture Experts Group (MPEG)</em>，這是一種有損資料壓縮格式（MP3 及 MPEG 指的是相同的格式）。如需相關資訊，請參閱
      [MP3](https://wikipedia.org/wiki/MP3)。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td>
      <em>8 位元 mu-law（或 u-law）音訊</em> 是一種單一頻道的有損音訊格式，它是使用 8 位元 u-law（或 mu-law）資料進行編碼的。您必須使用此音訊格式來指定取樣率。如需相關資訊，請參閱 [M-law algorithm](https://wikipedia.org/wiki/M-law_algorithm)。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=opus</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td>
      <em>Ogg 格式</em> (<code>.ogg</code>) 是一種自由且開放的容器格式，由 Xiph.org Foundation 維護。如需相關資訊，請參閱 [xiph.org/ogg/](https://www.xiph.org/ogg/)。您可以要求使用下列轉碼器壓縮的音訊串流：
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <em>Opus</em>。如需相關資訊，請參閱
	  [opus-codec.org](https://www.opus-codec.org/) 和
	  [Opus (audio format)](https://wikipedia.org/wiki/Opus_%28audio_format%29)。請特別查看 <em>Containers</em> 部分。
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <em>Vorbis</em>。如需相關資訊，請參閱
	  [xiph.org/vorbis](https://xiph.org/vorbis/) 和
	  [Vorbis](https://wikipedia.org/wiki/Vorbis)。
        </li>
      </ul>
      這兩個轉碼器都是自由且開放的有損音訊壓縮格式。Opus 是偏好的轉碼器，但根據 Ogg 規格，如果您省略轉碼器，則服務會以 Vorbis 格式傳回音訊。如果您完全省略音訊格式，則依預設服務會以 Ogg 格式傳回音訊，並搭配使用 Opus 轉碼器。</td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td>
      <em>Waveform Audio File Format (WAV)</em> (<code>.wav</code>) 是一種標準容器格式，通常用於未經壓縮的音訊位元串流，但也可以包含壓縮音訊。由於所傳回音訊的串流本質，產生的 WAV 檔可能無法在所有音訊播放程式中運作。尤其，無論音訊的長度為何，檔案標頭中的 <code>numSamples</code> 屬性都會設為 <code>0</code>。如需相關資訊，請參閱
      [WAV](https://wikipedia.org/wiki/WAV)。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code><br/>
    <code>audio/webm;codecs=vorbis</code>
    </td>
    <td>
      <em>Web 媒體 (WebM)</em> (<code>.webm</code>) 是一種開放式媒體檔案格式，支援使用 Osp 及 Vorbis 音訊轉碼器來壓縮的音訊串流。如果您省略轉碼器，服務會以 Opus 格式傳回音訊。如需相關資訊，請參閱
      [webmproject.org](https://www.webmproject.org/)。
    </td>
  </tr>
</table>

## 指定音訊格式
{: #formatSpecify}

指定音訊格式是選用的。依預設，服務會以 `audio/ogg;codecs=opus` 格式傳回音訊。但是，您可以指定 HTTP 或 WebSocket 介面的格式：

-   利用 HTTP `GET` 及 `POST /v1/synthesize` 方法，您可以使用 `Accept` 要求標頭或 `accept` 查詢參數來指定格式。若要以預設格式接收音訊，請同時省略標頭和查詢參數。如需相關資訊，請參閱[將文字合成為音訊](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#synthesize)。

    如果您使用 `accept` 查詢參數，請將引數以 URL 編碼為參數。例如，會將下列引數：

    ```
    audio/l16;rate=16000;endianness=little-endian
    ```
    {: codeblock}

    以 URL 編碼為：

    ```
    audio%2Fl16%3Brate%3D16000%3Bendianness%3Dlittle-endian
    ```
    {: codeblock}

-   利用 WebSocket 介面，您可以使用為了起始合成而傳遞之文字訊息的 `accept` 參數來指定格式。若要以預設格式接收音訊，請為參數指定 `*/*` 值。如需相關資訊，請參閱[傳送輸入文字](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket#WSsend)。

## 指定取樣率
{: #formatRate}

服務一律使用取樣率 22,050 Hz 來合成音訊。對於大部分格式，服務會以此預設取樣率傳回音訊。對於部分格式，您可以包括 `rate={rate}` 參數，以指定不同的取樣率。對於 `audio/l16` 和 `audio/mulate` 格式，您*必須* 指定取樣率。

當您指定取樣率時，服務會將音訊重新取樣，並以指定的取樣率將其傳回。指定的取樣率必須在 8 kHz 到 192 kHz 範圍內。

表 2 顯示針對每種格式傳回之音訊的預設取樣率，並指出您可以或必須指定取樣率的那些格式。

<table style="width:90%">
  <caption>表 2. 音訊格式的取樣率</caption>
  <tr>
    <th style="text-align:left">音訊格式</th>
    <th style="text-align:center">預設取樣率</th>
    <th style="text-align:center">使用 <code>rate</code> 參數</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td style="text-align:center">
      8000 Hz
    </td>
    <td style="text-align:center">
      不容許
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
      選用
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td style="text-align:center">
      無
    </td>
    <td style="text-align:center">
      必要；例如<br />
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
      選用
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td style="text-align:center">
      無
    </td>
    <td style="text-align:center">
      必要；例如<br />
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
      選用
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg;codecs=opus</code>
    </td>
    <td style="text-align:center">
      22,050 Hz [請參閱<strong>附註</strong>]
    </td>
    <td style="text-align:center">
      選用
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
      選用
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code>
    </td>
    <td style="text-align:center">
      48,000 Hz [請參閱<strong>附註</strong>]
    </td>
    <td style="text-align:center">
      不容許
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
      選用
    </td>
  </tr>
</table>

識別服務傳回之任何音訊串流取樣率的最可靠方法是從串流本身擷取資訊。您可以藉由使用一些簡單文字（例如，"hello world"）呼叫 `/v1/synthesize` 方法，並指定您計劃使用的格式和轉碼器，來判定取樣率。然後，您可以將音訊串流儲存至檔案並在音訊播放程式中開啟，以取得轉碼器及取樣率。

Opus 標準需要輸出取樣率符合音訊播放程式的功能。如需相關資訊，請參閱網際網路工程工作小組 (IETF) 的 [Request for Comments (RFC) 7845](http://tools.ietf.org/html/rfc6455){: external} 的第 5.1 節。對於軟體音訊播放程式，此表格指出一般輸出取樣率，但實際的音訊取樣率隨串流內的時間而有所不同。如前所述，服務會合成 22,050 Hz 的來源音訊。
{: note}

## 播放音訊檔
{: #formatsPlay}

若要播放服務產生的音訊檔，請使用下列其中一種工具：

-   Web 瀏覽器，例如 Google Chrome&trade;、Firefox&reg; 或 Microsoft&reg; Internet Explorer&reg;。
-   音訊播放程式，例如 Audacity&reg; ([audacityteam.org](http://www.audacityteam.org/){: external}) 或 FFmpeg ([ffmpeg.org](https://www.ffmpeg.org){: external})。
