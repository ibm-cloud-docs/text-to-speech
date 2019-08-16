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

# HTTP 介面
{: #usingHTTP}

若要使用 {{site.data.keyword.texttospeechfull}} 服務的 HTTP REST 介面將文字合成為語音，請呼叫 `GET` 或 `POST /v1/synthesize` 方法。請指定要合成的文字，以及口說音訊的語音及格式。您也可以指定要與要求搭配使用的自訂語音模型。
{: shortdesc}

如需 HTTP 介面的相關資訊，請參閱 [API 參考資料](https://{DomainName}/apidocs/text-to-speech){: external}。

## 將文字合成為音訊
{: #synthesize}

若要將文字合成為音訊，您可以呼叫服務的兩個 `/v1/synthesize` 方法版本之一：

-   `GET /v1/synthesize` 方法以必要的 `text` 查詢參數，接受要合成的文字。要求的大小上限為 8 KB，其中包括輸入文字、指定的任何 SSML 以及 URL 和標頭。
-   `POST /v1/synthesize` 方法以必要的要求內文，接受作為 JSON 建構的待合成文字。若為 URL 和標頭，要求的大小上限為 8 KB，若為要求內文中傳送的輸入文字，則為 5 KB。5 KB 限制包含您指定的任何 SSML。

`/v1/synthesize` 方法的兩個版本具有下列共同的參數：

<table>
  <caption>表 1. <code>/v1/synthesize</code> 方法的參數</caption>
  <tr>
    <th style="text-align:left; width:18%">參數</th>
    <th style="text-align:center; width:12%">類型</th>
    <th style="text-align:center; width:12%">資料類型</th>
    <th style="text-align:left">說明</th>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>選用</em></td>
    <td style="text-align:center">查詢</td>
    <td style="text-align:center">字串</td>
    <td>
      指定所要求的音訊格式或 MIME 類型，服務會以此格式或類型傳回音訊。您也可以使用 HTTP <code>Accept</code> 要求標頭來指定此值。將引數以 URL 編碼為 `accept` 查詢參數。如需相關資訊，請參閱[音訊格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>選用</em></td>
    <td style="text-align:center">查詢</td>
    <td style="text-align:center">字串</td>
    <td>
      指定要在音訊中用來說出文字的語音。請使用 <code>/v1/voices</code> 方法，取得支援語音的現行清單。預設語音為 <code>en-US_MichaelVoice</code>。如需相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>選用</em></td>
    <td style="text-align:center">查詢</td>
    <td style="text-align:center">字串</td>
    <td>
      為要用於合成的自訂語音模型指定廣域唯一 ID (GUID)。只有在指定的自訂語音模型符合用於合成之語音的語言時，才保證此模型可以運作。如果您包含了自訂作業 ID，則必須使用擁有自訂模型之服務實例的認證來提出要求。省略此參數，會使用沒有自訂作業的指定語音。如需相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。
    </td>
  </tr>
</table>

您也可以將下列要求標頭用於合成要求，這些要求標頭可供所有 {{site.data.keyword.watson}} 服務使用：

-   `X-Watson-Learning-Opt-Out` 指出服務是否會記載要求及回應資料，以改善服務供未來使用者使用。若要防止 IBM 存取您的資料進行一般服務改善，請將參數指定為 <code>true</code>。如需相關資訊，請參閱[控制 {{site.data.keyword.watson}} 服務的要求記載](/docs/services/watson?topic=watson-gs-logging-overview)。
-   `X-Watson-Metadata` 會建立客戶 ID 與隨要求傳遞之資料的關聯。如需相關資訊，請參閱[資訊安全](/docs/services/text-to-speech?topic=text-to-speech-information-security)。

如果您指定無效的查詢參數或 JSON 欄位，作為 `/v1/synthesize` 方法之輸入的一部分，則服務會傳回 `Warnings` 回應標頭，用於說明並列出每個無效的引數。儘管出現警告，要求仍會成功。
{: note}

## 指定輸入文字
{: #input}

`GET` 和 `POST /v1/synthesize` 方法接受純文字輸入，或以 SSML 標註的文字。兩個版本的差異主要在於您如何指定要合成的文字：

-   `GET /v1/synthesize` 方法接受 `text` 查詢參數所指定的輸入文字。請將輸入指定為純文字或 SSML，兩者都必須以 URL 編碼。
-   `POST /v1/synthesize` 方法接受要求內文中的輸入文字。請用封裝純文字或 SSML 的下列簡單 JSON 建構來指定輸入。您也必須針對 `Content-Type` 標頭指定 `application/json` 的值。

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

雖然 `GET` 和 `POST` 方法提供同等的功能，但使用 `POST` 方法將輸入文字傳遞給服務一定都會比較安全。`POST` 要求會在要求的內文中傳遞輸入，而 `GET` 要求會在 URL 中公開資料。

## 指定 SSML 輸入
{: #ssml-http}

「語音合成標記語言 (SSML)」是 XML 型標記語言，其設計旨在為語音合成應用程式（例如 {{site.data.keyword.texttospeechshort}} 服務）提供文字註釋。您可以使用 SSML 元素及其屬性，以便更進一步控制合成及產生的音訊輸出。

如需使用 SSML 來標註輸入文字的相關資訊，請參閱[使用 SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml)。文件會編列服務所支援的 SSML 元素及屬性。它也記錄了服務的表達和語音轉換延伸規格。

## 跳出 XML 控制字元
{: #escape}

因為您可以提交包含 XML 型 SSML 註釋的輸入文字，所以服務會驗證所有輸入，以確保任何 SSML 正確無誤且格式正確。因此，您必須跳出所有存在於輸入文字中的 XML 控制字元，不論輸入是否包含 SSML。請使用表 2 的相等跳出字串或字元編碼，而不是指出的字元。

<table style="width:80%">
  <caption>表 2. 跳出 XML 控制字元</caption>
  <tr>
    <th style="text-align:center; vertical-align:bottom; width:40%">字元</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">跳出字串</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">字元編碼</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>&quot;</code><br/>（雙引號）</td>
    <td style="text-align:center"><code>&amp;quot;</code></td>
    <td style="text-align:center"><code>&amp;#34;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>'</code><br/>（撇號或單引號）</td>
    <td style="text-align:center"><code>&amp;apos;</code></td>
    <td style="text-align:center"><code>&amp;#39;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&amp;</code><br/>（& 符號）</td>
    <td style="text-align:center"><code>&amp;amp;</code></td>
    <td style="text-align:center"><code>&amp;#38;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&lt;</code><br/>（左角括弧）</td>
    <td style="text-align:center"><code>&amp;lt;</code></td>
    <td style="text-align:center"><code>&amp;#60;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&gt;</code><br/>（右角括弧）</td>
    <td style="text-align:center"><code>&amp;gt;</code></td>
    <td style="text-align:center"><code>&amp;#62;</code></td>
  </tr>
</table>

如需服務如何驗證輸入文字的相關資訊，請參閱 [SSML 驗證](/docs/services/text-to-speech?topic=text-to-speech-ssml#errors)。

## 輸入文字的範例
{: #httpExamples}

下列範例顯示如何使用 HTTP 介面的任一種方法來指定輸入文字。它們也顯示如何跳出 XML 控制字元。這些範例包含換行符號，以方便閱讀。請*不要* 在實際輸入中包含換行符號。

### 具有 GET 要求的輸入範例
{: #getExamples}

下列範例使用 `GET /v1/synthesize` 方法的 `text` 查詢參數來傳遞 URL 編碼的輸入：

-   純文字輸入：

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   SSML 輸入：

    ```
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3C
    break%20time=%225s%22/%3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another
    %20sentence.%3C/s%3E%3Cs%3EFinally,%20this%20is%20the%20last%20sentence.
    %3C/s%3E%3C/p%3E%22
    ```
    {: codeblock}

### 具有 POST 要求的輸入範例
{: #postExamples}

下列範例會在 `POST /v1/synthesize` 方法的內文中傳遞輸入：

-   純文字輸入：

    ```javascript
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   SSML 輸入：

    ```javascript
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/>
        paragraph.</s><s>Here is another sentence.</s><s>Finally, this is
        the last sentence.</s></p>"
    }
    ```
    {: codeblock}

### 具有 XML 控制字元的輸入範例
{: #xmlExamples}

下列範例會將這兩個句子傳送至 `POST /v1/synthesize` 方法。這些範例會適當地跳出內嵌的 XML 字元。

```
"What have I learned?" he asked. "Everything!"
```
{: codeblock}

-   純文字輸入：

    ```javascript
    {
      "text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
    }
    ```
    {: codeblock}

-   SSML 輸入：

    ```javascript
    {
      "text": "<s>&quot;What have I learned?&quot; he asked.
        &quot;<express-as type=\"GoodNews\">Everything!</express-as>&quot;</s>"
    }
    ```
    {: codeblock}
