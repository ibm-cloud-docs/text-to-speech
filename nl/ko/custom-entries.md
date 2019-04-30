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

# 사용자 정의 항목 작성 및 관리
{: #customWords}

사용자 정의 모델이 존재하면 다음 단계는 합성 중에 지정된 단어가 발음되는 방식을 정의하기 위해 단어/변환 쌍의 양식으로 사용자 정의 항목을 추가하는 것입니다. 정의는 서비스의 기본 일반 발음 규칙을 대체합니다. 한 번에 하나 이상의 단어에 대한 변환을 추가하고 조회할 수 있으며 더 이상 필요하지 않은 개별 단어를 삭제할 수 있습니다. 사용자 정의 인터페이스에 익숙해지면 한 번에 여러 단어를 처리하는 것이 단어별로 작업하는 것보다 더욱 편리할 수 있습니다. 사용자 정의 ID가 필요한 메소드를 사용하려면 사용자 정의 모델을 소유하는 서비스의 인스턴스에 대한 서비스 인증 정보를 사용해야 합니다.
{: shortdesc}

## 사용자 정의 모델에 하나의 단어 추가
{: #cuWordAdd}

사용자 정의 모델에 하나의 단어/변환 쌍을 추가하려면 `PUT /v1/customizations/{customization_id}/words/{word}` 메소드를 사용하십시오. 메소드의 URL에서 추가될 단어를 지정합니다. JSON 오브젝트로서 단어에 대한 변환을 하나의 `translation` 속성에 제공합니다. 모델에 이미 존재하는 단어에 대한 새 변환을 추가하면 단어의 기존 변환을 겹쳐씁니다.

유사 발음 또는 음성 메소드(또는 둘의 조합)를 사용하여 변환을 제공할 수 있습니다. 음성 변환을 위해 IPA(International Phonetic Alphabet) 또는 {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation(SPR) 형식을 사용할 수 있습니다. 다음 예에서는 `IEEE` 단어의 동등한 변환을 사용자 정의 모델에 추가하기 위한 다른 방법을 사용합니다. 

-   **유사 발음:** 이 예에서 유사 발음 메소드는 가장 단순한 방법입니다. 

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"I triple E\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **음성 IPA:** IPA는 `alphabet` 속성이 `ipa`로 설정되고 `ph` 속성이 IPA 형식으로 정의된 `<phoneme>` 요소를 사용해야 합니다. 

    <pre><code class="language-bash">  curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#712;a&#618;.t&#633;&#712;&#616;p&#601;l.&#712;i\\\"&gt;&lt;/phoneme&gt;\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"</code></pre>

-   **음성 {{site.data.keyword.IBM_notm}} SPR:** SPR은 `alphabet` 속성이 `ibm`으로 설정되고 `ph` 속성이 SPR 형식으로 정의된 `<phoneme>` 요소를 사용해야 합니다. 

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

## 사용자 정의 모델에 여러 단어 추가
{: #cuWordsAdd}

한 번에 하나 이상의 단어를 사용자 정의 모델에 추가하려면 `POST /v1/customizations/{customization_id}/words` 메소드를 사용하십시오. 단어/변환 쌍의 JSON 배열로 사용자 정의 모델에 추가될 항목을 지정합니다. 다음 예는 `NCAA` 및 `iPhone` 단어에 대한 일반적인 유사 발음 변환을 사용자 정의 모델에 추가합니다. 

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

요청 본문에 전송된 JSON 컨텐츠는 다음과 같습니다. 

```javascript
{
  "words": [
    {"word":"NCAA", "translation":"N C double A"},
    {"word":"iPhone", "translation":"I phone"}
  ]
}
```
{: codeblock}

[사용자 정의 모델 업데이트](/docs/services/text-to-speech/custom-models.html#cuModelsUpdate)에 설명된 대로 `POST /v1/customizations/{customization_id}` 메소드를 사용하여 단어를 사용자 정의 모델에 추가할 수 있습니다. 다음 예에서는 이 메소드를 사용하여 이전 예와 동일한 두 개의 단어를 추가합니다. 이때 모델의 메타데이터는 변경되지 않습니다. URL을 제외하고 두 개의 메소드가 동일합니다. 

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

## 일본어 사용자 정의 모델에 단어 추가
{: #cuJapaneseAdd}

일본어 사용자 정의 모델에서 단어에 대한 항목을 작성할 때 추가 고려사항 및 추가 `part_of_speech` 필드가 적용됩니다. 자세한 정보는 [일본어 항목 관련 작업](/docs/services/text-to-speech/custom-rules.html#jaNotes)을 참조하십시오. 다음과 같이 일본어 사용자 정의 항목에 대한 품사를 지정하십시오. 

-   `PUT /v1/customizations/{customization_id}/words/{word}` 메소드의 경우 다음 양식의 JSON 오브젝트를 전달하십시오. 

    ```javascript
    {
      "translation": "value",
      "part_of_speech": "value"
    }
    ```
    {: codeblock}

-   `POST /v1/customizations/{customization_id}/words` 및 `POST customizations/{customization_id}` 메소드의 경우 다음과 유사한 JSON 오브젝트를 전달하십시오.

    ```javascript
    {
      "words": [
        {
          "word": "value",
          "translation": "value",
          "part_of_speech": "value"
        }
        . . .
      ]
    }
    ```
    {: codeblock}

`PUT /v1/customizations/{customization_id}/words/{word}` 메소드의 다음 예는 URL로 인코딩된 `NY`의 2바이트 문자열을 명사(`Mesi`) <code>&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;</code>(영어로는 `New York`)로 변환합니다. 사용자 정의 변환이 정의되지 않으면 문자열은 `enu wai`로 읽혀집니다.

-   **유사 발음:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **음성 IPA:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#626;&#623;&#720;&#106;&#111;&#720;&#107;&#623;\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **음성 {{site.data.keyword.IBM_notm}} SPR:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

## 사용자 정의 모델에서 하나의 단어 조회
{: #cuWordQueryModel}

사용자 정의 모델에서 하나의 단어에 대한 변환을 조회하려면 `GET /v1/customizations/{customization_id}/words/{word}` 메소드를 사용하십시오. 메소드의 URL에서 단어를 지정합니다. 변환은 사용자 정의 모델에 정의된 대로 리턴됩니다(유사 발음 또는 음성). 

다음 예에서는 `IEEE` 단어의 변환을 위해 사용자 정의 모델을 조회합니다. 

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

단어가 모델에서 유사 발음으로 변환된 경우 예에서는 다음 JSON 출력을 리턴합니다. 

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

## 사용자 정의 모델에서 모든 단어 조회
{: #cuWordsQueryModel}

사용자 정의 모델에 정의된 모든 단어의 변환을 보려면 `GET /v1/customizations/{customization_id}/words` 메소드를 사용하십시오. 다음 예에서는 세 가지 단어의 유사 발음 변환이 포함된 사용자 정의 모델에서 항목을 나열하기 위한 메소드를 사용합니다. 

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

메소드는 다음 데이터가 포함된 JSON 배열을 리턴합니다. 일본어 사용자 정의 모델의 경우 출력에는 개별 단어의 품사가 포함됩니다. 

```javascript
{
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

[사용자 정의 모델 조회](/docs/services/text-to-speech/custom-models.html#cuModelsQuery)에 설명된 대로 `GET /v1/customizations/{customization_id}` 메소드를 사용하여 사용자 정의 모델에 대한 메타데이터와 단어를 모두 볼 수도 있습니다. 

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

메소드는 다음 양식의 JSON 출력을 리턴합니다. 이 예와 이전 예에서는 동일한 사용자 정의 모델을 지정하므로 출력의 단어 배열이 동일합니다. 

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T19:15:17.926Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T19:46:01.387Z",
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

## 언어에서 단어 조회
{: #cuWordsQueryLanguage}

단어의 발음을 조회하려면 `GET /v1/pronunciation` 메소드를 사용하십시오. 해당 음성의 언어로 된 발음을 가져오려면 음성을 지정하십시오. 기본적으로 메소드는 서비스의 일반 발음 규칙에 따라 발음을 리턴하지만 지정된 사용자 정의 음성 모델의 발음을 요청할 수도 있습니다. 메소드에는 리턴될 정보를 지정할 수 있도록 네 개의 조회 매개변수가 포함됩니다. 

-   필수 `text` 매개변수는 발음이 리턴될 단어를 지정합니다. 
-   선택적인 `voice` 매개변수를 사용하면 발음의 언어를 지정할 수 있습니다. 원하는 언어를 표시하도록 음성 모델(예: `en-US_LisaVoice`) 중 하나를 지정합니다. 동일한 언어(예: `en-US`)의 모든 음성은 동일한 발음을 리턴합니다. 기본적으로 미국 영어의 발음이 리턴됩니다. 
-   선택적인 `format` 매개변수를 사용하면 `ipa` 또는 `ibm` 중 하나로 발음의 음성 형식을 지정할 수 있습니다. 기본적으로 발음은 IPA 형식으로 리턴됩니다. 
-   선택적인 `customization_id` 매개변수를 사용하면 발음이 리턴될 사용자 정의 음성 모델을 지정할 수 있습니다. 단어가 지정된 음성 모델에서 정의되지 않은 경우 서비스는 모델의 언어에 맞는 기본 발음을 리턴합니다. 사용자 정의가 없는 지정된 음성에 대한 변환을 확인하려면 매개변수를 생략하십시오. 음성 및 사용자 정의 음성 모델을 모두 지정하지 마십시오. 

이 메소드를 통해 모든 언어로 된 단어를 조회할 수 있으며, 사용자 정의 ID가 필요하지 않음에 따라 볼 수 있는 단어에 대한 제한이 없으므로 이 메소드는 유용합니다. 새 단어에 대한 음성 변환을 구성할 때 특히 유용합니다. 즉, 기존 단어에 대한 음성을 가져오기 위해 이 메소드를 사용한 후 새 변환을 기반으로 하여 이를 사용할 수 있습니다. 이 메소드를 사용하면 처음부터 변환을 구성하는 것 보다 훨씬 편리합니다. 

다음 예에서는 기본 IPA 형식으로 `IEEE` 단어에 대한 발음을 가져옵니다. 

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=IEEE"
```
{: pre}

<pre><code data-copy="false" class="language-javascript">{
  "pronunciation": ".&#712;a&#618; .&#712;i .&#712;i .&#712;i"
}</code></pre>

다음 예에서는 `IEEE` 단어에 대한 유사 발음 변환을 입력하고 {{site.data.keyword.IBM_notm}} SPR 형식으로 동등한 음성 항목을 가져옵니다. 음성 변환을 구성하기 위해 유사 발음 변환에 대한 음성 발음을 가져오는 것은 특히 흥미로운 방법입니다. 이 예에서 단어의 공백은 URL 인코딩입니다.

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=i%20triple%20e&format=ibm"
```
{: pre}

```javascript
{
  "pronunciation": "1Y.tr1Ipxl.1i"
}
```
{: codeblock}

## 사용자 정의 모델에서 단어 삭제
{: #cuWordDelete}

사용자 정의 모델에서 단어를 삭제하려면 `DELETE /v1/customizations/{customization_id}/words/{word}` 메소드를 사용하십시오. 메소드의 URL에서 삭제될 단어를 지정합니다. 개별 단어만 삭제할 수 있으며 하나의 메소드를 사용하여 여러 단어를 삭제할 수 없습니다. 

다음 예에서는 지정된 사용자 정의 모델에서 `IEEE` 단어를 삭제합니다.

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}
