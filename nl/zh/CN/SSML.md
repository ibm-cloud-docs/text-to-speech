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

语音合成标记语言 (SSML) 是一种基于 XML 的标记语言，为语音合成应用程序提供文本注释。根据 VoiceXML 2.0 规范，W3C 语音浏览器工作组建议将 SSML 用作语音合成的标准标记语言。SSML 为语音应用程序的开发者提供了一种标准方法，通过支持开发者利用标记来指定发音、音量、音高、语速和其他属性，从而控制合成过程的各个方面。
{: shortdesc}

通过 {{site.data.keyword.texttospeechfull}} 服务，可以使用 SSML 来控制所有支持的语言的文本合成。这包括使用 SSML `<phoneme>` 元素来定义用国际音标 (IPA) 或 {{site.data.keyword.IBM_notm}} 符号拼音表示法 (SPR) 表示的词发音。服务还通过其定制接口依赖于 SSML `<phoneme>` 元素来定义词的拼音转换项；有关更多信息，请参阅[了解定制](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。

## SSML 简介
{: #introduction-SSML}

SSML 的运作方式是通过一组预定义的元素或标记来扩充传递到合成器的纯文本。XML 解析器首先将纯输入文本与标记规范分离。这些规范随后就会作为一组指令，以合成器可理解并能生成所需效果的格式进行处理和发送。为了使 XML 解析器能执行此作业，需要正确设置标记的格式；例如，元素必须有结束标记，并且多个元素必须正确嵌套。有关基本 XML 概念的简介，请参阅 [w3schools.com/xml/xml_whatis.asp](http://www.w3schools.com/xml/xml_whatis.asp){: external}。

SSML 元素是包含在开始标记及其匹配的结束标记内的任何内容（包括开始和结束标记）。如以下示例中所示，元素可以包含其他元素（标记可以嵌套）和文本的组合。此外，元素可以要求或可选择接受设置为特定值的属性。

```xml
<tag1>
  <tag2 attributeName="attributeValue">
    ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

完整的合法 SSML 文档包含 XML 序言（其中包含用于据以验证 SSML 文档的编码和模式等信息），后跟根元素 `<speak>`。（有关序言结构的更多信息，请参阅 [tizag.com/xmlTutorial/xmlprolog.php](http://www.tizag.com/xmlTutorial/xmlprolog.php){: external}。）在 `<speak>` 元素范围内，可指定要合成的文本，并使用其他元素进行扩充。

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

服务支持 SSML 片段，这些片段是不包含完整 XML 头的 SSML 元素。

## SSML 支持
{: #ssmlSupport}

{{site.data.keyword.texttospeechshort}} 服务的支持基于 SSML V1.0，W3C 于 2004 年 9 月 7 日建议使用 SSML。有关 W3C SSML 建议的更多信息，请参阅 [W3C Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/speech-synthesis/){: external}。

有关将 SSML 用于服务的更多信息，请参阅以下内容：

-   有关对所有 SSML 元素的服务支持级别的完整信息，请参阅 [SSML 元素](/docs/services/text-to-speech?topic=text-to-speech-elements)。除了少数例外情况外，服务实现了大部分 W3C 规范以及 SSML 片段。
-   服务扩展了 SSML：增加了 `<express-as>` 元素，用于指示说话时如何表达文本（表达为好消息、道歉或不确定）。服务仅支持对美国英语 Allison 声音使用表现力。请参阅[使用表现力 SSML](/docs/services/text-to-speech?topic=text-to-speech-expressive)。
-   服务扩展了 SSML：增加了 `<voice-transformation>` 元素，使您能够控制所读文本的音高、音高范围、喉音张力、气息声、语速和音色，以便扩展可能的声音的范围。服务还提供了两个内置的虚拟声音：*Young* 和 *Soft*。服务仅支持对美国英语声音使用声音变换。请参阅[使用声音变换 SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation)。
-   服务的定制接口支持使用 SSML `<phoneme>` 元素来指定用于对词发音的拼音拼读。拼音拼读表示词的各个发音、对这些发音划分音节的方式以及哪些音节有重音。
    -   有关定制接口的信息，请参阅[了解定制](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。
    -   有关对于任何支持的语言，在 {{site.data.keyword.IBM_notm}} SPR 或 IPA 规范中可以使用的有效音标符号的信息，请参阅[使用 IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs)。

## SSML 验证
{: #errors}

服务会验证您在任何内容中作为用于合成的输入文本或者作为用于定制的词转换项的定义而提交的所有 SSML 元素。服务无法提前确定提交用于合成的文本是否包含 SSML 元素。因此，它会对所有输入文本执行相同的验证，而不管其中是否包含 SSML。

-   *所有 SSML 输入必须正确且格式无误。*服务以静默方式忽略不支持的 SSML 元素。服务会合成不支持的元素或使用不支持功能的元素内所含的文本；只有该元素会被忽略。
-   *服务会针对无效元素报告 HTTP 400 错误代码。*错误响应包含描述性消息，并且请求会失败。

具体来说，服务会在以下情况下返回错误：

-   *元素无效。*例如，您未正确指定标记，省略了必需属性，或者包含开始标记，但未包含匹配的结束标记。
-   *音标符号无效。*对于指定的语言，`<phoneme>` 元素的 `ph` 属性包含不支持的 IPA 或 SPR 音标符号。
-   *无元音。*`<phoneme>` 元素的 `ph` 属性指定了不包含元音的词发音。
-   *在无效的位置进行了法语联诵。*在 `<phoneme>` 元素的 `ph` 属性中，联诵字符未跟在辅音之后，或者出现在词发音的中间。
-   *日语 `:` 音标符号不在元音之前。*在 `<phoneme>` 元素的 `ph` 属性中，`:` 字符后面未跟元音（该字符与元音之间可能有其他音标符号，如音节边界）。
-   *音节重音无效。*{{site.data.keyword.IBM_notm}} SPR 的 `<phoneme>` 元素的 `ph` 属性包含无效的音节重音。对于法语，音节重音符号没有紧挨在元音之前。对于西班牙语或意大利语，使用了次重音 (`2`) 或无重音 (`0`) 符号。对于日语，使用了次重音符号 (`2`)。
-   *SSML `<express-as>` 或 `<voice-transformation>` 元素的使用无效。*只能将这些 SSML 扩展用于指定的标准美国英语声音。
-   *SSML `<prosody>` 元素的使用无效。*您无法将 `<prosody>` 元素的 `contour`、`duration` 和 `range` 属性用于任何声音。此外，您无法将 `<prosody>` 元素的 `volume` 属性用于神经声音（例如，`en-US_AllisonV3Voice`）。
-   *未转义的 XML 控制字符。*输入文本本身包含 <code>&quot;</code>、<code>&apos;</code>、`&`、`<` 或 `>` 字符，而不是其等效的转义字符串或字符编码。有关更多信息，请参阅[对 XML 控制字符转义](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#escape)。
