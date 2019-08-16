---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-06"

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

# 開發人員概觀
{: #overview}

您可以透過「HTTP 具象狀態傳輸 (REST)」API 或 WebSocket 介面，來存取 {{site.data.keyword.texttospeechfull}} 服務的語音合成功能。還提供了數個「軟體開發套件 (SDK)」，用來簡化各種程式設計語言中的應用程式開發。下列各節提供了使用服務進行應用程式開發的概觀。
{: shortdesc}

## HTTP 介面
{: #overview-http}

若要使用 HTTP API　合成文字，請呼叫服務之 `/v1/synthesize` 方法的 `GET` 或 `POST` 版本。此方法的這兩種版本提供一般而言相等的功能：

-   *輸入文字：*您可以傳遞要以兩種不同方式合成的輸入文字：
    -   `GET /v1/synthesize` 方法接受輸入文字作為查詢參數。要求的大小上限為 8 KB，其中包含輸入文字及 URL 和標頭。
    -   `POST /v1/synthesize` 方法接受要求內文中的輸入文字。若為 URL 和標頭，要求的大小上限為 8 KB，若為要求內文中傳送的輸入文字，則為 5 KB。

    您可以傳遞純文字給服務，或傳遞使用「語音合成標記語言 (SSML)」標註的文字給服務。SSML 是 XML 型標記語言，可為語音合成應用程式（例如 {{site.data.keyword.texttospeechshort}} 服務）提供文字註釋。服務會利用服務特有的表達及語音轉換元素來擴增 SSML，這些元素可用於某些標準美式英文語音。

    如需相關資訊，請參閱[指定輸入文字](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#input)。
-   *語音：* 服務接受文字並以各種語言、語音及用語來產生音訊。服務針對每種語言至少提供一個女性語音。針對部分語言，服務提供多種語音，可能同時包括男性和女性語音。服務也會提供不同的用語，例如美式英文和英式英文。對於大部分語音，同時提供標準（拼接）和增強的神經版本。

    您可以使用服務的 `GET /v1/voices` 或 `GET /v1/voices/{voice}` 方法，進一步瞭解支援的語音。此服務會將文字合成為指定語音的語言。請務必讓語音符合輸入文字。

    如需相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。
-   *音訊格式：* 服務可以產生下列格式的音訊：Ogg 或「Web 媒體 (WebM)」格式搭配使用 Opus（預設值）或 Vorbis 轉碼器、MP3（Motion Picture Experts Group 或 MPEG）格式、Waveform Audio File Format (WAV)、「自由無損音訊轉碼器 (FLAC)」、「線性 16 位元脈衝編碼調變 (PCM)」、8 位元 mu-law (u-law)，或基本音訊。

    如需相關資訊，請參閱[音訊格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。

## WebSocket 介面
{: #overview-websocket}

服務會提供您可以用來合成文字的 WebSocket 介面。此介面提供 `/v1/synthesize` 方法的單一版本，最多可接受 5 KB 的輸入文字。請指定要合成的文字、要使用的語音，以及音訊的格式。您可以提供純文字或使用 SSML 標註的文字。如需相關資訊，請參閱 [WebSocket 介面](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket)。

WebSocket 介面支援使用 SSML `<mark>` 元素來識別音訊中的特定位置。您也可以針對輸入文字的所有字組要求字組計時資訊。如需相關資訊，請參閱[取得字組計時](/docs/services/text-to-speech?topic=text-to-speech-timing)。

## 自訂作業介面
{: #overview-customization}

服務包含自訂作業介面，您可以用來建立自訂語音模型，以在語音合成期間使用。自訂語音模型是特定語言之字組及其轉換的字典。模型中的每個字組/轉換配對都會告訴服務在輸入文字中出現該字組時如何發音。

您可以使用自訂語音模型，針對服務的一般發音規則可能產生不完美發音的不常用字組，建立應用程式特定的轉換。您可以用標準「國際音標 (IPA)」表示法，或專屬「{{site.data.keyword.IBM_notm}} 符號語音表示法 (SPR)」，定義字組/轉換配對的自訂項目。

例如，您的應用程式可能會例行地遇到含有外來語、個人姓名或地理名稱，或是縮寫及字首語等等的特殊術語。藉由使用自訂作業，您可以定義轉換來告訴服務您想要如何針對這類術語發音。如需相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。

自訂作業介面是測試版。此外，您必須具有標準定價方案，才能使用語音模型自訂作業。精簡方案的使用者無法使用自訂作業介面。如需相關資訊，請參閱 {{site.data.keyword.texttospeechshort}} 服務的[定價頁面](https://www.ibm.com/cloud/watson-text-to-speech/pricing){: external}。
{: note}

## CORS 支援
{: #cors}

服務支援「跨原點資源共用 (CORS)」。使用 CORS，網頁可以直接從外來網域要求資源。CORS 會規避相同原點的安全原則，否則此原則會阻止這類要求。因為服務支援 CORS，所以網頁可以直接與服務通訊，而無需透過管理頁面的 Web 伺服器傳遞要求。

例如，從 {{site.data.keyword.cloud}} 中之伺服器載入的網頁，可以直接呼叫自訂作業 API，並略過 {{site.data.keyword.cloud_notm}} 伺服器。如需相關資訊，請參閱
      [enable-cors.org](https://enable-cors.org/){: external}。
    

## 使用軟體開發套件
{: #sdks}

SDK 可供 {{site.data.keyword.texttospeechshort}} 服務使用，以簡化語音應用程式的開發。許多熱門程式設計語言和平台都有可用的 {{site.data.keyword.ibmwatson}} SDK。

-   如需 SDK 及 GitHub 上之 SDK 鏈結的完整清單，請參閱[使用 SDK](/docs/services/watson?topic=watson-using-sdks)。
-   如需適用於 {{site.data.keyword.texttospeechshort}} 服務之所有 Node、Java&trade;、Python、Ruby、Swift 和 Go SDK 方法的詳細資訊，請參閱 [API 參考資料](https://{DomainName}/apidocs/text-to-speech){: external}。

## 進一步瞭解應用程式開發
{: #learn}

如需使用 {{site.data.keyword.watson}} 服務及 {{site.data.keyword.cloud_notm}} 的相關資訊，請參閱：

-   如需使用 {{site.data.keyword.watson}} 服務及 {{site.data.keyword.cloud_notm}} 的簡介，請參閱[開始使用 {{site.data.keyword.watson}} 和 {{site.data.keyword.cloud_notm}}](/docs/services/watson?topic=watson-about)。
-   所有新的服務實例都會使用 {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) 進行鑑別。較舊的服務實例可能繼續使用來自現有 Cloud Foundry 服務認證的 `{username}` 及 `{password}` 以進行鑑別。如需向服務進行鑑別的相關資訊，請參閱版本注意事項中的 [2018 年 10 月 30 日服務更新](/docs/services/text-to-speech?topic=text-to-speech-release-notes#October2018)。
-   如需控制針對所有 {{site.data.keyword.watson}} 服務執行之預設要求記載的相關資訊，請參閱[控制 {{site.data.keyword.watson}} 服務的要求記載](/docs/services/watson?topic=watson-gs-logging-overview)。
