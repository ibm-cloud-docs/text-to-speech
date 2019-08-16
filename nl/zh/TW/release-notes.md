---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-30"

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

# 版本注意事項
{: #release-notes}

下列各節記載了對於每個版本所包括的新特性及變更，以及 {{site.data.keyword.texttospeechfull}} 服務的更新。此資訊包括所有已知限制。除非另有說明，否則所有變更都與舊版相容，且會自動且透通地適用於所有新的及現有應用程式。
{: shortdesc}

## 已知限制
{: #limitations}

目前沒有已知限制。

## 2019 年 7 月 30 日
{: #July2019}

該服務現在提供日文的神經語音：`ja-JP_EmiV3Voice`。現在所有受支援語言中均同時提供所有可用語音的標準和神經版本。如需相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。

## 2019 年 6 月 24 日
{: #June2019}

-   該服務現在為其大部分可用的語音提供兩個版本：
    -   [標準語音](/docs/services/text-to-speech?topic=text-to-speech-voices#standardVoices)，使用拼接合成技術來組合錄製的語音區段，以產生音訊。標準語音的名稱（例如，`en-US_AllisonVoice`）中不包含版本字串。
    -   [神經語音](/docs/services/text-to-speech?topic=text-to-speech-voices#neuralVoices)，使用深層神經網路 (DNN) 來預測語音的聲學（譜）特性。神經語音的名稱（例如，`en-US_AllisonV3Voice`）中包含版本字串 (`V3`)。

    增強的神經版本可用於除 `ja-JP_EmiVoice` 語音之外的所有標準語音，該語音處於擱置狀態，即將可用。您無法將 SSML `<express-as>` 和 `<voice-transformation>` 元素用於神經語音，並且無法將 `<prosody>` 元素的 `volume` 屬性用於神經語音。

    如需所有可用語音的相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。
-   服務不再包含先前可用的 `V2` DNN 語音。如果您在應用程式中使用 `V2` 語音，服務會自動改用相等的 `V3` 語音。

## 2019 年 3 月 24 日
{: #March2019c}

-   現在，服務可提供其德文語音的 `V2` 深度神經網路 (DNN) 版本：
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

    如需以 DNN 為基礎之語音的相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。
-   服務的所有以 DNN 為基礎的語音現在支援 SSML `<prosody>` 元素的 `pitch` 和 `rate` 屬性。以 DNN 為基礎的語音不支援 `<prosody>` 元素的 `volume` 屬性。如需相關資訊，請參閱 [prosody 元素](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element)。

## 舊版本
{: #older}

-   [2019 年 3 月 21 日](#March2019b)
-   [2019 年 3 月 4 日](#March2019a)
-   [2019 年 1 月 28 日](#January2019)
-   [2018 年 12 月 13 日](#December2018)
-   [2018 年 11 月 7 日](#November2018)
-   [2018 年 10 月 30 日](#October2018)
-   [2018 年 6 月 12 日](#June2018)
-   [2018 年 5 月 15 日](#May2018)
-   [2017 年 10 月 2 日](#October2017)
-   [2017 年 7 月 14 日](#July2017)
-   [2017 年 4 月 10 日](#April2017)
-   [2016 年 12 月 1 日](#December2016)
-   [2016 年 9 月 22 日](#September2016)
-   [2016 年 6 月 23 日](#June2016)
-   [2016 年 3 月 10 日](#March2016)
-   [2016 年 2 月 22 日](#February2016)
-   [2015 年 12 月 17 日](#December2015)
-   [2015 年 9 月 21 日](#September2015)
-   [2015 年 7 月 1 日](#July2015)

### 2019 年 3 月 21 日
{: #March2019b}

現在，使用者可以只查看與已指派給其 {{site.data.keyword.cloud_notm}} 帳戶之角色相關聯的服務認證資訊。例如，如果您已獲指派 `reader` 角色，則再也看不到任何 `writer` 或更高層次的服務認證。

此變更不會影響含現有服務認證之使用者或應用程式的 API 存取權。此變更只會影響在 {{site.data.keyword.cloud_notm}} 內檢視認證。

如需服務金鑰和使用者角色的相關資訊，請參閱 [IAM 服務 API 金鑰](/docs/services/watson?topic=watson-api-key-bp#api-key-bp)。

### 2019 年 3 月 4 日
{: #March2019a}

現在，服務提供了四個新的 `V2` 語音，這些語音使用深度學習合成來產生音訊：

-   `it-IT_FrancescaV2Voice`
-   `en-US_AllisonV2Voice`
-   `en-US_LisaV2Voice`
-   `en-US_MichaelV2Voice`

這些新的語音會使用機器學習和 DNN 來將文字合成為語音。深度學習或以深度神經網路 (DNN) 為基礎的合成會產生韻律更自然且整體品質更一致的音訊。

但是，新語音也會產生信號品質與現有語音不同的音訊，因此它們可能不適用於所有應用程式。此外，新語音不支援 SSML 元素 `<prosody>`、`<express-as>` 及 `<voice-transformation>`。

如需這些以 DNN 基礎之語音及其與現有語音有何差異的相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。

### 2019 年 1 月 28 日
{: #January2019}

WebSocket 介面現在支援瀏覽器型 JavaScript 程式碼中的記號型 Identity and Access Management (IAM) 鑑別。已移除相反的限制。若要建立與 WebSocket `/v1/synthesize` 方法的已鑑別連線，請執行下列動作：

-   如果您使用 IAM 鑑別，請包含 `access_token` 查詢參數。
-   如果您使用 Cloud Foundry 服務認證，請包含 `watson-token` 查詢參數。

如需相關資訊，請參閱[開啟連線](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket#WSopen)。

### 2018 年 12 月 13 日
{: #December2018}

{{site.data.keyword.cloud}} 倫敦位置 (**eu-gb**) 現在可以使用 {{site.data.keyword.texttospeechshort}} 服務。與所有位置類似，倫敦會使用記號型 Identity and Access Management (IAM) 鑑別。所有在這個位置中建立的新服務實例都會使用 IAM 鑑別。

### 2018 年 11 月 7 日
{: #November2018}

{{site.data.keyword.cloud}} 東京位置 (**jp-tok**) 現在可以使用 {{site.data.keyword.texttospeechshort}} 服務。與所有位置類似，東京會使用記號型 Identity and Access Management (IAM) 鑑別。所有在這個位置中建立的新服務實例都會使用 IAM 鑑別。

### 2018 年 10 月 30 日
{: #October2018}

所有位置的 {{site.data.keyword.texttospeechshort}} 服務都已移轉至記號型 Identity and Access Management (IAM) 鑑別。所有 {{site.data.keyword.cloud_notm}} 服務現在都會使用 IAM 鑑別。每個位置已在下列日期移轉 {{site.data.keyword.texttospeechshort}} 服務：

-   達拉斯 (**us-south**)：2018 年 10 月 30 日
-   法蘭克福 (**eu-de**)：2018 年 10 月 30 日
-   華盛頓特區 (**us-east**)：2018 年 6 月 12 日
-   雪梨 (**a-syd**)：2018 年 5 月 15 日

移轉至 IAM 鑑別會對新的和現有的服務實例產生不同的影響：

-   *所有您在任何位置建立的新服務實例* 現在都會使用 IAM 鑑別來存取服務。您可以傳遞載送記號或 API 金鑰：記號支援已鑑別要求，無需在每個呼叫中內嵌服務認證；API 金鑰會使用 HTTP 基本鑑別。當您使用任何 {{site.data.keyword.ibmwatson}} SDK 時，可以傳遞 API 金鑰，並讓 SDK 管理記號的生命週期。
-   *在指出的移轉日期之前於位置中建立的現有服務實例* 會繼續使用其先前 Cloud Foundry 服務認證中的 `{username}` 及 `{password}` 進行鑑別，直到您移轉它們以使用 IAM 鑑別為止。如需移轉至 IAM 鑑別的相關資訊，請參閱[將 Cloud Foundry 服務實例移轉至資源群組](https://{DomainName}/docs/resources?topic=resources-migrate)。

如需相關資訊，請參閱下列文件：

-   若要瞭解您服務實例所使用的鑑別機制，請在 [{{site.data.keyword.cloud_notm}} 儀表板](https://{DomainName}/dashboard/apps){: external}上按一下實例來檢視服務認證。
-   如需搭配使用 IAM 記號與 {{site.data.keyword.watson}} 服務的相關資訊，請參閱[使用 IAM 記號鑑別](/docs/services/watson?topic=watson-iam)。
-   如需搭配使用 IAM API 金鑰與 {{site.data.keyword.watson}} 服務的相關資訊，請參閱 [IAM 服務 API 金鑰](/docs/services/watson?topic=watson-api-key-bp)。
-   如需使用 IAM 鑑別的範例，請參閱 [API 參考資料](https://{DomainName}/apidocs/text-to-speech){: external}。

### 2018 年 6 月 12 日
{: #June2018}

對於華盛頓特區 (**us-east**) 所管理的應用程式，已啟用下列特性：

-   服務現在支援新的 API 鑑別處理程序。如需相關資訊，請參閱 [2018 年 10 月 30 日服務更新](#October2018)。
-   服務現在支援 `X-Watson-Metadata` 標頭和 `DELETE /v1/user_data` 方法。如需相關資訊，請參閱[資訊安全](/docs/services/text-to-speech?topic=text-to-speech-information-security)。

### 2018 年 5 月 15 日
{: #May2018}

對於雪梨 (**au-syd**) 所管理的應用程式，已啟用下列特性：

-   服務現在支援新的 API 鑑別處理程序。如需相關資訊，請參閱 [2018 年 10 月 30 日服務更新](#October2018)。
-   服務現在支援 `X-Watson-Metadata` 標頭和 `DELETE /v1/user_data` 方法。如需相關資訊，請參閱[資訊安全](/docs/services/text-to-speech?topic=text-to-speech-information-security)。

### 2017 年 10 月 2 日
{: #October2017}

若為 `audio/l16` 格式，您現在可以選擇性地指定所傳回之音訊的排列法。（您必須已指定取樣率。）範例為 `audio/l16;rate=22050;endianness=big-endian` 和 `audio/l16;rate=22050;endianness=little-endian`；預設值是大序排列法。如需相關資訊，請參閱[音訊格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。

### 2017 年 7 月 14 日
{: #July2017}

服務現在支援 MP3 或 Motion Picture Experts Group (MPEG) 音訊格式。如需所支援音訊格式的相關資訊，請參閱[音訊格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。

### 2017 年 4 月 10 日
{: #April2017}

-   服務現在支援搭配使用 Opus 或 Vorbis 轉碼器的「Web 媒體 (WebM)」音訊格式。除了 Opus 轉碼器之外，服務現在還支援搭配使用 Vorbis 轉碼器的 Ogg 音訊格式。如需所支援音訊格式的相關資訊，請參閱[音訊格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。
-   服務現在支援「跨原點資源共用 (CORS)」，以容許瀏覽器型用戶端直接呼叫服務。如需相關資訊，請參閱 [CORS 支援](/docs/services/text-to-speech?topic=text-to-speech-overview#cors)。
-   順利完成自訂作業介面之某些方法的 HTTP 回應碼已變更：
    -   `POST /v1/customizations` 方法現在傳回 201（而非 200）。
    -   `POST /v1/customizations/{customization_id}` 方法現在傳回 200（而非 201）。
    -   `POST /v1/customizations/{customization_id}/words` 方法現在傳回 200（而非 201）。
    -   `PUT /v1/customizations/{customization_id}/words/{word}` 方法現在傳回 200（而非 201）。
-   如果您嘗試為日文以外的語言指定 `part_of_speech`，`POST /v1/customizations/{custom_id}/words` 及 `PUT /v1/customizations/{customization_id}/words/{word}` 方法現在會傳回 HTTP 回應碼 400，並顯示錯誤訊息 `Part of speech is supported for ja-JP language only`。
-   `POST /v1/customizations/{custom_id}/words` 方法現在傳回空的回應內文 (`{}`)。

### 2016 年 12 月 1 日
{: #December2016}

-   服務包括新的語音 `es-LA_SofiaVoice`，這是與 `es-US_SofiaVoice` 語音對等的拉丁美洲語音。這兩個語音之間的最主要差異在於它們解譯 `$`（錢幣符號）的方式：拉丁美洲版本使用*披索* 一詞，而北美版本則使用*美元* 一詞。這兩個語音之間也可能存在其他次要差異。
-   除了 `en-US_AllisonVoice` 之外，還有兩個語音現在可利用 SSML 語音轉換進行轉換：`en-US_LisaVoice` 和 `en-US_MichayVoice`。如需語音轉換的相關資訊，請參閱[語音轉換 SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation)。
-   當您使用自訂作業介面與日文搭配時，服務現在會比對字組/轉換配對中的最長字組，而這些轉換是針對自訂語音模型而定義的。例如，考量自訂語音的下列兩個項目：

    <pre><code data-copy="false" class="language-javascript">  {
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    如果服務在輸入文字中找到 <code>&#65326;&#65337;&#65315;</code> 字串，則它會比對該字組，因為它是長度超過 <code>&#65326;&#65337;</code> 的相符項。先前，服務將已比對字串 <code>&#65326;&#65337;</code>。如需針對自訂語音模型使用日文項目的相關資訊，請參閱[使用日文項目](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes)。

### 2016 年 9 月 22 日
{: #September2016}

-   自訂作業介面（包括自訂作業及 `GET /v1/pronunciation` 方法）現在可用於服務所支援的所有語言。此介面仍為測試版。如需相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。
-   服務現在支援日文的「語音合成標記語言 (SSML)」。如需關於 SSML 支援的一般資訊，請參閱[使用 SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml)。如需日文 SPR 和 IPA 符號的相關資訊，請參閱[日文符號](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols)。在日文自訂語音模型中建立字組的項目時，額外考量和 `part_of_speech` 欄位適用。如需相關資訊，請參閱[使用日文項目](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes)。
-   服務現在透過新的 `<voice-transformation>` 元素提供 SSML 語音轉換。您可以藉由建立自訂語音轉換來擴大可能的語音範圍，這些轉換會修改語音的音高、音高範圍、聲門張力、呼吸聲、速度及音色。服務也會提供兩個內建虛擬語音，即 *Young* 和 *Soft*。服務目前僅支援美式英文 Allison 語音的語音轉換。如需相關資訊，請參閱[語音轉換 SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation)。
-   服務現在可以為您傳遞至 WebSocket 介面之輸入文字的所有字串傳回字組計時資訊。若要接收輸入中每個字串的開始和結束時間，請針對您傳遞至服務之 JSON 物件的選用 `timings` 參數指定包括字串 `words` 的陣列。此特性目前無法用於日文輸入文字。如需相關資訊，請參閱[取得字組計時](/docs/services/text-to-speech?topic=text-to-speech-timing)。
-   服務現在會驗證您在任何環境定義中提交的所有 SSML 元素。如果它找到無效的標籤，則服務會報告 HTTP 400 回應碼，並顯示敘述性訊息，而且方法會失敗。在舊版中，服務以不一致方式處理錯誤；例如，指定無效的字組發音，可能導致無法預期或不一致的行為。如需相關資訊，請參閱 [SSML 驗證](/docs/services/text-to-speech?topic=text-to-speech-ssml#errors)。
-   已淘汰使用 `spr` 作為 `GET /v1/pronunciation` 方法之 `format` 選項的引數，以及搭配使用 `<phoneme>` 元素的 `alphabet` 屬性。若要使用「{{site.data.keyword.IBM_notm}} 符號語音表示法 (SPR)」，請在所有情況下使用 `ibm` 引數，而非 `spr`。
-   支援的音訊格式清單現在包括 `audio/mulaw;rate=8000`。與 `audio/basic` 類似，此格式提供單一頻道音訊，它是使用取樣率為 8 kHz 的 8 位元 u-law（或 mu-law）資料進行編碼的。如需相關資訊，請參閱[音訊格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。
-   `GET /v1/voices` 及 `GET /v1/voices/{voice}` 方法現在會傳回 `supported_features` 物件，作為每個語音之輸出的一部分。此物件說明語音是否支援自訂作業及 SSML `<voice_transformation>` 元素。如需相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。

### 2016 年 6 月 23 日
{: #June2016}

-   服務現在提供可將文字合成為語音的 WebSocket 介面。此介面提供與 HTTP 介面的 `/v1/synthesize` 方法相同的特性。它接受純文字或以 SSML 標註的文字。此外，它還支援使用 SSML `<mark>` 元素，來識別音訊中其完成合成標記之前所有文字的時間。如需相關資訊，請參閱 [WebSocket 介面](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket)。
-   對於卡斯提亞語以及北美洲西班牙文、義大利文及巴西葡萄牙文等語言，服務現在提供以 SSML 標註之文字的支援。服務已支援針對美式和英式英文、法文及德文使用 SSML。根據此更新，服務支援所有語言的 SSML，但日文除外。此外，您可以同時使用 {{site.data.keyword.IBM_notm}} SPR 及 IPA 表示法，搭配使用 SSML `<phoneme>` 元素來定義字組發音。如需相關資訊，請參閱[使用 SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml) 及 [使用 IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs)。

    若為美式英文，您也可以使用 SSML `<phoneme>` 元素，在自訂語音模型中建立字組項目；僅美式英文支援自訂作業。如需相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。
    -   服務特性已改善最常用語音的表達及自然度。這些改善會根據輸入文字的「遞迴神經網路 (RNN)」韻律預測。它們可用作下列語言的新服務引擎及語音模型更新：

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   `GET /v1/pronunciation` 方法現在接受選用的 `customization_id` 查詢參數。此參數會從指定的自訂語音模型中取得字組轉換。如果語音模型未包含字組，則此方法會傳回字組的預設發音。如需相關資訊，請參閱 [API 參考資料](https://{DomainName}/apidocs/text-to-speech){: external}。

    在沒有自訂作業 ID 的情況下使用 `GET /v1/pronunciation` 方法，以及對美式英文以外的語言使用此方法時，您只能在 {{site.data.keyword.IBM_notm}} SPR 表示法中要求字組的發音。對於美式英文以外的語言，您必須使用方法的 `format` 選項來指定 `spr`。
    {: note}
-   支援的音訊格式清單現在包括提供單一頻道音訊的 `audio/basic`，此音訊是使用取樣率為 8 kHz 的 8 位元 u-law（或 mu-law）資料進行編碼的。如需相關資訊，請參閱[音訊格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。
-   HTTP 和 WebSocket `/v1/synthesize` 方法可以傳回 `warnings` 回應，其中包括要求所隨附之無效查詢參數或 JSON 欄位的相關訊息。警告的格式已變更。下列範例顯示先前的格式：

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    相同的警告現在具有下列格式：

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

### 2016 年 3 月 10 日
{: #March2016}

-   `GET` 和 `POST /v1/synthesize` 方法現在可以傳回 `Warnings` 回應標頭，其中包括一個清單，列出要求所隨附之無效查詢參數或 JSON 欄位的相關警告訊息。清單的每個元素都包括一個字串，說明警告的本質，後面接著無效引數字串的陣列；例如，`Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']`。如需相關資訊，請參閱 [API 參考資料](https://{DomainName}/apidocs/text-to-speech){: external}。
-   適用於 Apple&reg; iOS 作業系統的測試版 *{{site.data.keyword.watson}} Speech Software Development Kit (SDK)* 已淘汰，並被 *{{site.data.keyword.watson}} Swift SDK* 取代。新的 SDK 可從 GitHub 上 `watson-developer-cloud` 名稱空間的 [swift-sdk 儲存庫](https://github.com/watson-developer-cloud/swift-sdk){: external}中獲取。

### 2016 年 2 月 22 日
{: #February2016}

已使用新的表達 SSML 特性更新服務。服務會使用 `<express-as>` 元素來擴充「語音合成標記語言 (SSML)」，您可以用來指出下列三種說話風格之一的表達：`GoodNews`、`Apology` 或 `Uncertainty`。您可以將此元素套用至整個文字內文、句子、詞組或字組。服務目前僅支援美式英文 Allison 語音 (`en-US_AllisonVoice`) 的表達。如需相關資訊，請參閱[表達 SSML](/docs/services/text-to-speech?topic=text-to-speech-expressive)。

### 2015 年 12 月 17 日
{: #December2015}

-   服務提供新的自訂作業介面，您可以用來指定其如何對輸入中出現的不尋常字組發音。此介面包括一些新方法，您可以用來建立及管理自訂語音模型，以及它們所包含的字組/轉換配對。然後，您可以在將文字合成為音訊時使用自訂模型。

    服務支援類似音轉換及語音轉換。語音轉換可以使用標準「國際音標 (IPA)」表示法，或專用的「{{site.data.keyword.IBM_notm}} 符號語音表示法 (SPR)」。您可以使用「語音合成標記語言 (SSML)」來指定語音轉換。

    自訂作業介面包括新的 HTTP 方法集合，這些方法具有名稱 `POST /v1/customizations`、`POST /v1/customizations/{customization_id}`、`POST /v1/customizations/{customization_id}/words` 及 `PUT /v1/customizations/{customization_id}/words/{word}`。服務也會提供新的 `GET /v1/pronunciation` 方法，用於傳回任何字組的發音，並且提供新的 `GET /v1/voices/{voice}` 方法，用於傳回特定語音的詳細資訊。此外，服務介面的現有方法現在可視需要接受自訂語音模型參數。

    如需自訂作業及其介面的相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech?topic=text-to-speech-customIntro)和 [API 參考資料](https://{DomainName}/apidocs/text-to-speech){: external}。

    自訂作業介面是測試版，目前僅支援美式英文。所有自訂作業方法及 `GET /v1/pronunciation` 方法，目前都可用來建立及操作自訂語音模型和字組轉換（僅限美式英文）。
    {: note}
-   服務支援新語音 `pt-BR_IsabelaVoice`，利用女性語音將音訊合成為巴西葡萄牙文。如需相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。

### 2015 年 9 月 21 日
{: #September2015}

-   提供了兩個新的測試版行動「軟體開發套件 (SDK)」供語音服務使用。這些 SDK 可讓行動應用程式與 {{site.data.keyword.texttospeechshort}} 及 {{site.data.keyword.speechtotextshort}} 服務兩者互動。您可以使用 SDK，將文字傳送至 {{site.data.keyword.texttospeechshort}} 服務，以及接收音訊回應。
    -   *{{site.data.keyword.watson}} Swift SDK* 可從 GitHub 上 `watson-developer-cloud` 名稱空間的 [swift-sdk 儲存庫](https://github.com/watson-developer-cloud/swift-sdk){: external}中獲取。
    -   *{{site.data.keyword.watson}} Speech Android SDK* 可從 GitHub 上 `watson-developer-cloud` 名稱空間的 [speech-android-sdk 儲存庫](https://github.com/watson-developer-cloud/speech-android-sdk){: external}中獲取。

    這兩個 SDK 都會使用您的 {{site.data.keyword.cloud_notm}} 服務認證或鑑別記號，來支援使用語音服務進行鑑別。

    因為 SDK 是測試版功能，所以在日後可能會變更。
    {: note}
-   服務支援新語言 - 日文。語音 `ja-JP_EmiVoice` 是日文女性語音。

### 2015 年 7 月 1 日
{: #July2015}

服務已在 2015 年 7 月 1 日從測試版移至通用版 (GA)。{{site.data.keyword.texttospeechshort}} API 的測試版與 GA 版本之間存在下列差異。GA 版本需要使用者升級至新的服務版本。

-   新的程式設計模型支援用戶端與服務之間的直接互動。使用此模型，用戶端可以取得鑑別記號，以直接與服務進行通訊。使用記號，用戶端即可略過 {{site.data.keyword.cloud_notm}} 中的伺服器端 Proxy 應用程式代表它呼叫服務的需求。記號是用戶端與服務互動的偏好方法。

    服務會繼續支援根據伺服器端 Proxy 的舊程式設計模型，以轉遞用戶端與服務之間的通訊及資料。但是，新模型更有效率，且提供更高的傳輸量。
-   您現在可以將「語音合成標記語言 (SSML)」傳遞至 `GET` 和 `POST` 版本的 `/v1/syntheingsize` 方法。SSML 是 XML 型標記語言，其設計旨在為語音合成應用程式（例如 {{site.data.keyword.texttospeechshort}} 服務）提供文字註釋。如需將 SSML 輸入傳遞至服務的相關資訊，請參閱[指定輸入文字](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#input)。

    服務最初僅支援對英式及美式英文、法文及德文語言使用 SSML。服務不支援將 SSML 與義大利文及西班牙文搭配使用。使用 SSML 時，請確定您未以其中一種不支援的語言選取音訊的語音。在此情況下，結果沒有意義。
-   合成語音支援的語音已變更並擴充。服務現在支援將一些額外的語音、語言及用語與 `/v1/synthesize` 方法搭配使用。如需支援之語音的相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。

    對於 GA，已重新命名測試版中提供的三種語音：
    -   `VoiceEnUsMichael` 現在為 `en-US_MichaelVoice`
    -   `VoiceEnUsLisa` 現在為 `en-US_LisaVoice`
    -   `VoiceEsEsEnrique` 現在為 `es-ES_EnriqueVoice`

    語音的先前名稱會繼續使用服務的測試版（透過 `-beta` API 端點），若該版本仍然可用的話。不過，您必須使用新名稱與服務的 GA 版本搭配。
-   您現在可以要求服務以「自由無損音訊轉碼器 (FLAC)」格式傳回音訊。服務仍然可以 Ogg 格式搭配使用 Opus 轉碼器（預設值），以及以 Waveform Audio File Format (WAV) 傳回音訊。如需使用音訊格式與 `/v1/syntheingsize` 方法搭配的相關資訊，請參閱[音訊格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。
-   您在 HTTP `GET` 要求的 URL 中，或在 HTTP `POST` 要求的內文中傳送至 `/v1/synthesize` 方法的文字現在限制為最大 5 KB。測試版文字的大小上限為 4 MB。
-   `/v1/synthesize` 方法現在包括標頭 `X-WDC-PL-OPT-OUT`，用來控制服務是否使用作業中的文字及音訊結果來改善未來結果。為標頭指定值 `1`，以防止服務使用文字及音訊結果。此參數僅適用於現行要求。新標頭會取代測試版方法中的 `X-logging` 標頭。如需相關資訊，請參閱[控制 {{site.data.keyword.watson}} 服務的要求記載](/docs/services/watson?topic=watson-gs-logging-overview)。
-   若為 `/v1/synthesize` 方法，下列錯誤碼已變更：
    -   已移除錯誤碼 406（「無法接受。不受支援的 MIME 類型。」）。
    -   已新增錯誤碼（「不受支援的媒體類型」）。
    -   已新增錯誤碼 503（「服務無法使用」）。
-   若為 `GET /v1/voices` 方法，下列錯誤碼已變更：
    -   已移除錯誤碼 406（「無法接受。不受支援的 MIME 類型。」）。
    -   已新增錯誤碼（「不受支援的媒體類型」）。
