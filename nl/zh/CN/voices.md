---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28"

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
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 语言和声音
{: #voices}

{{site.data.keyword.texttospeechfull}} 服务支持各种语言、声音和方言。对于每种语言，服务至少提供一个男声或女声，有时会同时提供这两者。每种声音会针对其方言使用相应的节奏和语调。
{: shortdesc}

## 支持的语言和声音
{: #languageVoices}

表 1 列出了可用于每种语言和方言的声音，包括其性别。如果在请求中省略可选的 `voice` 参数，那么缺省情况下，服务会使用 `en-US_MichaelVoice` 声音。要了解为什么服务会为一些声音提供两个版本，请参阅[语音合成技术](#technologiesVoices)。

部署 `V2` 声音时的某个问题目前会导致合成语音中有背景噪声。有关更多信息，请参阅[已知限制](/docs/services/text-to-speech/release-notes.html#limitations)。
{: note}

<table style="width:90%">
  <caption>表 1. 支持的语言和声音</caption>
  <tr>
    <th style="text-align:left">语言</th>
    <th style="text-align:center">声音</th>
    <th style="text-align:center">性别</th>
  </tr>
  <tr>
    <td style="text-align:left">巴西葡萄牙语</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">卡斯蒂利亚西班牙语</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">男声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">法语</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">德语</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code><br/>
      <code>de-DE_BirgitV2Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code><br/>
      <code>de-DE_DieterV2Voice</code></td>
    <td style="text-align:center">男声</td>
  </tr>
  <tr>
    <td style="text-align:left">意大利语</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code><br/>
      <code>it-IT_FrancescaV2Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">日语</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">拉丁美洲西班牙语</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">北美西班牙语</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">英国英语</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">美国英语</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code><br/>
      <code>en-US_AllisonV2Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaVoice</code><br/>
      <code>en-US_LisaV2Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code><br/>
      <code>en-US_MichaelV2Voice</code></td>
    <td style="text-align:center">男声</td>
  </tr>
</table>

声音 `es-LA_SofiaVoice` 和 `es-US_SofiaVoice` 本质上是相同的声音。这两种声音最重要的差异是如何解释 $（美元符号）。拉丁美洲版本使用词汇 *pesos*，而北美版本使用词汇 *d&oacute;lares*。除此之外，这两个声音之间还可能存在其他较小的差异。
{: note}

### 语音合成技术
{: #technologiesVoices}

服务为某些声音提供了两个版本，例如 `en-US_AllisonVoice` 和 `en-US_AllisonV2Voice`。这两个版本之间的主要差异反映在服务用于合成语音的技术：

-   *拼接合成*技术用于组合记录的语音段（或单元），以生成请求的音频。此技术生成的音频可能被视为更清脆的声音，但所记录音段的拼接点有时会导致语音失真。

    名称中不包含字符串 `V2` 的声音（例如，`en-US_AllisonVoice`）即为基于拼接合成技术的声音。
-   *深度学习合成*技术使用深度神经网络 (DNN) 来针对指定的文本合成语音。这种方法并不是将记录的音频段串接在一起，而是依赖机器学习对记录的语音数据进行 DNN 训练。基于深度学习（或 DNN）的合成所生成的音频在韵律方面更自然，总体质量更一致。

    名称中包含字符串 `V2` 的声音（例如，`en-US_AllisonV2Voice`）是更新的声音，使用的是基于 DNN 的合成。

在对您的应用采用新声音之前，您需要对这些声音进行试验。这两种技术会生成具有不同信号质量的音频，因此新声音可能并不是对于所有应用都更好。此外，基于 DNN 的声音不支持以下 SSML 元素或属性：

-   `<prosody>` 元素的 `volume` 属性
-   `<express-as>` 元素
-   `<voice-transformation>` 元素

如果您的应用使用了这些元素，请继续使用基于拼接合成的声音。

### 声音定制
{: #customizeVoice}

合成文本时，服务会应用与语言相关的发音规则，以将每个词的普通拼写转换为拼音拼写。服务的发音规则对于普通词非常适用，但是对于异常词（例如，外来词、人名、缩写或首字母缩略词），这些规则生成的结果可能并不理想。

如果您的应用的词汇中包含此类词，那么可以使用定制接口来指定服务如何对此类词发音。有关更多信息，请参阅[了解定制](/docs/services/text-to-speech/custom-intro.html)。

## 指定声音
{: #specifyVoice}

HTTP `GET` 和 `POST /v1/synthesize` 方法以及 WebSocket `/v1/synthesize` 方法都接受可选的 `voice` 查询参数来指定用于合成音频的声音。有关更多信息，请参阅 [HTTP 接口](/docs/services/text-to-speech/http.html)和 [WebSocket 接口](/docs/services/text-to-speech/websockets.html)。

服务对输入文本语言的理解基于指定的声音。请确保指定与输入文本的语言相匹配的声音。例如，如果指定法语声音 (`fr-FR_ReneeVoice`)，服务会假定输入文本是用法语编写的。如果传递的文本不是用该声音的语言编写的（例如，对于法语声音，传递了英语文本），那么服务可能无法生成有意义的结果。

## 列出所有可用声音
{: #listVoices}

`GET /v1/voices` 方法用于列出有关所有可用声音的信息。此方法不接受任何自变量，并返回名为 `voices` 的 JSON 数组。该数组针对每种声音包含一个单独的对象。

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaVoice",
      "language": "en-US",
      "gender": "female",
      "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
      "description": "Lisa: American English female voice.",
      "customizable": true,
      "supported_features": {
        "voice_transformation": true,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

声音对象的字段提供以下信息：

-   `name` 是声音的标识（例如，`en-US_LisaVoice`）。请为 `/v1/synthesize` 方法的 `voice` 参数指定此值。
-   `language` 指定声音的语言和区域（例如，`en-US`）。
-   `gender` 将声音标识为 `male` 或 `female`。
-   `url` 标识声音的 URL。
-   `description` 提供声音的简短描述。
-   `customizable` 是布尔值，用于指示是否可以使用服务的定制接口来定制声音。（此字段提供的信息与 `custom_pronunciation` 字段的相同，保留此字段是为了支持向后兼容性。）
-   `supported_features` 描述了声音支持的其他服务功能：
    -   `voice_transformation` 是布尔值，用于指示是否可以使用 SSML `<voice-transformation>` 元素对声音进行变换。
    -   `custom_pronunciation` 是布尔值，用于指示是否可以使用服务的定制接口来定制声音。

## 列出特定声音
{: #listVoice}

`GET /v1/voices/{voice}` 方法用于列出有关特定声音的信息。此方法接受两个参数。

<table>
  <caption>表 2. <code>voices</code> 方法的参数</caption>
  <tr>
    <th style="text-align:left; width:18%">参数</th>
    <th style="text-align:center; width:12%">类型</th>
    <th style="text-align:center; width:12%">数据类型</th>
    <th style="text-align:left">描述</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>必需</em></td>
    <td style="text-align:center">路径</td>
    <td style="text-align:center">String</td>
    <td>
      标识要返回其信息的声音。可通过其名称（例如，<code>en-US_LisaVoice</code>）来指定声音。
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>可选</em></td>
    <td style="text-align:center">查询</td>
    <td style="text-align:center">String</td>
    <td>
      提供为指定声音定义的定制声音模型的全局唯一标识 (GUID)。如果包含定制标识，那么必须使用定制模型所有者的服务凭证来调用此方法。
    </td>
  </tr>
</table>

如果省略 `customization_id` 参数，那么此方法针对指定声音返回的 JSON 输出与 `GET /v1/voices` 方法针对声音返回的信息相同。如果指定 `customization_id`，那么输出将包含 `customization` 字段，用于提供有关指定定制声音模型的信息。

```javascript
{
  "name": "en-US_LisaVoice",
  "language": "en-US",
  "gender": "female",
  "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
  "description": "Lisa: American English female voice.",
  "customizable": true,
  "supported_features": {
    "voice_transformation": true,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

其他 `customization` 字段的属性提供定制声音模型的 GUID、名称、语言和描述等信息。此外，还会显示模型所有者的服务凭证、创建模型的日期和时间，以及上次修改模型的日期和时间。
