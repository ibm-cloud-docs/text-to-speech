---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-21"

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

# HTTP インターフェース
{: #usingHTTP}

{{site.data.keyword.texttospeechfull}} サービスの HTTP REST インターフェースを使用してテキストから音声を合成するには、`GET /v1/synthesize` メソッドまたは `POST /v1/synthesize` メソッドを呼び出します。合成するテキスト、発話音声用の音声およびフォーマットを指定します。要求に使用するカスタム音声モデルを指定することもできます。
{: shortdesc}

HTTP インターフェースの詳細については、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/text-to-speech){: new_window} を参照してください。

## テキストからの音声の合成
{: #synthesize}

テキストを音声に合成するには、サービスの `/v1/synthesize` メソッドの 2 つのバージョンのいずれかを呼び出します。

-   `GET /v1/synthesize` メソッドは、必須の `text` 照会パラメーターで合成用のテキストを受け取ります。要求の最大サイズは 8 KB で、これには入力テキスト、指定する SSML、URL、ヘッダーが含まれます。
-   `POST /v1/synthesize` メソッドは、必須の要求本体に含まれた JSON 構造体として合成用のテキストを受け取ります。要求の最大サイズは、URL とヘッダーが 8 KB、要求本体で送信する入力テキストが 5 KB です。この 5 KB 制限には、指定する SSML も含まれます。

`/v1/synthesize` メソッドの 2 つのバージョンには、以下の共通のパラメーターがあります。

<table>
  <caption>表 1. <code>/v1/synthesize</code>
    メソッドのパラメーター</caption>
  <tr>
    <th style="text-align:left; width:18%">パラメーター</th>
    <th style="text-align:center; width:12%">タイプ</th>
    <th style="text-align:center; width:12%">データ型</th>
    <th style="text-align:left">説明</th>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>オプション</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
サービスから返される音声として要求する音声フォーマット (MIME タイプ) を指定します。この値は、HTTP の <code>Accept</code> 要求ヘッダーで指定することもできます。`accept` 照会パラメーターの引数を URL エンコードします。詳しくは、[音声フォーマット](/docs/services/text-to-speech/audio-formats.html)を参照してください。
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>オプション</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      テキストを音声で発話する際の声を指定します。 サポートされる音声の現在のリストを取得するには、<code>/v1/voices</code> メソッドを使用します。 デフォルトの音声は <code>en-US_MichaelVoice</code> です。 詳しくは、[言語と音声](/docs/services/text-to-speech/voices.html)を参照してください。</td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>オプション</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      合成で使用するカスタム音声モデルの GUID (Globally Unique Identifier) を
      指定します。 指定したカスタム音声モデルの動作が保証されるのは、そのモデルが合成用の音声の言語に一致している場合に限られます。カスタマイズ ID を含める場合、モデルの所有者のサービス資格情報を指定してメソッドを呼び出す必要があります。 カスタマイズなしで指定音声を使用する場合は、このパラメーターを省略します。 詳しくは、[カスタマイズの理解](/docs/services/text-to-speech/custom-intro.html)を参照してください。
    </td>
  </tr>
</table>

合成要求で以下の要求ヘッダーを使用することも可能です。どれも、すべての {{site.data.keyword.watson}} サービスで使用できます。

-   `X-Watson-Learning-Opt-Out` は、将来のユーザーのためにサービス向上を図る目的でサービスが要求と応答のデータを記録するかどうかを指定します。全般的なサービス向上のためにデータにアクセスすることを IBM に許可しない場合には、このパラメーターに <code>true</code> を指定してください。詳しくは、[{{site.data.keyword.watson}} サービスの要求ロギングの制御](/docs/services/watson/getting-started-logging.html)を参照してください。
-   `X-Watson-Metadata` では、要求で渡すデータに顧客 ID を関連付けます。詳しくは、[機密保護](/docs/services/text-to-speech/information-security.html)を参照してください。

`/v1/synthesize` メソッドの入力の一部として無効な照会パラメーターまたは JSON フィールドを指定すると、無効な引数のリストと説明が含まれる `Warnings` 応答ヘッダーがサービスから返されます。警告に関係なく要求は成功します。
{: note}

## 入力テキストの指定
{: #input}

`GET /v1/synthesize` メソッドと `POST /v1/synthesize` メソッドは、両方ともプレーン・テキストまたは SSML のアノテーション付きのテキストを入力として取ります。この 2 つのバージョンの違いは、主に合成用のテキストの指定方法にあります。

-   `GET /v1/synthesize` メソッドは、`text` 照会パラメーターで指定された入力テキストを受け取ります。入力はプレーン・テキストまたは SSML として指定します。これらはともに URL エンコードされている必要があります。
-   `POST /v1/synthesize` メソッドは、要求本体に指定された入力テキストを受け取ります。入力は、プレーン・テキストまたは SSML をカプセル化した以下のシンプルな JSON 構造体を使用して指定します。また、`Content-Type` ヘッダーに `application/json` という値を指定する必要もあります。

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

`GET` メソッドと `POST` メソッドの機能は同じですが、入力テキストは `POST` メソッドでサービスに渡すほうが常に安全です。`POST` 要求では要求の本体で入力を渡しますが、`GET` 要求では URL 内にデータが公開されます。

## SSML 入力の指定
{: #ssml-http}

SSML (Speech Synthesis Markup Language) は、{{site.data.keyword.texttospeechshort}} サービスなどの音声合成アプリケーションでテキストのアノテーションを利用するために設計された XML ベースのマークアップ言語です。SSML 要素およびその属性を使用して、合成および結果の音声出力をより詳細に制御できます。

SSML を使用して入力テキストにアノテーションを付ける方法について詳しくは、[SSML の使用 ](/docs/services/text-to-speech/SSML.html)を参照してください。この資料には、サービスでサポートされている SSML の要素と属性の一覧を記載しています。サービスの感情表出や音声変換という拡張機能についても説明しています。

## XML 制御文字のエスケープ
{: #escape}

ユーザーは XML ベースの SSML アノテーションを含む入力テキストを送信できるため、サービスではすべての入力を検証し、SSMLが正確で適切な形式になっていることを確認します。 したがって、入力に SSML が含まれているかどうかに関係なく、入力テキスト内に存在するすべての XML 制御文字をエスケープする必要があります。 表 2 に記している文字は、対応するエスケープ・ストリングまたは文字エンコードに置き換えてください。

<table style="width:80%">
  <caption>表 2. XML 制御文字のエスケープ</caption>
  <tr>
    <th style="text-align:center; vertical-align:bottom; width:40%">文字</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">エスケープ・ストリング</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">文字エンコード</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>&quot;</code><br/>(二重引用符)</td>
    <td style="text-align:center"><code>&amp;quot;</code></td>
    <td style="text-align:center"><code>&amp;#34;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>'</code><br/>(アポストロフィまたは単一引用符)</td>
    <td style="text-align:center"><code>&amp;apos;</code></td>
    <td style="text-align:center"><code>&amp;#39;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&amp;</code><br/>(アンパーサンド)</td>
    <td style="text-align:center"><code>&amp;amp;</code></td>
    <td style="text-align:center"><code>&amp;#38;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&lt;</code><br/>(左不等号括弧)</td>
    <td style="text-align:center"><code>&amp;lt;</code></td>
    <td style="text-align:center"><code>&amp;#60;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&gt;</code><br/>(右不等号括弧)</td>
    <td style="text-align:center"><code>&amp;gt;</code></td>
    <td style="text-align:center"><code>&amp;#62;</code></td>
  </tr>
</table>

サービスによる入力テキストの検証について詳しくは、[SSML 検証](/docs/services/text-to-speech/SSML.html#errors)を参照してください。

## 入力テキストの例
{: #httpExamples}

HTTP インターフェースの両方のメソッドについて、入力テキストの指定方法を示す例を以下に記載します。XML 制御文字のエスケープの方法も例から確認できます。例では、読みやすさのために改行を入れています。実際の入力には改行を*入れない* でください。

### GET 要求の入力例
{: #getExamples}

URL エンコードした入力を `GET /v1/synthesize` メソッドの `text` 照会パラメーターで渡す例を以下に示します。

-   プレーン・テキスト入力:

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   SSML 入力:

    ```
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3C
    break%20time=%225s%22/%3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another
    %20sentence.%3C/s%3E%3Cs%3EFinally,%20this%20is%20the%20last%20sentence.
    %3C/s%3E%3C/p%3E%22
    ```
    {: codeblock}

### POST 要求の入力例
{: #postExamples}

`POST /v1/synthesize` メソッドの本体で入力を渡す例を以下に示します。

-   プレーン・テキスト入力:

    ```javascript
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   SSML 入力:

    ```javascript
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/>
        paragraph.</s><s>Here is another sentence.</s><s>Finally, this is
        the last sentence.</s></p>"
    }
    ```
    {: codeblock}

### XML 制御文字を含む入力例
{: #xmlExamples}

2 つの文を `POST /v1/synthesize` メソッドに送信する例を以下に示します。例では、組み込まれている XML 文字を正しくエスケープしています。

```
"What have I learned?" he asked. "Everything!"
```
{: codeblock}

-   プレーン・テキスト入力:

    ```javascript
    {
      "text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
    }
    ```
    {: codeblock}

-   SSML 入力:

    ```javascript
    {
      "text": "<s>&quot;What have I learned?&quot; he asked.
        &quot;<express-as type=\"GoodNews\">Everything!</express-as>&quot;</s>"
    }
    ```
    {: codeblock}
