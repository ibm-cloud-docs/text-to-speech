---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28"

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

# 언어 및 음성
{: #voices}

{{site.data.keyword.texttospeechfull}} 서비스는 다양한 언어, 음성 및 통용어를 지원합니다. 서비스는 언어마다 하나 이상의 남성 또는 여성 음성(또는 둘 다)을 제공합니다. 각 음성은 통용어에 적합한 운율 및 억양을 사용합니다.
{: shortdesc}

## 지원되는 언어 및 음성
{: #languageVoices}

표 1에는 각 언어와 표준어 및 성별에 사용 가능한 음성이 나열되어 있습니다. 요청에서 선택적인 `voice` 매개변수를 생략하는 경우 기본적으로 서비스는 `en-US_MichaelVoice` 음성을 사용합니다. 서비스가 일부 음성의 두 가지 버전을 제공하는 경우 [음성 합성 기술](#technologiesVoices)을 참조하십시오.

`V2` 음성(voice) 배포에 대한 문제점으로 인해 현재 합성된 음성(speech)에서 배경 소음이 발생합니다. 자세한 정보는 [알려진 제한사항](/docs/services/text-to-speech/release-notes.html#limitations)을 참조하십시오.
{: note}

<table style="width:90%">
  <caption>표 1. 지원되는 언어 및 음성</caption>
  <tr>
    <th style="text-align:left">언어</th>
    <th style="text-align:center">음성</th>
    <th style="text-align:center">성별</th>
  </tr>
  <tr>
    <td style="text-align:left">브라질 포르투갈어</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">카스티야 스페인어</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">남성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">불어</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">독일어</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code><br/>
      <code>de-DE_BirgitV2Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code><br/>
      <code>de-DE_DieterV2Voice</code></td>
    <td style="text-align:center">남성</td>
  </tr>
  <tr>
    <td style="text-align:left">이탈리아어</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code><br/>
      <code>it-IT_FrancescaV2Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">일본어</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">라틴 아메리카 스페인어</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">북아메리카 스페인어</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">영국 영어</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td style="text-align:left">미국 영어</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code><br/>
      <code>en-US_AllisonV2Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaVoice</code><br/>
      <code>en-US_LisaV2Voice</code></td>
    <td style="text-align:center">여성</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code><br/>
      <code>en-US_MichaelV2Voice</code></td>
    <td style="text-align:center">남성</td>
  </tr>
</table>

`es-LA_SofiaVoice` 및 `es-US_SofiaVoice` 음성은 필수적으로 동일한 음성입니다. 가장 중요한 차이점은 두 가지 음성이 $(달러 부호)를 해석하는 방식에 관한 것입니다. 라틴 아메리카 버전은 *pesos* 용어를 사용하고 북아메리카 버전은 *d&oacute;lares* 용어를 사용합니다. 두 음성 간의 기타 사소한 차이점도 존재할 수 있습니다.
{: note}

### 음성 합성 기술
{: #technologiesVoices}

일부 음성의 두 가지 버전을 사용할 수 있는 서비스를 제공합니다. 예를 들면, `en-US_AllisonVoice` 및 `en-US_AllisonV2Voice`입니다. 두 가지 버전 간의 기본 차이는 서비스가 음성을 합성하는 데 사용하는 기술로 나타납니다. 

-   *연결 합성*은 요청된 오디오를 생성하기 위해 녹음된 음성의 단편(단위)을 결합합니다. 이를 통해 더욱 맑은 소리로 간주될 수 있는 오디오가 생성되지만 녹음된 단편의 연결 지점으로 인해 음성 왜곡이 발생합니다. 

    이름(예: `en-US_AllisonVoice`)에 문자열 `V2`가 포함되지 않은 음성은 연결 합성을 기반으로 합니다.
-   *딥러닝 합성*은 DNN(Deep Neural Network)을 사용하여 지정된 텍스트에 대한 음성을 합성합니다. 이 방법은 음성의 녹음된 단편을 함께 연결하지 않고 녹음된 음성 데이터에서 DNN을 훈련시키기 위해 기계 학습에 의존합니다. 딥러닝 합성 또는 DNN 기반 합성은 향상된 자연 운율과 좀 더 일관성 있는 전체 품질을 갖춘 오디오를 생성합니다. 

    이름(예: `en-US_AllisonV2Voice`)에 문자열 `V2`에 포함된 음성은 DNN 기반 합성을 사용하는 최신 음성입니다. 

애플리케이션에 맞는 음성을 적용하기 전에 새 음성으로 실험해야 합니다. 두 가지 기술은 다른 신호 품질을 갖춘 오디오를 생성함에 따라 새 음성이 모든 애플리케이션에 적합하지 않을 수 있습니다. 또한 DNN 기반 음성은 다음과 같은 SSML 요소 또는 속성을 지원하지 않습니다. 

-   `<prosody>` 요소의 `volume` 속성
-   `<express-as>` 요소
-   `<voice-transformation>` 요소

애플리케이션이 이 요소를 사용하는 경우 연결 합성을 기반으로 하는 음성을 계속해서 사용하십시오. 

### 음성 사용자 정의
{: #customizeVoice}

텍스트를 합성할 때 서비스는 언어 종속 발음 규칙을 적용하여 각 단어의 일반 철자를 음성 철자로 변환합니다. 서비스의 발음 규칙은 일반적인 단어에 올바르게 적용되지만 특이한 단어(예: 외국어의 어원, 개인 이름 및 약어 또는 두문자어)에 대한 불완전한 결과가 생성될 수 있습니다. 

애플리케이션의 용어집에 이러한 단어가 포함된 경우 사용자 정의 인터페이스를 사용하여 서비스에서 해당 단어를 발음하는 방식을 지정할 수 있습니다. 자세한 정보는 [사용자 정의 이해](/docs/services/text-to-speech/custom-intro.html)를 참조하십시오.

## 음성 지정
{: #specifyVoice}

WebSocket `/v1/synthesize` 메소드를 비롯한 HTTP `GET` 및 `POST /v1/synthesize` 메소드는 모두 선택적인 `voice` 조회 매개변수를 허용하여 합성된 오디오의 음성을 지정합니다. 자세한 정보는 [HTTP 인터페이스](/docs/services/text-to-speech/http.html) 및 [WebSocket 인터페이스](/docs/services/text-to-speech/websockets.html)를 참조하십시오.

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
      지정된 음성에 대해 정의되는 사용자 정의 음성 모델의 GUID(Globally Uique
      Identifier)를 제공합니다. 사용자 정의 ID를 포함하는 경우
      사용자 정의 모델의 소유자에 대한 서비스 인증 정보로 메소드를
      호출해야 합니다.
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

추가 `customization` 필드의 속성은 사용자 정의 음성 모델의 GUID, 이름, 언어 및 설명과 같은 정보를 제공합니다. 또한 모델 소유자의 서비스 인증 정보, 모델이 작성된 날짜와 시간 및 마지막으로 수정된 날짜 및 시간의 서비스 인증 정보도 표시합니다. 
