---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-04"

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

# 信息安全
{: #information-security}

{{site.data.keyword.IBM}} 致力于为客户和合作伙伴提供创新的数据隐私、安全性和监管解决方案。
{: shortdesc}

客户负责确保自己遵守各种法律和法规，包括《欧盟一般数据保护条例》。客户须自行负责从合格的法律顾问那里，就可能会影响客户业务和客户为了遵守此类法律和法规需要采取的任何行动，获得关于任何相关法律和法规要求的认定和解释的意见。
{: important}

此处描述的产品、服务和其他功能并不适用于所有客户情形，并且可用性可能受限。{{site.data.keyword.IBM_notm}} 不会提供法律、会计或审计建议，也不会表述或保证其服务或产品将确保客户遵守任何法律或法规。

如果需要为创建的 {{site.data.keyword.cloud}}{{site.data.keyword.watson}} 资源请求 GDPR 支持

-   在欧盟 (EU) 内，请参阅[请求对欧盟内创建的 {{site.data.keyword.cloud_notm}} Watson 资源的支持](/docs/services/watson?topic=watson-gdpr-sar#request-EU)。
-   在欧盟以外的地区，请参阅[请求对欧盟以外的资源的支持](/docs/services/watson?topic=watson-gdpr-sar#request-non-EU)。

## 欧盟一般数据保护条例 (GDPR)
{: #gdpr}

{{site.data.keyword.IBM_notm}} 致力于为客户和合作伙伴提供创新的数据隐私、安全和监管解决方案，以协助他们完成 GDPR 合规之旅。

在[此处](http://www.ibm.com/gdpr){: external}了解有关 {{site.data.keyword.IBM_notm}} 自己的 GDPR 就绪性旅程以及支持您合规旅程的 GDPR 功能和产品的更多信息。

## 在 Text to Speech 服务中标注和删除数据
{: #gdpr-text-to-speech}

通过 {{site.data.keyword.texttospeechfull}} 服务，您可以删除与语音合成请求和定制声音模型关联的所有数据。要删除数据，必须执行以下操作：

1.  使用 `X-Watson-Metadata` 头将客户标识与请求传递给服务的数据相关联；请参阅[指定客户标识](#specify-customer-id)。
1.  使用 `DELETE /v1/user_data` 方法删除与指定的客户标识关联的所有数据；请参阅[删除数据](#delete-pi)。

缺省情况下，没有客户标识与数据相关联。

试验性和 Beta 功能的目的不是用于生产环境，因此在标注和删除数据时，无法保证这些功能可按预期运行。在实现需要标注和删除数据的解决方案时，不应使用试验性和 Beta 功能。
{: note}

### 指定客户标识
{: #specify-customer-id}

要将客户标识与数据相关联，请在用于传递信息的请求中包含 `X-Watson-Metadata` 头。您可将字符串 `customer_id={id}` 作为头的自变量来传递。以下示例将客户标识 `my_ID` 与通过 `POST /v1/synthesize` 请求传递的数据相关联：

```bash
curl -X POST -u "apikey:{apikey}"
--header "X-Watson-Metadata: customer_id=my_ID"
--header "Content-Type: application/json"
--header "Accept: audio/wav"
--data "{\"text\":\"hello world\"}"
--output hello_world.wav
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```

客户标识可以包含除 `;`（分号）和 `=`（等号）以外的任何字符。请为客户标识指定随机或通用字符串；不要指定个人可标识字符串，例如电子邮件地址或推特标识。可以使用不同的请求指定不同的客户标识。指定的客户标识与其凭证用于请求的服务实例相关联；只有该服务实例的凭证才能用于删除与该标识关联的数据。

在以下方法中使用 `X-Watson-Metadata` 头：

-   使用 HTTP 请求：
    -   `POST /v1/synthesize`
    -   `GET /v1/synthesize`

    客户标识会与随请求一起发送的数据相关联。

-   使用 WebSocket 请求：
    -   `/v1/synthesize`

    使用 `x-watson-metadata` 查询参数来指定客户标识，以将标识与随请求一起发送的数据相关联。必须对该自变量进行 URL 编码，使其成为查询参数，例如 `customer_id%3dmy_ID`。

-   使用用于向定制声音模型添加定制词的请求：
    -   `POST /v1/customizations/{customization_id}`
    -   `POST /v1/customizations/{customization_id}/words`
    -   `PUT /v1/customizations/{customization_id}/words/{word}`

    客户标识会与请求添加或更新的定制词相关联。

### 删除数据
{: #delete-pi}

要删除与客户标识关联的所有数据，请使用 `DELETE /v1/user_data` 方法。您可将字符串 `customer_id={id}` 作为请求的查询参数来传递。以下示例将删除客户标识 `my_ID` 的所有数据：

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/user_data?customer_id=my_ID"
```

`/v1/user_data` 方法用于删除与指定客户标识关联的所有数据，而不考虑这些信息的添加方法。如果没有任何数据与客户标识关联，那么此方法不会有任何影响。您必须使用用于将客户标识与数据相关联的同一服务实例的凭证来发出该请求。
