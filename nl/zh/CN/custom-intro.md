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

# 了解定制
{: #customIntro}

使用 {{site.data.keyword.texttospeechfull}} 合成文本时，该服务会应用与语言相关的发音规则。服务通过应用规则，将每个词的普通（正字法）拼写转换为拼音拼写。词的拼音拼写使用音位符号来定义词的发音方式。这些符号是不同的声音单位，用于区分语言中的各个词、音节之间的边界和音节的重音标记。
{: shortdesc}

服务的常规发音规则对于普通词非常适用。但是，对于异常词，这些规则生成的结果可能并不理想。此类词包括特殊外来词、人名或地名，以及缩写或首字母缩略词。如果应用程序的词汇中包含此类词，那么可以使用定制接口来指定服务如何对此类词发音。

定制接口是 Beta 功能，可用于所有语言。
您必须具有标准价格套餐，才能使用声音模型定制。轻量套餐的用户无法使用定制接口。有关更多信息，请参阅 {{site.data.keyword.texttospeechshort}} 服务的[定价页面](https://www.ibm.com/cloud/watson-text-to-speech/pricing){: external}。
{: note}

## 定制工作方式
{: #ciHow}

通过 {{site.data.keyword.texttospeechshort}} 服务的定制接口，可为特定语言创建词及其转换项的字典。此字典称为*定制声音模型*，或简单称为定制模型。定制声音模型中的每个定制条目都由一个*词*/*转换项*对组成。词的转换项会指示服务在输入文本中出现该词时如何发音。

定制接口提供了多种方法，用于创建和管理由服务永久存储的定制声音模型。创建定制模型后，可以在使用任何版本的 `/v1/synthesize` 方法进行合成期间使用该模型。服务合成输入文本时，对于出现在定制模型中的词，会通过直接或间接应用其转换项来确定这些词的发音。由于您为特定语言创建了定制声音模型，因此定制模型可与该语言中可用的任何声音（标准或神经）一起使用。

可以将定制声音模型中词的转换项指定为*近似读音转换项*或*拼音转换项*。可以将这两种方法用于同一定制模型中的条目，并且可以在同一转换项中混合使用这两种方法。对于定制条目，有若干规则和准则适用。有关更多信息，请参阅[用于创建定制条目的规则](/docs/services/text-to-speech?topic=text-to-speech-rules)。

## 近似读音转换项
{: #soundsLike}

*近似读音转换项*使用服务的常规发音规则以间接方式表示目标词的发音。近似读音转换项是通过一个或多个其他词的常规发音而构成的。服务首先将输入文本中出现该词的地方全部替换为指定转换项。然后，将其常规发音规则应用于转换项，再将转换项转换为其拼音表示，从而获取发音。

例如，服务的常规发音规则可正确转换许多常见的缩写和首字母缩略词。服务会将缩写 *cm* 发音为 *centimeter*。对于不太常见的缩写，会逐个字母发音。例如，服务将字符串 *Str*（*street* 的缩写）发音为 *S T R*，即对每个字母分别发音。可以使用近似读音方法为字符串 *Str* 指定转换项 *street*。

首字母缩略词的另一个示例是词 *IEEE*，表示 Institute of Electrical and Electronic Engineers（电气电子工程师学会）。缺省情况下，服务将此首字母缩略词发音为 *I E E E*。但此首字母缩略词的通常发音是 *I triple E*，这可以使用简单的近似读音转换项 *I triple E* 来轻松定义。如果词 *IEEE* 出现在定制模型中并具有此转换项，那么每次出现该词时，服务都会将其替换为此转换项。然后，服务会将其常规发音规则应用于单独的词 *I*、*triple* 和 *E*，以生成普通发音。

近似读音方法不仅仅可应用于缩写和首字母缩略词。它也同样适用于复杂词或异常词。例如，以下这对近似读音转换项会为异常词生成正确的发音，这些词若通过服务的常规发音规则处理，结果并不理想。为此类词查找合适的转换项可能要比简单的缩写更困难。以下转换项使用常规发音规则来改变词的拼写。

<table style="width:35%">
  <caption>表 1. 示例近似读音转换项</caption>
  <tr>
    <th style="text-align:left">词</th>
    <th style="text-align:left">转换项</th>
  </tr>
  <tr>
    <td>ayurvedic</td>
    <td>aayervedic</td>
  </tr>
  <tr>
    <td>gastroenteritis</td>
    <td>gastro enteritis</td>
  </tr>
</table>

正如这些示例所示，开发近似读音转换项更偏向于试错法，而不是公式化转换。您根据自己的直觉和服务使用经验来创建候选转换项。然后，根据候选转换项将词合成为输入文本，并听取生成的音频。如果您对发音满意，那么可以在定制模型中使用该转换项；若不满意，可修改该转换项并再次对其进行测试。

## 拼音转换项
{: #phonetic}

近似读音方法是获得发音的相对简单且有用的方法。但这种方法并不总是能开发出近似读音转换项。直接替代方法，即拼音方法，可能看起来更复杂、更耗时，但它可以获得任何词的发音。

*拼音转换项*可根据音位符号、音节重音标记以及可选的音节边界来指定发音，这些将覆盖服务的常规发音规则。指定下列其中一种格式的拼音转换项：

-   标准国际音标 (IPA) 表示法
-   专有的 {{site.data.keyword.IBM_notm}} 符号拼音表示法 (SPR)

无论用哪种表示法，都可使用基于语音合成标记语言 (SSML) 的特定音位格式来指定转换项。SSML 是一种基于 XML 的标记语言，为语音合成应用程序提供文本注释。使用 SSML `<phoneme>` 元素可为词指定拼音转换项：

<pre><code>&lt;phoneme alphabet="{ipa | ibm}" ph="{translation}"&gt;&lt;/phoneme&gt;</code></pre>

`alphabet` 属性指定拼音表示法类型：`ipa` 或 `ibm`。`ph` 属性指定拼音转换项字符串。

例如，假设词为 `trinitroglycerin`。服务的常规发音规则生成的发音与化学家和医生通常使用的发音不同。正确的发音可以通过拼音转换项来获得。

<table style="width:35%">
  <caption>表 2. 拼音转换项示例</caption>
  <tr>
    <th style="text-align:left">Alphabet</th>
    <th style="text-align:left">转换项</th>
  </tr>
  <tr>
    <td>IPA</td>
    <td>t&#633;a&#618;n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n</td>
  </tr>
  <tr>
    <td>SPR</td>
    <td>trYn1YtrxglIsxrXn</td>
  </tr>
</table>

在这些示例中，拼音转换项字符串由音位符号和一个主重音标记组成。主重音标记在 IPA 中用 <code>&#712;</code> 表示，在 SPR 中用 `1` 表示。对于这两种表示法，主重音标记都会紧挨在重读元音符号之前。虽然这些示例并未在拼音转换项中显示音节边界和次重音位置，但您也可以指定这两项。这两个元素不是必需元素，并且通常不需要这些元素来获得发音。与近似读音转换项一样，可以通过多个字符串来编写一个拼音转换项，各字符串之间用空格定界。

您还可以将 IPA 转换项指定为 IPA Unicode 值。有关更多信息，请参阅[使用 IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs) 以及在[支持的语言](/docs/services/text-to-speech?topic=text-to-speech-sprs#supportedLanguages)中所引用页面上特定于语言的表。有关使用 IPA Unicode 值的示例转换项，请参阅 [phoneme 元素](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)。
{: note}

### 使用现有拼音转换项
{: #phoneticMethod}

除非您是音韵学专家，否则编写拼音转换项并不是件容易的任务。编辑现有拼音转换项总是要比从头开始编写更容易。为了帮助您创建拼音转换项，服务的 API 包含 `GET /v1/pronunciation` 方法。此方法会返回由服务的常规发音规则为指定语言的词生成的 IPA 或 SPR 表示法。您还可以向指定定制声音模型请求词的发音，以查看该模型的语言中的转换项。

可以使用 `/GET v/1/pronunciation` 方法来获取词的初始拼音转换项。然后，可以修改转换项以获得所需的发音。与近似读音方法一样，您遵循的也是试错过程。您将候选转换项提交给服务，将词合成为输入文本，听取生成的音频，然后编辑该候选转换项。您可以重复此过程，直到对发音满意为止。

有关更多信息，请参阅[查询某种语言的词](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryLanguage)。

### 有关拼音转换项的更多信息
{: #phoneticInfo}

以下资源提供了有关拼音转换项的信息：

-   有关使用 SSML 及其 `<phoneme>` 元素的更多信息，请参阅[使用 SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml)。
-   有关指定 SPR 转换项及其等效 IPA 音标符号的更多信息，请参阅[使用 IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs)。
-   有关使用 IPA 音标符号的更多信息，以及要获取音标符号的音频样本，请查阅 Web 上的源。您可以在 [International Phonetic Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external} 中找到详细的介绍性讨论。

## 混合的近似读音和拼音转换项

您可以在同一转换项中混合使用近似读音方法和拼音方法。此功能可以减少编写转换项所涉及的工作量。

例如，假定您使用近似读音方法获得某个词的发音，并对其中部分发音感到满意。但现在需要对该词的其余元素进行微调。您可以使用拼音方法来指定词中不满意的方面。以下示例将混合转换项应用于词 `trinitroglycerin`：

<pre><code>try&lt;phoneme alphabet="ipa" ph="n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n"&gt;&lt;/phoneme&gt;</code></pre>
