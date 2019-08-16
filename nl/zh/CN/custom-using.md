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

# 使用定制声音模型
{: #customUsing}

创建定制模型并使用定制条目填充该模型后，通过使用 HTTP `GET` 或 `POST /v1/synthesize` 方法或者 WebSocket `/v1/synthesize` 方法的 `customization_id` 查询参数来传递其定制标识 (GUID)，可使用该模型。如果包含定制标识，那么必须使用拥有指定定制模型的服务实例的凭证来调用 `synthesize` 方法。
{: shortdesc}

前两个示例根据指示的定制模型中的条目生成 `IEEE` 的定制发音。这将使用定制发音，而不使用服务的常规发音规则中的缺省发音。

-   HTTP `GET /v1/synthesize` 方法：

    ```bash
    curl -X GET -u "apikey:{apikey}"
    --header "Accept: audio/flac"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

-   HTTP `POST /v1/synthesize` 方法：

    ```bash
    curl -X POST -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --header "Accept: audio/flac"
    --data "{\"text\":\"IEEE\"}"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

第三个示例使用 `/v1/synthesize` 方法建立 WebSocket 连接，此方法使用指示的定制模型来合成通过该连接传递的文本：

```javascript
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
