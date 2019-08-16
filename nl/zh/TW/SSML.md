---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-23"

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

# 使用 SSML
{: #ssml}

「語音合成標記語言 (SSML)」是 XML 型標記語言，可為語音合成應用程式提供文字註釋。它是 W3C Voice-Browser Working Group 的建議，已被 VoiceXML 2.0 規格採用作為語音合成的標準標記語言。SSML 向語音應用程式的開發人員提供一種標準方式，用來控制合成處理程序的各個層面，方法是讓他們可以透過標記來指定發音、音量、音高、速度及其他屬性。
{: shortdesc}

搭配使用 {{site.data.keyword.texttospeechfull}} 服務，您可以使用 SSML 來控制文字與所有支援語言的合成。這包括使用 SSML `<phoneme>` 元素，在「國際音標 (IPA)」或「{{site.data.keyword.IBM_notm}} 符號語音表示法 (SPR)」中，定義字組的發音。此服務也會根據 SSML `<phoneme>` 元素，使用其自訂作業介面來定義字組的語音轉換；如需相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。

## SSML 簡介
{: #introduction-SSML}

SSML 的操作方式是利用預先定義的一組元素或標籤來擴增傳遞至合成器的純文字。XML 剖析器首先會區隔純文字輸入與標記規格。然後，處理規格，並以合成器可以瞭解的形式傳送這組指示，以產生所需的效果。對於要執行此工作的 XML 剖析器，需要妥善格式化標記；例如，元素必須關閉，而且多個元素必須適當地巢狀化。如需基本 XML 概念的簡介，請參閱 [w3schools.com/xml/xml_whatis.asp](http://www.w3schools.com/xml/xml_whatis.asp){: external}。

SSML 元素是其中包含的任何項目，並包括一個開始標籤及其成對的結束標籤。如下列範例所示，元素可以包含其他元素（標籤可以巢狀化）與文字的組合。此外，元素可以要求或選擇性地接受屬性設為特定值。

```xml
<tag1>
  <tag2 attributeName="attributeValue">
    ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

完整合法的 SSML 文件由 XML 前文組成，其中包含編碼以及用來驗證 SSML 文件的綱目這類資訊，後面接著根元素 `<speak>`。（如需前言結構的相關資訊，請參閱 [tizag.com/xmlTutorial/xmlprolog.php](http://www.tizag.com/xmlTutorial/xmlprolog.php){: external}。）在 `<speak>` 元素的文字段內，您可以指定要合成的文字，並以其他元素擴增。

```xml
<!-- The XML Prolog -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE speak PUBLIC "-//W3C//DTD SYNTHESIS 1.0//EN"
  "http://www.w3.org/TR/speech-synthesis/synthesis.dtd">

<!-- Root Element -->
<speak version="1.0" xmlns="www.w3.org/2001/10/synthesis"
  ... the body that contains text to be synthesized plus markup ...
</speak>
```
{: codeblock}

服務支援 SSML 片段，這些片段是不包括完整 XML 標頭的 SSML 元素。

## SSML 支援
{: #ssmlSupport}

{{site.data.keyword.texttospeechshort}} 服務的支援基於 W3C 在 2004 年 9 月 7 日所建議的 SSML 1.0 版。如需 W3C SSML 建議的相關資訊，請參閱 [W3C Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/speech-synthesis/){: external}。

如需使用 SSML 與服務搭配的相關資訊，請參閱下列資訊：

-   如需服務對所有 SSML 元素之支援層次的完整資訊，請參閱 [SSML 元素](/docs/services/text-to-speech?topic=text-to-speech-elements)。除了少數例外，服務會實作大部分 W3C 規格，以及 SSML 片段。
-   服務會使用 `<express-as>` 元素來擴充 SSML，此元素指出說話時如何表達文字（好消息、抱歉或不確定）。服務僅支援美式英文 Allison 語音的表達。請參閱[使用表達 SSML](/docs/services/text-to-speech?topic=text-to-speech-expressive)。
-   服務會使用 `<voice-transformation>` 元素來擴充 SSML，此元素可擴大可能的語音範圍，方法是讓您控制音高、音高範圍、聲門張力、呼吸聲、速度，以及說出文字的音色。服務也會提供兩個內建虛擬語音，即 *Young* 和 *Soft*。服務僅支援美式英文語音的語音轉換。請參閱[使用語音轉換 SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation)。
-   服務的自訂作業介面支援使用 SSML `<phoneme>` 元素，來指定其用來對字組發音的語音拼字。語音拼字代表字組的聲音、這些聲音如何分成多個音節，以及哪些音節接收重音。
    -   如需自訂作業介面的資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。
    -   如需您可以在 {{site.data.keyword.IBM_notm}} SPR 或 IPA 規格中針對任何受支援語言使用之有效符號的相關資訊，請參閱[使用 IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs)。

## SSML 驗證
{: #errors}

服務會驗證您在任何內容中提交的所有 SSML 元素，此內容會作為輸入文字以進行合成，或作為字組轉換的定義以進行自訂作業。服務無法預先判定提交以進行合成的文字是否包含 SSML 元素。因此，不論它是否包含 SSML，都會針對所有輸入文字執行相同的驗證。

-   *所有 SSML 輸入都必須正確無誤並已妥善格式化。* 服務會無聲自動忽略不受支援的 SSML 元素。服務會合成下列元素內含的文字：不受支援的元素，或使用不受支援特性的元素；只會忽略元素。
-   *服務會針對無效元素報告 HTTP 400 錯誤碼。* 錯誤回應包括敘述性訊息，且要求失敗。

具體而言，服務會在下列情況下傳回錯誤：

-   *元素無效。* 例如，您不正確地指定標籤、忽略必要屬性，或包括開始標籤但沒有成對的結束標籤。
-   *符號無效。* `<phoneme>` 元素的 `ph` 屬性包括所指定語言不支援的 IPA 或 SPR 符號。
-   *無母音。* `<phoneme>` 元素的 `ph` 屬性指定未包括任何母音的字組發音。
-   *法文連音位於無效位置。* 在 `<phoneme>` 元素的 `ph` 屬性中，連音字元不會跟在子音之後，或出現在字組發音的中間。
-   *日文 `:` 符號未在母音前面。* 在 `<phoneme>` 元素的 `ph` 屬性中，`:` 字元不會出現在母音之前（可能之間有其他符號，例如音節界限）。
-   *音節重音無效。* {{site.data.keyword.IBM_notm}} SPR 之 `<phoneme>` 元素的 `ph` 屬性包括無效的音節重音。若為法文，音節重音符號不會緊接在母音前面。若為西班牙文或義大利文，則會使用次重音 (`2`) 或無重音 (`0`) 符號。若為日文，則會使用次重音符號 (`2`)。
-   *無效使用 SSML `<express-as>` 或 `<voice-transformation>` 元素。* 只能將這些 SSML 延伸用於指定的標準美式英文語音。
-   *無效使用 SSML `<prosody>` 元素。* 您無法將 `<prosody>` 元素的 `contour`、`duration` 和 `range` 屬性用於任何語音。此外，您無法將 `<prosody>` 元素的 `volume` 屬性用於神經語音（例如，`en-US_AllisonV3Voice`）。
-   *未跳出的 XML 控制字元。* 輸入文字本身包含 <code>&quot;</code>、<code>&apos;</code>、`&`、`<` 或 `>` 字元，而非其對等的跳出字串或字元編碼。如需相關資訊，請參閱[跳出 XML 控制字元](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#escape)。
