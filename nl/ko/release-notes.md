---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-30"

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

# 릴리스 정보
{: #release-notes}

다음 절에서는 {{site.data.keyword.texttospeechfull}} 서비스의 각 릴리스 및 업데이트에 포함된 새 기능과 변경사항을 문서화합니다. 정보에는 알려진 제한사항이 포함됩니다. 별도로 언급하지 않는 한 모든 변경사항은 이전 릴리스와 호환되며 모든 새 애플리케이션 및 기존 애플리케이션에 자동으로 투명하게 적용됩니다.
{: shortdesc}

## 알려진 제한사항
{: #limitations}

현재 알려진 제한사항이 없습니다.

## 2019년 7월 30일
{: #July2019}

이 서비스에서는 이제 일본어로 된 신경 음성(`ja-JP_EmiV3Voice`)을 제공합니다. 이제 지원되는 모든 언어로 된 사용 가능한 모든 음성의 표준 및 신경 버전을 사용할 수 있습니다. 자세한 정보는 [언어 및 음성](/docs/services/text-to-speech?topic=text-to-speech-voices)을 참조하십시오.

## 2019년 6월 24일
{: #June2019}

-   서비스에서는 이제 두 가지 버전으로 된 사용 가능한 대부분의 음성을 제공합니다.
    -   [표준 음성](/docs/services/text-to-speech?topic=text-to-speech-voices#standardVoices)에서는 오디오를 생성하기 위해 연결 합성을 사용하여 녹음된 음성의 단편을 결합합니다. 표준 음성의 이름(예: `en-US_AllisonVoice`)에는 버전 문자열이 포함되지 않습니다.
    -   DNN(Deep Neural Network)을 사용하여 음성의 음향(스펙트럼) 기능을 예측하는 [신경 음성](/docs/services/text-to-speech?topic=text-to-speech-voices#neuralVoices)입니다. 신경 음성의 이름(예: `en-US_AllisonV3Voice`)에는 버전 문자열(`V3`)이 포함됩니다.

    `ja-JP_EmiVoice` 음성(현재 보류 중이며 곧 지원 예정)을 제외한 모든 표준 음성에 향상된 신경 버전이 지원됩니다. SSML `<express-as>` 및 `<voice-transformation>` 요소와 함께 신경 음성을 사용할 수 없으며 `<prosody>` 요소의 `volume` 속성을 신경 음성과 함께 사용할 수 없습니다.

    사용 가능한 모든 음성에 관한 자세한 정보는 [언어 및 음성](/docs/services/text-to-speech?topic=text-to-speech-voices)을 참조하십시오.
-   서비스에는 이전에 사용 가능한 `V2` DNN 음성이 더 이상 포함되지 않습니다. 애플리케이션에서 `V2` 음성을 사용하는 경우 서비스에서 동등한 `V3` 음성을 자동으로 사용합니다.


## 2019년 3월 24일
{: #March2019c}

-   서비스는 이제 독일어 음성을 지원하는 `V2` DNN(Deep Neural Network) 버전을 제공합니다. 
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

   DNN 기반 음성에 관한 자세한 정보는 [언어 및 음성](/docs/services/text-to-speech?topic=text-to-speech-voices)을 참조하십시오.
-   모든 서비스의 DNN 기반 음성은 이제 SSML `<prosody>` 요소의 `pitch` 및 `rate` 속성을 지원합니다. DNN 기반 음성은 `<prosody>` 요소의 `volume` 속성을 지원하지 않습니다. 자세한 정보는 [prosody 요소](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element)를 참조하십시오.

## 이전 릴리스
{: #older}

-   [2019년 3월 21일](#March2019b)
-   [2019년 3월 4일](#March2019a)
-   [2019년 1월 28일](#January2019)
-   [2018년 12월 13일](#December2018)
-   [2018년 11월 7일](#November2018)
-   [2018년 10월 30일](#October2018)
-   [2018년 6월 12일](#June2018)
-   [2018년 5월 15일](#May2018)
-   [2017년 10월 2일](#October2017)
-   [2017년 7월 14일](#July2017)
-   [2017년 4월 10일](#April2017)
-   [2016년 12월 1일](#December2016)
-   [2016년 9월 22일](#September2016)
-   [2016년 6월 23일](#June2016)
-   [2016년 3월 10일](#March2016)
-   [2016년 2월 22일](#February2016)
-   [2015년 12월 17일](#December2015)
-   [2015년 9월 21일](#September2015)
-   [2015년 7월 1일](#July2015)

### 2019년 3월 21일
{: #March2019b}

사용자는 이제 {{site.data.keyword.cloud_notm}} 계정에 지정되었던 역할과 연관된 서비스 인증 정보만 볼 수 있습니다. 예를 들어, `reader` 역할이 지정된 경우 `writer` 또는 상위 레벨의 서비스 인증 정보는 더 이상 표시되지 않습니다.

이 변경사항은 기존 서비스 인증 정보를 사용한 사용자 또는 애플리케이션의 API 액세스에 영향을 주지 않습니다. 변경사항은 {{site.data.keyword.cloud_notm}} 내의 인증 정보 보기에만 영향을 줍니다.

서비스 키 및 사용자 역할에 대한 자세한 정보는 [IAM 서비스 API 키](/docs/services/watson?topic=watson-api-key-bp#api-key-bp)를 참조하십시오.

### 2019년 3월 4일
{: #March2019a}

이 서비스에서는 이제 오디오를 생성하기 위해 딥러닝(deep-learning) 합성을 사용하는 네 가지 새로운 `V2` 음성을 제공합니다.

-   `it-IT_FrancescaV2Voice`
-   `en-US_AllisonV2Voice`
-   `en-US_LisaV2Voice`
-   `en-US_MichaelV2Voice`

새 음성은 기계 학습 및 DNN을 사용하여 문자-음성 변환을 합성합니다. 딥러닝 합성 또는 DNN(Deep Neural Network) 기반 합성을 통해 향상된 자연 운율과 좀 더 일관성 있는 전체 품질을 갖춘 오디오가 생성됩니다. 

그러나 새 음성은 기존 음성과는 다른 신호 품질을 갖춘 오디오도 생성함에 따라 모든 애플리케이션에 적합하지 않을 수 있습니다. 또한 새 음성은 `<prosody>`, `<express-as>` 및 `<voice-transformation>`의 SSML 요소를 지원하지 않습니다.

DNN 기반 음성, DNN 기반 음성과 기존 음성 간의 차이점에 대한 자세한 정보는 [언어 및 음성](/docs/services/text-to-speech?topic=text-to-speech-voices)을 참조하십시오.

### 2019년 1월 28일
{: #January2019}

WebSocket 인터페이스는 이제 브라우저 기반 JavaScript 코드에서 토큰 기반 IAM(Identity and Access Management) 인증을 지원합니다. 반대되는 제한사항은 제거되었습니다. WebSocket `/v1/synthesize` 메소드를 사용하여 인증된 연결을 설정하려면 다음을 수행하십시오.

-   IAM 인증을 사용하는 경우 `access_token` 조회 매개변수를 포함하십시오.
-   Cloud Foundry 서비스 인증 정보를 사용하는 경우 `watson-token` 조회 매개변수를 포함하십시오.

자세한 정보는 [연결 열기](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket#WSopen)를 참조하십시오.

### 2018년 12월 13일
{: #December2018}

이제 {{site.data.keyword.cloud}} 런던 위치(**eu-gb**)에서 {{site.data.keyword.texttospeechshort}} 서비스를 사용할 수 있습니다. 모든 위치와 마찬가지로 런던은 토큰 기반 IAM(Identity and Access Management) 인증을 사용합니다. 이 위치에서 작성하는 모든 새 서비스 인스턴스는 IAM 인증을 사용합니다.

### 2018년 11월 7일
{: #November2018}

이제 {{site.data.keyword.cloud}} 도쿄 위치(**jp-tok**)에서 {{site.data.keyword.texttospeechshort}} 서비스를 사용할 수 있습니다. 모든 위치와 마찬가지로 도쿄는 토큰 기반 IAM(Identity and Access Management) 인증을 사용합니다. 이 위치에서 작성하는 모든 새 서비스 인스턴스는 IAM 인증을 사용합니다.

### 2018년 10월 30일
{: #October2018}

{{site.data.keyword.texttospeechshort}} 서비스는 모든 위치에 적합한 토큰 기반 IAM(Identity and Access Management) 인증으로 마이그레이션됩니다. 모든 {{site.data.keyword.cloud_notm}} 서비스는 이제 IAM 인증을 사용합니다. {{site.data.keyword.texttospeechshort}} 서비스는 다음 날짜에 각 위치에서 마이그레이션되었습니다.

-   댈러스(**us-south**): 2018년 10월 30일
-   프랑크푸르트(**eu-de**): 2018년 10월 30일
-   워싱턴, DC(**us-east**): 2018년 6월 12일
-   시드니(**au-syd**): 2018년 5월 15일

IAM 인증으로 마이그레이션하면 새 서비스 인스턴스와 기존 서비스 인스턴스에 각각 영향을 줍니다.

-   *임의의 위치에서 작성하는 모든 새 서비스 인스턴스*는 이제 IAM 인증을 사용하여 서비스에 액세스합니다. 전달자 토큰 또는 API 키 중 하나를 전달할 수 있습니다. 토큰은 모든 호출에서 서비스 인증 정보를 임베드하지 않고 인증된 요청을 지원하며, API 키는 HTTP 기본 인증을 사용합니다. {{site.data.keyword.ibmwatson}} SDK를 사용하는 경우 API 키를 전달하고 SDK가 토큰의 라이프사이클을 관리하도록 할 수 있습니다.
-   *표시된 마이그레이션 날짜 전에 위치에서 작성한 기존 서비스 인스턴스*는 IAM 인증을 사용하도록 서비스 인증 정보를 마이그레이션할 때까지 인증을 위해 이전 Cloud Foundry 서비스 인증 정보에서 `{username}` 및 `{password}`를 계속 사용합니다. IAM 인증으로의 마이그레이션에 대한 자세한 정보는 [Cloud Foundry 서비스 인스턴스를 리소스 그룹으로 마이그레이션](https://{DomainName}/docs/resources?topic=resources-migrate)을 참조하십시오.

자세한 정보는 다음 문서를 참조하십시오.

-   서비스 인스턴스에서 사용하는 인증 메커니즘에 대해 알아보려면 [{{site.data.keyword.cloud_notm}} 대시보드](https://{DomainName}/dashboard/apps){: external}의 인스턴스를 클릭하여 서비스 인증 정보를 보십시오.
-   {{site.data.keyword.watson}} 서비스를 통한 IAM 토큰 사용에 대한 자세한 정보는 [IAM 토큰으로 인증](/docs/services/watson?topic=watson-iam)을 참조하십시오.
-   {{site.data.keyword.watson}} 서비스를 통한 IAM API 키 사용에 대한 자세한 정보는 [IAM 서비스 API 키](/docs/services/watson?topic=watson-api-key-bp)를 참조하십시오.
-   IAM 인증을 사용하는 예는 [API 참조](https://{DomainName}/apidocs/text-to-speech){: external}를 확인하십시오.

### 2018년 6월 12일
{: #June2018}

다음 기능은 워싱턴, DC(**us-east**)에서 호스팅하는 애플리케이션에 사용할 수 있습니다.

-   서비스는 이제 새 API 인증 프로세스를 지원합니다. 자세한 정보는 [2018년 10월 30일 서비스 업데이트](#October2018)를 참조하십시오.
-   서비스는 이제 `X-Watson-Metadata` 헤더 및 `DELETE /v1/user_data` 메소드를 지원합니다. 자세한 정보는 [정보 보안](/docs/services/text-to-speech?topic=text-to-speech-information-security)을 참조하십시오.

### 2018년 5월 15일
{: #May2018}

다음 기능은 시드니(**au-syd**)에서 호스팅하는 애플리케이션에 사용할 수 있습니다.

-   서비스는 이제 새 API 인증 프로세스를 지원합니다. 자세한 정보는 [2018년 10월 30일 서비스 업데이트](#October2018)를 참조하십시오.
-   서비스는 이제 `X-Watson-Metadata` 헤더 및 `DELETE /v1/user_data` 메소드를 지원합니다. 자세한 정보는 [정보 보안](/docs/services/text-to-speech?topic=text-to-speech-information-security)을 참조하십시오.

### 2017년 10월 2일
{: #October2017}

`audio/l16` 형식의 경우 이제 리턴된 오디오의 엔디언을 선택적으로 지정할 수 있습니다. (미리 샘플링 속도를 지정해야 합니다.) 예를 들면, `audio/l16;rate=22050;endianness=big-endian` 및 `audio/l16;rate=22050;endianness=little-endian`입니다. 기본값은 빅 엔디언입니다. 자세한 정보는 [오디오 형식](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)을 참조하십시오.

### 2017년 7월 14일
{: #July2017}

서비스는 이제 MP3 또는 MPEG(Motion Picture Experts Group) 오디오 형식을 지원합니다. 지원되는 오디오 형식에 대한 자세한 정보는 [오디오 형식](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)을 참조하십시오.

### 2017년 4월 10일
{: #April2017}

-   서비스는 이제 Opus 또는 Vorbis 코덱이 포함된 WebM(Web Media) 오디오 형식을 지원합니다. 또한 Opus 코덱 외에도 Vorbis 코덱이 포함된 Ogg 오디오 형식을 지원합니다. 지원되는 오디오 형식에 대한 자세한 정보는 [오디오 형식](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)을 참조하십시오.
-   서비스는 이제 브라우저 기반 클라이언트가 서비스를 직접 호출할 수 있도록 CORS(Cross-Origin Resource Sharing)를 지원합니다. 자세한 정보는 [CORS 지원](/docs/services/text-to-speech?topic=text-to-speech-overview#cors)을 참조하십시오.
-   사용자 정의 인터페이스의 일부 메소드를 완료하기 위해 HTTP 응답 코드가 다음과 같이 변경되었습니다.
    -   `POST /v1/customizations` 메소드는 이제 201을 리턴합니다(200 대신).
    -   `POST /v1/customizations/{customization_id}` 메소드는 이제 200을 리턴합니다(201 대신).
    -   `POST /v1/customizations/{customization_id}/words` 메소드는 이제 200을 리턴합니다(201 대신).
    -   `PUT /v1/customizations/{customization_id}/words/{word}` 메소드는 이제 200을 리턴합니다(201 대신).
-   일본어 이외의 언어로 `part_of_speech`를 지정하려는 경우 `POST /v1/customizations/{custom_id}/words` 및 `PUT /v1/customizations/{customization_id}/words/{word}` 메소드는 이제 HTTP 리턴 코드 400을 리턴하며 오류 메시지는 `Part of speech is supported for ja-JP language only`입니다.
-   `POST /v1/customizations/{custom_id}/words` 메소드는 이제 비어 있는 응답 본문(`{}`)을 리턴합니다.

### 2016년 12월 1일
{: #December2016}

-   서비스에는 `es-US_SofiaVoice` 음성과 동등한 라틴 아메리카의 새 음성인 `es-LA_SofiaVoice`가 포함됩니다. 두 음성의 가장 중요한 차이점은 `$`(달러 부호)의 해석 방식에 관한 것입니다. 라틴 아메리카 버전에서는 *pesos* 용어를 사용하지만 북아메리카 버전에서는 *dolares* 용어를 사용합니다. 두 음성 간의 기타 사소한 차이점도 존재할 수 있습니다.
-   `en-US_AllisonVoice` 외에도 이제 `en-US_LisaVoice` 및 `en-US_MichaelVoice`의 두 가지 추가 음성이 SSML 음성 변환으로 변환될 수 있습니다. 음성 변환에 대한 자세한 정보는 [음성 변환 SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation)을 참조하십시오.
-   일본어로 된 사용자 정의 인터페이스를 사용하는 경우 서비스는 이제 사용자 정의 음성 모델에 대해 정의된 단어/변환 쌍에서 가장 긴 단어와 일치합니다. 예를 들어, 사용자 정의 음성에 대해 다음 두 가지 항목을 고려하십시오:

    <pre><code data-copy="false" class="language-javascript">  {
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    서비스에서 입력 텍스트에 있는 문자열 <code>&#65326;&#65337;&#65315;</code>를 찾은 경우 이 문자열이 <code>&#65326;&#65337;</code>보다 길기 때문에 해당 단어와 일치합니다. 이전에 서비스는 문자열 <code>&#65326;&#65337;</code>과 일치했습니다. 사용자 정의 음성 모델의 일본어 항목 관련 작업에 대한 자세한 정보는 [일본어 항목 관련 작업](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes)을 참조하십시오.

### 2016년 9월 22일
{: #September2016}

-   사용자 정의와 `GET /v1/pronunciation` 메소드에 포함되는 사용자 정의 인터페이스는 이제 서비스에서 지원되는 모든 언어로 사용할 수 있습니다. 인터페이스는 베타 릴리스로 유지됩니다. 자세한 정보는 [사용자 정의 이해](/docs/services/text-to-speech?topic=text-to-speech-customIntro)를 참조하십시오.
-   서비스는 이제 일본어가 제공되는 SSML(Speech Synthesis Markup Language)를 지원합니다. SSML 지원에 대한 일반 정보는 [SSML 사용](/docs/services/text-to-speech?topic=text-to-speech-ssml)을 참조하십시오. 일본어 SPR 및 IPA 기호에 대한 자세한 정보는 [일본어 기호](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols)를 참조하십시오. 일본어 사용자 정의 음성 모델에서 단어에 대한 항목을 작성할 때 추가 고려사항 및 `part_of_speech` 필드가 적용됩니다. 자세한 정보는 [일본어 항목 관련 작업](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes)을 참조하십시오.
-   서비스는 이제 새 `<voice-transformation>` 요소를 통해 SSML 음성 변환을 제공합니다. 음성의 음역, 음역 범위, 성문 장력, 호흡, 속도 및 음색을 수정하는 사용자 정의 음성 변환을 작성하여 가능한 음성 범위를 확장할 수 있습니다. 서비스는 두 가지 기본 제공 가상 음성인 *Young* 및 *Soft*를 제공합니다. 현재 서비스는 미국 영어의 Allison 음성으로만 음성 변환을 지원합니다. 자세한 정보는 [음성 변환 SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation)을 참조하십시오.
-   서비스는 이제 WebSocket 인터페이스로 전달하는 입력 텍스트의 모든 문자열에 대한 단어 시간 지정 정보를 리턴합니다. 입력에서 모든 문자열의 시작 시간 및 종료 시간을 가져오려면 서비스로 전달하는 JSON 오브젝트의 선택적인 `timings` 매개변수의 `words` 문자열이 포함된 배열을 지정하십시오. 이 기능은 현재 일본어 입력 텍스트에 사용할 수 없습니다. 자세한 정보는 [단어 시간 지정 가져오기](/docs/services/text-to-speech?topic=text-to-speech-timing)를 참조하십시오.
-   서비스는 컨텍스트에서 제출하는 모든 SSML 요소를 유효성 검증합니다. 올바르지 않은 태그가 발견되면 서비스는 설명 메시지가 포함된 HTTP 400 응답 코드를 보고하고 메소드는 실패합니다. 이전 릴리스에서 서비스는 오류를 일관성 없이 처리했습니다. 예를 들어, 올바르지 않은 단어 발음을 지정하면 예기치 않거나 일관성 없는 동작이 발생합니다. 자세한 정보는 [SSML 유효성 검증](/docs/services/text-to-speech?topic=text-to-speech-ssml#errors)을 참조하십시오.
-   `spr`은 `GET /v1/pronunciation` 메소드의 `format` 옵션에 대한 인수로 더 이상 사용되지 않거나 SSML `<phoneme>` 요소의 `alphabet` 속성 사용에 더 이상 사용되지 않습니다. {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation(SPR) 표기법을 사용하려면 모든 경우에 `spr` 대신 `ibm` 요소를 사용하십시오.
-   이제 지원되는 오디오 형식의 목록에는 `audio/mulaw;rate=8000`이 포함됩니다. `audio/basic`과 같이 이 형식은 8kHz로 샘플링되는 8비트 u-law(또는 mu-law) 데이터를 사용하여 인코딩된 단일 채널 오디오를 제공합니다. 자세한 정보는 [오디오 형식](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)을 참조하십시오.
-   `GET /v1/voices` 및 `GET /v1/voices/{voice}` 메소드는 이제 음성마다 출력의 일부로 `supported_features` 오브젝트를 리턴합니다. 오브젝트에서는 음성이 사용자 정의 및 SSML `<voice_transformation>` 요소에 지원하는지 여부에 설명합니다. 자세한 정보는 [언어 및 음성](/docs/services/text-to-speech?topic=text-to-speech-voices)을 참조하십시오.

### 2016년 6월 23일
{: #June2016}

-   서비스는 이제 문자-음성 변환을 합성하기 위해 WebSocket 인터페이스를 제공합니다. 인터페이스는 HTTP 인터페이스의 `/v1/synthesize` 메소드와 동일한 기능을 제공합니다. 일반 텍스트 또는 SSML로 표시되는 텍스트를 허용합니다. 또한 표시 앞에 오는 모든 텍스트의 합성을 완료하는 오디오의 시간을 식별하기 위해 SSML `<mark>` 요소의 사용도 지원합니다. 자세한 정보는 [WebSocket 인터페이스](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket)를 참조하십시오.
-   서비스는 이제 카스티야어 및 북아메리카 스페인어, 이탈리아어, 브라질 포르투갈어가 사용된 SSML로 어노테이션을 작성하는 텍스트에 대한 지원을 제공합니다. 서비스는 이미 미국 및 영국 영어, 프랑스어 및 독일어가 사용된 SSML 사용을 지원했습니다. 이 업데이트부터 서비스는 일본어를 제외한 모든 언어가 사용된 SSML을 지원합니다. 또한 SSML `<phoneme>` 요소로 단어 발음을 정의하는 데 {{site.data.keyword.IBM_notm}} SPR 및 IPA 표기법을 모두 사용할 수 있습니다. 자세한 정보는 [SSML 사용](/docs/services/text-to-speech?topic=text-to-speech-ssml) 및 [IBM SPR 사용](/docs/services/text-to-speech?topic=text-to-speech-sprs)을 참조하십시오.

    미국 영어의 경우 SSML `<phoneme>` 요소를 사용하여 사용자 정의 음성 모델의 단어 항목을 작성할 수 있습니다. 사용자 정의는 미국 영어로만 지원됩니다. 자세한 정보는 [사용자 정의 이해](/docs/services/text-to-speech?topic=text-to-speech-customIntro)를 참조하십시오.
-   서비스 기능으로 자주 사용되는 음성에 대한 표현성 및 자연성이 개선되었습니다. 개선은 입력 텍스트의 RNN(Recursive Neural Network) 기반 운율 예측에 따라 달라집니다. 이는 다음 언어가 사용된 새 서비스 엔진 및 음성 모델 업데이트로 사용할 수 있습니다.

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   `GET /v1/pronunciation` 메소드는 이제 선택적인 `customization_id` 조회 매개변수를 허용합니다. 매개변수는 지정된 사용자 정의 음성 모델에서 단어 변환을 가져옵니다. 음성 모델에 단어가 포함되지 않으면 메소드는 단어의 기본 발음을 리턴합니다. 자세한 정보는 [API 참조](https://{DomainName}/apidocs/text-to-speech){: external}를 확인하십시오.

    사용자 정의 ID를 사용하지 않고 미국 영어 이외의 언어로 `GET /v1/pronunciation` 메소드를 사용하는 경우 {{site.data.keyword.IBM_notm}} SPR 표기법에서 단어의 발음만 요청할 수 있습니다. 미국 영어 이외의 언어의 경우 메소드의 `format` 옵션을 사용하여 `spr`을 지정해야 합니다.
    {: note}
-   지원되는 오디오 형식의 목록에는 이제 8kHz로 샘플링되는 8비트 u-law(또는 mu-law) 데이터를 사용하여 인코딩된 단일 채널 오디오를 사용하는 `audio/basic`이 포함됩니다. 자세한 정보는 [오디오 형식](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)을 참조하십시오.
-   HTTP 및 WebSocket `/v1/synthesize` 메소드는 요청에 포함되는 올바르지 않은 조회 매개변수 또는 JSON 필드에 대한 메시지를 포함한 `warnings` 응답을 리턴할 수 있습니다. 경고의 형식이 변경되었습니다. 다음 예에서는 이전 형식이 표시됩니다.

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    동일한 경고의 형식은 다음과 같습니다.

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

### 2016년 3월 10일
{: #March2016}

-   `GET` 및 `POST /v1/synthesize` 메소드는 이제 요청에 포함되는 올바르지 않은 조회 매개변수 또는 JSON 필드에 대한 경고 메시지의 목록이 포함된 `Warnings` 응답 헤더를 리턴할 수 있습니다. 목록의 각 요소에는 올바르지 않은 인수 문자열의 배열 앞에 오는 경고의 속성에 대해 설명하는 문자열이 포함됩니다. 예를 들면, `Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']`입니다. 자세한 정보는 [API 참조](https://{DomainName}/apidocs/text-to-speech){: external}를 확인하십시오.
-   베타 *Apple&reg; iOS 운영 체제용 {{site.data.keyword.watson}} Speech Software Development Kit(SDK)*은 더 이상 사용되지 않고 *{{site.data.keyword.watson}} Swift SDK*로 대체됩니다. 새 SDK는 GitHub의 `watson-developer-cloud` 네임스페이스에 있는 [swift-sdk 저장소](https://github.com/watson-developer-cloud/swift-sdk){: external}에서 사용할 수 있습니다.

### 2016년 2월 22일
{: #February2016}

서비스는 새 표현 SSML 기능으로 업데이트되었습니다. 서비스는 세 가지 말하기 방식인 `GoodNews`, `Apology` 또는 `Uncertainty` 중 하나를 사용하여 표현성을 표시하는 데 사용할 수 있는 `<express-as>` 요소로 SSML(Speech Synthesis Markup Language)을 확장합니다. 요소를 텍스트, 문장, 구문 또는 단어의 전체 본문에 적용할 수 있습니다. 서비스는 현재 미국 영어의 Allison 음성(`en-US_AllisonVoice`)에만 표현성을 지원합니다. 자세한 정보는 [표현 SSML](/docs/services/text-to-speech?topic=text-to-speech-expressive)을 참조하십시오.

### 2015년 12월 17일
{: #December2015}

-   서비스는 입력에서 발생하는 특이한 단어를 발음하는 방법을 지정하는 데 사용할 수 있는 새 사용자 정의 인터페이스를 제공합니다. 인터페이스에는 새 메소드에 포함되는 사용자 정의 음성 모델 및 단어/변환 쌍을 작성하고 관리하는 데 사용할 수 있는 다수의 새 메소드가 포함되어 있습니다. 그런 다음 텍스트-오디오 변환을 합성할 때 사용자 정의 모델을 사용할 수 있습니다.

    서비스는 유사 발음 변환 및 음성 변환을 지원합니다. 음성 변환은 표준 IPA(International Phonetic Alphabet) 표시 또는 자체 {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation(SPR) 중 하나를 사용할 수 있습니다. SSML(Speech Synthesis Markup Language)을 사용하여 음성 변환을 지정할 수 있습니다.

    사용자 정의 인터페이스에는 `POST /v1/customizations`, `POST /v1/customizations/{customization_id}`, `POST /v1/customizations/{customization_id}/words` 및 `PUT /v1/customizations/{customization_id}/words/{word}` 이름이 있는 새 HTTP 메소드의 콜렉션이 포함됩니다. 서비스는 단어의 발음을 리턴하는 새 `GET /v1/pronunciation` 메소드와 특정 음성에 대한 자세한 정보를 리턴하는 새 `GET /v1/voices/{voice}` 메소드도 제공합니다. 또한 서비스 인터페이스의 기존 메소드는 이제 필요에 따라 사용자 정의 음성 모델 매개변수를 허용합니다.

    사용자 정의 및 해당 인터페이스에 관한 자세한 정보는 [사용자 정의 이해](/docs/services/text-to-speech?topic=text-to-speech-customIntro) 및 [API 참조](https://{DomainName}/apidocs/text-to-speech){: external}를 확인하십시오.

    사용자 정의 인터페이스는 현재 미국 영어만 지원하는 베타 릴리스입니다. 모든 사용자 정의 메소드 및 `GET /v1/pronunciation` 메소드는 현재 미국 영어로만 사용자 정의 음성 모델 및 단어 변환을 작성하고 조작하는 데 사용될 수 있습니다.
    {: note}
-   서비스는 새 음성인 `pt-BR_IsabelaVoice`를 지원하여 여성 음성의 브라질 포르투갈어로 오디오를 합성합니다. 자세한 정보는 [언어 및 음성](/docs/services/text-to-speech?topic=text-to-speech-voices)을 참조하십시오.

### 2015년 9월 21일
{: #September2015}

-   음성 서비스에 두 가지 새 베타 모바일 SDK(Software Development Kits)를 사용할 수 있습니다. SDK는 모바일 애플리케이션을 사용하여 {{site.data.keyword.texttospeechshort}} 및 {{site.data.keyword.speechtotextshort}} 서비스와 상호작용합니다. SDK를 사용하여 텍스트를 {{site.data.keyword.texttospeechshort}} 서비스로 전송하고 오디오 응답을 수신할 수 있습니다.
    -   *{{site.data.keyword.watson}} Swift SDK*는 GitHub의 `watson-developer-cloud` 네임스페이스에 있는 [swift-sdk 저장소](https://github.com/watson-developer-cloud/swift-sdk){: external}에서 사용할 수 있습니다.
    -   *{{site.data.keyword.watson}} Speech Android SDK*는 GitHub의 `watson-developer-cloud` 네임스페이스에 있는 [speech-android-sdk 저장소](https://github.com/watson-developer-cloud/speech-android-sdk){: external}에서 사용할 수 있습니다.

    두 SDK는 {{site.data.keyword.cloud_notm}} 서비스 인증 정보 또는 인증 토큰 중 하나를 사용하여 음성 서비스로의 인증을 지원합니다.

    SDK는 베타 기능이므로 이후에 변경될 수 있습니다.
    {: note}
-   서비스는 새 언어인 일본어를 지원합니다. `ja-JP_EmiVoice` 음성은 일본인 여성의 음성입니다.

### 2015년 7월 1일
{: #July2015}

서비스는 2015년 7월 1일에 베타에서 GA(General Availability) 상태로 변경되었습니다. {{site.data.keyword.texttospeechshort}} API의 베타 및 GA 버전에 대한 차이점은 다음과 같습니다. GA 릴리스에서는 사용자가 서비스의 새 버전으로 업그레이드해야 합니다.

-   새 프로그래밍 모델은 클라이언트와 서비스 간의 직접적인 상호작용을 지원합니다. 이 모델을 사용하여 클라이언트는 서비스와 직접 통신하기 위해 인증 토큰을 가져올 수 있습니다. 토큰을 사용하여 클라이언트는 서비스를 대신 호출하기 위해 {{site.data.keyword.cloud_notm}}에서 서버 측 프록시 애플리케이션을 필요로 하지 않을 수 있습니다. 토큰은 클라이언트가 서비스와 상호작용하는 선호 수단입니다.

    서비스는 클라이언트와 서비스 간의 통신 및 데이터를 전달하기 위해 서버 측 프록시를 필요로 하는 이전 프로그래밍 모델을 계속해서 지원합니다. 그러나 새 모델은 더욱 효율적이며 더 높은 처리량을 제공합니다.
-   이제 SSML(Speech Synthesis Markup Language)을 `/v1/synthesize` 메소드의 HTTP `GET` 및 `POST` 버전으로 전달할 수 있습니다. SSML은 {{site.data.keyword.texttospeechshort}} 서비스와 같은 음성 합성 애플리케이션을 위해 텍스트의 어노테이션을 제공하도록 설계된 XML 기반 마크업 언어입니다. SSML 입력을 서비스에 전달하는 데 대한 자세한 정보는 [입력 텍스트 지정](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#input)을 참조하십시오.

    서비스는 초기에 미국 영어 및 영국 영어, 프랑스어, 독일어로만 SSML 사용을 지원합니다. 서비스는 이탈리아어 및 스페인어에 사용할 SSML은 지원하지 않습니다. SSML을 사용하는 경우 지원되는 언어 중 하나로 오디오를 위한 음성을 선택해야 합니다. 이 경우의 결과는 중요하지 않습니다.
-   합성된 음성(speech)에 지원되는 음성(voice)은 변경되고 확장되었습니다. 서비스는 이제 `/v1/synthesize` 메소드를 사용하여 다수의 추가 음성, 언어 및 통용어를 지원합니다. 지원되는 음성에 대한 자세한 정보는 [언어 및 음성](/docs/services/text-to-speech?topic=text-to-speech-voices)을 참조하십시오.

    베타에서 사용할 수 있는 세 가지 음성이 GA에서는 이름이 변경됩니다.
    -   `VoiceEnUsMichael`은 이제 `en-US_MichaelVoice`입니다.
    -   `VoiceEnUsLisa`는 이제 `en-US_LisaVoice`입니다.
    -   `VoiceEsEsEnrique`는 이제 `es-ES_EnriqueVoice`입니다.

    음성의 이전 이름은 버전이 사용 가능한 상태로 유지되는 동안 계속해서 서비스의 베타 버전에서 사용됩니다(`-beta` API 엔드포인트를 통해). 그러나 서비스의 GA 버전에서는 새 이름을 사용해야 합니다.
-   이제 FLAC(Free Lossless Audio Codec) 형식으로 오디오를 리턴하도록 서비스를 요청할 수 있습니다. 서비스는 파형 오디오 파일 형식(WAV)에서 Opus 코덱(기본값)이 포함된 Ogg 형식으로 오디오를 계속해서 리턴할 수 있습니다. `/v1/synthesize` 메소드를 사용하여 오디오 형식 사용에 대한 자세한 정보는 [오디오 형식](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)을 참조하십시오.
-   HTTP `GET` 요청의 URL 또는 HTTP `POST` 요청의 본문에서 `/v1/synthesize` 메소드로 전송하는 텍스트는 이제 최대 5KB로 제한됩니다. 베타 버전에서 최대 텍스트 크기는 4MB입니다.
-   `/v1/synthesize` 메소드에는 이제 `X-WDC-PL-OPT-OUT` 헤더가 포함되어 서비스가 향후 결과를 개선하기 위해 조작에서 텍스트 및 오디오 결과를 사용하는지 여부를 제어합니다. 서비스에서 텍스트 및 오디오 결과를 사용할 수 없도록 헤더에 대해 `1` 값을 지정하십시오. 매개변수는 현재 요청에만 적용됩니다. 새 헤더는 베타 메소드의 `X-logging` 헤더를 대체합니다. 자세한 정보는 [{{site.data.keyword.watson}} 서비스에 대한 요청 로깅 제어](/docs/services/watson?topic=watson-gs-logging-overview)를 참조하십시오.
-   `/v1/synthesize` 메소드의 경우 다음 오류 코드가 변경되었습니다.
    -   오류 코드 406("허용할 수 없음. 지원되지 않는 MIME 유형.")이 제거되었습니다.
    -   오류 코드 415("지원되지 않는 매체 유형")이 추가되었습니다.
    -   오류 코드 503("서비스 사용 불가능")이 추가되었습니다.
-   `GET /v1/voices` 메소드의 경우 다음 오류 코드가 변경되었습니다.
    -   오류 코드 406("허용할 수 없음. 지원되지 않는 MIME 유형.")이 제거되었습니다.
    -   오류 코드 415("지원되지 않는 매체 유형")이 추가되었습니다.
