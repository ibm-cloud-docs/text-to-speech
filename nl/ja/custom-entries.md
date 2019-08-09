---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-24"

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

# カスタム項目の作成と管理
{: #customWords}

カスタム・モデルを作成したら、次のステップは、単語/トランスレーションのペアの形式でカスタム項目を追加することです。カスタム項目により、指定した単語を合成中にどのように発音するかを定義します。 この定義は、サービスのデフォルトの通常の発音ルールをオーバーライドします。 1 つ以上の単語のトランスレーションを同時に追加および照会できます。また、不要になった個別の単語を削除できます。 カスタマイズ・インターフェースに慣れたら、複数の単語を同時に操作すると、単語ごとに作業するよりも便利な場合があります。 カスタム・モデルのカスタマイズ ID を必要とするメソッドを使用する場合は、そのモデルを所有するサービス・インスタンスの資格情報を使用する必要があります。
{: shortdesc}

## カスタム・モデルへの単一の単語の追加
{: #cuWordAdd}

単一の単語/トランスレーションのペアをカスタム・モデルに追加するには、`PUT /v1/customizations/{customization_id}/words/{word}` メソッドを使用します。 メソッドの URL で、追加する単語を指定します。 単一の `translation` 属性を使用して JSON オブジェクトとして単語のトランスレーションを指定します。 モデル内に既に存在している単語の新規トランスレーションを追加した場合、その単語の既存のトランスレーションが上書きされます。

トランスレーションを指定するには、同音異字方式または表音方式 (またはその 2 つの組み合わせ) を使用します。 表音トランスレーションの場合は、International Phonetic Alphabet (IPA) フォーマットまたは {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) フォーマットを使用できます。 以下の例では、`IEEE` という単語に対応するトランスレーションをカスタム・モデルに追加するさまざまな方法を示しています。

-   **同音異字:** この例の場合は、以下のように同音異字方式を使用するのが最も簡単です。

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"I triple E\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **表音 IPA:** IPA では、以下のように、`alphabet` 属性を `ipa` に設定し、`ph` 属性を IPA フォーマットで定義した `<phoneme>` 要素を使用する必要があります。

    <pre><code class="language-bash">  curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#712;a&#618;.t&#633;&#712;&#616;p&#601;l.&#712;i\\\"&gt;&lt;/phoneme&gt;\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"</code></pre>

-   **表音 {{site.data.keyword.IBM_notm}} SPR:** SPR では、以下のように、`alphabet` 属性を `ibm` に設定し、`ph` 属性を SPR フォーマットで定義した `<phoneme>` 要素を使用する必要があります。

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

## カスタム・モデルへの複数の単語の追加
{: #cuWordsAdd}

同時に 1 つ以上の単語をカスタム・モデルに追加するには、`POST /v1/customizations/{customization_id}/words` メソッドを使用します。 カスタム・モデルに追加する項目は、単語/トランスレーションのペアの JSON 配列として指定します。 以下の例では、単語 `NCAA` および `iPhone` の一般的な同音異字トランスレーションをカスタム・モデルに追加します。

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

要求本体で送信される JSON の内容は、以下と同じです。

```javascript
{
  "words": [
    {"word":"NCAA", "translation":"N C double A"},
      {"word":"iPhone", "translation":"I phone"}
  ]
}
```
{: codeblock}

[カスタム・モデルの更新](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsUpdate)で説明したように、`POST /v1/customizations/{customization_id}` メソッドを使用して、単語をカスタム・モデルに追加することもできます。 以下の例では、このメソッドを使用して、前の例と同じ 2 つの単語を追加しています。モデルのメタデータに違いはありません。 URL を除き、2 つのメソッドは同じです。

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

## 日本語のカスタム・モデルへの単語の追加
{: #cuJapaneseAdd}

日本語のカスタム・モデルの単語に対する項目を作成する場合は、追加の考慮事項と `part_of_speech` フィールドが適用されます。詳しくは、[日本語の項目の処理](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes)を参照してください。 以下のように、日本語のカスタム項目の品詞を指定します。

-   `PUT /v1/customizations/{customization_id}/words/{word}` メソッドの場合は、以下の形式で JSON オブジェクトを渡します。

    ```javascript
    {
      "translation": "value",
      "part_of_speech": "value"
    }
    ```
    {: codeblock}

-   `POST /v1/customizations/{customization_id}/words` メソッドおよび `POST customizations/{customization_id}` メソッドの場合は、以下の形式で JSON オブジェクトを渡します。

    ```javascript
    {
      "words": [
      {
          "word": "value",
          "translation": "value",
          "part_of_speech": "value"
        }
        . . .
      ]
    }
    ```
    {: codeblock}

以下の `PUT /v1/customizations/{customization_id}/words/{word}` メソッドの例では、`NY` を表す 2 バイト・ストリングの URL エンコード表記を、名詞 (`Mesi`) の<code>&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;</code> (英語の `New York`) に変換しています。 このカスタム・トランスレーションが定義されていない場合、ストリングは`エヌワイ`と読まれます。

-   **同音異字:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **表音 IPA:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#626;&#623;&#720;&#106;&#111;&#720;&#107;&#623;\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **表音 {{site.data.keyword.IBM_notm}} SPR:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

## カスタム・モデルに含まれている単一の単語の照会
{: #cuWordQueryModel}

カスタム・モデルに含まれている単一の単語のトランスレーションを照会するには、`GET /v1/customizations/{customization_id}/words/{word}` メソッドを使用します。 メソッドの URL に単語を指定します。 トランスレーションが、カスタム・モデルで定義されているとおりに (同音異字または表音)、返されます。

以下の例では、単語 `IEEE` のトランスレーションについてカスタム・モデルに照会しています。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

この単語の同音異字トランスレーションがモデルに定義されていれば、この例では、以下の JSON 出力が返されます。

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

## カスタム・モデルに含まれているすべての単語の照会
{: #cuWordsQueryModel}

カスタム・モデルに定義されているすべての単語のトランスレーションを表示するには、`GET /v1/customizations/{customization_id}/words` メソッドを使用します。 以下の例では、このメソッドにより、3 つの単語の同音異字トランスレーションが含まれているカスタム・モデルの項目がリストされます。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

このメソッドは、以下のデータが含まれている JSON 配列を返します。 日本語のカスタム・モデルの場合は、個々の単語の品詞が出力に含まれます。

```javascript
{
  "words": [
      {
      "word": "IEEE",
         "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

[カスタム・モデルの照会](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery)で説明したように、以下のように `GET /v1/customizations/{customization_id}` メソッドを使用して、カスタム・モデルのメタデータと単語の両方を表示することもできます。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

このメソッドは、以下の形式の JSON 出力を返します。 この例と前の例では同じカスタム・モデルを指定しているので、以下のように、出力に含まれている単語の配列は同じです。

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T19:15:17.926Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T19:46:01.387Z",
  "words": [
    {
      "word": "IEEE",
         "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

## 言語の単語の照会
{: #cuWordsQueryLanguage}

単語の発音を照会するには、`GET /v1/pronunciation` メソッドを使用します。 特定の音声の言語での発音を取得するために、その音声を指定します。 デフォルトでは、このメソッドは、サービスの通常の発音ルールに基づいて発音を返しますが、指定のカスタム音声モデルの発音を要求することもできます。 メソッドには、返される情報を指定できる以下の 4 つのクエリー・パラメーターが含まれています。

-   必須の `text` パラメーターは、発音を返す単語を指定します。
-   オプションの `voice` パラメーターでは、発音の言語を指定できます。 音声モデルのいずれか (例えば、`en-US_LisaVoice`) を指定して、対象言語を示します。同じ言語に対するすべての音声 (例えば `en-US`) からは、同じ発音が返されます。 デフォルトでは、米国英語の発音が返されます。
-   オプションの `format` パラメーターでは、発音の表音フォーマット (`ipa` または `ibm`) を指定できます。 デフォルトでは、IPA フォーマットの発音が返されます。
-   オプションの `customization_id` パラメーターでは、発音を返すカスタム音声モデルを指定できます。 単語が指定音声モデルで定義されていない場合、サービスはそのモデルの言語のデフォルトの発音を返します。 カスタマイズなしで指定音声のトランスレーションを表示する場合は、このパラメーターを省略します。 音声とカスタム音声モデルの両方は指定しないでください。

このメソッドは、任意の言語の単語を照会できるため、またカスタマイズ ID が不要で、表示できる単語に制限が課されないため、便利です。 特に、新規単語の表音トランスレーションを作成する際に役立つことがあります。これを使用して既存の単語の発音を取得してから、それを新規トランスレーションの基盤として使用できます。これは、トランスレーションを最初から作成するよりも、はるかに簡便です。

以下の例では、デフォルトの IPA フォーマットで単語 `IEEE` の発音を取得しています。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=IEEE"
```
{: pre}

<pre><code data-copy="false" class="language-javascript">{
  "pronunciation": ".&#712;a&#618; .&#712;i .&#712;i .&#712;i"
}</code></pre>

以下の例では、単語の `IEEE` の同音異字トランスレーションを入力し、{{site.data.keyword.IBM_notm}} SPR フォーマットで相当する表音トランスレーションを取得しています。 書き起こしトランスレーションに対する表音表記の取得は、特に興味深い表音トランスレーション作成方法です。 以下の例では、単語のスペースは URL エンコードされています。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=i%20triple%20e&format=ibm"
```
{: pre}

```javascript
{
  "pronunciation": "1Y.tr1Ipxl.1i"
}
```
{: codeblock}

## カスタム・モデルからの単語の削除
{: #cuWordDelete}

カスタム・モデルから単語を削除するには、`DELETE /v1/customizations/{customization_id}/words/{word}` メソッドを使用します。 メソッドの URL で、削除する単語を指定します。 個別の単語のみを削除できます。単一のメソッドで複数の単語を削除することはできません。

以下の例では、指定したカスタム・モデルから単語 `IEEE` を削除しています。

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}
