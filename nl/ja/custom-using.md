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

# カスタム音声モデルの使用
{: #customUsing}

カスタム・モデルを作成してカスタム項目を設定したら、HTTP の `GET /v1/synthesize` または `POST /v1/synthesize` メソッド、または WebSocket の `/v1/synthesize` メソッドの `customization_id` 照会パラメーターを使用して、カスタム・モデルのカスタマイズ ID (GUID) を渡して使用します。カスタム・モデルを使用して `synthesize` メソッドを呼び出すには、そのモデルの所有者のサービス資格情報を使用する必要があります。
{: shortdesc}

最初の 2 つの例は、指定したカスタム・モデルの項目に基づいて `IEEE` のカスタム発音を生成するものです。サービスの標準の発音ルールによるデフォルトの発音の代わりに、カスタム発音が使用されます。

-   HTTP の `GET /v1/synthesize` メソッドを使用する場合

    ```bash
    curl -X GET -u "apikey:{apikey}"
    --header "Accept: audio/flac"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

-   HTTP の `POST /v1/synthesize` メソッドを使用する場合

    ```bash
    curl -X POST -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --header "Accept: audio/flac"
    --data "{\"text\":\"IEEE\"}"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

3 つ目の例は、`/v1/synthesize` メソッドを使用して WebSocket 接続を確立し、指定したカスタム・モデルを使用して、接続を介して渡されるテキストの音声合成を行うものです。

```javascript
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
