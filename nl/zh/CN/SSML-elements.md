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

通过 {{site.data.keyword.texttospeechfull}} 服务，您可以使用大多数语音合成标记语言 (SSML) 元素来控制文本的合成。这些元素可用于所有支持的语言。下表概述了该服务对 SSML 元素和属性的支持。

-   *完全*表示服务完全支持通过其 HTTP 和 WebSocket 接口使用该元素或属性。
-   *部分*表示服务不支持该元素或属性的所有方面。此外，还可能意味着服务仅支持通过其中一个接口使用该元素或属性，或者并非所有声音都支持该元素或属性。
-   *无*表示服务不支持该元素或属性。

有关某个元素或属性的更多信息，请参阅其描述。在特别说明之处，对某些属性和值的支持与 SSML 规范略有不同。有关更多信息，请参阅 [W3C Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/speech-synthesis/){: external}。

<table>
  <caption>表 1. SSML 元素</caption>
  <tr>
    <th style="text-align:left; width:30%">元素或属性</th>
    <th style="text-align:center; width:12%">支持</th>
    <th style="text-align:left; width:46%; padding-left:75px">元素或属性</th>
    <th style="text-align:center; width:12%">支持</th>
  </tr>
  <tr>
    <td>[Audio](#audio_element)</td>
    <td style="text-align:center">无</td>
    <td style="padding-left:75px">[Say-as](#say-as_element)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td>[Break](#break_element)</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:100px">[cardinal](#sayAsCardinal)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td>[Desc](#desc_element)</td>
    <td style="text-align:center">无</td>
    <td style="padding-left:100px">[date](#sayAsDate)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td>[Emphasis](#emphasis_element)</td>
    <td style="text-align:center">无</td>
    <td style="padding-left:100px">[digits](#sayAsDigits)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td>[Lexicon](#lexicon_element)</td>
    <td style="text-align:center">无</td>
    <td style="padding-left:100px">[letters](#sayAsLetters)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td>[Mark](#mark_element)</td>
    <td style="text-align:center">部分</td>
    <td style="padding-left:100px">[number](#sayAsNumber)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td>[Meta](#mm_element)</td>
    <td style="text-align:center">无</td>
    <td style="padding-left:125px">cardinal</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td>[Metadata](#mm_element)</td>
    <td style="text-align:center">无</td>
    <td style="padding-left:125px">ordinal</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td>[Paragraph](#ps_element)</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:125px">telephone</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td>[Phoneme](#phoneme_element)</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:150px">punctuation</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:100px">[ordinal](#sayAsOrdinal)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:100px">[vxml:boolean](#vxml-boolean)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td>[Prosody](#prosody_element)</td>
    <td style="text-align:center">部分</td>
    <td style="padding-left:100px">[vxml:currency](#vxml-currency)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td style="padding-left:25px">contour</td>
    <td style="text-align:center">无</td>
    <td style="padding-left:100px">[vxml:date](#vxml-date)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td style="padding-left:25px">duration</td>
    <td style="text-align:center">无</td>
    <td style="padding-left:100px">[vxml:digits](#vxml-digits)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[pitch](#prosody-pitch)</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:100px">[vxml:phone](#vxml-phone)</td>
    <td style="text-align:center">部分</td>
  </tr>
  <tr>
    <td style="padding-left:25px">range</td>
    <td style="text-align:center">无</td>
    <td style="padding-left:75px">[Sentence](#ps_element)</td>
    <td style="text-align:center">完全</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[rate](#prosody-rate)</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:75px">[Speak](#speak_element)</td>
    <td style="text-align:center">完全</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[volume](#prosody-volume)</td>
    <td style="text-align:center">部分</td>
    <td style="padding-left:75px">[Sub](#sub_element)</td>
    <td style="text-align:center">完全</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td style="padding-left:75px">[Voice](#voice_element)</td>
    <td style="text-align:center">无</td>
  </tr>
</table>

## audio 元素
{: #audio_element}

`<audio>` 元素用于将记录的元素插入到服务生成的音频中。不支持此元素。

## break 元素
{: #break_element}

`<break>` 元素用于在语音文本中插入停顿。此元素具有以下可选属性：

-   `strength` 指定各种不同强度值的停顿长度：
    -   `none` 禁止在处理期间可能生成的停顿。
    -   `x-weak`、`weak`、`medium`、`strong` 或 `x-strong` 会插入强度依次递增的停顿。
-   `time` 指定停顿的长度（以秒或毫秒为单位）。有效值的格式为 `{integer}s`（表示秒）或 `{integer}ms`（表示毫秒）。

```xml
<speak version="1.0">
  Different sized <break strength="none">无停顿</break>
  Different sized <break strength="x-weak">超弱停顿</break>
  Different sized <break strength="weak">弱停顿</break>
  Different sized <break strength="medium">中等停顿</break>
  Different sized <break strength="strong">强停顿</break>
  Different sized <break strength="x-strong">超强停顿</break>
  Different sized <break time="1s">1 秒停顿</break>
  Different sized <break time="1500ms">1500 毫秒停顿</break>
</speak>
```
{: codeblock}

## desc 元素
{: #desc_element}

`<desc>` 元素只能在 `<audio>` 元素中出现。因为不支持 `<audio>` 元素，所以也不支持 `<desc>` 元素。

## emphasis 元素
{: #emphasis_element}

`<emphasis>` 元素用于请求以强调方式对所含文本发音。不支持此元素。

## lexicon 元素
{: #lexicon_element}

`<lexicon>` 元素用于引入给定 SSML 文档的发音字典。不支持此元素。

可以使用服务的定制接口来定义在语音合成期间使用的定制条目（词/转换项对）字典。有关更多信息，请参阅[了解定制](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。

## mark 元素
{: #mark_element}

仅服务的 WebSocket 接口支持 `<mark>` 元素，服务的 HTTP 接口不支持此元素，会将其忽略。有关更多信息，请参阅[指定 SSML 标记](/docs/services/text-to-speech?topic=text-to-speech-timing#mark)。
{: note}

`<mark>` 元素是一个空元素，用于在要合成的文本中放入标记。在合成了 `<mark>` 元素前面的所有文本后，系统会通知客户机。此元素接受单个 `name` 属性，用于指定唯一标识 mark 的字符串；名称必须以字母数字字符开头。名称会与在合成音频中遇到 mark 的时间一起返回。

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

## meta 和 metadata 元素
{: #mm_element}

`<meta>` 和 `<metadata>` 元素是容器，可在其中放入有关文档的信息。不支持这两个元素。

## paragraph 和 sentence 元素
{: #ps_element}

`<paragraph>`（或 `<p>`）和 `<sentence>`（或 `<s>`）元素是可选元素，可用于提供有关文本结构的提示。如果 `<paragraph>` 或 `<sentence>` 元素所含的文本未以句末标点字符（如句点）结尾，那么服务向合成音频添加的停顿时间要长于正常停顿时间。

其中任一元素的唯一有效属性是 `xml:lang`，此属性允许切换语言。不支持此属性。

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

`<phoneme>` 元素用于为所含文本提供拼音发音。拼音拼写表示词的发音、对发音划分音节的方式以及哪些音节重读。此元素具有两个属性：

-   `alphabet` 是可选属性，用于指定要使用的音位。支持的 alphabet 包括：
    -   标准国际音标 (IPA)：`alphabet="ipa"`
    -   {{site.data.keyword.IBM_notm}} 符号拼音表示法 (SPR)：`alphabet="ibm"`

    如果未指定 alphabet，那么缺省情况下，服务会使用 IBM SPR。
-   `ph` 是必需属性，用于以所指示的 alphabet 提供发音。以下示例显示了词 *tomato* 的这两种格式的发音：

    -   IPA 格式：

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   具有 Unicode 符号的 IPA 格式：

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   IBM SPR 格式：

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

有关将 SPR 和 IPA 表示法用于 `<phoneme>` 元素的更多信息，请参阅[使用 IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs)。

## prosody 元素
{: #prosody_element}

`<prosody>` 元素用于控制文本的音高、语速和音量。所有属性都是可选的，但如果未指定任何属性，那么会发生错误。SSML 规范允许使用以下三个属性，但服务并不支持这三个属性：`contour`、`range` 和 `duration`。服务支持的属性是：`pitch`、`rate` 和 `volume`。

### pitch 属性
{: #prosody-pitch}

`pitch` 属性用于修改 prosody 元素内文本的基线音高。接受的值如下：

-   数字，后跟 `Hz`（赫兹）单位：基线音高将变换（升高或降低）为指定的值。
-   相对更改值（以半音程为单位）：数字，用于从当前基线进行绝对位移。数字前面附加 `+`（表示升高）或 `-`（表示降低），并且后跟 `st`（半音程），例如 `+5st`。
-   相对更改（以百分比为单位）：数字，用于从当前基线进行相对位移。数字前面附加 `+`（表示升高）或 `-`（表示降低），并且后跟 `%`（百分比符号），例如 `-10%`。
-   下列六个关键字中的一个关键字，用于将音高修改为对应的预定义值：
    -   `default` 使用服务的缺省基线音高。
    -   `x-low` 将音高基线下移 12 个半音程。
    -   `low` 将音高基线下移 6 个半音程。
    -   `medium` 产生的行为与 `default` 相同。
    -   `high` 将音高基线上移 6 个半音程。
    -   `x-high` 将音高基线上移 12 个半音程。

    ```xml
    <speak version="1.0">
      <prosody pitch="150Hz">使音高变换为 150 赫兹</prosody>
      <prosody pitch="-20Hz">使音高从基线降低 20 赫兹</prosody>
      <prosody pitch="+20Hz">使音高从基线升高 20 赫兹</prosody>
      <prosody pitch="-12st">使音高从基线降低 12 个半音程</prosody>
      <prosody pitch="+12st">使音高从基线升高 12 个半音程</prosody>
      <prosody pitch="x-low">使音高从基线降低 12 个半音程</prosody>
    </speak>
    ```
    {: codeblock}

### rate 属性
{: #prosody-rate}

`rate` 属性用于指示 prosody 元素内文本的语速变化。语速是以每分钟字数指定的；如果语速为 50 个字/分钟，那么 `rate` 等于 `50`。`rate` 设置为正数时，该实现不符合当前的 W3C prosody rate 属性规范。此外，服务支持相对百分比更改（例如，`+15%`），但不支持相对值更改（例如，`+15`）。接受的值如下：

-   相对百分比增加或减少：`+10%`。
-   每分钟字数（正数）：`75`。
-   `default` 使用服务的缺省语速。
-   `x-slow` 使语速降低 50%。
-   `slow` 使语速降低 25%。
-   `medium` 产生的行为与 `default` 相同。
-   `fast` 使语速增加 25%。
-   `x-fast` 使语速增加 50%。

```xml
<speak version="1.0">
  <prosody rate="slow">使语速降低 25%</prosody>
  <prosody rate="50">将语速设置为 50 个字/分钟</prosody>
  <prosody rate="+5%">使语速增加 5%</prosody>
</speak>
```
{: codeblock}

### volume 属性
{: #prosody-volume}

服务不支持 `<prosody>` 元素的 `volume` 属性用于其神经声音（例如，`en-US_AllisonV3Voice`）。有关更多信息，请参阅[神经声音](/docs/services/text-to-speech?topic=text-to-speech-voices#neuralVoices)。
{: note}

`volume` 属性用于修改 prosody 元素内文本的音量。可以指定范围在 1.0 到 100.0（最大音量）之间的整数或小数值。此外，还可以使用下列其中一个字符串值，这些值对应于范围在 0 到 100 之间的预定义设置。（不支持 `silent` 值。）

-   `x-soft` 的值为 30。
-   `soft` 的值为 50。
-   `medium` 的值为 80。
-   `loud` 的值为 90。
-   `default` 的值为 92。
-   `x-loud` 的值为 100。

```xml
<speak version="1.0">
  <prosody volume="75">音量修改为 75</prosody>
  <prosody volume="88.9">音量修改为 88.9</prosody>
  <prosody volume="loud">音量修改为 90</prosody>
</speak>
```
{: codeblock}

## say-as 元素
{: #say-as_element}

大多数语言仅部分支持 `<say-as>` 元素。对于除美国英语以外的其他语言，服务通常仅支持 prosody 元素的 `digits` 和 `letters` 属性。
{: note}

`<say-as>` 元素提供有关元素中所含文本类型的信息，并指定呈现文本的详细级别。此元素有一个必需属性 `interpret-as`，用于指示如何解释所含文本。有两个可选属性：`format` 和 `detail`，这两个属性仅与 `interpret-as` 属性中的特定值一起使用，如以下示例中所示。

下面是 `interpret-as` 属性的可接受值和每个值的示例。

### cardinal
{: #sayAsCardinal}

`cardinal` 值用于将 say-as 元素中的数字读作基数。以下示例读作 *Super Bowl forty-nine*。第一个示例是多余的，因为它不会更改服务的缺省行为。

```xml
<speak version="1.0">
  Super Bowl <say-as interpret-as="cardinal">49</say-as>
  Super Bowl <say-as interpret-as="cardinal">XLIX</say-as>
</speak>
```
{: codeblock}

### date
{: #sayAsDate}

`date` 值用于根据关联的 `format` 属性中给出的格式来对 say-as 元素内的日期发音。`format` 属性对于 `date` 值是必需的。如果未提供 `format`，服务仍会尝试对日期发音。以下示例以指定格式对指示的日期发音，其中 `d`、`m` 和 `y` 分别表示日、月和年。

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

`digits` 值用于对 say-as 元素内数字中的每位数发音。以下示例将对 *123456* 中的每位数发音。

```xml
<speak version="1.0">
  <say-as interpret-as="digits">123456</say-as>
</speak>
```
{: codeblock}

### letters
{: #sayAsLetters}

`letters` 值用于拼读 say-as 元素内词中的字符。以下示例将拼读词 *hello* 中的字母。

```xml
<speak version="1.0">
  <say-as interpret-as="letters">Hello</say-as>
</speak>
```
{: codeblock}

### number
{: #sayAsNumber}

`number` 值是 `cardinal` 和 `ordinal` 值的替代项。可以使用可选的 `format` 属性来指示如何解释一系列数字。第一个示例省略了 `format` 属性，以将数字作为 cardinal 值发音。第二个示例显式指定数字将作为 `cardinal` 值发音。第三个示例指定数字将作为 `ordinal` 值发音。

```xml
<speak version="1.0">
  <say-as interpret-as="number">123456</say-as>
  <say-as interpret-as="number" format="cardinal">123456</say-as>
  <say-as interpret-as="number" format="ordinal">123456</say-as>
</speak>
```
{: codeblock}

此外，还可以为 `format` 属性指定值 `telephone`。以下示例说明了通过两种不同的方法，将一系列数字作为电话号码发音。要对包含标点的数字发音，请为可选的 `detail` 属性指定值 `punctuation`。

```xml
<speak version="1.0">
  <say-as interpret-as="number" format="telephone">555-555-5555</say-as>
  <say-as interpret-as="number" format="telephone" detail="punctuation">555-555-5555</say-as>
</speak>
```
{: codeblock}

### ordinal
{: #sayAsOrdinal}

`ordinal` 值用于将 say-as 元素内的数字读作序数值。以下示例读作 *second first*。

```xml
<speak version="1.0">
  <say-as interpret-as="ordinal">2</say-as>
  <say-as interpret-as="ordinal">1</say-as>
</speak>
```
{: codeblock}

### vxml:boolean
{: #vxml-boolean}

根据 `vxml:boolean` 在 say-as 元素中的值是 `true` 还是 `false`，会分别读作 *yes* 或 *no*。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:boolean">true</say-as>
  <say-as interpret-as="vxml:boolean">false</say-as>
</speak>
```
{: codeblock}

### vxml:currency
{: #vxml-currency}

`vxml:currency` 值用于控制货币值的合成。该字符串的编写格式必须为 `UUUmm.nn`，其中 `UUU` 是 ISO 标准 4217 指定的三字符货币指示符，`mm` 是数量。以下示例读作 *forty-five dollars and thirty cents*。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.30</say-as>
</speak>
```
{: codeblock}

如果指定的数字包含两个以上的小数位，那么会将金额合成为十进制数，后跟货币指示符。如果未提供三字符货币指示符，那么仅将金额合成为十进制数，且货币类型不发音。以下示例读作 *forty-five point three two nine US dollars*。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.329</say-as>
</speak>
```
{: codeblock}

### vxml:date
{: #vxml-date}

`vxml:date` 值的工作方式类似于 `date` 值，但格式已预定义为 `YYYYMMDD`。如果日、月或年值未知，或者您不希望值发音，请将值替换为 `?`（问号）。第二个和第三个示例包含问号。

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

`vxml:digits` 值提供的功能与 `digits` 值的相同。

### vxml:phone
{: #vxml-phone}

`vxml:phone` 值用于对包含数字和标点的电话号码发音。此值相当于使用 `number` 值，为 `format` 属性指定 `telephone`，并为 `detail` 属性指定 `punctuation`。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:phone">555-555-5555</say-as>
</speak>
```
{: codeblock}

## speak 元素
{: #speak_element}

`<speak>` 元素是 SSML 文档的根元素。有效属性如下：

-   `version` 是用于指定 SSML 规范的必需属性。接受的值为 `1.0`。
-   服务不需要 `xml:lang`。使用 speak 元素时，请省略此属性。
-   `xml:base` 没有任何影响。

```xml
<speak version="1.0">
  The text to be spoken.
</speak>
```
{: codeblock}

## sub 元素
{: #sub_element}

`<sub>` 元素用于指示在合成语音时，将 `alias` 属性指定的文本替换为此元素内所含的文本。`alias` 属性是 sub 元素的唯一属性，也是必需的属性。

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

## voice 元素
{: #voice_element}

`<voice>` 元素用于请求更改声音。不支持此元素。
