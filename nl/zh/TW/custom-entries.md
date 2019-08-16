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

# 建立及管理自訂項目
{: #customWords}

自訂模型存在之後，下一步是以字組/轉換配對的形式新增自訂項目，以定義在合成期間指定的字組如何發音。這些定義會置換服務的預設一般發音規則。您可以一次新增並查詢一個以上字組的轉換，以及刪除不再需要的個別字組。在熟悉自訂作業介面之後，一次操作多個字組就會比逐字運作更為便利。您必須將認證用於擁有自訂模型的服務實例，才能使用任何需要其自訂作業 ID 的方法。
{: shortdesc}

## 將單一字組新增至自訂模型
{: #cuWordAdd}

若要將單一字組/轉換配對新增至自訂模型，請使用 `PUT /v1/customizations/{customization_id}/nwords/{word}` 方法。請在方法 URL 中指定要新增的字組。您可以使用單一 `translation` 屬性，以 JSON 物件的形式提供字組的轉換。為已存在於模型中的字組新增轉換，會改寫字組的現有轉換。

您可以使用類似音或語音方法（或兩者的組合）來提供轉換。對於語音轉換，您可以使用「國際音標 (IPA)」或「{{site.data.keyword.IBM_notm}} 符號語音表示法 (SPR)」格式。下列範例使用不同的方法，將字組 `IEEE` 的對等轉換新增至自訂模型。

-   **類似音：**對於此範例，類似音方法是最簡單的方法。

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"I triple E\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **語音 IPA：**IPA 需要使用 `<phoneme>` 元素，並將 `alphabet` 屬性設為 `ipa`，且 `ph` 屬性以 IPA 格式定義：

    <pre><code class="language-bash">curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#712;a&#618;.t&#633;&#712;&#616;p&#601;l.&#712;i\\\"&gt;&lt;/phoneme&gt;\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"</code></pre>

-   **語音 {{site.data.keyword.IBM_notm}} SPR：**SPR 會使用 `<phoneme>` 元素，並將 `alphabet` 屬性設為 `ibm`，且 `ph` 屬性以 SPR 格式定義：

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

## 將多個字組新增至自訂模型
{: #cuWordsAdd}

若要一次將一個以上字組新增至自訂模型，請使用 `POST /v1/customizations/{customization_id}/words` 方法。請以字組/轉換配對的 JSON 陣列來指定要新增至自訂模型的項目。下列範例會將字組 `NCAA` 和 `iPhone` 的常用類似音轉換新增至自訂模型：

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

在要求內文中傳送的 JSON 內容相當於下列內容：

```javascript
{
  "words": [
    {"word":"NCAA", "translation":"N C double A"},
    {"word":"iPhone", "translation":"I phone"}
  ]
}
```
{: codeblock}

如[更新自訂模型](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsUpdate)中所述，您也可以使用 `POST /v1/customizations/{customization_id}` 方法將字組新增至自訂模型。下列範例使用此方法，新增與前一個範例相同的兩個字組；它不會變更模型的 meta 資料。除了 URL 之外，這兩種方法是相同的。

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

## 將字組新增至日文自訂模型
{: #cuJapaneseAdd}

為日文自訂模型中的字組建立項目時，其他考量和額外的 `part_of_speech` 欄位會適用；如需相關資訊，請參閱[使用日文項目](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes)。請指定日文自訂項目的詞性，如下所示：

-   針對 `PUT /v1/customizations/{customization_id}/words/{word}` 方法，傳遞下列形式的 JSON 物件：

    ```javascript
    {
      "translation": "value",
      "part_of_speech": "value"
    }
    ```
    {: codeblock}

-   針對 `POST /v1/customizations/{customization_id}/words` 及 `POST customizations/{customization_id}` 方法，傳遞如下的 JSON 物件：

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

`PUT /v1/customizations/{customization_id}/words/{word}` 方法的下列範例會將 `NY` 的 URL 編碼雙位元組字串，轉換為名詞 (`Mesi`) <code>&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;</code>（英文的 `New York`）。如果未定義此自訂轉換，則會將字串讀做 `enu wai`。

-   **類似音：**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **語音 IPA：**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#626;&#623;&#720;&#106;&#111;&#720;&#107;&#623;\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **語音 {{site.data.keyword.IBM_notm}} SPR：**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

## 從自訂模型查詢單一字組
{: #cuWordQueryModel}

若要從自訂模型查詢單一字組的轉換，請使用 `GET /v1/customizations/{customization_id}/words/{word}` 方法。請在方法 URL 中指定字組。轉換會依其在自訂模型中的定義（類似音或語音）傳回。

下列範例會查詢自訂模型，以取得字組 `IEEE` 的轉換：

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

如果該字組在模型中具有類似音轉換，則範例會傳回下列 JSON 輸出：

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

## 從自訂模型查詢所有字組
{: #cuWordsQueryModel}

若要查看自訂模型中定義之所有字組的轉換，請使用 `GET /v1/customizations/{customization_id}/words` 方法。下列範例使用方法來列出自訂模型中的項目，而自訂模型包含三個字組的類似音轉換：

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

此方法會傳回具有下列資料的 JSON 陣列。若為日文自訂模型，輸出包括個別字組的詞性。

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

如[查詢自訂模型](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery)中所述，您也可以使用 `GET /v1/customizations/{customization_id}` 方法來查看自訂模型的 meta 資料及字組：

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

此方法會傳回下列形式的 JSON 輸出。因為此範例和前一個範例指定相同的自訂模型，所以其輸出中的字組陣列是相同的。

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

## 從語言查詢字組
{: #cuWordsQueryLanguage}

若要查詢字組的發音，請使用 `GET /v1/pronunciation` 方法。指定語音，以便取得使用該語音之語言的發音。依預設，此方法會根據服務的一般發音規則來傳回發音，但您也可以要求所指定之自訂語音模型的發音。此方法包括四個查詢參數，可讓您指定要傳回的資訊：

-   必要的 `text` 參數，用來指定要傳回其發音的字組。
-   選用性的 `voice` 參數，可讓您指定發音的語言。您可以指定其中一個語音模型（例如，`en-US_LisaVoice`）來指出所需語言；相同語言（例如，`en-US`）的所有語音都會傳回相同的發音。依預設，會傳回美式英文的發音。
-   選用性的 `format` 參數，可讓您指定發音的語音格式，即 `ipa` 或 `ibm`。依預設，會傳 IPA 格式的發音。
-   選用性的 `customization_id` 參數，可讓您指定要傳回其發音的自訂語音模型。如果未在指定的語音模型中定義該字組，則服務會傳回模型語言的預設發音。省略此參數，可在沒有自訂作業的情形下查看所指定語音的轉換。請不要同時指定語音和自訂語音模型。

此方法很有用，因為它可讓您查詢任何語言中的某個字組，且由於不需要自訂作業 ID，因此不會對您可以看到的字組產生任何限制。在組合新字組的語音轉換時，它可能特別有用；您可以用它來取得現有字組的發音，然後用來作為新轉換的基礎，這比從頭開始建立轉換方便很多。

下列範例會以預設 IPA 格式，取得 `IEEE` 字組的發音。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=IEEE"
```
{: pre}

<pre><code data-copy="false" class="language-javascript">{
  "pronunciation": ".&#712;a&#618; .&#712;i .&#712;i .&#712;i"
}</code></pre>

下列範例會輸入 `IEEE` 字組的類似音轉換，並取得 {{site.data.keyword.IBM_notm}} SPR 格式的語音對等項目。取得語音發音以進行類似音轉換，是組合語音轉換時的特別有趣方法。範例中的字組空格是以 URL 方式編碼。

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

## 從自訂模型刪除字組
{: #cuWordDelete}

若要從自訂模型刪除字組，請使用 `DELETE /v1/customizations/{customization_id}/words/{word}` 方法。請在方法 URL 中指定要刪除的字組。您只能刪除個別字組；無法使用單一方法來刪除多個字組。

下列範例會從指定的自訂模型刪除 `IEEE` 字組：

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}
