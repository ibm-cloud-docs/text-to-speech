---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-14"

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# 入門指導教學
{: #gettingStarted}

{{site.data.keyword.texttospeechfull}} 服務會將撰寫的文字轉換為自然發音的語音，以提供應用程式的語音合成功能。這個 curl 型指導教學可協助您快速開始使用服務。範例顯示如何呼叫服務的 `POST` 和 `GET /v1/synthesize` 方法來要求音訊串流。
{: shortdesc}

指導教學使用 {{site.data.keyword.cloud}} Identity and Access Management (IAM) API 金鑰進行鑑別。舊版服務實例可能會繼續使用來自其現有 Cloud Foundry 服務認證的 `{username}` 及 `{password}` 進行鑑別。使用適合您服務實例的方法進行鑑別。如需對服務使用 IAM 鑑別的相關資訊，請參閱版本注意事項中的 [2018 年 10 月 30 日服務更新](/docs/services/text-to-speech/release-notes.html#October2018)。
{: important}

## 開始之前
{: #before-you-begin}

- {: hide-dashboard}  建立服務的實例：
    1.  {: hide-dashboard} 移至「{{site.data.keyword.cloud_notm}} 型錄」中的 [{{site.data.keyword.texttospeechshort}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/catalog/services/text-to-speech){: new_window} 頁面。
    1.  {: hide-dashboard} 註冊免費的 {{site.data.keyword.cloud_notm}} 帳戶或登入。
    1.  {: hide-dashboard} 按一下**建立**。
-   將要鑑別的認證複製到您的服務實例。
    1.  {: hide-dashboard} 從 [{{site.data.keyword.cloud_notm}} 儀表板 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/dashboard/apps){: new_window} 中，按一下您的 {{site.data.keyword.texttospeechshort}} 服務實例，以移至 {{site.data.keyword.texttospeechshort}} 服務儀表板頁面。
    1.  在**管理**頁面上，按一下**顯示**以檢視您的認證。
    1.  複製 `API 金鑰`和 `URL` 值。
-   確定您具有 `curl` 指令。
    -   這些範例使用 `curl` 指令來呼叫 HTTP 介面的方法。從 [curl.haxx.se ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://curl.haxx.se/){: new_window} 安裝作業系統的版本。安裝支援 Secure Sockets Layer (SSL) 通訊協定的版本。請確定在 `PATH` 環境變數中包括已安裝的二進位檔。

輸入指令時，請將 `{apikey}` 和 `{url}` 取代為您的實際 API 金鑰及 URL。從指令中省略指出變數值的大括弧。實際值類似下列範例：
{: hide-dashboard}

```bash
curl -X POST -u "apikey:L_HALhLVIksh1b73l97LSs6R_3gLo4xkujAaxm7i-b9x"
. . .
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```
{:pre}
{: hide-dashboard}

您可以使用瀏覽器或其他工具，來播放本指導教學中範例所產生的音訊檔。如需相關資訊，請參閱[播放音訊檔](/docs/services/text-to-speech/audio-formats.html#formatsPlay)。
{: note}

## 步驟 1：合成美式英文的文字
{: #synthesizeEnglish}

下列指令使用 `POST /v1/syntheize` 方法，以兩種不同格式將美式英文輸入合成為音訊檔。這兩個要求皆會使用預設美式英文語音 `en-US_MichaelVoice`。

1.  發出下列指令來合成 "hello world" 字串，並產生名為 `hello_world.wav` 的 WAV 檔案。
    -   {: hide-dashboard} 將 `{apikey}` 和 `{url}` 取代為您的 API 金鑰及 URL。

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

1.  發出下列指令來合成相同文字，但產生名為 `hello_world.ogg` 的 Ogg 檔（預設格式）。
    -   {: hide-dashboard} 將 `{apikey}` 和 `{url}` 取代為您的 API 金鑰及 URL。

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

## 步驟 2：合成西班牙文的文字
{: #synthesizeSpanish}

下列指令使用 `GET /v1/synthesize` 方法，將西班牙文輸入合成為音訊檔。

1.  發出下列指令來合成 "hola mundo" 字串，並產生名為 `hola_mundo.wav` 的 WAV 檔案。輸入文字是 URL 編碼文字。此方法包括查詢參數 `accept` 以指定音訊格式，以及查詢參數 `voice` 以指定西班牙文語音 `-ES_EnriqueVoice`。
    -   {: hide-dashboard} 將 `{apikey}` 和 `{url}` 取代為您的 API 金鑰及 URL。

    ```bash
    curl -X GET -u "apikey:{apikey}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## 後續步驟

-   在 [HTTP 介面](/docs/services/text-to-speech/http.html)中進一步瞭解服務的 HTTP 介面。
-   在 [WebSocket 介面](/docs/services/text-to-speech/websockets.html)中瞭解服務的 WebSocket 介面。
-   在 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/text-to-speech){: new_window} 中取得服務介面之方法的詳細資訊。
