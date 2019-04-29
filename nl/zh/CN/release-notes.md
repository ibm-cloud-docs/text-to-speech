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

# 发行说明
{: #release-notes}

以下各部分记录了 {{site.data.keyword.texttospeechfull}} 服务的每个发行版和更新所包含的新功能和更改。这些信息包含任何已知限制。除非另有说明，否则所有更改都与较早的发行版兼容，并且会自动、透明地可供所有新应用程序和现有应用程序使用。
{: shortdesc}

## 已知限制
{: #limitations}

部署 `V2` 时发生问题，深度神经网络 (DNN) 语音会导致合成语音中有背景噪声。{{site.data.keyword.IBM_notm}} 正在努力解决此问题。

## 2019 年 3 月 24 日
{: #March2019c}

-   现在，服务可提供其德语声音的深度神经网络 (DNN) 版本：
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

    有关基于 DNN 的声音的更多信息，请参阅[语音合成技术](/docs/services/text-to-speech/voices.html#technologiesVoices)。
-   现在，服务的所有基于 DNN 的声音都支持 SSML `<prosody>` 元素的 `pitch` 和 `rate` 属性。基于 DNN 的声音不支持 `<prosody>` 元素的 `volume` 属性。有关更多信息，请参阅 [prosody 元素](/docs/services/text-to-speech/SSML-elements.html#prosody_element)。

## 2019 年 3 月 21 日
{: #March2019b}

现在，用户只能查看与分配给其 {{site.data.keyword.cloud_notm}} 帐户的角色相关联的服务凭证信息。例如，如果您分配有 `reader` 角色，那么任何 `writer` 或更高级别的服务凭证不再可见。

此更改不会影响具有现有服务凭证的用户或应用程序的 API 访问权。此更改仅影响在 {{site.data.keyword.cloud_notm}} 中查看凭证。

有关服务密钥和用户角色的更多信息，请参阅 [IAM 服务 API 密钥](/docs/services/watson?topic=watson-api-key-bp#api-key-bp)。

## 2019 年 3 月 4 日
{: #March2019a}

现在，服务提供了四个新的声音，这些声音使用深度学习合成来生成音频：

-   `it-IT_FrancescaV2Voice`
-   `en-US_AllisonV2Voice`
-   `en-US_LisaV2Voice`
-   `en-US_MichaelV2Voice`

这些新声音使用机器学习和 DNN 将文本合成为语音。基于深度学习（或 DNN）的合成所生成的音频在韵律方面更自然，总体质量更一致。

但是，新的声音还会生成信号质量不同于现有声音的音频，因此可能并不适合所有应用。此外，新的声音不支持 SSML 元素 `<prosody>`、`<express-as>` 和 `<voice-transformation>`。

有关这些基于 DNN 的声音及其与现有声音的差异的更多信息，请参阅[语音合成技术](/docs/services/text-to-speech/voices.html#technologiesVoices)。

## 较旧的发行版
{: #older}

-   [2019 年 1 月 28 日](#January2019)
-   [2018 年 12 月 13 日](#December2018)
-   [2018 年 11 月 7 日](#November2018)
-   [2018 年 10 月 30 日](#October2018)
-   [2018 年 6 月 12 日](#June2018)
-   [2018 年 5 月 15 日](#May2018)
-   [2017 年 10 月 2 日](#October2017)
-   [2017 年 7 月 14 日](#July2017)
-   [2017 年 4 月 10 日](#April2017)
-   [2016 年 12 月 1 日](#December2016)
-   [2016 年 9 月 22 日](/docs/services/text-to-speech/release-notes.html#September2016)
-   [2016 年 6 月 23 日](/docs/services/text-to-speech/release-notes.html#June2016)
-   [2016 年 3 月 10 日](/docs/services/text-to-speech/release-notes.html#March2016)
-   [2016 年 2 月 22 日](/docs/services/text-to-speech/release-notes.html#February2016)
-   [2015 年 12 月 17 日](/docs/services/text-to-speech/release-notes.html#December2015)
-   [2015 年 9 月 21 日](/docs/services/text-to-speech/release-notes.html#September2015)
-   [2015 年 7 月 1 日](/docs/services/text-to-speech/release-notes.html#July2015)

### 2019 年 1 月 28 日
{: #January2019}

现在，WebSocket 接口支持通过基于浏览器的 JavaScript 代码，进行基于令牌的 Identity and Access Management (IAM) 认证。与此相反的限制已除去。要使用 WebSocket `/v1/synthesize` 方法建立已认证的连接，请执行以下操作：

-   如果使用的是 IAM 认证，请包含 `access_token` 查询参数。
-   如果使用的是 Cloud Foundry 服务凭证，请包含 `watson-token` 查询参数。

有关更多信息，请参阅[打开连接](/docs/services/text-to-speech/websockets.html#WSopen)。

### 2018 年 12 月 13 日
{: #December2018}

现在，{{site.data.keyword.texttospeechshort}} 服务在 {{site.data.keyword.cloud}} 伦敦位置 (**eu-gb**) 可用。与所有位置一样，伦敦也使用的是基于令牌的 Identity and Access Management (IAM) 认证。在此位置中创建的所有新服务实例都会使用 IAM 认证。

### 2018 年 11 月 7 日
{: #November2018}

现在，{{site.data.keyword.texttospeechshort}} 服务在 {{site.data.keyword.cloud}} 东京位置 (**jp-tok**) 可用。与所有位置一样，东京也使用的是基于令牌的 Identity and Access Management (IAM) 认证。在此位置中创建的所有新服务实例都会使用 IAM 认证。

### 2018 年 10 月 30 日
{: #October2018}

所有位置的 {{site.data.keyword.texttospeechshort}} 服务都已迁移到基于令牌的 Identity and Access Management (IAM) 认证。现在，所有 {{site.data.keyword.cloud_notm}} 服务都使用 IAM 认证。每个位置的 {{site.data.keyword.texttospeechshort}} 服务已于以下日期迁移：

-   达拉斯 (**us-south**)：2018 年 10 月 30 日
-   法兰克福 (**eu-de**)：2018 年 10 月 30 日
-   华盛顿 (**us-east**)：2018 年 6 月 12 日
-   悉尼 (**au-syd**)：2018 年 5 月 15 日

迁移到 IAM 认证对新服务实例和现有服务实例的影响方式不同：

-   *在任何位置创建的所有新服务实例*现在都使用 IAM 认证来访问服务。可以传递不记名令牌或 API 密钥：令牌支持已认证的请求，而无需在每个调用中嵌入服务凭证；API 密钥使用 HTTP 基本认证。使用任何 {{site.data.keyword.ibmwatson}} SDK 时，都可以传递 API 密钥，并让 SDK 来管理令牌的生存期。
-   *在指示的迁移日期之前在某个位置中创建的现有服务实例*将继续使用其先前 Cloud Foundry 服务凭证中的 `{username}` 和 `{password}` 进行认证，直到将其迁移为使用 IAM 认证为止。有关迁移为 IAM 认证的更多信息，请参阅[将 Cloud Foundry 服务实例迁移到资源组](https://{DomainName}/docs/resources/instance_migration.html)。

有关更多信息，请参阅以下文档：

-   要了解服务实例使用的认证机制，请通过在 [{{site.data.keyword.cloud_notm}} 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/dashboard/apps){: new_window} 上单击该实例来查看服务凭证。
-   有关将 IAM 令牌用于 {{site.data.keyword.watson}} 服务的更多信息，请参阅[使用 IAM 令牌进行认证](/docs/services/watson/getting-started-iam.html)。
-   有关将 IAM API 密钥用于 {{site.data.keyword.watson}} 服务的更多信息，请参阅 [IAM 服务 API 密钥](/docs/services/watson/apikey-bp.html)。
-   有关使用 IAM 认证的示例，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/text-to-speech){: new_window}。

### 2018 年 6 月 12 日
{: #June2018}

在华盛顿 (**us-east**) 托管的应用程序支持以下功能：

-   现在，服务支持新的 API 认证过程。有关更多信息，请参阅 [2018 年 10 月 30 日服务更新](#October2018)。
-   现在，服务支持 `X-Watson-Metadata` 头和 `DELETE /v1/user_data` 方法。有关更多信息，请参阅[信息安全](/docs/services/text-to-speech/information-security.html)。

### 2018 年 5 月 15 日
{: #May2018}

在悉尼 (**au-syd**) 托管的应用程序支持以下功能：

-   现在，服务支持新的 API 认证过程。有关更多信息，请参阅 [2018 年 10 月 30 日服务更新](#October2018)。
-   现在，服务支持 `X-Watson-Metadata` 头和 `DELETE /v1/user_data` 方法。有关更多信息，请参阅[信息安全](/docs/services/text-to-speech/information-security.html)。

### 2017 年 10 月 2 日
{: #October2017}

对于 `audio/l16` 格式，现在可以选择指定返回的音频的字节序。（您必须已指定采样率。）例如，`audio/l16;rate=22050;endianness=big-endian` 和 `audio/l16;rate=22050;endianness=little-endian`；缺省值为大尾数法。有关更多信息，请参阅[音频格式](/docs/services/text-to-speech/audio-formats.html)。

### 2017 年 7 月 14 日
{: #July2017}

现在，服务支持 MP3 或运动图像专家组 (MPEG) 音频格式。有关受支持音频格式的更多信息，请参阅[音频格式](/docs/services/text-to-speech/audio-formats.html)。

### 2017 年 4 月 10 日
{: #April2017}

-   现在，服务支持使用 Opus 或 Vorbis 编码解码器的 Web 媒体 (WebM) 音频格式。服务现在除了支持 Opus 编码解码器外，还支持使用 Vorbis 编码解码器的 Ogg 音频格式。有关受支持音频格式的更多信息，请参阅[音频格式](/docs/services/text-to-speech/audio-formats.html)。
-   现在，服务支持跨源资源共享 (CORS)，以允许基于浏览器的客户机直接调用服务。有关更多信息，请参阅 [CORS 支持](/docs/services/text-to-speech/developer-overview.html#cors)。
-   更改了表示定制接口的某些方法成功完成的 HTTP 响应代码：
    -   现在，`POST /v1/customizations` 方法会返回 201（而不是 200）。
    -   现在，`POST /v1/customizations/{customization_id}` 方法会返回 200（而不是 201）。
    -   现在，`POST /v1/customizations/{customization_id}/words` 方法会返回 200（而不是 201）。
    -   现在，`PUT /v1/customizations/{customization_id}/words/{word}` 方法会返回 200（而不是 201）。
-   现在，如果尝试对非日语语言指定 `part_of_speech`，`POST /v1/customizations/{custom_id}/words` 和 `PUT /v1/customizations/{customization_id}/words/{word}` 方法会返回 HTTP 响应代码 400，错误消息为：`仅 ja-JP 语言支持词性`。
-   现在，`POST /v1/customizations/{custom_id}/words` 方法会返回空的响应主体 (`{}`)。

### 2016 年 12 月 1 日
{: #December2016}

-   服务包含一个新的声音 `es-LA_SofiaVoice`，这是 `es-US_SofiaVoice` 声音的拉丁美洲等效版本。这两个声音之间最重要的差异在于如何解释 `$`（美元符号）：拉丁美洲版本使用词汇 *pesos*，而北美版本使用词汇 *dolares*。除此之外，这两个声音之间还可能存在其他较小的差异。
-   除了 `en-US_AllisonVoice` 外，现在还有另外两个声音可使用 SSML 声音变换来进行变换：`en-US_LisaVoice` 和 `en-US_MichaelVoice`。有关声音变换的更多信息，请参阅[声音变换 SSML](/docs/services/text-to-speech/SSML-transformation.html)。
-   现在，将定制接口用于日语时，服务会从为定制声音模型定义的词/转换项对中，选择最长的词进行匹配。例如，假设定制声音有以下两个条目：

    <pre><code data-copy="false" class="language-javascript">  {
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    如果服务在输入文本中找到了字符串 <code>&#65326;&#65337;&#65315;</code>，那么会与该词相匹配，因为此字符串长于 <code>&#65326;&#65337;</code>。先前，服务会与字符串 <code>&#65326;&#65337;</code> 相匹配。有关使用定制声音模型的日语条目的更多信息，请参阅[使用日语条目](/docs/services/text-to-speech/custom-rules.html#jaNotes)。

### 2016 年 9 月 22 日
{: #September2016}

-   现在，定制接口（包括定制和 `GET /v1/pronunciation` 方法）可用于服务支持的所有语言。该接口仍是 Beta 发行版。有关更多信息，请参阅[了解定制](/docs/services/text-to-speech/custom-intro.html)。
-   现在，服务支持语音合成标记语言 (SSML) 用于日语。有关 SSML 支持的常规信息，请参阅[使用 SSML](/docs/services/text-to-speech/SSML.html)。有关日语 SPR 和 IPA 音标符号的信息，请参阅[日语音标符号](/docs/services/text-to-speech/ja-JP-SPRs.html)。在日语定制声音模型中创建词的条目时，有额外的注意事项和 `part_of_speech` 字段适用。有关更多信息，请参阅[使用日语条目](/docs/services/text-to-speech/custom-rules.html#jaNotes)。
-   现在，服务支持通过新的 `<voice-transformation>` 元素进行 SSML 声音变换。可以通过创建定制声音变换，以修改声音的音高、音高范围、喉音张力、气息声、语速和音色，从而扩展可能的声音的范围。服务还提供了两个内置虚拟声音：*Young* 和 *Soft*。目前，服务仅支持对美国英语 Allison 声音使用声音变换。有关更多信息，请参阅[声音变换 SSML](/docs/services/text-to-speech/SSML-transformation.html)。
-   现在，服务可以返回传递到 WebSocket 接口的输入文本中所有字符串的词计时信息。要接收输入中每个字符串的开始时间和结束时间，请指定一个数组，其中包含用于传递到服务的 JSON 对象的可选 `timings` 参数的字符串 `words`。此功能目前不可用于日语输入文本。有关更多信息，请参阅[获取词计时](/docs/services/text-to-speech/word-timing.html)。
-   现在，服务会验证在任何上下文中提交的所有 SSML 元素。如果服务找到无效的标记，那么会报告 HTTP 400 响应代码以及描述性消息，并且该方法会失败。在前发行版中，服务处理错误的方式不一致；例如，指定无效的词发音可能会导致不可预测或不一致的行为。有关更多信息，请参阅 [SSML 验证](/docs/services/text-to-speech/SSML.html#errors)。
-   不推荐将 `spr` 用作 `GET /v1/pronunciation` 方法的 `format` 选项的自变量，也不推荐将其与 SSML `<phoneme>` 元素的 `alphabet` 属性一起使用。要使用 {{site.data.keyword.IBM_notm}} 符号拼音表示法 (SPR)，请在所有情况下都使用 `ibm` 自变量，而不要使用 `spr`。
-   现在，支持的音频格式列表包含 `audio/mulaw;rate=8000`。与 `audio/basic` 一样，此格式提供的是单声道音频，使用 8 位 u-law（或 mu-law）数据进行编码，采样率为 8 千赫兹。有关更多信息，请参阅[音频格式](/docs/services/text-to-speech/audio-formats.html)。
-   现在，`GET /v1/voices` 和 `GET /v1/voices/{voice}` 方法在其每个声音的输出中，都会返回 `supported_features` 对象。此对象描述该声音是否支持定制和 SSML `<voice_transformation>` 元素。    有关更多信息，请参阅[语言和声音](/docs/services/text-to-speech/voices.html)。


### 2016 年 6 月 23 日
{: #June2016}

-   现在，服务提供了 WebSocket 接口，用于将文本合成为语音。此接口提供的功能与 HTTP 接口的 `/v1/synthesize` 方法相同。此接口接受纯文本或使用 SSML 标记的文本。此外，还支持使用 SSML `<mark>` 元素在音频中标识其对 mark 元素之前所有文本进行合成的完成时间。有关更多信息，请参阅 [WebSocket 接口](/docs/services/text-to-speech/websockets.html)。
-   现在，服务支持卡斯蒂利亚和北美西班牙语、意大利语和巴西葡萄牙语使用通过 SSML 进行注释的文本。服务已经支持 SSML 用于美国英国、英国英语、法语和德语。自此更新后，服务将支持 SSML 用于除日语以外的其他所有语言。此外，可以同时使用 {{site.data.keyword.IBM_notm}} SPR 和 IPA 表示法通过 `<phoneme>` 元素来定义词发音。有关更多信息，请参阅[使用 SSML](/docs/services/text-to-speech/SSML.html) 和[使用 IBM SPR](/docs/services/text-to-speech/SPRs.html)。

    对于美国英语，还可以使用 SSML `<phoneme>` 元素在定制声音模型中创建词条目；仅美国英语支持定制。有关更多信息，请参阅[了解定制](/docs/services/text-to-speech/custom-intro.html)。
-   服务改进了最常用的声音的表达性和自然性。这些改进立足于根据输入文本进行的基于递归神经网络 (RNN) 的韵律预测。这些改进可用作以下语言的新服务引擎和声音模型更新：

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   现在，`GET /v1/pronunciation` 方法接受可选的 `customization_id` 查询参数。此参数从指定的定制声音模型获取词转换项。如果声音模型不包含该词，那么此方法会返回该词的缺省发音。有关更多信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/text-to-speech){: new_window}。

    使用不带定制标识的 `GET /v1/pronunciation` 方法以及用于除美国英语以外的语言时，只能请求以 {{site.data.keyword.IBM_notm}} SPR 表示法表示的词发音。对于除美国英语之外的其他语言，必须使用此方法的 `format` 选项指定 `spr`。
    {: note}
-   现在，支持的音频格式列表包含 `audio/basic`，此格式提供的是单声道音频，使用 8 位 u-law（或 mu-law）数据进行编码，采样率为 8 千赫兹。有关更多信息，请参阅[音频格式](/docs/services/text-to-speech/audio-formats.html)。
-   HTTP 和 WebSocket `/v1/synthesize` 方法可以返回 `warnings` 响应，其中包含有关请求中所含的无效查询参数或 JSON 字段的消息。warnings 的格式已更改。以下示例显示的是先前的格式：

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    现在，同一警告的格式如下：

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

### 2016 年 3 月 10 日
{: #March2016}

-   现在，`GET` 和 `POST /v1/synthesize` 方法可以返回 `Warnings` 响应头，其中包含有关请求中所含的无效查询参数或 JSON 字段的警告消息列表。列表的每个元素都包含一个字符串，用于描述警告的性质，后跟无效自变量字符串数组；例如 `Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']`。有关更多信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/text-to-speech){: new_window}。
-   不推荐使用*针对 Apple&reg; iOS 操作系统的 Beta {{site.data.keyword.watson}} Speech 软件开发包 (SDK)*，此 SDK 已替换为 *{{site.data.keyword.watson}} Swift SDK*。新的 SDK 可从 GitHub 上 `watson-developer-cloud` 名称空间的 [swift-sdk 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} 中获取。

### 2016 年 2 月 22 日
{: #February2016}

服务已更新为使用新的表达性 SSML 功能。服务扩展了语音合成标记语言 (SSML)，增加了 `<express-as>` 元素，可用于通过三种说话风格中的一种风格来指示表达性：`GoodNews`、`Apology` 或 `Uncertainty`。可以将此元素应用于文本的整个主体，也可应用于句子、短语或词。目前，服务仅支持对美国英语 Allison 声音 (`en-US_AllisonVoice`) 使用表达性。有关更多信息，请参阅[表达性 SSML](/docs/services/text-to-speech/SSML-expressive.html)。

### 2015 年 12 月 17 日
{: #December2015}

-   服务提供了一个新的定制接口，可用于指定如何对输入中出现的异常词发音。此接口包含若干新的方法，可用于创建和管理定制声音模型及其包含的词/转换项对。然后，可以在将文本合成为音频时使用定制模型。

    服务支持近似读音转换项和拼音转换项。拼音转换项可以使用标准国际音标 (IPA) 表示法或专有 {{site.data.keyword.IBM_notm}} 符号拼音表示法 (SPR)。可使用语音合成标记语言 (SSML) 来指定拼音转换项。

    定制界面包含新 HTTP 方法的集合，这些方法的名称为 `POST /v1/customizations`、`POST /v1/customizations/{customization_id}`、`POST /v1/customizations/{customization_id}/words` 和 `PUT /v1/customizations/{customization_id}/words/{word}`。服务还提供了新的 `GET /v1/pronunciation` 方法和新的 `GET /v1/voices/{voice}` 方法，前者用于返回任何词的发音，后者用于返回有关特定声音的详细信息。此外，现在服务接口的现有方法会根据需要接受定制声音模型参数。

    有关定制及其接口的更多信息，请参阅[了解定制](/docs/services/text-to-speech/custom-intro.html)和 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/text-to-speech){: new_window}。

    定制接口是 Beta 发行版，目前仅支持美国英语。目前，所有定制方法和 `GET /v1/pronunciation` 方法都只能用于创建和处理美国英语的定制声音模型和词转换项。
    {: note}
-   服务支持新的声音 `pt-BR_IsabelaVoice`，用于合成巴西葡萄牙语女声音频。有关更多信息，请参阅[语言和声音](/docs/services/text-to-speech/voices.html)。


### 2015 年 9 月 21 日
{: #September2015}

-   有两个新的 Beta 移动软件开发包 (SDK) 可用于语音服务。这两个 SDK 支持移动应用程序与 {{site.data.keyword.texttospeechshort}} 和 {{site.data.keyword.speechtotextshort}} 服务进行交互。您可以使用这两个 SDK 将文本发送到 {{site.data.keyword.texttospeechshort}} 服务并接收音频响应。
    -   *{{site.data.keyword.watson}} Swift SDK* 可从 GitHub 上 `watson-developer-cloud` 名称空间的 [swift-sdk 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} 中获取。
    -   *{{site.data.keyword.watson}} Speech Android SDK* 可从 GitHub 上 `watson-developer-cloud` 名称空间的 [speech-android-sdk 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/watson-developer-cloud/speech-android-sdk){: new_window} 中获取。

    这两个 SDK 都支持使用 {{site.data.keyword.cloud_notm}} 服务凭证或认证令牌对语音服务进行认证。

    由于 SDK 是 Beta 功能，因此未来会随时更改。
    {: note}
-   服务支持新的语言 - 日语。声音 `ja-JP_EmiVoice` 是日语女声。

### 2015 年 7 月 1 日
{: #July2015}

服务于 2015 年 7 月 1 日从 Beta 转为一般可用 (GA)。{{site.data.keyword.texttospeechshort}} API 的 Beta 和 GA 版本之间存在以下差异。GA 发行版需要用户升级到服务的新版本。

-   新的编程模型支持客户机与服务之间进行直接交互。通过使用此模型，客户机可以获取用于直接与服务进行通信的认证令牌。通过使用令牌，客户机无需 {{site.data.keyword.cloud_notm}} 中的服务器端代理应用程序，就可代表它来调用服务。令牌是客户机与服务进行交互的首选方法。

    该服务会继续支持依赖于服务器端代理在客户机与服务之间中继通信和数据的旧编程模型。但是，新模型的效率更高，吞吐量更大。有关新编程模型的更多信息，请参阅 [{{site.data.keyword.watson}} 服务的编程模型](/docs/services/watson/getting-started-develop.html)。
-   现在，可以将语音合成标记语言 (SSML) 传递到 `/v1/synthesize` 方法的 HTTP `GET` 和 `POST` 版本。SSML 是一种基于 XML 的标记语言，旨在为语音合成应用程序（例如，{{site.data.keyword.texttospeechshort}} 服务）提供文本注释。有关将 SSML 输入传递到服务的更多信息，请参阅[指定输入文本](/docs/services/text-to-speech/http.html#input)。

    服务初始仅支持 SSML 用于英国英语、美国英语、法语和德语。服务不支持 SSML 用于意大利语和西班牙语。使用 SSML 时，请确保不要为音频选择其中一种不支持的语言的声音。否则，会获得没有意义的结果。
-   更改和扩展了合成语音支持的声音。现在，服务通过 `/v1/synthesize` 方法支持其他若干声音、语言和方言。有关受支持声音的更多信息，请参阅[语言和声音](/docs/services/text-to-speech/voices.html)。

    Beta 中可用的三个声音在 GA 中已重命名：
    -   `VoiceEnUsMichael` 现在名为 `en-US_MichaelVoice`
    -   `VoiceEnUsLisa` 现在名为 `en-US_LisaVoice`
    -   `VoiceEsEsEnrique` 现在名为 `es-ES_EnriqueVoice`

    在服务的 Beta 版本保持可用期间，这些声音先前的名称在 Beta 版本中将继续有效（通过 `-beta` API 端点使用）。但是，对于服务的 GA 版本，必须使用新名称。
-   现在，可以请求服务返回自由无损音频编码解码器 (FLAC) 格式的音频。服务仍可以返回使用 Opus 编码解码器的 Ogg 格式（缺省值）和波形音频文件格式 (WAV) 的音频。有关将音频格式与 `/v1/synthesize` 方法配合使用的更多信息，请参阅[音频格式](/docs/services/text-to-speech/audio-formats.html)。
-   现在，发送到 HTTP `GET` 请求 URL 中的 `/v1/synthesize` 方法的文本，或 HTTP `POST` 请求主体中的文本限制为最大 5 KB。对于 Beta 版本，文本的最大大小为 4 MB。
-   现在，`/v1/synthesize` 方法包含 `X-WDC-PL-OPT-OUT` 头，用于控制服务是否使用操作生成的文本和音频结果来改进未来的结果。为此头指定值 `1` 将阻止服务使用文本和音频结果。该参数仅应用于当前请求。此新头将替换 Beta 方法中的 `X-logging` 头。有关更多信息，请参阅[控制 {{site.data.keyword.watson}} 服务的请求日志记录](/docs/services/watson/getting-started-logging.html)。
-   对于 `/v1/synthesize` 方法，更改了以下错误代码：
    -   除去了错误代码 406（“不可接受。不支持的 MIME 类型。”）。
    -   添加了错误代码 415（“不支持的媒体类型”）。
    -   添加了错误代码 503（“服务不可用”）。
-   对于 `GET /v1/voices` 方法，更改了以下错误代码：
    -   除去了错误代码 406（“不可接受。不支持的 MIME 类型。”）。
    -   添加了错误代码 415（“不支持的媒体类型”）。
