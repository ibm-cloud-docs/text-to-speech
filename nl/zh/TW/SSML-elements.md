---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-21"

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

# SSML 元素
{: #elements}

搭配使用 {{site.data.keyword.texttospeechfull}} 服務，您可以使用大部分的「語音合成標記語言 (SSML)」元素來控制文字的合成。這些元素適用於所有支援的語言。下表彙總此服務支援的 SSML 元素及屬性。

-   *完整* 表示服務完整支援元素或屬性與其 HTTP 和 WebSocket 介面搭配使用。
-   *局部* 表示服務不支援元素或屬性的所有層面。它也可以表示服務支援元素或屬性只與它的其中一個介面搭配使用，或表示並非所有語音都支援元素或屬性。
-   *無* 表示服務不支援元素或屬性。

如需元素或屬性的相關資訊，請參閱其說明。注意，部分屬性和值的支援，與 SSML 規格略有不同。如需相關資訊，請參閱 [W3C Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/speech-synthesis/){: external}。

<table>
  <caption>表 1. SSML 元素</caption>
  <tr>
    <th style="text-align:left; width:30%">元素或屬性</th>
    <th style="text-align:center; width:12%">支援</th>
    <th style="text-align:left; width:46%; padding-left:75px">元素或屬性</th>
    <th style="text-align:center; width:12%">支援</th>
  </tr>
  <tr>
    <td>[Audio](#audio_element)</td>
    <td style="text-align:center">無</td>
    <td style="padding-left:75px">[Say-as](#say-as_element)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td>[Break](#break_element)</td>
    <td style="text-align:center">完整</td>
    <td style="padding-left:100px">[cardinal](#sayAsCardinal)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td>[Desc](#desc_element)</td>
    <td style="text-align:center">無</td>
    <td style="padding-left:100px">[date](#sayAsDate)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td>[Emphasis](#emphasis_element)</td>
    <td style="text-align:center">無</td>
    <td style="padding-left:100px">[digits](#sayAsDigits)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td>[Lexicon](#lexicon_element)</td>
    <td style="text-align:center">無</td>
    <td style="padding-left:100px">[letters](#sayAsLetters)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td>[Mark](#mark_element)</td>
    <td style="text-align:center">局部</td>
    <td style="padding-left:100px">[number](#sayAsNumber)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td>[Meta](#mm_element)</td>
    <td style="text-align:center">無</td>
    <td style="padding-left:125px">cardinal</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td>[Metadata](#mm_element)</td>
    <td style="text-align:center">無</td>
    <td style="padding-left:125px">ordinal</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td>[Paragraph](#ps_element)</td>
    <td style="text-align:center">完整</td>
    <td style="padding-left:125px">telephone</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td>[Phoneme](#phoneme_element)</td>
    <td style="text-align:center">完整</td>
    <td style="padding-left:150px">punctuation</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">完整</td>
    <td style="padding-left:100px">[ordinal](#sayAsOrdinal)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">完整</td>
    <td style="padding-left:100px">[vxml:boolean](#vxml-boolean)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td>[Prosody](#prosody_element)</td>
    <td style="text-align:center">局部</td>
    <td style="padding-left:100px">[vxml:currency](#vxml-currency)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">contour</td>
    <td style="text-align:center">無</td>
    <td style="padding-left:100px">[vxml:date](#vxml-date)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">duration</td>
    <td style="text-align:center">無</td>
    <td style="padding-left:100px">[vxml:digits](#vxml-digits)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[pitch](#prosody-pitch)</td>
    <td style="text-align:center">完整</td>
    <td style="padding-left:100px">[vxml:phone](#vxml-phone)</td>
    <td style="text-align:center">局部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">range</td>
    <td style="text-align:center">無</td>
    <td style="padding-left:75px">[Sentence](#ps_element)</td>
    <td style="text-align:center">完整</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[rate](#prosody-rate)</td>
    <td style="text-align:center">完整</td>
    <td style="padding-left:75px">[Speak](#speak_element)</td>
    <td style="text-align:center">完整</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[volume](#prosody-volume)</td>
    <td style="text-align:center">局部</td>
    <td style="padding-left:75px">[Sub](#sub_element)</td>
    <td style="text-align:center">完整</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td style="padding-left:75px">[Voice](#voice_element)</td>
    <td style="text-align:center">無</td>
  </tr>
</table>

## audio 元素
{: #audio_element}

此 `<audio>` 元素會將錄製的元素插入至服務產生的音訊。不支援此元素。

## break 元素
{: #break_element}

`<break>` 元素會在說出的文字中插入一個 pause。它具有下列選用屬性：

-   `strength` 根據各種強度值指定 pause 的長度。
    -   `none` 抑制在處理期間可能以其他方式產生的中斷。
    -   `x-weak`、`weak`、`medium`、`strong` 或 `x-strong` 插入越來越強的中斷。
-   `time` 指定 pause 的長度（以秒或毫秒為單位）。有效值格式為 `{integer}s` 表示秒，或 `{integer}ms` 表示毫秒。

```xml
<speak version="1.0">
  Different sized <break strength="none">no pause</break>
  Different sized <break strength="x-weak">x-weak pause</break>
  Different sized <break strength="weak">weak pause</break>
  Different sized <break strength="medium">medium pause</break>
  Different sized <break strength="strong">strong pause</break>
  Different sized <break strength="x-strong">x-strong pause</break>
  Different sized <break time="1s">one-second pause</break>
  Different sized <break time="1500ms">1500-millisecond pause</break>
</speak>
```
{: codeblock}

## desc 元素
{: #desc_element}

`<desc>` 元素只能在 `<audio>` 元素中出現。因為不支援 `<audio>` 元素，所以也不支援 `<desc>` 元素。

## emphasis 元素
{: #emphasis_element}

`<emphasis>` 元素要求以強調方式說出括住的文字。不支援此元素。

## lexicon 元素
{: #lexicon_element}

此 `<lexicon>` 元素針對給定的 SSML 文件引進發音字典。不支援此元素。

您可以使用服務的自訂作業介面來定義自訂項目（字組/轉換配對）的字典，以在語音合成期間使用。如需相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。

## mark 元素
{: #mark_element}

只有服務的 WebSocket 介面才支援 `<mark>` 元素，而其 HTTP 介面不支援且會忽略此元素。如需相關資訊，請參閱[指定 SSML 標記](/docs/services/text-to-speech?topic=text-to-speech-timing#mark)。
{: note}

`<mark>` 元素是一個空白元素，可將標記放置在要合成的文字中。在 `<mark>` 元素之前的所有文字都已完成合成時，即會通知用戶端。此元素接受單一 `name` 屬性，此屬性指定用來唯一識別標記的字串；名稱必須以英數字元開頭。傳回的名稱隨附標記在合成音訊中出現的時間。

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

## meta 及 metadata 元素
{: #mm_element}

`<meta>` 及 `<metadata>` 元素是您可以將文件相關資訊放置在其中的容器。不支援這兩種元素。

## paragraph 及 sentence 元素
{: #ps_element}

`<paragraph>`（或 `<p>`）及 `<sentence>`（或 `<s>`）是選用元素，可用來提供關於文字結構的提示。如果以 `<paragraph>` 或 `<sentence>` 元素括住的文字不是以句尾標點符號字元（如句點）結尾，則服務會將超過正常長度的 pause 新增至合成音訊。

任一元素的唯一有效屬性是 `xml:lang`，其容許語言切換。不支援此屬性。

```xml
<speak version="1.0">
  <paragraph>
    <sentence>Text within a sentence element.</sentence>
    <s>More text in another sentence.</s>
  </paragraph>
</speak>
```
{: codeblock}

## phoneme 元素
{: #phoneme_element}

`<phoneme>` 元素提供括住文字的語音發音。語音拼字代表字組的聲音、這些聲音如何分成多個音節，以及哪些音節接收重音。此元素有兩個屬性：

-   `alphabet` 是選用屬性，用來指定要使用的語音。支援的 alphabet 包含：
    -   標準國際音標 (IPA)：`alphabet="ipa"`
    -   {{site.data.keyword.IBM_notm}} 符號語音表示法 (SPR)：`alphabet="ibm"`

    如果未指定 alphabet，依預設服務會使用 IBM SPR。
-   `ph` 是必要屬性，可在指出的 alphabet 中提供發音。下列範例顯示兩種格式中 *tomato* 這個字的發音：

    -   IPA 格式：

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   搭配使用 Unicode 符號的 IPA 格式：

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   IBM SPR 格式：

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

如需使用 SPR 及 IPA 表示法與 `<phoneme>` 元素搭配的相關資訊，請參閱[使用 IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs)。

## prosody 元素
{: #prosody_element}

`<prosody>` 元素可控制文字的音高、說話速度及音量。所有屬性都是選用的，但如果未指定任何屬性，則會發生錯誤。SSML 規格容許服務不支援的三個屬性：`contour`、`range` 及 `duration`。服務支援 `pitch`、`rate` 及 `volume` 屬性。

### pitch 屬性
{: #prosody-pitch}

`pitch` 屬性可修改元素內文字的基準線音高。接受值為：

-   後面接著 `Hz`（赫茲）指定的數字：基準線音高會變調（向上或向下）至指定的值。
-   相對變更值（以半音為單位）：導致從現行基準線絕對移位的數字。數字前面會加上 `+`（增加）或 `-`（減少），後面接著 `st`（半音），例如 `+5st`。
-   相對變更（以百分比為單位）：導致從現行基準線相對移位的數字。數字前面會加上 `+`（增加）或 `-`（減少），後面接著 `%`（百分比符號），例如，`-10%`。
-   下列六個關鍵字的其中一個，可將音高修改為對應的預定值：
    -   `default` 使用服務的預設基準線音高。
    -   `x-low` 將音高基準線向下移位 12 個半音。
    -   `low` 將音高基準線向下移位 6 個半音。
    -   `medium` 產生與 `default` 相同的行為。
    -   `high` 將音高基準線向上移位 6 個半音。
    -   `x-high` 將音高基準線向上移位 12 個半音。

    ```xml
    <speak version="1.0">
      <prosody pitch="150Hz">Transpose pitch to 150 Hz</prosody>
      <prosody pitch="-20Hz">Lower pitch by 20 Hz from baseline</prosody>
      <prosody pitch="+20Hz">Increase pitch by 20 Hz from baseline</prosody>
      <prosody pitch="-12st">Lower pitch by 12 semitones from baseline</prosody>
      <prosody pitch="+12st">Increase pitch by 12 semitones from baseline</prosody>
      <prosody pitch="x-low">Lower pitch by 12 semitones from baseline</prosody>
    </speak>
    ```
    {: codeblock}

### rate 屬性
{: #prosody-rate}

`rate` 屬性指出元素內文字說話速度的變更。速度是根據每分鐘多少個字組來指定的；如果說話速度為每分鐘 50 個字，則 `rate` 等於 `50`。當 `rate` 設為正數時，實作不會遵守現行 W3C prosody rate 屬性規格。同時，服務支援相對百分比變更（例如，`+15%`），但不支援相對值變更（例如，`+15`）。接受值為：

-   相對百分比增加或減少：`+10%`。
-   每分鐘字組數（正數）：`75`。
-   `default` 使用服務的預設速度。
-   `x-slow` 將速度減少百分之 50。
-   `slow` 將速度減少百分之 25。
-   `medium` 產生與 `default` 相同的行為。
-   `fast` 將速度增加百分之 25。
-   `x-fast` 將速度增加百分之 50。

```xml
<speak version="1.0">
  <prosody rate="slow">Decrease speaking rate by 25%</prosody>
  <prosody rate="50">Set speaking rate at 50 words per minute</prosody>
  <prosody rate="+5%">Increase speaking rate by 5 percent</prosody>
</speak>
```
{: codeblock}

### volume 屬性
{: #prosody-volume}

服務不支援 `<prosody>` 元素的 `volume` 屬性用於其神經語音（例如，`en-US_AllisonV3Voice`）。如需相關資訊，請參閱[神經語音](/docs/services/text-to-speech?topic=text-to-speech-voices#neuralVoices)。
{: note}

`volume` 屬性可修改元素內文字的音量。您可以指定在 1.0 到 100.0（最大音量）範圍內的整數或小數值。您也可以使用下列其中一個字串值，這些字串值對應於在 0 到 100 範圍內的預先定義設定。（不支援 `silent` 值。）

-   `x-soft` 具有值 30。
-   `soft` 具有值 50。
-   `medium` 具有值 80。
-   `loud` 具有值 90。
-   `default` 具有值 92。
-   `x-loud` 具有值 100。

```xml
<speak version="1.0">
  <prosody volume="75">Modified volume is 75</prosody>
  <prosody volume="88.9">Modified volume is 88.9</prosody>
  <prosody volume="loud">Modified volume is 90</prosody>
</speak>
```
{: codeblock}

## say-as 元素
{: #say-as_element}

大部分語言僅局部支援 `<say-as>` 元素。對於美式英文以外的語言，服務通常只支援元素的 `digits` 和 `letters` 屬性。
{: note}

`<say-as>` 元素提供元素內包含之文字類型的相關資訊，以及指定用於呈現文字的詳細程度。元素有一個必要屬性 `interpret-as`，其指出如何解譯括住的文字。它有兩個選用屬性：`format` 和 `detail`，僅與 `interpret-as` 屬性內的特定值搭配使用，如下列範例所示。

隨後有 `interpret-as` 屬性的可接受值，以及每一個屬性的範例。

### cardinal
{: #sayAsCardinal}

`cardinal` 值會說出元素內數字的基數。下列範例會說出 *Super Bowl forty-nine*。第一個是多餘的，因為它不會變更服務的預設行為。

```xml
<speak version="1.0">
  Super Bowl <say-as interpret-as="cardinal">49</say-as>
  Super Bowl <say-as interpret-as="cardinal">XLIX</say-as>
</speak>
```
{: codeblock}

### date
{: #sayAsDate}

`date` 值根據關聯的 `format` 屬性中提供的格式說出元素內的日期。`date` 值需要 `格式` 屬性。如果沒有 `format`，服務仍會嘗試對日期發音。下列範例以指定的格式說出指出的日期，其中 `d`、`m` 及 `y` 代表日、月和年。

```xml
<speak version="1.0">
  <say-as interpret-as="date" format="mdy">12/17/2005</say-as>
  <say-as interpret-as="date" format="ymd">2005/12/17</say-as>
  <say-as interpret-as="date" format="dmy">17/12/2005</say-as>
  <say-as interpret-as="date" format="ydm">2005/17/12</say-as>
  <say-as interpret-as="date" format="my">12/2005</say-as>
  <say-as interpret-as="date" format="md">12/17</say-as>
  <say-as interpret-as="date" format="ym">2005/12</say-as>
</speak>
```
{: codeblock}

### digits
{: #sayAsDigits}

`digits` 值會說出元素內數字的各個數字。下列範例會說出個別數字 *123456*。

```xml
<speak version="1.0">
  <say-as interpret-as="digits">123456</say-as>
</speak>
```
{: codeblock}

### letters
{: #sayAsLetters}

`letters` 值會拼出元素內字組的各字元。下列範例拼寫字組 *hello* 的字母。

```xml
<speak version="1.0">
  <say-as interpret-as="letters">Hello</say-as>
</speak>
```
{: codeblock}

### number
{: #sayAsNumber}

`number` 值提供 `cardinal` 和 `ordinal` 值的替代方案。您可以使用選用 `format` 屬性，指出如何解譯一連串數字。第一個範例會省略 `format` 屬性，將數字發音為基數值。第二個範例明確指定數字將發音為 `cardinal` 值。第三個範例指定數字將發音為 `ordinal` 值。

```xml
<speak version="1.0">
  <say-as interpret-as="number">123456</say-as>
  <say-as interpret-as="number" format="cardinal">123456</say-as>
  <say-as interpret-as="number" format="ordinal">123456</say-as>
</speak>
```
{: codeblock}

您也可以針對 `format` 屬性指定 `telephone` 值。這些範例顯示兩種不同的方式，可將一連串數字發音為電話號碼。若要對包括標點符號的數字發音，請為選用的 `detail` 屬性指定值 `punctuation`。

```xml
<speak version="1.0">
  <say-as interpret-as="number" format="telephone">555-555-5555</say-as>
  <say-as interpret-as="number" format="telephone" detail="punctuation">555-555-5555</say-as>
</speak>
```
{: codeblock}

### ordinal
{: #sayAsOrdinal}

`ordinal` 值會說出元素內數字的序數值。下列範例會說出 *second first*。

```xml
<speak version="1.0">
  <say-as interpret-as="ordinal">2</say-as>
  <say-as interpret-as="ordinal">1</say-as>
</speak>
```
{: codeblock}

### vxml:boolean
{: #vxml-boolean}

`vxml:boolean` 值會說出 *yes* 或 *no*，視元素內的 `true` 或 `false` 值而定。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:boolean">true</say-as>
  <say-as interpret-as="vxml:boolean">false</say-as>
</speak>
```
{: codeblock}

### vxml:currency
{: #vxml-currency}

`vxml:currency` 值用來控制貨幣值的合成。字串必須以 `UUUmm.nn` 格式撰寫，其中 `UUU` 是 ISO 標準 4217 所指定的三個字元貨幣指示器，而 `mm.nn` 是數量。下列範例會說出 *forty-five dollars and thirty cents*。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.30</say-as>
</speak>
```
{: codeblock}

如果指定的數字包括超過兩個小數位數，則會將金額合成為小數，後面接著貨幣指示器。如果未呈現三個字元貨幣指示器，則只會將金額合成為十進位數，且貨幣類型不會發音。下列範例會說出 *forty-five point three two nine US dollars*。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.329</say-as>
</speak>
```
{: codeblock}

### vxml:date
{: #vxml-date}

`vxml:date` 值的作用類似於 `date` 值，但格式預先定義為 `YYYYMMDD`。如果日、月或年值未知，或者您不希望值發音，請將值取代為 `?`（問號）。第二個和第三個範例包括問號。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:date">20050720</say-as>
  <say-as interpret-as="vxml:date">????0720</say-as>
  <say-as interpret-as="vxml:date">200507??</say-as>
</speak>
```
{: codeblock}

### vxml:digits
{: #vxml-digits}

`vxml:digits` 值提供與 `digits` 值相同的函數。

### vxml:phone
{: #vxml-phone}

`vxml:phone` 值會連同數字及標點符號說出電話號碼。它相當於使用 `number` 值，並針對 `format` 屬性指定 `telephone`，以及針對 `detail` 屬性指定 `punctuation`。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:phone">555-555-5555</say-as>
</speak>
```
{: codeblock}

## speak 元素
{: #speak_element}

`<speak>` 元素是 SSML 文件的根元素。有效屬性為：

-   `version` 是指定 SSML 規格的必要屬性。接受值為 `1.0`。
-   `xml:lang` 不是服務所需的屬性。使用此元素時，請省略該屬性。
-   `xml:base` 無效。

```xml
<speak version="1.0">
  The text to be spoken.
</speak>
```
{: codeblock}

## sub 元素
{: #sub_element}

`<sub>` 元素指出，當合成語音時，`alias` 屬性所指定的文字，將取代此元素內括住的文字。`alias` 屬性是元素的唯一屬性，且是必要屬性。

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

## voice 元素
{: #voice_element}

此 `<voice>` 元素要求變更語音。不支援此元素。
