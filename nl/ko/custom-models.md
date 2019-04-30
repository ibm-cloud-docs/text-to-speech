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

# 사용자 정의 음성 모델 작성 및 관리
{: #customModels}

사용자 정의 모델 관련 작업의 첫 번째 단계는 사용자 정의를 작성하는 것입니다. 사용자 정의가 있으면 메타데이터 및 항목을 조회하거나 업데이트하고 삭제하여(더 이상 필요하지 않은 경우) 모델을 관리할 수 있습니다. 시작하기 전에 사용자 정의 모델에 대한 다음과 같은 일반 사용 정보를 검토하십시오.
{: shortdesc}

## 사용 시 참고사항
{: #customGuidelines}

사용자 정의 인터페이스 관련 작업을 수행할 때 다음 가이드라인을 고려하십시오. 

### 사용자 정의 음성 모델의 소유권
{: #customOwner}

사용자 정의 음성 모델은 인증 정보를 사용하여 사용자 정의 음성 모델을 작성하는 {{site.data.keyword.texttospeechshort}} 서비스의 인스턴스에서 소유합니다. 임의의 방법으로 사용자 정의 모델 관련 작업을 수행하려면 사용자 정의 인터페이스의 메소드를 사용하여 해당 서비스 인스턴스에 대해 작성된 서비스 인증 정보를 사용해야 합니다. 

{{site.data.keyword.texttospeechshort}} 서비스의 동일한 인스턴스를 위해 가져오는 모든 서비스 인증 정보는 해당 서비스 인스턴스에 대해 작성된 모든 사용자 정의 모델에 대한 액세스 권한을 공유합니다. 사용자 정의 모델에 대한 액세스 권한을 제한하려면 서비스의 개별 인스턴스를 작성하고 해당 서비스 인스턴스에 대한 인증 정보만 사용하여 모델을 작성하고 모델 관련 작업을 수행하십시오. 기타 서비스 인스턴스에 대한 인증 정보는 사용자 정의 모델에 영향을 줄 수 없습니다. 

서비스 인증 정보의 소유권을 공유하여 얻을 수 있는 이점은 인증 정보 세트를 취소할 수 있는 것입니다(예: 인증 정보 세트가 손상되는 경우). 그러면 동일한 서비스 인스턴스에 대한 새 인증 정보를 작성하고 계속해서 기존 인증 정보의 소유권을 유지하고 기존 인증 정보로 작성된 사용자 정의 모델에 액세스할 수 있습니다. 

### 로깅 및 데이터 개인정보 보호 요청
{: #customLogging}

서비스가 사용자 정의 인터페이스에 대한 호출을 위해 요청 로깅을 처리하는 방법은 요청에 따라 달라집니다. 

-   서비스는 사용자 정의 음성 모델을 빌드하는 데 사용되는 데이터(단어 및 변환)를 *로깅하지 않습니다*. 사용자 정의 인터페이스를 사용하여 사용자 정의 모델에서 단어 및 변환을 관리하는 경우 `X-Watson-Learning-Opt-Out` 요청 헤더를 설정할 필요가 없습니다. 훈련 데이터는 서비스의 기본 모델을 향상시키는 데 사용되지 않습니다. 
-   서비스는 사용자 정의 모델이 합성 요청에서 사용될 때 데이터를 *로깅합니다*. 합성 요청을 위한 로깅을 방지하려면 `X-Watson-Learning-Opt-Out` 요청 헤더를 `true`로 설정해야 합니다. 

자세한 정보는 [{{site.data.keyword.watson}} 서비스에 대한 요청 로깅 제어](/docs/services/watson/getting-started-logging.html)를 참조하십시오.

### 정보 보안
{: #customSecurity}

서비스를 통해 고객 ID를 사용자 정의 음성 모델에 대해 추가되거나 업데이트되는 데이터와 연관시킬 수 있습니다. 다음 메소드로 `X-Watson-Metadata` 헤더를 전달하여 고객 ID를 사용자 정의 단어와 연관시킬 수 있습니다. 

-   `POST /v1/customizations/{customization_id}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word}`

필요한 경우 `DELETE /v1/user_data` 메소드를 사용하여 고객 ID와 연관된 데이터를 삭제할 수 있습니다. 자세한 정보는 [정보 보안](/docs/services/text-to-speech/information-security.html)을 참조하십시오.

## 사용자 정의 모델 작성
{: #cuModelsCreate}

새 사용자 정의 모델을 작성하려면 `POST /v1/customizations` 메소드를 사용하십시오. 처음 새 사용자 모델을 작성할 때 새 모델은 항상 비어 있습니다. 다른 메소드를 사용하여 해당 모델을 단어/변환 쌍으로 채워야 합니다. 새 사용자 정의 모델은 서비스 인증 정보를 사용하여 새 사용자 정의 모델을 작성하는 사용자가 소유합니다. 자세한 정보는 [사용자 정의 음성 모델의 소유권](#customOwner)을 참조하십시오.

요청의 본문을 사용하여 JSON 오브젝트로 다음 속성을 전달합니다. 

<table>
  <caption>표 1. <code>POST /v1/customizations</code> 메소드의
    매개변수</caption>
  <tr>
    <th style="text-align:left; width:18%">매개변수</th>
    <th style="text-align:center; width:12%">데이터 유형</th>
    <th style="text-align:left">설명</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>필수</em></td>
    <td style="text-align:center">문자열</td>
    <td>
      새 사용자 정의 모델의 사용자 정의 이름입니다. 이름은 쉽게 식별할 수 있도록
      모델을 레이블 지정하는 데 사용됩니다. 이름은 소유하는 모든 사용자 정의 모델 사이에서
      고유해야 합니다.
    </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>선택사항</em></td>
    <td style="text-align:center">문자열</td>
    <td>
      사용자 정의 모델의 언어의 ID입니다. 기본값은
      <code>en-US</code>(미국 영어)입니다.
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>선택사항</em></td>
    <td style="text-align:center">문자열</td>
    <td>
      새 모델의 설명입니다. 선택사항이지만 설명은
      권장사항입니다.
    </td>
  </tr>
</table>

다음 예에서 `curl` 명령으로 `curl Test`라고 하는 새 사용자 정의 모델이 생성됩니다. `Content-Type` 헤더는 `application/json`으로 입력 유형을 식별합니다.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test\", \"language\":\"en-US\", \"description\":\"Customization test via curl\"}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

메소드는 새 모델의 GUID(Globally Unique Identifier)가 포함된 JSON 오브젝트를 리턴합니다. 모델에 액세스하기 위해 GUID는 모델 및 단어의 조회, 수정 및 사용과 같은 호출에서 `customization_id` 매개변수로 사용됩니다. 

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

## 사용자 정의 모델 조회
{: #cuModelsQuery}

기존 사용자 정의 모델에 대한 정보를 조회하려면 `GET /v1/customizations/{customization_id}` 메소드를 사용하십시오. 이는 메소드에 포함된 메타데이터 및 단어/변환 쌍 모두에서 모델에 대한 모든 정보를 표시하기 위한 가장 직접적인 방법입니다.  

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

메소드는 다음 양식의 JSON 오브젝트로 결과를 리턴합니다. 

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

모델이 작성되었을 때 입력된 정보 외에도 출력에는 모델 소유자, 모델의 언어 및 모델이 작성되고 마지막으로 수정된 시간의 서비스 인증 정보가 포함됩니다. 모델이 작성 이후에 수정되지 않았으므로 예에서 두 가지 시간이 동일합니다. 

출력에는 모델의 사용자 정의 항목을 나열하는 `words` 배열도 포함되어 있습니다. 모델이 아직 업데이트되지 않았기 때문에 예의 배열은 비어 있습니다.

## 모든 사용자 정의 모델 조회
{: #cuModelsQueryAll}

소유하는 모든 사용자 정의 모델에 대한 정보를 보려면 `GET /v1/customizations` 메소드를 참조하십시오. 

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

메소드는 요청자가 소유하는 사용자 정의 모델마다 오브젝트를 포함하는 JSON 배열을 리턴합니다. 소유자의 서비스 인증 정보가 `owner` 필드에 표시됩니다.

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

첫 번째 모델의 `created` 및 `last_modified` 시간은 아직 업데이트되지 않았기 때문에 동일합니다. 두 번째 모델의 시간이 다르며 초기 작성 이후에 시간이 변경되었음을 표시합니다. 정보에는 모델에 대해 정의된 사용자 정의 항목이 포함되지 않습니다. 

## 사용자 정의 모델 업데이트
{: #cuModelsUpdate}

사용자 정의 모델에 대한 정보를 업데이트하려면 `POST /v1/customizations/{customization_id}` 메소드를 사용하십시오. JSON 오브젝트로 업데이트를 지정합니다. 이름 및 설명의 수정 외에도 이 메소드를 사용하여 모델에서 단어/변환 쌍을 추가하거나 업데이트할 수도 있습니다. 모델의 언어가 작성되면 변경할 수 없습니다.

다음 예에서는 사용자 정의 모델의 이름 및 설명을 업데이트합니다. 비어 있는 JSON 배열은 모델의 항목이 변경되지 않았음을 나타내는 `words` 매개변수와 함께 전송됩니다. 

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test Update\", \"description\":\"Customization test update via curl\", \"words\":[]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

모델에서 단어 업데이트에 대한 자세한 정보는 [사용자 정의 모델에 여러 단어 추가](/docs/services/text-to-speech/custom-entries.html#cuWordsAdd)를 참조하십시오.

## 사용자 정의 모델 삭제
{: #cuModelsDelete}

더 이상 필요하지 않은 사용자 정의 모델을 삭제하려면 `DELETE /v1/customizations/{customization_id}` 메소드를 사용하십시오. 삭제는 영구적이므로 모델이 더 이상 필요하지 않은 경우에만 이 메소드를 사용하십시오. 

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}
