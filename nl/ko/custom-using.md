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

# 사용자 정의 음성 모델 사용
{: #customUsing}

사용자 정의 모델을 작성하고 이를 사용자 정의 항목으로 채우면 HTTP `GET` 또는 `POST /v1/synthesize` 메소드 또는 WebSocket `/v1/synthesize` 메소드의 `customization_id` 조회 매개변수로 사용자 정의 ID(GUID)를 전달하여 사용자 정의 항목을 사용합니다. 사용자 정의 ID를 포함하는 경우 지정된 사용자 정의 모델을 소유하는 서비스 인스턴스의 인증 정보를 사용하여 `synthesize` 메소드를 호출해야 합니다.
{: shortdesc}

처음 두 개의 예는 표시된 사용자 정의 모델의 항목을 기반으로 하는 `IEEE`에 대한 사용자 정의 발음을 생성합니다. 사용자 정의 발음은 서비스의 일반 발음 규칙으로 생성된 기본 발음 대신 사용됩니다.

-   HTTP `GET /v1/synthesize` 메소드:

    ```bash
    curl -X GET -u "apikey:{apikey}"
    --header "Accept: audio/flac"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

-   HTTP `POST /v1/synthesize` 메소드:

    ```bash
    curl -X POST -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --header "Accept: audio/flac"
    --data "{\"text\":\"IEEE\"}"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

세 번째 예에서는 연결을 통해 전달되는 텍스트를 합성하기 위해 표시된 사용자 정의 모델을 사용하는 `/v1/synthesize` 메소드로 WebSocket 연결을 설정합니다.

```javascript
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
