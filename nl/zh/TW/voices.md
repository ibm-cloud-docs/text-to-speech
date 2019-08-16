---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-25"

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

# 語言和語音
{: #voices}

{{site.data.keyword.texttospeechfull}} 服務支援各種語言、語音及用語。服務針對每種語言至少提供一個女性語音。針對部分語言，服務提供多種語音，同時包括男性和女性語音。每種語音都會針對其用語使用適當的抑揚頓挫和語調。
{: shortdesc}

先前隨服務提供的 `V2` 語音已停止使用。如果您在應用程式中使用 `V2` 語音，服務會自動改用相等的 `V3` 語音。
{: note}

## 支援的語言和語音
{: #languageVoices}

表 1 列出了可用於每種語言和用語的語音，包括其類型和性別。所有語音都提供了[標準語音](#standardVoices)和[神經語音](#neuralVoices)。如果在要求中省略選用性的 `voice` 參數，則依預設此服務會使用標準 `en-US_MichaelVoice` 語音。

<table style="width:100%">
  <caption>表 1. 支援的語言和語音</caption>
  <tr>
    <th style="text-align:left">語言</th>
    <th style="text-align:center">類型</th>
    <th style="text-align:center">語音</th>
    <th style="text-align:center">性別</th>
  </tr>
  <tr>
    <td style="text-align:left">巴西葡萄牙文</td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">卡斯提亞西班牙文</td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">法文</td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">德文</td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
  <tr>
    <td style="text-align:left">義大利文</td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">日文</td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>ja-JP_EmiV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">拉丁美洲西班牙文</td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">北美洲西班牙文</td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">英式英文</td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">美式英文</td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>en-US_LisaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">標準</td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">神經</td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
</table>

語音 `es-LA_SofiaVoice` 及 `es-US_SofiaVoice` 基本上是相同的語音。最主要差異在於這兩個語音解譯 $（錢幣符號）的方式。拉丁美洲版本使用 *pesos* 一詞，而北美洲版本則使用 *d&oacute;lares* 一詞。這兩個語音之間也可能存在其他次要差異。
{: note}

### 標準語音
{: #standardVoices}

標準語音的名稱（例如，`pt-BR_IsabelaVoice` 和 `en-US_AllisonVoice`）中不包含版本字串 (`V3`)。標準語音使用拼接合成技術來組合錄製語音的區段（或單位），以產生要求的音訊。錄製區段的拼接點有時會導致語音中斷，因此降低所產生語音的品質和自然性。

### 神經語音
{: #neuralVoices}

神經語音的名稱（例如，`pt-BR_IsabelaV3Voice` 和 `en-US_AllisonV3Voice`）中包含版本字串 (`V3`)。與依賴於語音區段選擇和拼接不同，神經語音技術使用多個深度神經網路 (DNN) 來預測語音的聲學（譜）特性。DNN 根據自然人語音進行訓練，並根據預測的聲學特性產生相應的音訊。

在合成期間，DNN 會預測語音的音高和標音持續時間（韻律）、音譜結構和波形。神經語音會產生清脆而清楚的語音，且音訊品質會聽起來很自然平順。因此，神經語音在整體品質上比標準語音具有更高的一致性。

如需服務神經語音技術的相關資訊，請參閱

-   部落格文章 [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   研究論文 [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

神經語音不支援下列 SSML 元素或屬性：

-   `<prosody>` 元素的 `volume` 屬性
-   `<express-as>` 元素
-   `<voice-transformation>` 元素

但是，您可能發現在使用神經語音時，不再需要這些 SSML 特性。此外，您可以藉由使用 `<prosody>` 元素取代 `<voice-transformation>` 元素，對神經語音進行音高和語速修改。如需相關資訊，請參閱 [prosody 元素](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element)。

### 語音自訂作業
{: #customizeVoice}

當您合成文字時，服務會套用和語言有關的發音規則，將每個字組的普通拼字轉換為語音拼字。服務的發音規則非常適用於常用字組，但它們可能會針對不常用的字組（例如含有外來語、個人姓名和縮寫或字首語的術語）產生不完美的結果。

如果應用程式的辭彙包含這類字組，您可以使用自訂作業介面來指定服務對於這類字組如何發音。如需相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。

您為特定語言而非特定語音建立自訂語音模型。因此，自訂模型可搭配以指定語言提供的任何語音（標準或神經）使用。

## 指定語音
{: #specifyVoice}

HTTP `GET` 和 `POST /v1/synthesize` 方法，以及 WebSocket `/v1/synthesize` 方法，都接受選用性的 `voice` 查詢參數，以指定合成音訊的語音。如需相關資訊，請參閱 [HTTP 介面](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP)及 [WebSocket 介面](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket)。

服務對於輸入文字之語言的瞭解，是以所指定的語音為基礎。請務必指定與輸入文字之語言相符的語音。例如，如果您指定法文語音 (`fr-FR_ReneeVoice`)，則服務假設輸入文字是以法文撰寫。如果您傳遞的文字不是以語音的語言撰寫（例如，英文文字配上法文語音），則服務可能無法產生有意義的結果。

## 列出所有可用的語音
{: #listVoices}

`GET /v1/voices` 方法列出所有可用語音的相關資訊。它不接受任何引數，且會傳回名稱為 `voices` 的 JSON 陣列。陣列包含每個語音的個別物件。

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

語音物件的欄位提供下列資訊：

-   `name` 是語音 ID（例如 `en-US_LisaVoice`）。請對 `/v1/synthesize` 方法的 `voice` 參數指定此值。
-   `language` 指定語音的語言和地區（例如 `en-US`）。
-   `gender` 會將語音識別為 `male` 或 `female`。
-   `url` 識別語音的 URL。
-   `description` 提供語音的簡要說明。
-   `customizable` 是布林值，指出是否可以利用服務的自訂作業介面來自訂語音。（此欄位提供與 `custom_pronunciation` 欄位相同的資訊，並且會受到維護以保持舊版相容性。）
-   `supported_features` 說明語音所支援的其他服務特性：
    -   `voice_transformation` 是布林值，指出是否可以利用 SSML `<voice-transformation>` 元素來轉換語音。
    -   `custom_pronunciation` 是布林值，指出是否可以利用服務的自訂作業介面來自訂語音。

## 列出特定語音
{: #listVoice}

`GET /v1/voices/{voice}` 方法會列出特定語音的相關資訊。它接受兩個參數。

<table>
  <caption>表 2. <code>voices</code> 方法的參數</caption>
  <tr>
    <th style="text-align:left; width:18%">參數</th>
    <th style="text-align:center; width:12%">類型</th>
    <th style="text-align:center; width:12%">資料類型</th>
    <th style="text-align:left">說明</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>必要</em></td>
    <td style="text-align:center">路徑</td>
    <td style="text-align:center">字串</td>
    <td>
      識別要傳回其資訊的語音。請依語音名稱來指定語音（例如 <code>en-US_LisaVoice</code>）。
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>選用</em></td>
    <td style="text-align:center">查詢</td>
    <td style="text-align:center">字串</td>
    <td>
      針對為指定語音之語言而定義的自訂語音模型，提供廣域唯一 ID (GUID)。如果您包含了自訂作業 ID，則必須使用擁有自訂模型之服務實例的認證來提出要求。</td>
  </tr>
</table>

如果您省略 `customization_id` 參數，則方法會傳回所指定語音的 JSON 輸出，而這與 `GET /v1/voices` 方法針對語音所傳回的資訊相同。如果您指定 `customization_id`，則輸出會包含一個 `customization` 欄位，其中提供所指定自訂語音模型的相關資訊。

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

其他 `customization` 欄位的屬性提供例如自訂語音模型的 GUID、名稱、語言和說明等資訊。此外，還會顯示模型擁有者的認證、建立模型的日期和時間，以及前次修改模型的日期和時間。
