---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-25"

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

# 语言和声音
{: #voices}

{{site.data.keyword.texttospeechfull}} 服务支持各种语言、声音和方言。对于每种语言，服务至少提供一个女声。对于某些语言，服务提供多个声音，同时包含男声和女声。每种声音会针对其方言使用相应的节奏和语调。
{: shortdesc}

先前随服务提供的 `V2` 声音已停止使用。如果您的应用程序中使用的是 `V2` 声音，那么服务会自动改为使用等效的 `V3` 声音。
{: note}

## 支持的语言和声音
{: #languageVoices}

表 1 列出了可用于每种语言和方言的声音，包括其类型和性别。所有声音都提供了[标准声音](#standardVoices)和[神经声音](#neuralVoices)。如果在请求中省略可选的 `voice` 参数，那么缺省情况下，服务会使用标准 `en-US_MichaelVoice` 声音。

<table style="width:100%">
  <caption>表 1. 支持的语言和声音</caption>
  <tr>
    <th style="text-align:left">语言</th>
    <th style="text-align:center">类型</th>
    <th style="text-align:center">声音</th>
    <th style="text-align:center">性别</th>
  </tr>
  <tr>
    <td style="text-align:left">巴西葡萄牙语</td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">卡斯蒂利亚西班牙语</td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">男声</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
    <td style="text-align:center">男声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">法语</td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">德语</td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code></td>
    <td style="text-align:center">男声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
    <td style="text-align:center">男声</td>
  </tr>
  <tr>
    <td style="text-align:left">意大利语</td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">日语</td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>ja-JP_EmiV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">拉丁美洲西班牙语</td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">北美西班牙语</td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">英国英语</td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left">美国英语</td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>en-US_LisaVoice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
    <td style="text-align:center">女声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">标准</td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code></td>
    <td style="text-align:center">男声</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">神经</td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
    <td style="text-align:center">男声</td>
  </tr>
</table>

声音 `es-LA_SofiaVoice` 和 `es-US_SofiaVoice` 本质上是相同的声音。这两种声音最重要的差异是如何解释 $（美元符号）。拉丁美洲版本使用词汇 *pesos*，而北美版本使用词汇 *d&oacute;lares*。除此之外，这两个声音之间还可能存在其他较小的差异。
{: note}

### 标准声音
{: #standardVoices}

标准声音的名称（例如，`pt-BR_IsabelaVoice` 和 `en-US_AllisonVoice`）中不包含版本字符串 (`V3`)。标准声音使用拼接合成技术来组合记录的语音段（或单元），以生成请求的音频。所记录音段的拼接点有时会导致语音中断，由此降低所生成语音的质量和自然性。

### 神经声音
{: #neuralVoices}

神经声音的名称（例如，`pt-BR_IsabelaV3Voice` 和 `en-US_AllisonV3Voice`）中包含版本字符串 (`V3`)。与依赖于音段选择和拼接不同，神经声音技术使用多个深度神经网络 (DNN) 来预测语音的声学（谱）特征。DNN 通过自然的人声进行训练，并根据预测的声学特征生成相应的音频。

在合成期间，DNN 会预测语音的音高和音位持续时间（韵律）、谱结构和波形。神经声音生成的语音既清脆又清晰，具有非常自然且流畅的音频质量。因此，神经声音在整体质量上比标准声音具有更高的一致性。

有关服务的神经声音技术的更多信息，请参阅

-   博客帖子 [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   研究论文 [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

神经声音不支持以下 SSML 元素或属性：

-   `<prosody>` 元素的 `volume` 属性
-   `<express-as>` 元素
-   `<voice-transformation>` 元素

但是，您可能发现在使用神经声音时，不再需要这些 SSML 功能。此外，您可以通过使用 `<prosody>` 元素替换 `<voice-transformation>` 元素，对神经声音进行音高和语速修改。有关更多信息，请参阅 [prosody 元素](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element)。

### 声音定制
{: #customizeVoice}

合成文本时，服务会应用与语言相关的发音规则，以将每个词的普通拼写转换为拼音拼写。服务的发音规则对于普通词非常适用，但是对于异常词（例如，外来词、人名、缩写或首字母缩略词），这些规则生成的结果可能并不理想。

如果您的应用的词汇中包含此类词，那么可以使用定制接口来指定服务如何对此类词发音。有关更多信息，请参阅[了解定制](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。

您为特定语言而非特定声音创建了定制声音模型。因此，定制模型可与其指定语言中的任何声音（标准或神经）一起使用。

## 指定声音
{: #specifyVoice}

HTTP `GET` 和 `POST /v1/synthesize` 方法以及 WebSocket `/v1/synthesize` 方法都接受可选的 `voice` 查询参数来指定用于合成音频的声音。有关更多信息，请参阅 [HTTP 接口](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP)和 [WebSocket 接口](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket)。

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
    <td><code>customization_id</code><br/><em>      可选
    </em></td>
    <td style="text-align:center">查询</td>
    <td style="text-align:center">String</td>
    <td>
      针对为指定声音的语言定义的定制声音模型，提供全局唯一标识 (GUID)。如果包含定制标识，那么必须使用拥有定制模型的服务实例的凭证来发出请求。</td>
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

其他 `customization` 字段的属性提供定制声音模型的 GUID、名称、语言和描述等信息。此外，还会显示模型所有者的凭证、创建模型的日期和时间，以及上次修改模型的日期和时间。
