---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-05"

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

# 开发者概述
{: #overview}

您可以通过 HTTP 具象状态传输 (REST) API 或 WebSocket 接口来访问 {{site.data.keyword.texttospeechfull}} 服务的语音合成功能。此外，还有多个软件开发包 (SDK) 可用于简化使用各种编程语言开发应用程序的工作。以下各部分提供了使用该服务开发应用程序的概述。
{: shortdesc}

## HTTP 接口
{: #http}

要使用 HTTP API 来合成文本，请调用服务的 `/v1/synthesize` 方法的 `GET` 或 `POST` 版本。此方法的这两个版本提供了一般等效功能：

-   *输入文本：*通过两种不同的方式传递要合成的输入文本：
    -   `GET /v1/synthesize` 方法接受作为查询参数的输入文本。请求的最大大小为 8 KB，其中包括输入文本、URL 和头。
    -   `POST /v1/synthesize` 方法接受请求主体中的输入文本。在请求中，URL 和头的最大大小为 8 KB，在请求主体中发送的输入文本的最大大小为 5 KB。

    可以向服务传递纯文本或使用语音合成标记语言 (SSML) 进行注释的文本。SSML 是一种基于 XML 的标记语言，为语音合成应用程序（例如，{{site.data.keyword.texttospeechshort}} 服务）提供文本注释。该服务使用特定于服务的表达元素和声音变换元素来扩充 SSML。

    有关更多信息，请参阅[指定输入文本](/docs/services/text-to-speech/http.html#input)。
-   *声音：*服务接受文本，并生成各种语言、声音和方言的音频。对于每种支持的语言和不同的方言（例如，美国英语和英国英语），服务至少提供一个男声或女声，有时会同时提供这两者。服务还会提供一些声音的使用深度神经网络 (DNN) 技术将文本合成为语音的版本。

    可以使用服务的 `GET /v1/voices` 或 `GET /v1/voices/{voice}` 方法来了解有关受支持声音的更多信息。服务会将文本合成为指定声音的语言。请确保将声音与输入文本相匹配。

    有关更多信息，请参阅[语言和声音](/docs/services/text-to-speech/voices.html)。
-   *音频格式：*服务可以生成以下格式的音频：Ogg 或 Web 媒体 (WebM) 格式（使用 Opus（缺省）或 Vorbis 编码解码器）、MP3（运动图像专家组或 MPEG）格式、波形音频文件格式 (WAV)、自由无损音频编码解码器 (FLAC)、线性 16 位脉冲编码调制 (PCM)、8 位 mu-law (u-law) 或基本音频。

    有关更多信息，请参阅[音频格式](/docs/services/text-to-speech/audio-formats.html)。

## WebSocket 接口
{: #websocket}

服务提供了一个 WebSocket 接口，可用于合成文本。该接口提供了单个版本的 `/v1/synthesize` 方法，最多可接受 5 KB 的输入文本。您可指定要合成的文本、要使用的声音以及音频的格式。可以提供纯文本或使用 SSML 进行注释的文本。有关更多信息，请参阅 [WebSocket 接口](/docs/services/text-to-speech/websockets.html)。

WebSocket 接口支持使用 SSML `<mark>` 元素来标识音频中的特定位置。您还可以请求对输入文本中所有词的词计时信息。有关更多信息，请参阅[获取词计时](/docs/services/text-to-speech/word-timing.html)。

## 定制接口
{: #customization}

服务包含一个定制接口，可以用于创建定制声音模型，以供语音合成期间使用。定制声音模型是由词及其特定语言的转换项构成的字典。模型中的每个词/转换项对会指示服务在输入文本中出现该词时如何发音。

可以使用定制声音模型为异常词创建特定于应用程序的转换项，若对异常词使用服务的常规发音规则，生成的发音可能并不理想。您可以使用标准国际音标 (IPA) 表示法或专有 {{site.data.keyword.IBM_notm}} 符号拼音表示法 (SPR) 来定义词/转换项对的定制条目。

例如，应用程序可能经常遇到包含特殊外来词、人名或地名或者缩写和首字母缩略词。通过使用定制，可以定义转换项，用于指示服务您希望这类词汇如何发音。有关更多信息，请参阅[了解定制](/docs/services/text-to-speech/custom-intro.html)。

定制接口是 Beta 发行版。
{: note}

## CORS 支持
{: #cors}

服务支持跨源资源共享 (CORS)。通过使用 CORS，Web 页面可以直接从外部域请求资源。CORS 可绕过同源安全策略；否则，这些策略会阻止此类请求。由于服务支持 CORS，因此 Web 页面可以直接与服务进行通信，而无需通过托管该页面的 Web 服务器来传递请求。

例如，从 {{site.data.keyword.cloud}} 中的服务器装入的 Web 页面可以直接调用定制 API，而绕过 {{site.data.keyword.cloud_notm}} 服务器。有关更多信息，请参阅 [enable-cors.org ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://enable-cors.org/){: new_window}。

## 使用软件开发包
{: #sdks}

SDK 可供 {{site.data.keyword.texttospeechshort}} 服务用于简化语音应用程序的开发工作。{{site.data.keyword.ibmwatson}} SDK 可用于许多常用的编程语言和平台。

-   有关 SDK 以及 GitHub 上 SDK 的链接的完整列表，请参阅[使用 SDK](/docs/services/watson/getting-started-sdks.html)。
-   有关 {{site.data.keyword.texttospeechshort}} 服务的 Node、Java、Python、Ruby 和 Go SDK 的所有方法的详细信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/text-to-speech){: new_window}。

## 了解有关应用程序开发的更多信息
{: #learn}

有关使用 {{site.data.keyword.watson}} 服务和 {{site.data.keyword.cloud_notm}} 的更多信息，请参阅：

-   有关使用 {{site.data.keyword.watson}} 服务和 {{site.data.keyword.cloud_notm}} 的简介，请参阅 [{{site.data.keyword.watson}} 和 {{site.data.keyword.cloud_notm}} 入门](/docs/services/watson/index.html)。
-   所有新的服务实例都使用 {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) 进行认证。较旧的服务实例可能会继续使用其现有 Cloud Foundry 服务凭证中的 `{username}` 和 `{password}` 进行认证。有关向服务进行认证的更多信息，请参阅发行说明中的 [2018 年 10 月 30 日服务更新](/docs/services/text-to-speech/release-notes.html#October2018)。
-   有关控制对所有 {{site.data.keyword.watson}} 服务执行的缺省请求日志记录的信息，请参阅[控制 {{site.data.keyword.watson}} 服务的请求日志记录](/docs/services/watson/getting-started-logging.html)。
