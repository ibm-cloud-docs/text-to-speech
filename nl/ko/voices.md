---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-25"

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

# 언어 및 음성
{: #voices}

{{site.data.keyword.texttospeechfull}} 서비스는 다양한 언어, 음성 및 통용어를 지원합니다. 이 서비스에서는 언어마다 하나 이상의 여성 음성을 제공합니다. 이 서비스에서는 일부 언어용으로 남성과 여성 음성을 모두 포함하는 여러 음성을 제공합니다. 각 음성은 통용어에 적합한 운율 및 억양을 사용합니다.
{: shortdesc}

서비스에서 이전에 사용 가능했던 `V2` 음성은 중단되었습니다. 애플리케이션에서 `V2` 음성을 사용하는 경우 서비스에서 동등한 `V3` 음성을 자동으로 사용합니다.
{: note}

## 지원되는 언어 및 음성
{: #languageVoices}

표 1에는 유형과 성별을 포함하여 각 언어와 방언에 사용 가능한 음성이 나열되어 있습니다. 모든 음성은 [표준 음성](#standardVoices)과 [신경 음성](#neuralVoices) 둘 다로 사용할 수 있습니다. 요청에서 선택적인 `voice` 매개변수를 생략하는 경우 기본적으로 서비스는 표준 `en-US_MichaelVoice` 음성을 사용합니다. 

<table style="width:100%">
  <caption>표 1. 지원되는 언어 및 음성</caption>
  <tr>
    <th style="text-align:left">언어</th>
    <th style="text-align:center">유형</th>
    <th style="text-align:center">음성</th>
    <th style="text-align:center">성별</th>
  </tr>
  <tr>
    <td style="text-align:left">브라질 포르투갈어</td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">카스티야 스페인어</td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">남성</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
    <td style="text-align:center">남성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">불어</td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">독일어</td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code></td>
    <td style="text-align:center">남성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
    <td style="text-align:center">남성</td>
  </tr>
  <tr>
    <td style="text-align:left">이탈리아어</td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">일본어</td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>ja-JP_EmiV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">라틴 아메리카 스페인어</td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">북아메리카 스페인어</td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">영국 영어</td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">미국 영어</td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>en-US_LisaVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">표준</td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code></td>
    <td style="text-align:center">남성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">신경</td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
    <td style="text-align:center">남성</td>
  </tr>
</table>

`es-LA_SofiaVoice` 및 `es-US_SofiaVoice` 음성은 필수적으로 동일한 음성입니다. 가장 중요한 차이점은 두 가지 음성이 $(달러 부호)를 해석하는 방식에 관한 것입니다. 라틴 아메리카 버전은 *pesos* 용어를 사용하고 북아메리카 버전은 *d&oacute;lares* 용어를 사용합니다. 두 음성 간의 기타 사소한 차이점도 존재할 수 있습니다.
{: note}

### 표준 음성
{: #standardVoices}

표준 음성의 이름(예: `pt-BR_IsabelaVoice` 및 `en-US_AllisonVoice`)에는 버전 문자열(`V3`)이 포함되지 않습니다. 표준 음성에서는 요청된 오디오를 생성하기 위해 연결 합성을 사용하여 녹음된 음성의 단편(단위)을 결합합니다. 녹음된 세그먼트의 연결 지점 때문에 음성이 단절될 수 있으므로, 결과적으로 생성되는 음성의 품질과 자연스러움이 저하될 수 있습니다.

### 신경 음성
{: #neuralVoices}

신경 음성의 이름(예: `pt-BR_IsabelaV3Voice` 및 `en-US_AllisonV3Voice`)에는 버전 문자열(`V3`)이 포함됩니다. 신경 음성 기술에서는 세그먼트 선택과 연결을 사용하지 않고 DNN(Deep Neural Networks)을 사용하여 음성의 음향(스펙트럼) 특성을 예측합니다. DNN은 자연스러운 인간의 음성을 학습하고 예측된 음향 특성에서 결과 오디오를 생성합니다.

합성 중에 DNN에서 피치와 음소 기간(운율), 스펙트럼 구조 및 음성의 파형을 예측합니다. 신경 음성을 통해서는 매우 자연스럽게 들리고 부드러운 오디오 품질의 또렷하고 명확한 음성을 생성합니다. 따라서 표준 음성에 비해 신경 음성의 전체적 품질이 더 일관됩니다.

서비스의 신경 음성 기술에 관한 자세한 정보는 다음을 참조하십시오.

-   블로그 게시물 [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   연구 문서 [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

신경 음성에서는 다음과 같은 SSML 요소 또는 속성을 지원하지 않습니다.

-   `<prosody>` 요소의 `volume` 속성
-   `<express-as>` 요소
-   `<voice-transformation>` 요소

그러나 신경 음성을 사용할 때 이 SSML 기능은 더 이상 필요하지 않습니다. 또한 `<voice-transformation>` 요소 대신 `<prosody>` 요소를 사용하여 신경 음성의 피치와 속도를 수정할 수 있습니다. 자세한 정보는 [prosody 요소](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element)를 참조하십시오.

### 음성 사용자 정의
{: #customizeVoice}

텍스트를 합성할 때 서비스는 언어 종속 발음 규칙을 적용하여 각 단어의 일반 철자를 음성 철자로 변환합니다. 서비스의 발음 규칙은 일반적인 단어에 올바르게 적용되지만 특이한 단어(예: 외국어의 어원, 개인 이름 및 약어 또는 두문자어)에 대한 불완전한 결과가 생성될 수 있습니다.

애플리케이션의 용어집에 이러한 단어가 포함된 경우 사용자 정의 인터페이스를 사용하여 서비스에서 해당 단어를 발음하는 방식을 지정할 수 있습니다. 자세한 정보는 [사용자 정의 이해](/docs/services/text-to-speech?topic=text-to-speech-customIntro)를 참조하십시오.

특정 음성이 아니라 특정 언어에 맞는 사용자 정의 음성 모델을 작성합니다. 따라서 사용자 정의 모델은 지정된 언어의 모든 음성(표준 또는 신경)과 함께 사용할 수 있습니다.

## 음성 지정
{: #specifyVoice}

WebSocket `/v1/synthesize` 메소드를 비롯한 HTTP `GET` 및 `POST /v1/synthesize` 메소드는 모두 선택적인 `voice` 조회 매개변수를 허용하여 합성된 오디오의 음성을 지정합니다. 자세한 정보는 [HTTP 인터페이스](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) 및 [WebSocket 인터페이스](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket)를 참조하십시오.

서비스는 지정된 음성에서 입력 텍스트에 적합한 언어의 이해를 기반으로 합니다. 입력 텍스트의 언어와 일치하는 음성을 지정해야 합니다. 예를 들어, 프랑스어 음성(`fr-FR_ReneeVoice`)을 지정하는 경우 서비스는 입력 텍스트가 프랑스어로 작성된다고 가정합니다. 음성의 언어로 작성되지 않은 텍스트를 전달하는 경우(예: 음성이 프랑스어인 영어 텍스트) 서비스는 의미 있는 결과를 생성하지 않을 수 있습니다.

## 사용 가능한 모든 음성 나열
{: #listVoices}

`GET /v1/voices` 메소드는 사용 가능한 모든 음성에 대한 정보를 나열합니다. 인수를 사용하지 않고 `voices` 이름의 JSON 배열을 리턴합니다. 배열에는 각 음성에 대한 개별 오브젝트가 포함됩니다.

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaVoice",
      "language": "en-US",
      "gender": "female",
      "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
      "description": "Lisa: American English female voice.",
      "customizable": true,
      "supported_features": {
        "voice_transformation": true,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

음성 오브젝트의 필드에서는 다음 정보를 제공합니다.

-   `name`은 음성의 ID입니다(예: `en-US_LisaVoice`). `/v1/synthesize` 메소드의 `voice` 매개변수에 값을 지정하십시오.
-   `language`는 음성의 언어 및 지역을 지정합니다(예: `en-US`).
-   `gender`는 `male` 또는 `female`로 음성을 식별합니다.
-   `url`은 음성에 대한 URL을 식별합니다.
-   `description`은 음성에 대한 간략한 설명을 제공합니다.
-   `customizable`은 음성이 서비스의 사용자 정의 인터페이스로 사용자 정의될 수 있는지 여부를 표시하는 부울 값입니다. (`custom_pronunciation` 필드와 동일한 정보를 제공하는 이 필드는 이전 버전과의 호환성을 위해 유지보수됩니다.)
-   `supported_features`는 음성으로 지원되는 추가 서비스 기능에 대해 설명합니다.
    -   `voice_transformation`은 음성이 SSML `<voice-transformation>` 요소를 사용하여 변환될 수 있는 있는지 여부를 표시하는 부울 값입니다.
    -   `custom_pronunciation`은 음성이 서비스의 사용자 정의 인터페이스로 사용자 정의될 수 있는지 여부를 표시하는 부울 값입니다.

## 특정 음성 나열
{: #listVoice}

`GET /v1/voices/{voice}` 메소드는 특정 음성에 대한 정보를 나열합니다. 이는 두 가지 매개변수를 허용합니다.

<table>
  <caption>표 2. <code>voices</code> 메소드의 매개변수</caption>
  <tr>
    <th style="text-align:left; width:18%">매개변수</th>
    <th style="text-align:center; width:12%">유형</th>
    <th style="text-align:center; width:12%">데이터 유형</th>
    <th style="text-align:left">설명</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>필수</em></td>
    <td style="text-align:center">경로</td>
    <td style="text-align:center">문자열</td>
    <td>
      정보가 리턴되는 음성을 식별합니다. 
      해당 이름으로 음성을 지정합니다(예: <code>en-US_LisaVoice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>선택사항</em></td>
    <td style="text-align:center">조회</td>
    <td style="text-align:center">문자열</td>
    <td>
      지정된 음성의 언어용으로 정의되는 사용자 정의 음성 모델의
      GUID(Globally Uique Identifier)를 제공합니다. 사용자 정의
      ID를 포함하는 경우 사용자 정의 모델을 소유하는
      서비스 인스턴스의 인증 정보를 사용하여 요청해야
      합니다.
</td>
  </tr>
</table>

`customization_id` 매개변수를 생략하는 경우 메소드는 `GET /v1/voices` 메소드를 통해 음성에 대해 리턴된 정보와 동일한 지정된 음성에 대한 JSON 출력을 리턴합니다. `customization_id`를 지정하는 경우 출력에는 지정된 사용자 정의 음성 모델에 대한 정보를 제공하는 `customization` 필드가 포함됩니다.

```javascript
{
  "name": "en-US_LisaVoice",
  "language": "en-US",
  "gender": "female",
  "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
  "description": "Lisa: American English female voice.",
  "customizable": true,
  "supported_features": {
    "voice_transformation": true,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

추가 `customization` 필드의 속성은 사용자 정의 음성 모델의 GUID, 이름, 언어 및 설명과 같은 정보를 제공합니다. 또한 모델 소유자의 인증 정보, 모델이 작성된 날짜와 시간 및 마지막으로 수정된 날짜 및 시간도 표시합니다.
