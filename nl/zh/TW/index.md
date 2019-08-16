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

# 關於
{: #about}

> **服務更新**：*{{site.data.keyword.texttospeechshort}} 服務已於 2019 年 7 月 30 日更新。服務現在支援日文的神經語音：`ja-JP_EmiV3Voice`。如需相關資訊，請參閱版本注意事項中的 [2019 年 7 月 30 日服務更新](/docs/services/text-to-speech?topic=text-to-speech-release-notes#July2019)*。

{{site.data.keyword.texttospeechfull}} 服務提供的應用程式設計介面 (API) 會使用 {{site.data.keyword.IBM_notm}} 的語音合成功能，將撰寫的文字轉換為自然發音的語音。此服務會以最低延遲將結果串流回至用戶端。此服務同時提供 [HTTP](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) 及 [WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket) 介面。

## 特性與功能

{{site.data.keyword.texttospeechshort}} 服務提供下列特性與功能：

-   **音訊格式** - 搭配使用 Ogg 或 WebM 與 Opus 或 Vorbis 轉碼器，或者使用 WAV、FLAC、MP3 (MPEG)、l16 (PCM)、mulaw 或基本格式來產生音訊。如需相關資訊，請參閱[音訊格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。
-   **語音** - 在各種語言、語音及用語中，將文字合成為音訊。對於大部分語音，該服務同時提供標準（拼接）和神經版本。如需相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。
-   **SSML** - 接受純文字或以 XML 型「語音合成標記語言 (SSML)」標註的文字。如需相關資訊，請參閱[使用 SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml)。
-   **表達** - 使用表達元素來擴充 SSML，您可以用來指出說話風格為 *GoodNews*、*Apology* 或 *Uncertainty*。僅適用於標準美式英文 Allison 語音。如需相關資訊，請參閱[表達 SSML](/docs/services/text-to-speech?topic=text-to-speech-expressive)。
-   **語音轉換** - 藉由新增語音轉換元素來擴充 SSML。您可以使用元素，藉由控制音高、速度及音色這類層面來擴充可能語音範圍。同時提供兩個內建虛擬語音，即 *Young* 和 *Soft*。僅可用於標準美式英文語音。如需相關資訊，請參閱[語音轉換 SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation)。
-   **字組計時** - 使用 WebSocket 介面，可支援 SSML `<mark>` 元素，以及輸入文字之所有字串的選用字組計時資訊。計時資訊會同步處理輸入文字及產生的音訊。如需相關資訊，請參閱[取得字組計時](/docs/services/text-to-speech?topic=text-to-speech-timing)。
-   **自訂作業** - 提供一個自訂作業介面，您可以用來指定服務如何對輸入中出現的不尋常字組發音。您可以使用「國際音標 (IPA)」或「{{site.data.keyword.IBM_notm}} 符號語音表示法 (SPR)」來定義發音。如需相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。

如需服務定價方案的相關資訊，請參閱 [{{site.data.keyword.cloud_notm}} 型錄](https://{DomainName}/catalog/services/text-to-speech){: external}中的 {{site.data.keyword.texttospeechshort}} 服務。

## 語言支援
{: #languages-index}

此服務支援下列語言的語音：巴西葡萄牙文、英文（英式和美式用語）、法文、德文、義大利文、日文，以及西班牙文（卡斯提亞語、拉丁美洲及北美用語）。

服務針對每種語言至少提供一個女性語音。針對部分語言，服務提供多種語音，同時包括男性和女性語音。每種語音都會針對其用語使用適當的抑揚頓挫和語調。對於大部分語音，該服務同時提供標準和神經版本。

如需每種語言可用之語音的相關資訊，請參閱[語言和語音](/docs/services/text-to-speech?topic=text-to-speech-voices)。

## 使用案例
{: #usecases}

服務適用於語音驅動及無螢幕的應用程式，在這些應用程式中，音訊是偏好的輸出方法：

-   適用於殘障人士的介面，例如視障者的協助工具
-   大聲閱讀寄至驅動程式的文字和電子郵件訊息
-   視訊 Script 旁白和視訊配音
-   閱讀型教育工具
-   首頁自動化解決方案

## 試用服務

如需動作中的服務範例，請參閱：

-   {{site.data.keyword.texttospeechshort}} 服務的[快速示範](https://text-to-speech-demo.ng.bluemix.net/){: external}，此服務會接受文字，並產生不同的語音。它會提供支援的表達和轉換。
-   {{site.data.keyword.ibmwatson}} [入門範本套件](http://www.ibm.com/watson/developercloud/starter-kits.html){: external}中示範 {{site.data.keyword.texttospeechshort}} 服務的應用程式。
