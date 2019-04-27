---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28"

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

# 言語と音声
{: #voices}

{{site.data.keyword.texttospeechfull}} サービスは、さまざまな言語、音声、方言をサポートしています。どの言語についても、男性または女性の声のどちらか一方、または両方が用意されています。音声ごとに、方言に応じた抑揚とイントネーションが使用されます。
{: shortdesc}

## サポートされる言語と音声
{: #languageVoices}

表 1 に、言語と方言ごとに用意されている音声とその性別をまとめます。要求のオプションの `voice` パラメーターの指定を省略した場合、サービスはデフォルトの `en-US_MichaelVoice` 音声を使用します。一部の音声に 2 つのバージョンが存在する理由については、[音声合成テクノロジー](#technologiesVoices)を参照してください。

現在、`V2` 音声のデプロイメントに問題があるために、合成音声にバックグラウンド・ノイズが含まれます。詳しくは、[既知の制限](/docs/services/text-to-speech/release-notes.html#limitations)を参照してください。
{: note}

<table style="width:90%">
  <caption>表 1. サポートされる言語と音声</caption>
  <tr>
    <th style="text-align:left">言語</th>
    <th style="text-align:center">音声</th>
    <th style="text-align:center">性別</th>
  </tr>
  <tr>
    <td style="text-align:left">ブラジル・ポルトガル語</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">カスティリャ・スペイン語</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">フランス語</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">ドイツ語</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code><br/>
      <code>de-DE_BirgitV2Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code><br/>
      <code>de-DE_DieterV2Voice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
  <tr>
    <td style="text-align:left">イタリア語</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code><br/>
      <code>it-IT_FrancescaV2Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">日本語</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">中南米スペイン語</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">北米スペイン語</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">英国英語</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">米国英語</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code><br/>
      <code>en-US_AllisonV2Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaVoice</code><br/>
      <code>en-US_LisaV2Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code><br/>
      <code>en-US_MichaelV2Voice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
</table>

`es-LA_SofiaVoice` 音声と `es-US_SofiaVoice` 音声は本質的には同じ音声です。この 2 つの音声の最も大きな違いは、$ (ドル記号) の解釈方法です。中南米バージョンでは*ペソ* という語を使用するのに対し、北米バージョンでは*ドル* という語を使用します。他にもこの 2 つの音声には小さな違いが存在します。
{: note}

### 音声合成テクノロジー
{: #technologiesVoices}

一部の音声については 2 つのバージョンが用意されています。例えば、`en-US_AllisonVoice` と `en-US_AllisonV2Voice` です。この 2 つのバージョンの主な違いは、音声合成のためにサービスが使用するテクノロジーにあります。

-   *連結的合成* は、録音音声のセグメント (または単位) を組み立てることで、要求された音声を生成します。明瞭な印象を与える音声が生成されますが、録音セグメントの連結点で音声のひずみが生じることがあります。

    名前に `V2` という文字を含まない音声 (例: `en-US_AllisonVoice`) は、連結的合成によるものです。
-   *ディープ・ラーニング合成* は、ディープ・ニューラル・ネットワーク (DNN) を使用して、指定されたテキストの音声を合成します。このアプローチは、録音音声のセグメントをつなぎ合わせるのではなく、機械学習を使用して、録音音声データによるトレーニングを DNN に行います。ディープ・ラーニング合成、すなわち DNN ベースの合成では、より自然な韻律で全体的に一貫した品質の音声が生成されます。

    名前に `V2` という文字を含む音声 (例: `en-US_AllisonV2Voice`) は、DNN ベース合成による新しい音声です。

新しい音声は、アプリケーションに採用する前に試験する必要があります。この 2 つのテクノロジーで生成される音声の信号品質は異なるため、どのアプリケーションにも新しい音声のほうが適しているというわけではありません。また、DNN ベース音声は、以下の SSML 要素または属性をサポートしていません。

-   `<prosody>` 要素の `volume` 属性
-   `<express-as>` 要素
-   `<voice-transformation>` 要素

アプリケーションでこれらの要素を使用している場合は、連結的合成による音声の使用を継続してください。

### 音声のカスタマイズ
{: #customizeVoice}

テキストから音声合成を行うときには、サービスは言語依存の発音ルールを適用して、各単語の通常のつづりを表音つづりに変換します。サービスの発音ルールは一般的な単語には十分に機能しますが、外来語、人名、略語、頭文字などの一般的でない単語には十分に機能しないことがあります。

アプリケーションの語彙にそのような単語が含まれている場合は、カスタマイズ・インターフェースを使用して、サービスにどのように単語を発音させるかを指定できます。詳しくは、[カスタマイズの理解](/docs/services/text-to-speech/custom-intro.html)を参照してください。

## 音声の指定
{: #specifyVoice}

HTTP の `GET /v1/synthesize` および `POST /v1/synthesize` メソッドの両方、ならびに WebSocket の `/v1/synthesize` メソッドは、合成音声を指定するオプションの `voice` 照会パラメーターを取ります。詳しくは、[HTTP インターフェース](/docs/services/text-to-speech/http.html)および [WebSocket インターフェース](/docs/services/text-to-speech/websockets.html)を参照してください。

サービスは、指定された音声に基づいて、入力テキストの言語を認識します。必ず、入力テキストの言語に一致する音声を指定するようにしてください。 例えば、フランス語音声 (`fr-FR_ReneeVoice`) を指定した場合、サービスは、入力テキストがフランス語で記述されているものと想定します。
音声の言語で記述されていないテキスト (例えば、フランス語音声用に英語テキスト) を渡した場合、サービスで意味のある結果が生成されないことがあります。

## 使用可能なすべての音声のリスト表示
{: #listVoices}

`GET /v1/voices` メソッドは、使用可能なすべての音声に関する情報をリスト表示します。このメソッドは引数は取らず、`voices` という JSON 配列を戻します。この配列には、音声ごとに別のオブジェクトが含まれています。

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

音声オブジェクトのフィールドには、以下の情報が示されています。

-   `name`。音声の識別子 (例えば、`en-US_LisaVoice`)。 `/v1/synthesize` メソッドの `voice` パラメーターには、この値を指定します。
-   `language`。音声の言語と地域を示します (例えば、`en-US`)。
-   `gender`。音声を `male` または `female` として識別します。
-   `url`。音声の URL を識別します。
-   `description`。音声の要旨を示します。
-   `customizable`。サービスのカスタマイズ・インターフェースを使用して音声をカスタマイズできるかどうかを示すブール値。 (このフィールドの情報は `custom_pronunciation` フィールドと同じですが、後方互換性のために保持されています)。
-   `supported_features`。この音声でサポートされる以下の追加のサービス機能が表されます。
    -   `voice_transformation`。SSML 要素 `<voice-transformation>` を使用して音声を変換できるかどうかを示すブール値。
    -   `custom_pronunciation`。サービスのカスタマイズ・インターフェースを使用して音声をカスタマイズできるかどうかを示すブール値。

## 特定の音声のリスト表示
{: #listVoice}

`GET /v1/voices/{voice}` メソッドは、特定の音声に関する情報をリスト表示します。2 つのパラメーターを取ります。

<table>
  <caption>表 2. <code>voices</code> メソッドのパラメーター</caption>
  <tr>
    <th style="text-align:left; width:18%">パラメーター</th>
    <th style="text-align:center; width:12%">タイプ</th>
    <th style="text-align:center; width:12%">データ型</th>
    <th style="text-align:left">説明</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>必須</em></td>
    <td style="text-align:center">Path</td>
    <td style="text-align:center">String</td>
    <td>
      情報を返す音声を指定します。 音声はその名前で指定します (例えば、<code>en-US_LisaVoice</code>)。
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>オプション</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      指定した音声に定義されているカスタム音声モデルの
      GUID (Globally Unique Identifier) を指定します。カスタマイズ ID を含める場合、
      カスタム・モデルの所有者のサービス資格情報を指定して
      メソッドを呼び出す必要があります。
    </td>
  </tr>
</table>

`customization_id` パラメーターを省略した場合、指定した音声についてこのメソッドから返される JSON 出力は、`GET /v1/voices` メソッドで 1 つの音声について返される情報と同じです。`customization_id` を指定した場合は、指定したカスタム音声モデルに関する情報を示す `customization` フィールドが出力に含められます。

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

追加の `customization` フィールドには、カスタム音声モデルの GUID、名前、言語、説明などの情報を示す属性があります。また、モデルの所有者のサービス資格情報、モデルの作成日時、最終変更日時も表示されます。
