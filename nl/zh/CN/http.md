---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-24"

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

# HTTP 接口
{: #usingHTTP}

要使用 {{site.data.keyword.texttospeechfull}} 服务的 HTTP REST 接口将文本合成为语音，可调用 `GET` 或 `POST /v1/synthesize` 方法。请指定要合成的文本，以及语音音频的声音和格式。此外，还可以指定要用于请求的定制声音模型。
{: shortdesc}

有关 HTTP 接口的更多信息，请参阅 [API 参考](https://{DomainName}/apidocs/text-to-speech){: external}。

## 将文本合成为音频
{: #synthesize}

要将文本合成为音频，请调用服务的 `/v1/synthesize` 方法的两个版本之一：

-   `GET /v1/synthesize` 方法接受要合成的文本作为必需的 `text` 查询参数。请求的最大大小为 8 KB，其中包括输入文本、指定的任何 SSML 以及 URL 和头。
-   `POST /v1/synthesize` 方法接受要合成的文本作为必需的请求主体中的 JSON 构造。在请求中，URL 和头的最大大小为 8 KB，在请求主体中发送的输入文本的最大大小为 5 KB。5 KB 限制包括指定的任何 SSML。

`/v1/synthesize` 方法的两个版本具有以下相同参数：

<table>
  <caption>表 1. <code>/v1/synthesize</code> 方法的参数</caption>
  <tr>
    <th style="text-align:left; width:18%">参数</th>
    <th style="text-align:center; width:12%">类型</th>
    <th style="text-align:center; width:12%">数据类型</th>
    <th style="text-align:left">描述</th>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>      可选
    </em></td>
    <td style="text-align:center">查询</td>
    <td style="text-align:center">String</td>
    <td>
      指定请求的音频格式或 MIME 类型，服务将使用此种格式返回音频。您还可以使用 HTTP <code>Accept</code> 请求头来指定此值。请对该自变量进行 URL 编码，使其成为 `accept` 查询参数。有关更多信息，请参阅[音频格式](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)。
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>      可选
    </em></td>
    <td style="text-align:center">查询</td>
    <td style="text-align:center">String</td>
    <td>
      指定音频中读文本的声音。使用 <code>/v1/voices</code> 方法来获取受支持声音的当前列表。缺省声音为 <code>en-US_MichaelVoice</code>。有关更多信息，请参阅[语言和声音](/docs/services/text-to-speech?topic=text-to-speech-voices)。
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>      可选
    </em></td>
    <td style="text-align:center">查询</td>
    <td style="text-align:center">String</td>
    <td>
      指定将用于合成的定制声音模型的全局唯一标识 (GUID)。仅当指定的定制声音模型与用于合成的声音的语言相匹配时，才可保证该模型正常工作。如果包含定制标识，那么必须使用拥有定制模型的服务实例的凭证来发出请求。省略此参数可使用没有任何定制的指定声音。有关更多信息，请参阅[了解定制](/docs/services/text-to-speech?topic=text-to-speech-customIntro)。
    </td>
  </tr>
</table>

您还可以在合成请求中，使用可用于所有 {{site.data.keyword.watson}} 服务的以下请求头：

-   `X-Watson-Learning-Opt-Out` 用于指示服务是否记录请求和响应数据以针对未来用户改进服务。要阻止 IBM 访问您的数据以进行常规服务改进，请为此参数指定 <code>true</code>。有关更多信息，请参阅[控制 {{site.data.keyword.watson}} 服务的请求日志记录](/docs/services/watson?topic=watson-gs-logging-overview)。
-   `X-Watson-Metadata` 用于将客户标识与通过请求传递的数据相关联。有关更多信息，请参阅[信息安全](/docs/services/text-to-speech?topic=text-to-speech-information-security)。

如果在 `/v1/synthesize` 方法的输入中指定了无效的查询参数或 JSON 字段，那么服务会返回 `Warnings` 响应头，用于描述并列出每个无效的自变量。尽管出现警告，请求仍会成功。
{: note}

## 指定输入文本
{: #input}

`GET` 和 `POST /v1/synthesize` 方法接受纯输入文本或使用 SSML 进行注释的文本。这两个版本的主要区别在于如何指定要合成的文本：

-   `GET /v1/synthesize` 方法接受由 `text` 查询参数指定的输入文本。您可将输入指定为纯文本或 SSML，这两种文本都必须进行 URL 编码。
-   `POST /v1/synthesize` 方法接受请求主体中的输入文本。您指定输入具有以下简单的 JSON 构造，用于封装纯文本或 SSML。此外，还必须为 `Content-Type` 头指定 `application/json` 值。

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

虽然 `GET` 和 `POST` 方法提供的是等效功能，但使用 `POST` 方法将输入文本传递给服务始终更安全。`POST` 请求在请求主体中传递输入，而 `GET` 请求会在 URL 中公开数据。

## 指定 SSML 输入
{: #ssml-http}

语音合成标记语言 (SSML) 是一种基于 XML 的标记语言，旨在为语音合成应用程序（例如，{{site.data.keyword.texttospeechshort}} 服务）提供文本注释。可以使用 SSML 元素及其属性更好地控制合成和生成的音频输出。

有关使用 SSML 来注释输入文本的更多信息，请参阅[使用 SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml)。该文档列出了服务支持的 SSML 元素和属性的清单。此外，还记录了服务的表现力和声音变换扩展。

## 对 XML 控制字符进行转义
{: #escape}

因为您提交的输入文本可以包含基于 XML 的 SSML 注释，所以服务会验证所有输入，以确保所有 SSML 正确且格式无误。因此，不管输入是否包含 SSML，都必须对输入文本中存在的任何 XML 控制字符进行转义。请使用表 2 中的等效转义字符串或字符编码而不是指示的字符。

<table style="width:80%">
  <caption>表 2. 对 XML 控制字符进行转义</caption>
  <tr>
    <th style="text-align:center; vertical-align:bottom; width:40%">字符</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">转义字符串</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">字符编码</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>&quot;</code><br/>（双引号）</td>
    <td style="text-align:center"><code>&amp;quot;</code></td>
    <td style="text-align:center"><code>&amp;#34;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>'</code><br/>（撇号或单引号）</td>
    <td style="text-align:center"><code>&amp;apos;</code></td>
    <td style="text-align:center"><code>&amp;#39;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&amp;</code><br/>（& 符号）</td>
    <td style="text-align:center"><code>&amp;amp;</code></td>
    <td style="text-align:center"><code>&amp;#38;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&lt;</code><br/>（左尖括号）</td>
    <td style="text-align:center"><code>&amp;lt;</code></td>
    <td style="text-align:center"><code>&amp;#60;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&gt;</code><br/>（右尖括号）</td>
    <td style="text-align:center"><code>&amp;gt;</code></td>
    <td style="text-align:center"><code>&amp;#62;</code></td>
  </tr>
</table>

有关服务如何验证输入文本的更多信息，请参阅 [SSML 验证](/docs/services/text-to-speech?topic=text-to-speech-ssml#errors)。

## 输入文本示例
{: #httpExamples}

以下示例说明了如何使用 HTTP 接口的任一方法来指定输入文本。此外，还说明了如何对 XML 控制字符进行转义。出于可读性目的，示例包含换行符。但在实际输入中，*不要*包含换行符。

### 使用 GET 请求的示例输入
{: #getExamples}

以下示例通过 `GET /v1/synthesize` 方法的 `text` 查询参数传递经过 URL 编码的输入：

-   纯文本输入：

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   SSML 输入：

    ```
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3C
    break%20time=%225s%22/%3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another
    %20sentence.%3C/s%3E%3Cs%3EFinally,%20this%20is%20the%20last%20sentence.
    %3C/s%3E%3C/p%3E%22
    ```
    {: codeblock}

### 使用 POST 请求的示例输入
{: #postExamples}

以下示例在 `POST /v1/synthesize` 方法的主体中传递输入：

-   纯文本输入：

    ```javascript
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   SSML 输入：

    ```javascript
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/>
        paragraph.</s><s>Here is another sentence.</s><s>Finally, this is
        the last sentence.</s></p>"
    }
    ```
    {: codeblock}

### 具有 XML 控制字符的示例输入
{: #xmlExamples}

以下示例将两个句子发送到 `POST /v1/synthesize` 方法。示例将嵌入的 XML 字符进行适当转义。

```
"What have I learned?" he asked. "Everything!"
```
{: codeblock}

-   纯文本输入：

    ```javascript
    {
      "text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
    }
    ```
    {: codeblock}

-   SSML 输入：

    ```javascript
    {
      "text": "<s>&quot;What have I learned?&quot; he asked.
        &quot;<express-as type=\"GoodNews\">Everything!</express-as>&quot;</s>"
    }
    ```
    {: codeblock}
