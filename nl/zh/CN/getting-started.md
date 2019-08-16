---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-03"

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

## 开始之前
{: #before-you-begin}

- {: hide-dashboard} 创建服务的实例：
    1.  {: hide-dashboard} 转至 {{site.data.keyword.cloud_notm}} 目录中的 [{{site.data.keyword.texttospeechshort}}](https://{DomainName}/catalog/services/text-to-speech){: external} 页面。
    1.  {: hide-dashboard} 注册免费的 {{site.data.keyword.cloud_notm}} 帐户或登录。
    1.  {: hide-dashboard} 单击**创建**。
-   复制凭证以向服务实例进行认证：
    1.  {: hide-dashboard} 在 [{{site.data.keyword.cloud_notm}} 资源列表](https://{DomainName}/resources){: external}中，单击 {{site.data.keyword.texttospeechshort}} 服务实例以转至 {{site.data.keyword.texttospeechshort}} 服务仪表板页面。
    1.  在**管理**页面上，单击**显示**以查看凭证。
    1.  复制 `API 密钥`和 `URL` 值。

### 使用 curl 示例
{: #getting-started-curl}

本教程使用 `curl` 命令来调用服务的 HTTP 接口的方法。确保您的系统上已安装 `curl` 命令。

1.  要测试是否已安装 `curl`，请在命令行上运行以下命令。如果输出中列出了支持安全套接字层 (SSL) 的 `curl` 版本，那么您已为教程设置好。

    ```bash
    curl -V
    ```
    {: pre}

1.  如有必要，请从 [curl.haxx.se](https://curl.haxx.se/){: external} 安装适合您操作系统的已启用 SSL 的 `curl` 版本。

请省略示例中的花括号。花括号用于指示变量值。
{: tip}

## 步骤 1：合成美国英语文本
{: #synthesizeEnglish}

以下命令使用 `POST /v1/synthesize` 方法将美国英语输入合成为两种不同格式的音频文件。这两个请求均使用缺省美国英语声音 `en-US_MichaelVoice`。

1.  发出以下命令来合成字符串“hello world”，并生成名为 `hello_world.wav` 的 WAV 文件。
    -   {: hide-dashboard} 将 `{apikey}` 和 `{url}` 替换为您的 API 密钥和 URL。

    *Windows 用户，*将每行末尾的反斜杠 (``\`) 替换为插入标记 (``^`)。确保无结尾空格。
    {: tip}

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

可以使用浏览器或其他工具来播放本教程中示例所生成的音频文件。有关更多信息，请参阅[播放音频文件](/docs/services/text-to-speech?topic=text-to-speech-audioFormats#formatsPlay)。
{: note}

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

-   在 [HTTP 接口](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP)中了解有关服务的 HTTP 接口的更多信息。
-   在 [WebSocket 接口](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket)中了解有关服务的 WebSocket 接口的信息。
-   在 [API 参考](https://{DomainName}/apidocs/text-to-speech){: external}中获取有关服务接口方法的详细信息。
