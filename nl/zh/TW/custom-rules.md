---

copyright:
  years: 2015, 2019
lastupdated: "2018-06-04"

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

# 用於建立自訂項目的規則
{: #rules}

下列規則及準則適用於在自訂模型中移入自訂項目（字組/轉換配對）。

## 自訂項目數上限

單一自訂模型可包含的自訂項目不得超過 20,000 個。

## 字元編碼

服務針對 *word* 和 *translation* 項目接受 ASCII 和 UTF-8 字元編碼。針對轉換，對於 SPR 表示法請使用 ASCII 編碼，對於 IPA 表示法則請使用 UTF-8 編碼。

## 空格

*word* 不得包含空格。服務使用空格來分隔輸入文字中的個別字組。

## 區分大小寫

*word* 會區分大小寫。例如，假設自訂模型包含項目 `{word='Sun', translation='Sunday'}`。服務會將其預設發音套用至字組 `sun`，但會將自訂轉換套用至字組 `Sun`，因為只有後者的首字母為大寫。


## 上下文相關

部分字組的發音與上下文相關。例如，請考量下列輸入句子範例：

```
St. Anthony lives on Henry St.
```
{: codeblock}

服務的預設發音規則會正確地將此文字合成為

```
Saint Anthony lives on Henry Street
```
{: codeblock}

不過，如果您置換字串 `St.` 的預設發音規則，成為將它轉換成 `saint`，則服務不會再根據上下文對字組發音。套用包括這類轉換的自訂語音模型，會導致服務將前一個輸入句子發音為

```
Saint Anthony lives on Henry saint
```
{: codeblock}

當您開發字組/轉換配對時，請考量這類案例。

## 尾端句點

服務只會將自訂模型中的字組套用至輸入文字中與字組完全相符的那些字串。word 項目中的尾端 `.`（句點）會變更字組的合成方式：

-   *沒有尾端句點的字組* 可以實際包含任何字元。字元包含字母、數字、標點符號（尾端句點除外）、非字母符號（例如 %、&amp; 及 @）、引號、括弧、方括弧等等。其 *translation* 可包含對服務的任何合法輸入，包括空格及 SSML 格式的語音表示法。
-   *具有尾端句點的字組* 只能包含字母、句點及內部單引號（不可作為第一個或最後一個字元）。字組的 *translation* 只能包含具有普通拼法，並以空格或連字號區隔的一般字組。它不能包含語音表示法。

具有尾端句點的字組範例為 "`div.`"。假設，自訂模型包含項目 `{word='div.', translation='division'}`。服務不會將轉換套用至字串 "`div`"，因為它不包含尾端句點，因此不符合項目。

## 使用 IBM SPR 項目
{: #sprNotes}

「符號語音表示法 (SPR)」是由 {{site.data.keyword.IBM_notm}} 開發的專屬語言相依格式，用於指定字組的發音。對於每種支援的語言，SPR 包含標音字母、音節界限的符號，以及詞彙重音層次的符號。下列基本規則適用於 SPR 項目的建立作業：

-   自訂作業介面針對字組傳回的預設發音，會以 <code>&#96;</code>（反引號）為開頭，並以 `[]`（方括弧）括住。例如，介面會針對字組 `tomato` 傳回下列發音：

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    使用自訂作業介面的方法來指定字組的轉換時，請省略反引號和方括弧。
-   您可以使用句點來指出轉換中的音節開頭，但句點是選用性的，不會影響字組的發音。只有當您在字組的轉換中包含它們時，它們才會出現在字組的發音中。請不要使用空格來指出音節界限。
-   {{site.data.keyword.IBM_notm}} 建議您在具有字組主要重音的母音前面加上 `1` 符號，但並非絕對必要。如果您未指出重音，服務會判定重音所在位置。您也可以使用 `2` 符號來指出每個次重音位置，但 `2` 符號的使用也是選用性的。只有當您在字組的轉換中包含它們時，它們才會出現在字組的發音中。

如需使用 SPR 的相關資訊，請參閱[使用 IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs)。

## 使用日文項目
{: #jaNotes}

額外的規則和 `part_of_speech` 欄位適用於日文自訂語音模型中的字組項目建立作業：

-   類似音轉換只能包含*片假名* 字元。不接受*日文漢字* 及*平假名* 字元。
-   建立字組的轉換（例如類似音或語音）時，您也可以指定選用性的 `part_of_speech` 欄位，來識別字組的詞性。服務使用詞性來產生字組的正確語調。如需完整清單，請參閱[日文詞性](#partsOfSpeech)。
-   您只能為任何字組建立單一項目，也只能為任何字組指定單一詞性。您無法為相同字組建立具有不同詞性（例如，名詞和動詞）的多個項目。為模型中已存在的字組新增轉換，會改寫字組的現有轉換，包括其詞性。
-   服務會從針對自訂語音模型定義的字組/轉換配對，套用最長的相符字組。例如，考量自訂模型的下列三個項目。

    <pre><code>{
      "words": [
        {
          "word": "&#65326;&#65337;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65326;&#65337;&#65315;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65337;&#65315;",
          "translation": "&#12520;&#12467;&#12495;&#12510;&#12481;&#12517;&#12540;&#12459;&#12460;&#12452;",
          "part_of_speech": "Mesi"
        }
      ]
    }</code></pre>

    使用這些項目時，假設服務收到下列輸入文字：<code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>。在此案例中，服務會符合字組 <code>&#65326;&#65337;&#65315;</code>，因為 <code>&#65326;&#65337;&#65315;</code> 的長度超過 <code>&#65326;&#65337;</code>，且因為 <code>&#65326;&#65337;&#65315;</code> 在 <code>&#65337;&#65315;</code> 之前先符合。

### 日文詞性
{: #partsOfSpeech}

下表列出針對日文自訂項目支援的詞性。如需指定日文自訂項目之詞性的相關資訊，請參閱[將字組新增至日文自訂模型](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuJapaneseAdd)。

<table style="width:75%">
  <caption>表 1. 日文詞性</caption>
  <tr>
    <th style="text-align:center"><code>part_of_speech</code> 引數</th>
    <th style="text-align:center; width:35%">日文意義</th>
    <th style="text-align:center; width:35%">英文意義</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>Josi</code></td>
    <td style="text-align:center"><em>Joshi</em></td>
    <td style="text-align:center">分詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Mesi</code></td>
    <td style="text-align:center"><em>Meishi</em></td>
    <td style="text-align:center">名詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kigo</code></td>
    <td style="text-align:center"><em>Kigou</em></td>
    <td style="text-align:center">符號</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Gobi</code></td>
    <td style="text-align:center"><em>Gobi</em></td>
    <td style="text-align:center">字形變化</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Dosi</code></td>
    <td style="text-align:center"><em>Doushi</em></td>
    <td style="text-align:center">動詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Jodo</code></td>
    <td style="text-align:center"><em>Jodoushi</em></td>
    <td style="text-align:center">輔助動詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Koyu</code></td>
    <td style="text-align:center"><em>Koyuumeishi</em></td>
    <td style="text-align:center">專有名詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stbi</code></td>
    <td style="text-align:center"><em>Setsubiji</em></td>
    <td style="text-align:center">字尾</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Suji</code></td>
    <td style="text-align:center"><em>Suuji</em></td>
    <td style="text-align:center">數字</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kedo</code></td>
    <td style="text-align:center"><em>Keiyodoushi</em></td>
    <td style="text-align:center">形容動詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Fuku</code></td>
    <td style="text-align:center"><em>Fukishi</em></td>
    <td style="text-align:center">副詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Keyo</code></td>
    <td style="text-align:center"><em>Keiyoshi</em></td>
    <td style="text-align:center">形容動詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stto</code></td>
    <td style="text-align:center"><em>Settoji</em></td>
    <td style="text-align:center">字首</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Reta</code></td>
    <td style="text-align:center"><em>Rentaishi</em></td>
    <td style="text-align:center">限定詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stzo</code></td>
    <td style="text-align:center"><em>Setsuzokushi</em></td>
    <td style="text-align:center">連接詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kato</code></td>
    <td style="text-align:center"><em>Kantoushi</em></td>
    <td style="text-align:center">感歎詞</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Hoka</code></td>
    <td style="text-align:center"><em>Hoka</em></td>
    <td style="text-align:center">其他</td>
  </tr>
</table>
