---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-03"

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# 入門指導教學
{: #gettingStarted}

{{site.data.keyword.texttospeechfull}} 服務會將書面文字轉換為自然發音的語音，以便為應用程式提供語音合成功能。本指導教學是以 curl 為基礎，可協助您快速開始使用服務。範例會顯示如何呼叫服務的 `POST` 和 `GET /v1/synthesize` 方法來要求音訊串流。
{: shortdesc}

## 開始之前
{: #before-you-begin}

- {: hide-dashboard}建立服務的實例：
    1.  {: hide-dashboard} 移至 {{site.data.keyword.cloud_notm}} 型錄中的 [{{site.data.keyword.texttospeechshort}}](https://{DomainName}/catalog/services/text-to-speech){: external} 頁面。
    1.  {: hide-dashboard}註冊免費的 {{site.data.keyword.cloud_notm}} 帳戶，或者登入。
    1.  {: hide-dashboard}按一下**建立**。
-   複製認證以便向服務實例進行鑑別：
    1.  {: hide-dashboard} 在 [{{site.data.keyword.cloud_notm}} 資源清單](https://{DomainName}/resources){: external}中，按一下 {{site.data.keyword.texttospeechshort}} 服務實例以移至 {{site.data.keyword.texttospeechshort}} 服務儀表板頁面。
    1.  在**管理**頁面上，按一下**顯示**以檢視您的認證。
    1.  複製 `API 金鑰`及 `URL` 值。

### 使用 curl 範例
{: #getting-started-curl}

本指導教學使用 `curl` 指令來呼叫服務的 HTTP 介面的方法。確保您的系統上已安裝 `curl` 指令。

1.  若要測試是否已安裝 `curl`，請在指令行上執行下列指令。如果輸出中列出支援 Secure Sockets Layer (SSL) 的 `curl` 版本，則您已準備好進行指導教學。

    ```bash
    curl -V
    ```
    {: pre}

1.  必要的話，請從 [curl.haxx.se](https://curl.haxx.se/){: external} 安裝適合您作業系統並且已啟用 SSL 的 `curl` 版本。

請省略範例中的大括弧。大括弧用於指示變數值。
{: tip}

## 步驟 1：合成美式英文的文字
{: #synthesizeEnglish}

下列指令使用 `POST /v1/synthesize` 方法，以兩種不同格式將美式英文輸入合成為音訊檔。這兩個要求皆會使用預設美式英文語音 `en-US_MichaelVoice`。

1.  發出下列指令來合成 "hello world" 字串，並產生名稱為 `hello_world.wav` 的 WAV 檔案。
    -   {: hide-dashboard} 將 `{apikey}` 和 `{url}` 取代為您的 API 金鑰及 URL。

    *Windows 使用者，*將每行結尾的反斜線 (`\`) 取代為脫字符號 (`^`)。請確定沒有尾端空格。
    {: tip}

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

1.  發出下列指令來合成相同文字，但產生名稱為 `hello_world.ogg` 的 Ogg 檔（預設格式）。
    -   {: hide-dashboard} 將 `{apikey}` 和 `{url}` 取代為您的 API 金鑰及 URL。

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

您可以使用瀏覽器或其他工具，來播放本指導教學中的範例所產生的音訊檔。如需相關資訊，請參閱[播放音訊檔](/docs/services/text-to-speech?topic=text-to-speech-audioFormats#formatsPlay)。
{: note}

## 步驟 2：合成西班牙文的文字
{: #synthesizeSpanish}

下列指令使用 `GET /v1/synthesize` 方法，將西班牙文輸入合成為音訊檔。

1.  發出下列指令來合成 "hola mundo" 字串，並產生名稱為 `hola_mundo.wav` 的 WAV 檔案。輸入文字是 URL 編碼文字。此方法會包含查詢參數 `accept` 以指定音訊格式，以及查詢參數 `voice` 以指定西班牙文語音 `es-ES_EnriqueVoice`。
    -   {: hide-dashboard} 將 `{apikey}` 和 `{url}` 取代為您的 API 金鑰及 URL。

    ```bash
    curl -X GET -u "apikey:{apikey}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## 後續步驟

-   在 [HTTP 介面](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP)中進一步瞭解服務的 HTTP 介面。
-   在 [WebSocket 介面](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket)中瞭解服務的 WebSocket 介面。
-   在 [API 參考資料](https://{DomainName}/apidocs/text-to-speech){: external}中取得服務介面之方法的詳細相關資訊。
