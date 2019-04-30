---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-07"

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

# 使用自訂語音模型
{: #customUsing}

建立自訂模型並在其中移入自訂項目之後，您就可以藉由傳遞其自訂 ID (GUID)，搭配使用 HTTP `GET` 或 `POST /v1/syntheize` 方法、或是 WebSocket `/v1/synthesize` 方法的 `customization_id` 查詢參數來使用它。模型擁有者的服務認證必須用來呼叫一個使用自訂模型的 `synthesize` 方法。
{: shortdesc}

前兩個範例會根據所指出自訂模型中的項目，產生 `IEEE` 的自訂發音。使用的是自訂發音，而不是來自服務一般發音規則的預設發音。

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

第三個範例建立與 `/v1/synthesize` 方法的 WebSocket 連線，此方法使用指出的自訂模型，來合成透過連線傳遞的文字：

```javascript
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
