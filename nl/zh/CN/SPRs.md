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

{{site.data.keyword.texttospeechfull}} 服务同时支持标准国际音标 (IPA) 和 {{site.data.keyword.IBM}} 符号拼音表示法 (SPR) 来表示词的发音。SPR 是一种拼音编码，表示词的整体读音、构成词的各个发音、对这些发音划分音节的方式以及哪些音节重读。SPR 是 IPA 的替代表示法。
{: shortdesc}

以下各部分介绍了 {{site.data.keyword.IBM_notm}} SPR 表示法。由于 IPA 是标准表示法，因此本文档并未提供 IPA 的基本用法信息。有关简要用法指南，请参阅[使用 IPA](#ipa)。

## IBM SPR 简介
{: #introduction-SPRs}

SPR 发音是使用语音合成标记语言 (SSML) 的 [phoneme 元素](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)定义的。此元素包含给定语言允许的音标符号序列，用双引号括起。音标符号定义 `<phoneme>` 元素中所含的词如何发音。此元素的 `alphabet` 属性的值 `ibm` 用于指示发音是以 SPR 定义的，而 `ph` 属性用于定义发音。下面是美国英语中单词 *through* 和 *shocking* 的有效 SPR 表示法示例：

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

在定义中，`.`（句点）表示新音节的开头，数字 `1` 和 `0` 指示音节的重音级别，字母表示美国英语语音的特定发音。不符合必需规范的 SPR 条目无效。

## 音节边界

可以使用 `.`（句点）来标记每个音节的开头。但是，为了保留语言的有效拼音，在某些情况下（例如，如果音节边界的放置位置对于某种语言是不合法或不自然的位置），服务可以选择不采用句点。通常，在用户可以指示音节边界的有效首选项或词发音其他方面的情况下，服务会采用此类请求。

## 音节重音

可以使用下表中的音标符号来标记发音的音节重音。{{site.data.keyword.IBM_notm}} 建议在 SPR 或 IPA 中标明发音中的主重音。而在这两种格式中标明音节重音不是必需的；如果未标明，服务会确定音节重音出现的位置。

<table style="width:80%">
  <caption>表 1. 音节重音</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IBM SPR 音标符号
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA 音标符号
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      含义
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
    <td style="text-align:center">无音标符号</td>
    <td style="text-align:center">无值</td>
    <td>
      无重音
    </td>
  </tr>
</table>

**注：**

-   在 IPA 中，对于法语，将忽略音节重音符号。在 SPR 中，对于法语，不会忽略音节重音；如果指定了音节重音，那么音节重音必须紧挨在该音节的元音之前。在 SPR 中，法语的音节重音要比其他语言严格得多；如果重音符号位于无效位置，那么会发生错误。
-   在 SPR 中，对于西班牙语和意大利语，只能指定 `1`（主重音）。如果指定次重音或未指定重音，那么会发生错误。
-   在 SPR 中，对于日语，仅支持 `1`（主重音）和 `0`（无重音）。如果指定次重音，那么会发生错误。

必须将音节重音标记放在音节边界内，但必须始终位于音节元音的左侧。可以将标记放置在重读元音左侧的任何位置。例如，以下每个 SPR 示例都将主重音放在词 *construction* 的正确元音上：

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

## 语音发音符号

每种语言都使用自己的 SPR 音标符号清单来表示该语言的语音发音。以下规则适用于指定 SPR 音标符号：

-   字母是区分大小写的，例如 `e` 和 `E` 表示两个不同的发音。
-   双字符和三字符音标符号必须用单引号括起；例如，德语单词 *heim* 中的音标符号 `aj`：`"h'aj'm"`。
-   服务会将包含语言中不允许使用的发音符号的任何 SPR 定义视为无效。

此外，以 SPR 格式定义词的发音时，请考虑以下因素：

-   每种语言的发音都具有该语言的特定分布模式。例如，在英语的所有方言中，*sing* (`".1sIG"`) 中的 `G` 音不会出现在单词开头。其他分布范围极窄的美国英语发音是喉塞音 (`?`)、闪音 (`F`) 和元音化鼻辅音 (`N`)。如果在上下文中输入了一个正常情况下不会在该处出现的发音符号，那么生成的语音可能会听起来不自然。
-   {{site.data.keyword.texttospeechshort}} 服务会将一组复杂的语言规则应用于其输入，以反映发音在自然语言中特定上下文中的变化过程。例如，在美国英语中，单词 *write* (`".1r1Yt"`) 的 `t` 音在 *writer* (`".1rY.0FR"`) 中发为闪音 (`F`)。SPR 输入会像普通输入文本一样经历这些修改。在此示例中，输入 `".1rY.0tR"` 或 `".1rY.0FR"` 不会影响生成的语音。

## 使用 IPA
{: #ipa}

以下信息适用于使用 IPA 表示法的发音：

-   仅使用记录的 IPA 音标符号。如果针对一个 SPR 音标符号列出了多个 IPA 音标符号（或音标符号组合），所有这些 IPA 音标符号都等效于这个 SPR 音标符号。在这种情况下，服务会将所有这些 IPA 音标符号都视为相同，并且不会实现 IPA 系统想要描述的细微差异或区域性差异。
-   还可以将 IPA 发音指定为 IPA Unicode 值。在以下部分中列出的特定于语言的表中记录了 IPA 音标符号及其等效的 IPA Unicode 值。有关使用 IPA Unicode 值的示例发音，请参阅 [phoneme 元素](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)。

要了解更多信息，请参阅以下内容：

-   有关 IPA 的更多信息，请参阅 [International Phonetic Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}。
-   有关 Unicode 的拼音符号的更多信息，请参阅 [Phonetic symbols in Unicode](https://wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: external}。

## 支持的语言
{: #supportedLanguages}

以下各页面记录了每种语言的 SPR 音标符号、IPA 音标符号和等效的 IPA Unicode 值。其中显示了相应语言的词中每种音标符号的示例。由于方言差异，示例可能并不总是与您的发音相匹配。

-   [巴西葡萄牙语音标符号](/docs/services/text-to-speech?topic=text-to-speech-ptSymbols)
-   [英国英语音标符号](/docs/services/text-to-speech?topic=text-to-speech-gbSymbols)
-   [法语音标符号](/docs/services/text-to-speech?topic=text-to-speech-frSymbols)
-   [德语音标符号](/docs/services/text-to-speech?topic=text-to-speech-deSymbols)
-   [意大利语音标符号](/docs/services/text-to-speech?topic=text-to-speech-itSymbols)
-   [日语音标符号](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols)
-   [西班牙语音标符号](/docs/services/text-to-speech?topic=text-to-speech-esSymbols)
-   [美国英语音标符号](/docs/services/text-to-speech?topic=text-to-speech-usSymbols)
