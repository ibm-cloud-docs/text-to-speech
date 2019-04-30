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

# 語言與語音
{: #voices}

{{site.data.keyword.texttospeechfull}} 服務支援各種語言、語音及用語。此服務針對每種語言至少提供一個男性或女性語音（有時兩者）。每種語音都會針對其用語使用適當的抑揚頓挫和語調。
{: shortdesc}

## 支援的語言與語音
{: #languageVoices}

表 1 列出每種語言和用語的可用語音，包括其性別。如果您省略要求中的選用 `voice` 參數，則依預設此服務會使用 `en-US_MichayVoice` 語音。若要瞭解服務為何對部分語音提供兩種版本，請參閱[語音合成技術](#technologiesVoices)。

部署 `V2` 語音時發生的問題，目前在合成的語音中產生背景噪音。如需相關資訊，請參閱[已知限制](/docs/services/text-to-speech/release-notes.html#limitations)。
{: note}

<table style="width:90%">
  <caption>表 1. 支援的語言與語音</caption>
  <tr>
    <th style="text-align:left">語言</th>
    <th style="text-align:center">語音</th>
    <th style="text-align:center">性別</th>
  </tr>
  <tr>
    <td style="text-align:left">巴西葡萄牙文</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">卡斯提亞西班牙文</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">法文</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">德文</td>
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
    <td style="text-align:left">義大利文</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code><br/>
      <code>it-IT_FrancescaV2Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">日文</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">拉丁美洲西班牙文</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">北美洲西班牙文</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">英式英文</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">美式英文</td>
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

語音 `es-LA_SofiaVoice` 及 `es-US_SofiaVoice` 基本上是相同的語音。最主要差異在於這兩個語音解譯 $（錢幣符號）的方式。拉丁美洲版本使用*披索* 一詞，而北美洲版本則使用*美元* 一詞。這兩個語音之間也可能存在其他次要差異。
{: note}

### 語音合成技術
{: #technologiesVoices}

服務會對部分語音提供兩種版本，例如，`en-US_AllisonVoice` 和 `en-US_AllisonV2Voice`。這兩個版本之間的主要差異反映了服務用來合成語音的技術：

-   *連結式合成* 可組合所記錄語音的區段（或單位）來產生所要求的音訊。它產生的音訊可能被視為更清晰的聲音，但所記錄區段的連結點有時會產生語音失真。

    在其名稱中不包括字串 `V2` 的語音（例如，`en-US_AllisonVoice`）是以連結式合成為基礎。
-   *深度學習合成* 使用「深度神經網路 (DNN)」來合成所指定文字的語音。此方法不是將記錄的音訊區段串在一起，而是依靠機器學習，根據記錄的語音資料訓練 DNN。深度學習或 DNN 型合成會產生韻律更自然且整體品質更一致的音訊。

    在其名稱中包括字串 `V2` 的語音（例如，`en-US_AllisonV2Voice`）是使用 DNN 型合成的更新語音。

您需要先實驗新的語音，然後才能針對您的應用程式採用它們。這兩種技術會產生具有不同信號品質的音訊，因此，對於所有應用程式而言，新的語音不見得更好。此外，DNN 型語音不支援下列 SSML 元素或屬性：

-   `<prosody>` 元素的 `volume` 屬性
-   `<express-as>` 元素
-   `<voice-transformation>` 元素

如果您的應用程式使用這些元素，請繼續使用以連結式合成為基礎的語音。

### 語音自訂作業
{: #customizeVoice}

當您合成文字時，服務會套用語言相依的發音規則，將每個字組的普通拼字轉換為語音拼字。服務的發音規則非常適用於常用字組，但它們可能會針對不尋常的字組產生不完美的結果，例如，具有外來語、個人姓名和縮寫或字首語的術語。

如果應用程式的辭彙包含這類字組，您可以使用自訂作業介面來指定服務如何對它們發音。如需相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech/custom-intro.html)。

## 指定語音
{: #specifyVoice}

HTTP `GET` 和 `POST /v1/synthesize` 方法，以及 WebSocket `/v1/synthesize` 方法，都接受選用的 `voice` 查詢參數，以指定合成音訊的語音。如需相關資訊，請參閱 [HTTP 介面](/docs/services/text-to-speech/http.html)及 [WebSocket 介面](/docs/services/text-to-speech/websockets.html)。

服務會將其對輸入文字之語言的瞭解作為所指定語音的基礎。請務必指定與輸入文字之語言相符的語音。例如，如果您指定法文語音 (`fr-FR_ReneeVoice`)，則服務假設輸入文字是以法文撰寫。如果您傳遞的文字不是以語音的語言撰寫（例如，對法文語音使用英文文字），則服務可能不會產生有意義的結果。

## 列出所有可用的語音
{: #listVoices}

`GET /v1/voices` 方法列出所有可用語音的相關資訊。它不採用任何引數，且會傳回名為 `voices` 的 JSON 陣列。每個語音的陣列都包括個別物件。

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

-   `name` 是語音 ID（例如，`en-US_LisaVoice`）。請對 `/v1/synthesize` 方法的 `voice` 參數指定此值。
-   `language` 指定語音的語言和地區（例如，`en-US`）。
-   `gender` 會將語音識別為 `male` 或 `female`。
-   `url` 識別語音的 URL。
-   `description` 提供語音的簡要說明。
-   `customizable` 是布林值，指出是否可以利用服務的自訂作業介面來自訂語音。（此欄位會提供與 `custom_pronunciation` 欄位相同的資訊，以保持舊版相容性。）
-   `supported_features` 說明語音支援的其他服務特性：
    -   `voice_transformation` 是布林值，指出是否可以使用 SSML `<voice-transformation>` 元素來轉換語音。
    -   `custom_pronunciation` 是布林值，指出是否可以利用服務的自訂作業介面來自訂語音。

## 列出特定語音
{: #listVoice}

`GET /v1/voices/{voice}` 方法列出特定語音的相關資訊。它接受兩個參數。

<table>
  <caption>表 2. <code>Voices</code> 方法的參數</caption>
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
      識別要傳回其資訊的語音。您可以依語音名稱來指定語音（例如，<code>en-US_LisaVoice</code>）。
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>選用</em></td>
    <td style="text-align:center">查詢</td>
    <td style="text-align:center">字串</td>
    <td>
      提供針對所指定語音定義之自訂語音模型的廣域唯一 ID (GUID)。如果您包括自訂作業 ID，則必須使用自訂模型擁有者的服務認證來呼叫此方法。
    </td>
  </tr>
</table>

如果您省略 `customization_id` 參數，則此方法會傳回所指定語音的 JSON 輸出，此輸出與 `GET /v1/voice` 方法針對語音所傳回的資訊相同。如果您指定 `customization_id`，則輸出會包括 `customization` 欄位，其中提供所指定自訂語音模型的相關資訊。

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

其他 `customization` 欄位的屬性提供自訂語音模型的 GUID、名稱、語言和說明這類資訊。它們也會顯示模型擁有者的服務認證、建立模型的日期和時間，以及其前次修改的日期和時間。
