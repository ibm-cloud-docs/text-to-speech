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

# 建立及管理自訂語音模型
{: #customModels}

使用任何自訂模型的第一步是建立它。一旦它存在，您就可以藉由查詢或更新模型的 meta 資料和項目來管理模型，如果不再需要，也可以將它刪除。開始之前，請檢閱有關自訂模型的下列一般用法資訊。
{: shortdesc}

## 使用注意事項
{: #customGuidelines}

使用自訂作業介面時，請考量下列準則。

### 自訂語音模型的所有權
{: #customOwner}

擁有自訂語音模型的服務實例，是使用其認證來建立該模型的 {{site.data.keyword.texttospeechshort}} 服務實例。您必須使用該服務實例的服務認證，搭配自訂作業介面的方法，才能以任何方式使用自訂模型。

對於相同 {{site.data.keyword.texttospeechshort}} 服務實例取得的所有認證，會共用對針對該服務實例建立之所有自訂模型的存取權。若要限制對自訂模型的存取權，請建立個別服務實例，並且只使用該服務實例的認證來建立及使用模型。其他服務實例的認證無法影響自訂模型。

在認證之間共用所有權的優點是，您可以取消一組認證（例如，如果認證遭洩露的話）。然後，您可以為相同的服務實例建立新的認證，並且仍然保留對使用原始認證建立之自訂模型的所有權和存取權。

### 要求記載和資料隱私權
{: #customLogging}

服務如何處理自訂作業介面呼叫的要求記載，取決於要求：

-   服務*不會* 記載用來建置自訂語音模型的資料（字組及轉換）。使用自訂作業介面來管理自訂模型中的字組和轉換時，您不需要設定 `X-Watson-Learning-Opt-Out` 要求標頭。您的訓練資料絕不會用來改善服務的基礎模型。
-   服務*會* 在搭配使用自訂模型與合成要求時記載資料。您必須將 `X-Watson-Learning-Opt-Out` 要求標頭設為 `true`，以防止記載合成要求。

如需相關資訊，請參閱[控制 {{site.data.keyword.watson}} 服務的要求記載](/docs/services/watson?topic=watson-gs-logging-overview)。

### 資訊安全
{: #customSecurity}

服務容許您為客戶 ID 與針對自訂語音模型新增或更新的資料，建立兩者的關聯。您可以使用下列方法傳遞 `X-Watson-Metadata` 標頭，以建立客戶 ID 與自訂字組的關聯：

-   `POST /v1/customizations/{customization_id}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word}`

必要的話，您可以使用 `DELETE /v1/user_data` 方法來刪除與客戶 ID 相關聯的資料。如需相關資訊，請參閱[資訊安全](/docs/services/text-to-speech?topic=text-to-speech-information-security)。

## 建立自訂模型
{: #cuModelsCreate}

若要建立新的自訂模型，請使用 `POST /v1/customizations` 方法。新模型在剛建立時一律是空的。您必須使用其他方法，將字組/轉換配對移入其中。如果新的自訂模型是使用某個服務實例的認證建立的，則該模型由該服務實例所擁有。如需相關資訊，請參閱[自訂語音模型的所有權](#customOwner)。

您可以使用要求的內文，將下列屬性當作 JSON 物件來傳遞。

<table>
  <caption>表 1. <code>POST /v1/customizations</code> 方法的參數</caption>
  <tr>
    <th style="text-align:left; width:18%">參數</th>
    <th style="text-align:center; width:12%">資料類型</th>
    <th style="text-align:left">說明</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>必要</em></td>
    <td style="text-align:center">字串</td>
    <td>
      新自訂模型的使用者定義名稱。此名稱用來標示模型，以方便識別。在您擁有的所有自訂模型之間，此名稱必須是唯一的。
    </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>選用</em></td>
    <td style="text-align:center">字串</td>
    <td>
      自訂模型的語言 ID。預設值為 <code>en-US</code>，表示美式英文。
    自訂模型可搭配以該語言提供的任何語音（標準或神經）使用。</td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>選用</em></td>
    <td style="text-align:center">字串</td>
    <td>
      新模型的說明。雖然它是選用的，但強烈建議使用說明。
    </td>
  </tr>
</table>

下列範例 `curl` 指令會建立名稱為 `curl Test` 的新自訂模型。`Content-Type` 標頭會將輸入類型識別為 `application/json`。

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test\", \"language\":\"en-US\", \"description\":\"Customization test via curl\"}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

此方法會傳回 JSON 物件，其中包含新模型的廣域唯一 ID (GUID)。GUID 用來作為各呼叫中的 `customization_id` 參數以存取模型，例如用於查詢、修改及使用模型及其字組的呼叫。

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

## 查詢自訂模型
{: #cuModelsQuery}

若要查詢現有自訂模型的相關資訊，請使用 `GET /v1/customizations/{customization_id}` 方法。這是查看模型所有相關資訊（其 meta 資料以及它所包含的字組/轉換配對）的最直接方法。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

此方法會將其結果傳回為下列格式的 JSON 物件：

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T18:12:31.743Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T18:12:31.743Z",
  "words": []
}
```
{: codeblock}

輸出中除了包含在建立模型時輸入的資訊外，還包含模型擁有者的認證、模型的語言，以及建立模型和前次修改模型的時間。因為模型自建立之後尚未經過修改，所以範例中的兩個時間相同。

輸出也包含 `words` 陣列，其中列出模型的自訂項目。因為模型尚未經過更新，所以範例中的陣列是空的。

## 查詢所有自訂模型
{: #cuModelsQueryAll}

若要查看您擁有之所有自訂模型的相關資訊，請使用 `GET /v1/customizations` 方法：

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

此方法會傳回一個 JSON 陣列，其中包含要求者所擁有之每個自訂模型的物件。擁有者的認證會顯示在 `owner` 欄位中。

```javascript
{
  "customizations": [
    {
      "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T19:15:17.926Z",
      "name": "curl Test",
      "language": "en-US",
      "description": "Customization test via curl",
      "last_modified": "2016-07-15T19:15:17.926Z"
    },
    {
      "customization_id": "63f5807f-a4f2-5766-914e-7abb1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T18:12:31.743Z",
      "name": "curl Test Two",
      "language": "en-US",
      "description": "Second customization test via curl",
      "last_modified": "2016-07-15T18:23:50.912Z"
    }
  ]
}
```
{: codeblock}

第一個模型的 `created` 及 `last_modified` 時間相同，因為它尚未經過更新。第二個模型的時間不同，指出它自起始建立之後已變更過。此資訊不包含針對模型定義的自訂項目。

## 更新自訂模型
{: #cuModelsUpdate}

若要更新自訂模型的相關資訊，請使用 `POST /v1/customizations/{customization_id}` 方法。您可以將更新指定為 JSON 物件。除了修改其名稱及說明之外，您也可以使用此方法來新增或更新模型中的字組/轉換配對。建立模型之後，即無法變更其語言。

下列範例會更新自訂模型的名稱和說明。空的 JSON 陣列會與 `words` 參數一起傳送，指出模型的項目將維持不變。

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test Update\", \"description\":\"Customization test update via curl\", \"words\":[]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

如需更新模型中字組的相關資訊，請參閱[將多個字組新增至自訂模型](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsAdd)。

## 刪除自訂模型
{: #cuModelsDelete}

若要捨棄您不再需要的自訂模型，請使用 `DELETE /v1/customizations/{customization_id}` 方法。只有在您確定不再需要模型時，才使用此方法，因為刪除作業是永久性的。

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}
