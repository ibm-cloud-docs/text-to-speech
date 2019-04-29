---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-14"

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# 入门教程
{: #gettingStarted}

{{site.data.keyword.texttospeechfull}} 服务用于将书面文本转换为自然发音的语音，从而为应用程序提供语音合成功能。本教程基于 curl，可帮助您快速开始使用服务。以下示例说明了如何调用服务的 `POST` 和 `GET /v1/synthesize` 方法来请求音频流。
{: shortdesc}

本教程使用 {{site.data.keyword.cloud}} Identity and Access Management (IAM) API 密钥进行认证。较旧的服务实例可能会继续使用其现有 Cloud Foundry 服务凭证中的 `{username}` 和 `{password}` 进行认证。请使用适合您服务实例的方法进行认证。有关服务使用 IAM 认证的更多信息，请参阅发行说明中的 [2018 年 10 月 30 日服务更新](/docs/services/text-to-speech/release-notes.html#October2018)。
{: important}

## 开始之前
{: #before-you-begin}

- {: hide-dashboard} 创建服务的实例：
    1.  {: hide-dashboard} 转至 {{site.data.keyword.cloud_notm}}“目录”中的 [{{site.data.keyword.texttospeechshort}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/catalog/services/text-to-speech){: new_window} 页面。
    1.  {: hide-dashboard} 注册免费的 {{site.data.keyword.cloud_notm}} 帐户或登录。
    1.  {: hide-dashboard} 单击**创建**。
-   复制凭证以向服务实例进行认证：
    1.  {: hide-dashboard} 在 [{{site.data.keyword.cloud_notm}}“仪表板” ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/dashboard/apps){: new_window} 中，单击 {{site.data.keyword.texttospeechshort}} 服务实例以转至 {{site.data.keyword.texttospeechshort}} 服务仪表板页面。
    1.  在**管理**页面上，单击**显示**以查看凭证。
    1.  复制 `API 密钥`和 `URL` 值。
-   确保您具有 `curl` 命令。
    -   示例使用 `curl` 命令来调用 HTTP 接口的方法。通过 [curl.haxx.se ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://curl.haxx.se/){: new_window} 来安装适用于您操作系统的版本。请安装支持安全套接字层 (SSL) 协议的版本。确保在 `PATH` 环境变量上包含安装的二进制文件。

输入命令时，请将 `{apikey}` 和 `{url}` 替换为实际的 API 密钥和 URL。在命令中省略花括号，这用于指示变量值。实际值类似于以下示例：
{: hide-dashboard}

```bash
curl -X POST -u "apikey:L_HALhLVIksh1b73l97LSs6R_3gLo4xkujAaxm7i-b9x"
. . .
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```
{:pre}
{: hide-dashboard}

可以使用浏览器或其他工具来播放本教程中示例所生成的音频文件。有关更多信息，请参阅[播放音频文件](/docs/services/text-to-speech/audio-formats.html#formatsPlay)。
{: note}

## 步骤 1：合成美国英语文本
{: #synthesizeEnglish}

以下命令使用 `POST /v1/synthesize` 方法将美国英语输入合成为两种不同格式的音频文件。这两个请求均使用缺省美国英语声音 `en-US_MichaelVoice`。

1.  发出以下命令来合成字符串“hello world”，并生成名为 `hello_world.wav` 的 WAV 文件。
    -   {: hide-dashboard} 将 `{apikey}` 和 `{url}` 替换为您的 API 密钥和 URL。

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

1.  发出以下命令来合成相同的文本，但生成名为 `hello_world.ogg` 的 Ogg 文件（缺省格式）。
    -   {: hide-dashboard} 将 `{apikey}` 和 `{url}` 替换为您的 API 密钥和 URL。

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

## 步骤 2：合成西班牙语文本
{: #synthesizeSpanish}

以下命令使用 `GET /v1/synthesize` 方法将西班牙语输入合成为音频文件。

1.  发出以下命令来合成字符串“hola mundo”，并生成名为 `hola_mundo.wav` 的 WAV 文件。输入文本已经过 URL 编码。该方法包含查询参数 `accept`（用于指定音频格式）和 `voice`（用于指定西班牙语声音 `es-ES_EnriqueVoice`）。
    -   {: hide-dashboard} 将 `{apikey}` 和 `{url}` 替换为您的 API 密钥和 URL。

    ```bash
    curl -X GET -u "apikey:{apikey}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## 后续步骤

-   在 [HTTP 接口](/docs/services/text-to-speech/http.html)中了解有关服务的 HTTP 接口的更多信息。
-   在 [WebSocket 接口](/docs/services/text-to-speech/websockets.html)中了解有关服务的 WebSocket 接口的信息。
-   在 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/text-to-speech){: new_window} 中获取有关服务接口方法的详细信息。
