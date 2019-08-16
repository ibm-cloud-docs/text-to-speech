---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-06"

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

# 使用 IBM SPR
{: #sprs}

{{site.data.keyword.texttospeechfull}} 服務支援標準「國際音標 (IPA)」表示法及「{{site.data.keyword.IBM}} 符號語音表示法 (SPR)」兩者，用來表示字組的聲音。SPR 是一種語音碼，代表字組的發音、構成字組的聲音、這些聲音如何分成多個音節，以及哪些音節有重音。SPR 是 IPA 的替代表示法。
{: shortdesc}

下列各節介紹 {{site.data.keyword.IBM_notm}} SPR 表示法。因為 IPA 是標準表示法，所以本文件並未提供 IPA 的基本用法資訊。如需簡要用法指引，請參閱[使用 IPA](#ipa)。

## IBM SPR 簡介
{: #introduction-SPRs}

SPR 發音是使用語音合成標記語言 (SSML) 的 [phoneme 元素](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)定義的。它包括一系列可容許的符號，而這些符號適用於以雙引號括住的給定語言。這些符號定義以 `<phoneme>` 元素括住的字組如何發音。元素的 `alphabet` 屬性具有值 `ibm`，指出發音定義在 SPR 中，而 `ph` 屬性則定義發音。以下是美式英文字組 *through* 及 *shocking* 的有效 SPR 表示法範例：

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

在定義中，`.`（句點）代表新音節的開頭，數字 `1` 和 `0` 指示音節的重音層次，字母代表美式英文語音的特定發音。不符合必要規格的 SPR 項目無效。

## 音節界限

可以使用 `.`（句點）來標示每個音節的開頭。不過，為了保留語言的有效語音，服務可以選擇在某些情況下不得許使用句點（例如，如果將音節界限置於語言的非法或非自然位置中）。通常，如果使用者可以指示音節界限的有效喜好設定或字組發音的其他層面，服務就會遵循這類要求。

## 音節重音

您可以使用下表中的符號，來標示發音的音節重音。{{site.data.keyword.IBM_notm}} 建議您在 SPR 或 IPA 中指出發音的主要重音。不過，對於這兩種格式，指出音節重音是選用的；如果您未指出重音，服務會判定重音所在位置。

<table style="width:80%">
  <caption>表 1. 音節重音</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IBM SPR 符號
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA 符號
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      意義
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      1
    </td>
    <td style="text-align:center">
      <code>&#712;</code>
    </td>
    <td style="text-align:center">
      02C8
    </td>
    <td>
      主重音
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      2
    </td>
    <td style="text-align:center">
      <code>&#716;</code>
    </td>
    <td style="text-align:center">
      02CC
    </td>
    <td>
      次重音
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      0
    </td>
    <td style="text-align:center">無符號</td>
    <td style="text-align:center">沒有值</td>
    <td>
      無重音
    </td>
  </tr>
</table>

**附註：**

-   在法文的 IPA 中，會忽略音節的重音符號。在法文的 SPR 中，不會忽略音節重音；如果已指定，音節重音必須緊接在音節的母音之前。在 SPR 中，法文的音節重音比其他語言更為嚴格；如果重音符號位於無效位置，則會發生錯誤。
-   在西班牙文和義大利文的 SPR 中，您只能指定 `1`（主要重音）。如果指定次重音或無重音，則會發生錯誤。
-   在日文的 SPR 中，僅支援 `1`（主要重音）及 `0`（無重音）。如果指定次重音，則會發生錯誤。

您必須將音節重音標記放置在音節界限之內，但一律在音節母音的左側。您可以將標記放置在重母音左側的任何位置。例如，下列每個 SPR 範例都會將主要重音放置在字組 *construction* 的正確母音上：

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

## 語音聲音符號

每種語言都使用自己的 SPR 符號庫存來代表該語言的語音聲音。下列規則適用於指定 SPR 符號：

-   字母會區分大小寫，因此，舉例而言 `e` 及 `E` 代表兩個不同的聲音。
-   兩個字元和三個字元的符號必須內含在單引號中；例如，德文字組 *hin*: `"h'aj'm"` 中的符號 `aj`。
-   任何 SPR 定義只要包含語言中不容許的聲音符號，服務就會將此定義視為無效。

以 SPR 格式定義字組的發音時，另請考量下列事項：

-   每種語言的聲音在該語言內都具有特定的分佈型樣。例如，在英文的所有用語中，*sing* (`".1sIG"`) 中的 `G` 這個音不會出現在字組的開頭。其他分佈範圍極窄的美式英文發音是喉塞音 (`?`)、彈舌音 (`F`) 和鼻元音 (`N`)。如果您在上下文中輸入正常情況下不會出現的聲音符號，則產生的語音可能發出不自然的聲音。
-   {{site.data.keyword.texttospeechshort}} 服務會將一組更準確的語言規則套用至其輸入，以將聲音變更所用的處理程序反映在自然語言中的特定上下文。例如，在美式英文中，*write* (`".1r1Yt"`) 這個字的 `t` 這個音會發音為 *writer* (`".1rY.0FR"`) 中的拍打聲 (`F`)。正如同一般輸入文字所做一般，SPR 輸入會進行這些修改。在此範例中，無論您是輸入 `".1rY.0tR"` 還是 `".1rY.0FR"`，都不會影響其產生的語音。

## 使用 IPA
{: #ipa}

下列資訊適用於使用 IPA 表示法中的發音：

-   僅使用記載的 IPA 符號。針對 SPR 符號列出數個 IPA 符號（或符號組合）時，全部等同於單一 SPR 符號。在此情況下，服務會將所有這些 IPA 符號視為相同，並且沒有意識到 IPA 系統用來說明的細微或地區差異。
-   您也可以將 IPA 發音指定為 IPA Unicode 值。下節中列出的語言特定表格記載了 IPA 符號及其對等的 IPA Unicode 值兩者。如需使用 IPA Unicode 值的範例發音，請參閱 [phoneme 元素](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)。

若要進一步瞭解，請參閱下列資訊：

-   如需 IPA 的相關資訊，請參閱 [International Phonetic Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}。
-   如需 Unicode 之拼音符號的相關資訊，請參閱 [Phonetic symbols in Unicode](https://wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: external}。

## 支援的語言
{: #supportedLanguages}

下列頁面記載每種語言的 SPR 符號、IPA 符號及對等 IPA Unicode 值。它們會從語言顯示字組中每個符號的範例。因為用語差異，範例不一定會符合您的發音。

-   [巴西葡萄牙文符號](/docs/services/text-to-speech?topic=text-to-speech-ptSymbols)
-   [英式英文符號](/docs/services/text-to-speech?topic=text-to-speech-gbSymbols)
-   [法文符號](/docs/services/text-to-speech?topic=text-to-speech-frSymbols)
-   [德文符號](/docs/services/text-to-speech?topic=text-to-speech-deSymbols)
-   [義大利文符號](/docs/services/text-to-speech?topic=text-to-speech-itSymbols)
-   [日文符號](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols)
-   [西班牙文符號](/docs/services/text-to-speech?topic=text-to-speech-esSymbols)
-   [美式英文符號](/docs/services/text-to-speech?topic=text-to-speech-usSymbols)
