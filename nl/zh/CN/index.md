---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-30"

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

# 关于
{: #about}

> **服务更新：***{{site.data.keyword.texttospeechshort}} 服务已于 2019 年 7 月 30 日更新。该服务现在支持日语的神经声音：`ja-JP_EmiV3Voice`。有关更多信息，请参阅发行说明中的 [2019 年 7 月 30 日服务更新](/docs/services/text-to-speech?topic=text-to-speech-release-notes#July2019)*。

{{site.data.keyword.texttospeechfull}} 服务提供了一个应用程序编程接口 (API)，使用 {{site.data.keyword.IBM_notm}} 的语音合成功能将书面文本转换为自然发音的语音。服务会以最短的延迟将结果流式返回给客户机。服务提供了 [HTTP](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) 和 [WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket) 接口。

## 特性和功能

{{site.data.keyword.texttospeechshort}} 服务提供了以下特性和功能：

-   **音频格式** - 生成以下格式的音频：Ogg 或 WebM（使用 Opus 或 Vorbis 编码解码器）、WAV、FLAC、MP3 (MPEG)、l16 (PCM)、mulaw 或基本格式。有关更多信息，请参阅[音频格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。
-   **声音** - 将文本合成为各种语言、声音和方言的音频。对于大部分声音，该服务同时提供标准（拼接）和神经版本。有关更多信息，请参阅[语言和声音](/docs/services/text-to-speech?topic=text-to-speech-voices)。
-   **SSML** - 接受纯文本或使用基于 XML 的语音合成标记语言 (SSML) 标记的文本。有关更多信息，请参阅[使用 SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml)。
-   **表现力** - 扩展了 SSML：增加了表现力元素，可用于指示说话风格 *GoodNews*、*Apology* 或 *Uncertainty*。仅可用于标准美国英语 Allison 声音。有关更多信息，请参阅[表现力 SSML](/docs/services/text-to-speech?topic=text-to-speech-expressive)。
-   **声音变换** - 通过添加声音变换元素扩展了 SSML。您可以使用此元素通过控制音高、语速和音色等方面来扩展可能的声音的范围。还提供了两个内置虚拟声音：*Young* 和 *Soft*。仅可用于标准美国英语声音。有关更多信息，请参阅[声音变换 SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation)。
-   **词计时** - 使用 WebSocket 接口时，支持 SSML `<mark>` 元素以及输入文本中所有字符串的可选的词计时信息。计时信息可用于对输入文本和生成的音频进行同步。有关更多信息，请参阅[获取词计时](/docs/services/text-to-speech?topic=text-to-speech-timing)。
-   **定制** - 提供了一个新的定制接口，可用于指定服务如何对输入中出现的异常词发音。可以使用国际音标 (IPA) 或 {{site.data.keyword.IBM_notm}} 符号拼音表示法 (SPR) 来定义发音。有关更多信息，请参阅[了解定制](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。

有关服务价格套餐的更多信息，请参阅 [{{site.data.keyword.cloud_notm}} 目录](https://{DomainName}/catalog/services/text-to-speech){: external}中的 {{site.data.keyword.texttospeechshort}} 服务。

## 语言支持
{: #languages-index}

服务支持以下语言的声音：巴西葡萄牙语、英语（英国和美国方言）、法语、德语、意大利语、日语和西班牙语（卡斯蒂利亚、拉丁美洲和北美方言）。

对于每种语言，服务至少提供一个女声。对于某些语言，服务提供多个声音，同时包含男声和女声。每种声音会针对其方言使用相应的节奏和语调。对于大部分声音，该服务同时提供标准和神经版本。

有关可用于每种语言的声音的更多信息，请参阅[语言和声音](/docs/services/text-to-speech?topic=text-to-speech-voices)。

## 用例
{: #usecases}

服务适用于声音驱动和无屏幕应用程序，其中音频是输出的首选方法：

-   针对残障人士的界面，例如面向视力受损人士的辅助工具
-   向驾驶员朗读文本和电子邮件消息
-   视频脚本叙述和视频话外音
-   基于朗读的教育工具
-   家庭自动化解决方案

## 试用服务

有关运行中服务的示例，请参阅：

-   {{site.data.keyword.texttospeechshort}} 服务的[快速演示](https://text-to-speech-demo.ng.bluemix.net/){: external}，用于演示接受文本并生成具有不同声音的语音。它在支持的情况下提供了表现力和变换。
-   {{site.data.keyword.ibmwatson}} [入门模板工具包](http://www.ibm.com/watson/developercloud/starter-kits.html){: external}中的应用程序，用于演示 {{site.data.keyword.texttospeechshort}} 服务。
