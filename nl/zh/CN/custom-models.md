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

# 创建和管理定制声音模型
{: #customModels}

使用任何定制模型的第一步都是创建模型。模型存在后，可以通过查询或更新其元数据和条目，并在不再需要时将其删除，从而管理模型。开始之前，请查看有关定制模型的以下常规用法信息。
{: shortdesc}

## 用法说明
{: #customGuidelines}

使用定制接口时，请考虑以下准则。

### 定制声音模型的所有权
{: #customOwner}

定制声音模型由使用其凭证来创建该模型的 {{site.data.keyword.texttospeechshort}} 服务实例所拥有。要以任何方式使用定制模型，您必须使用该服务实例的凭证以及定制接口的各种方法。

针对同一 {{site.data.keyword.texttospeechshort}} 服务实例获取的所有凭证将共享对为该服务实例创建的所有定制模型的访问权。要限制对定制模型的访问权，请创建单独的服务实例，并仅使用该服务实例的凭证来创建和使用该模型。这样，其他服务实例的凭证就无法影响该定制模型。

在凭证之间共享所有权的优点是可以取消一组凭证（例如，如果凭证泄露）。然后，可以为同一服务实例创建新凭证，并仍保持对使用原始凭证创建的定制模型的所有权和访问权。

### 请求日志记录和数据隐私
{: #customLogging}

服务如何处理对定制接口调用的请求日志记录取决于请求：

-   服务*不会*记录用于构建定制声音模型的数据（词和转换项）。使用定制接口来管理定制模型中的词和转换项时，无需设置 `X-Watson-Learning-Opt-Out` 请求头。您的训练数据绝不会用于改进服务的基本模型。
-   定制模型用于合成请求时，服务*会*记录数据。您必须将 `X-Watson-Learning-Opt-Out` 请求头设置为 `true`，以阻止对合成请求进行日志记录。

有关更多信息，请参阅[控制 {{site.data.keyword.watson}} 服务的请求日志记录](/docs/services/watson?topic=watson-gs-logging-overview)。

### 信息安全
{: #customSecurity}

服务允许您将客户标识与针对定制声音模型添加或更新的数据相关联。通过使用以下方法来传递 `X-Watson-Metadata` 头，可以将客户标识与定制词相关联：

-   `POST /v1/customizations/{customization_id}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word}`

然后，可以在需要时使用 `DELETE /v1/user_data` 方法来删除与客户标识关联的数据。有关更多信息，请参阅[信息安全](/docs/services/text-to-speech?topic=text-to-speech-information-security)。

## 创建定制模型
{: #cuModelsCreate}

要创建新的定制模型，请使用 `POST /v1/customizations` 方法。新模型在刚创建时始终为空。您必须使用其他方法向其填充词/转换项对。如果新的定制模型是使用某个服务实例的凭证创建的，那么该模型由该服务实例所拥有。有关更多信息，请参阅[定制声音模型的所有权](#customOwner)。

可在请求主体中将以下属性作为 JSON 对象传递。

<table>
  <caption>表 1. <code>POST /v1/customizations</code> 方法的参数</caption>
  <tr>
    <th style="text-align:left; width:18%">参数</th>
    <th style="text-align:center; width:12%">数据类型</th>
    <th style="text-align:left">描述</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>必需</em></td>
    <td style="text-align:center">String</td>
    <td>
      用户为新定制模型定义的名称。此名称用于标注模型，以方便识别。此名称在您拥有的所有定制模型中必须唯一。
    </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>      可选
    </em></td>
    <td style="text-align:center">String</td>
    <td>
      定制模型语言的标识。对于美国英语，缺省值为 <code>en-US</code>。
    定制模型可与指定语言中可用的任何声音（标准或神经）一起使用。</td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>      可选
    </em></td>
    <td style="text-align:center">String</td>
    <td>
      新模型的描述。虽然描述是可选的，但强烈建议使用描述。
    </td>
  </tr>
</table>

以下示例 `curl` 命令将创建名为 `curl Test` 的新定制模型。`Content-Type` 头将输入的类型标识为 `application/json`。

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test\", \"language\":\"en-US\", \"description\":\"Customization test via curl\"}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

此方法将返回包含新模型的全局唯一标识 (GUID) 的 JSON 对象。在用于访问模型的调用（例如，用于查询、修改和使用模型及其词的调用）中，该 GUID 用作 `customization_id` 参数。

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

## 查询定制模型
{: #cuModelsQuery}

要查询有关现有定制模型的信息，请使用 `GET /v1/customizations/{customization_id}` 方法。这是查看模型所有相关信息（包括其元数据及其包含的词/转换项对）的最直接方法。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

此方法会将其结果作为以下格式的 JSON 对象返回：

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T18:12:31.743Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T18:12:31.743Z",
  "words": []
}
```
{: codeblock}

输出中除了包含在创建模型时输入的信息外，还包含模型所有者的凭证、模型的语言以及模型的创建时间和上次修改时间。由于模型自创建以来尚未进行修改，因此在示例中这两个时间相同。

输出还包含 `words` 数组，用于列出模型的定制条目。由于模型尚未更新，因此示例中的该数组为空。

## 查询所有定制模型
{: #cuModelsQueryAll}

要查看有关您拥有的所有定制模型的信息，请使用 `GET /v1/customizations` 方法：

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

此方法将返回一个 JSON 数组，其中包含请求者拥有的每个定制模型的对象。所有者的凭证会显示在 `owner` 字段中。

```javascript
{
  "customizations": [
    {
      "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T19:15:17.926Z",
      "name": "curl Test",
      "language": "en-US",
      "description": "Customization test via curl",
      "last_modified": "2016-07-15T19:15:17.926Z"
    },
    {
      "customization_id": "63f5807f-a4f2-5766-914e-7abb1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T18:12:31.743Z",
      "name": "curl Test Two",
      "language": "en-US",
      "description": "Second customization test via curl",
      "last_modified": "2016-07-15T18:23:50.912Z"
    }
  ]
}
```
{: codeblock}

第一个模型的 `created` 和 `last_modified` 时间相同，因为该模型尚未更新。第二个模型的这两个时间不同，指示该模型自初始创建以来已更改过。这些信息不包含为模型定义的定制条目。

## 更新定制模型
{: #cuModelsUpdate}

要更新有关定制模型的信息，请使用 `POST /v1/customizations/{customization_id}` 方法。您可将更新指定为 JSON 对象。此方法除了用于修改模型名称和描述外，还可用于在模型中添加或更新词/转换项对。创建模型后，就无法再更改模型的语言。

以下示例将更新定制模型的名称和描述。使用 `words` 参数发送空的 JSON 数组，以指示模型的条目将保持不变。

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test Update\", \"description\":\"Customization test update via curl\", \"words\":[]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

有关更新模型中词的信息，请参阅[向定制模型添加多个词](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsAdd)。

## 删除定制模型
{: #cuModelsDelete}

要废弃不再需要的定制模型，请使用 `DELETE /v1/customizations/{customization_id}` 方法。仅当您确定不再需要模型时，才可使用此方法，因为删除是永久性操作。

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}
