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

# 音声フォーマット
{: #audioFormats}

{{site.data.keyword.texttospeechfull}} サービスは、合成音声をいくつかのフォーマットで返すことができます。ほとんどのフォーマットでは、デフォルトのサンプリング・レート 22,050 Hz の音声が返されます。一部のフォーマットでは、音声のサンプリング・レートを指定できます (あるいは指定する必要があります)。どのフォーマットでも、サービスから返される音声は、常に単一チャネル音声です。
{: shortdesc}

## サポートされる音声フォーマット
{: #formatsSupported}

表 1 に、要求できる合成音声の音声フォーマット (MIME タイプ) をリストします。デフォルトでは、サービスは Opus コーデック (`audio/ogg;codecs=opus`) を使用した Ogg フォーマットの音声を返します。

<table>
  <caption>表 1. サポートされる音声フォーマット</caption>
  <tr>
    <th style="text-align:left; width:25%">音声フォーマット</th>
    <th style="text-align:left">説明</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td>
      <em>基本音声</em>。サンプリング・レート 8 kHz で 8 ビットの u-law (または mu-law) データを使用してエンコードされた単一チャネルの非可逆音声フォーマット。
      このフォーマットが最低限の水準のメディア・タイプになります。詳しくは、
      IETF の <a target="_blank" href="https://tools.ietf.org/html/rfc2046">Request for Comment (RFC) 2046 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> および
      <a target="_blank" href="http://www.iana.org/assignments/media-types/audio/basic">iana.org/assignments/media-types/audio/basic ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> を参照してください。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>FLAC (Free Lossless Audio Codec)</em> (<code>.flac</code>)。無損失圧縮音声コーディング・フォーマット。 詳しくは、
      <a target="_blank" href="https://en.wikipedia.org/wiki/FLAC">en.wikipedia.org/wiki/FLAC ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> を参照してください。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td>
      <em>16 ビットのリニア PCM (Pulse-Code Modulation)</em>。非圧縮音声データ・フォーマット (多くの場合は <code>.raw</code> または <code>.pcm</code>)。 詳しくは、
      Internet Engineering Task Force (IETF) の <a target="_blank" href="https://tools.ietf.org/html/rfc2586">Request for Comment (RFC) 2586 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> および
      <a target="_blank" href="https://en.wikipedia.org/wiki/Pulse-code_modulation">en.wikipedia.org/wiki/Pulse-code_modulation ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> を参照してください。<br/><br/>
      この音声フォーマットでは、サンプリング・レートを指定する必要があります。例えば、16 kHz で音声をサンプリングする場合は <code>audio/l16;rate=16000</code> を指定します。
      オプションで、
      <code>audio/l16;rate={rate};endianness=big-endian</code> または <code>audio/l16;rate={rate};endianness=little-endian</code> としてエンディアンネスを指定することもできます。
      デフォルトはリトル・エンディアンです。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td>
      <em>MP3</em> または <em>Motion Picture Experts Group (MPEG)</em>。
      非可逆データ圧縮フォーマット (MP3 と MPEG は同じフォーマットを意味します)。
      詳しくは、
      <a target="_blank" href="https://en.wikipedia.org/wiki/MP3">en.wikipedia.org/wiki/MP3 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> を参照してください。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td>
      <em>8 ビットの mu-law (または u-law) 音声</em>。8 ビット u-law (または mu-law) データを使用してエンコードされた単一チャネルの非可逆音声フォーマット。
      この音声フォーマットでは、サンプリング・レートを指定する必要があります。詳しくは、
      <a target="_blank" href="https://en.wikipedia.org/wiki/M-law_algorithm">en.wikipedia.org/wiki/M-law_algorithm ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> を参照してください。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=opus</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td>
      <em>Ogg フォーマット</em> (<code>.ogg</code>)。無料で公開されているコンテナー・フォーマット (Xiph.org Foundation が管理しています)。
      詳しくは、
      <a target="_blank" href="https://www.xiph.org/ogg/">xiph.org/ogg/ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> を参照してください。
      以下のコーデックを使用して圧縮されたオーディオ・ストリームを要求できます。
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <em>Opus</em>。詳しくは、
          <a target="_blank" href="https://www.opus-codec.org/">opus-codec.org ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> および
          <a target="_blank" href="https://en.wikipedia.org/wiki/Opus">en.wikipedia.org/wiki/Opus (音声フォーマット) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> を参照してください。
          <em>Opus (音声フォーマット)</em> ページでは、
          特に<em>コンテナー</em> のセクションを参照してください。
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <em>Vorbis</em>。詳しくは、
          <a target="_blank" href="https://xiph.org/vorbis/">xiph.org/vorbis ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> および
          <a target="_blank" href="https://en.wikipedia.org/wiki/Vorbis">en.wikipedia.org/wiki/Vorbis ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> を参照してください。
        </li>
      </ul>
      どちらのコーデックも無料で公開されている非可逆音声圧縮フォーマットです。Opus が推奨コーデックですが、
      コーデックを省略した場合は、Ogg の仕様に従い、Vorbis フォーマットの音声が返されます。
      音声フォーマットをすべて省略した場合、サービスは、
      Opus コーデックを使用した Ogg フォーマットの音声をデフォルトで返します。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td>
      <em>Waveform Audio ファイル・フォーマット (WAV)</em> (<code>.wav</code>) は、
      非圧縮音声ビット・ストリームによく使用される標準的なコンテナー・フォーマットですが、
      圧縮音声も入れることができます。返される音声がストリーミングの性質を持つため、
      音声プレイヤーによっては、生成された WAV ファイルを再生できないことがあります。
      具体的には、音声の長さに関係なく、ファイルのヘッダーの属性 <code>numSamples</code> が <code>0</code> に設定されます。
      詳しくは、
      <a target="_blank" href="https://en.wikipedia.org/wiki/WAV">en.wikipedia.org/wiki/WAV ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> を参照してください。
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code><br/>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td>
      <em>Web メディア (WebM)</em> (<code>.webm</code>)。
      Opus および Vorbis の音声コーデックを使用して圧縮された音声ストリームをサポートするオープンなメディア・ファイル・フォーマット。
      コーデックを省略すると、サービスは Opus フォーマットの音声を返します。
      詳しくは、
      <a target="_blank" href="https://www.webmproject.org/">webmproject.org ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")</a> を参照してください。
    </td>
  </tr>
</table>

## 音声フォーマットの指定
{: #formatSpecify}

音声フォーマットの指定はオプションです。デフォルトでは、サービスは `audio/ogg;codecs=opus` のフォーマットの音声を返します。ただし、HTTP インターフェースでも WebSocket インターフェースでも、以下のようにフォーマットを指定できます。

-   HTTP の `GET /v1/synthesize` および `POST /v1/synthesize` メソッドでは、`Accept` 要求ヘッダーまたは `accept` 照会パラメーターを使用してフォーマットを指定します。デフォルトのフォーマットの音声を受け取るには、ヘッダーと照会パラメーターの両方を省略してください。詳しくは、[テキストからの音声の合成](/docs/services/text-to-speech/http.html#synthesize)を参照してください。

    `accept` 照会パラメーターを使用する場合は、パラメーターの引数を URL エンコードしてください。例えば、次の引数を URL エンコードすると、

    ```
    audio/l16;rate=16000;endianness=little-endian
    ```
    {: codeblock}

    次になります。

    ```
    audio%2Fl16%3Brate%3D16000%3Bendianness%3Dlittle-endian
    ```
    {: codeblock}

-   WebSocket インターフェースでは、合成を開始するために渡すテキスト・メッセージの `accept` パラメーターを使用して、フォーマットを指定します。デフォルトのフォーマットの音声を受け取るには、パラメーターに値 `*/*` を指定します。詳しくは、[入力テキストを送信する](/docs/services/text-to-speech/websockets.html#WSsend)を参照してください。

## サンプリング・レートの指定
{: #formatRate}

サービスは、常にサンプリング・レート 22,050 Hz で音声を合成します。ほとんどの音声フォーマットでは、このデフォルトのサンプリング・レートによる音声が返されます。一部のフォーマットでは、`rate={rate}` パラメーターを使用して別のサンプリング・レートを指定できます。`audio/l16` フォーマットと `audio/mulaw` フォーマットでは、サンプリング・レートの指定が*必須です*。

サンプリング・レートを指定した場合、サービスは音声のサンプリングを再実行し、指定されたレートの音声を返します。指定するサンプリング・レートは、8 kHz から 192 kHz までの範囲の値でなければなりません。

表 2 に、各フォーマットで返される音声のデフォルトのサンプリング・レートと、サンプリング・レートの指定が可能かどうか (あるいは必須かどうか)を示します。

<table style="width:90%">
  <caption>表 2. 音声フォーマットのサンプリング・レート</caption>
  <tr>
    <th style="text-align:left">音声フォーマット</th>
    <th style="text-align:center">デフォルトのサンプリング・レート</th>
    <th style="text-align:center"><code>rate</code> パラメーターの使用</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td style="text-align:center">
      8000 Hz
    </td>
    <td style="text-align:center">
      使用不可
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
      オプション
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td style="text-align:center">
      なし
    </td>
    <td style="text-align:center">
      必須。例:<br />
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
      オプション
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td style="text-align:center">
      なし
    </td>
    <td style="text-align:center">
      必須。例:<br />
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
      オプション
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg;codecs=opus</code>
    </td>
    <td style="text-align:center">
      22,050 Hz [<strong>注</strong>を参照]
    </td>
    <td style="text-align:center">
      オプション
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
      オプション
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code>
    </td>
    <td style="text-align:center">
      48,000 Hz [<strong>注</strong>を参照]
    </td>
    <td style="text-align:center">
      使用不可
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
      オプション
    </td>
  </tr>
</table>

サービスから返される音声ストリームのサンプリング・レートを調べる最も確実な方法は、ストリーム自体から情報を抽出することです。レートを調べるには、シンプルなテキスト (「hello world」など) で、使用する予定のフォーマットとコーデックを指定して `/v1/synthesize` メソッドを呼び出します。そして、音声ストリームをファイルに保存し、そのファイルをオーディオ・プレイヤーで開けば、コーデックとサンプリング・レートがわかります。

Opus 標準には、オーディオ・プレイヤーの能力に合った出力サンプリング・レートにすることが規定されています。詳しくは、Internet Engineering Task Force (IETF) の [Request for Comments (RFC) 7845 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://tools.ietf.org/html/rfc6455){: new_window} のセクション 5.1 を参照してください。ソフトウェア・オーディオ・プレイヤーの場合、この表は一般的な出力サンプリング・レートを示していますが、音声の実際のサンプリング・レートは、ストリーム内の時間によって異なります。既に説明したように、サービスはソース音声を 22,050 Hz で合成します。
{: note}

## 音声ファイルの再生
{: #formatsPlay}

サービスで生成された音声ファイルを再生するには、以下のいずれかのツールを使用します。

-   Web ブラウザー (Google Chrome&trade;、Firefox&reg;、Microsoft&reg; Internet Explorer&reg; など)。
-   オーディオ・プレイヤー (Audacity&reg; ([audacityteam.org ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.audacityteam.org/){: new_window}) や FFmpeg ([ffmpeg.org ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ffmpeg.org){: new_window}) など)。
