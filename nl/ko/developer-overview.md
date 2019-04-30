---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-05"

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

# 개발자를 위한 개요
{: #overview}

HTTP REST(Representational State Transfer) API 또는 WebSocket 인터페이스를 통해 {{site.data.keyword.texttospeechfull}} 서비스의 음성 합성 기능에 액세스할 수 있습니다. 다양한 프로그래밍 언어로 애플리케이션 개발을 단순화하는 데 여러 SDK(Software Development Kits)도 사용할 수 있습니다. 다음 절에서는 서비스를 사용한 애플리케이션 개발의 개요를 제공합니다.
{: shortdesc}

## HTTP 인터페이스
{: #http}

HTTP API로 텍스트를 합성하기 위해 `GET` 또는 `POST` 버전으로 서비스의 `/v1/synthesize` 메소드를 호출합니다. 메소드의 두 가지 버전은 일반적으로 동등한 기능을 제공합니다. 

-   *입력 텍스트:* 두 가지 방법으로 합성될 입력 텍스트를 전달합니다. 
    -   `GET /v1/synthesize` 메소드는 조회 매개변수로 입력 텍스트를 허용합니다. 최대 요청 크기는 8KB이며 입력 텍스트, URL 및 헤더가 포함됩니다. 
    -   `POST /v1/synthesize` 메소드는 요청의 본문에서 입력 텍스트를 허용합니다. 최대 요청 크기는 8KB(URL 및 헤더용) 및 5KB(요청의 본문에 전송된 입력 텍스트용)입니다. 

    서비스 일반 텍스트 또는 SSML(Speech Synthesis Markup Language)로 어노테이션을 작성하는 텍스트를 전달할 수 있습니다. SSML은 {{site.data.keyword.texttospeechshort}} 서비스와 같은 음성 합성 애플리케이션을 위해 텍스트의 어노테이션을 제공하는 XML 기반 마크업 언어입니다. 서비스는 서비스별 표현 및 음성 변환 요소로 SSML의 기능을 보강합니다. 

    자세한 정보는 [입력 텍스트 지정](/docs/services/text-to-speech/http.html#input)을 참조하십시오.
-   *음성:* 서비스는 텍스트를 허용하고 다양한 언어, 음성 및 통용어로 오디오를 생성합니다. 서비스는 지원되는 언어와 다른 통용어(예: 미국 및 영국 영어)마다 하나 이상의 남성 또는 여성 음성(때로는 둘 다)을 제공합니다. 문자-음성 변환을 합성하는 데 DNN(Deep Neural Network) 기술을 사용하는 몇 가지 음성의 버전을 제공합니다. 

    서비스의 `GET /v1/voices` 또는 `GET /v1/voices/{voice}` 메소드를 사용하여 지원되는 음성에 대해 지세히 알아볼 수 있습니다. 서비스는 텍스트를 지정된 음성의 언어로 합성합니다. 음성을 입력 텍스트와 일치시켜야 합니다. 

    자세한 정보는 [언어 및 음성](/docs/services/text-to-speech/voices.html)을 참조하십시오.
-   *오디오 형식:* 서비스는 Opus(기본값) 또는 Vorbis 코덱이 포함된 Ogg 또는 WebM(Web Media) 형식, MP3(Motion Picture Experts Group 또는 MPEG) 형식, 파형 오디오 파일 형식(WAV), FLAC(Free Lossless Audio Codec), 선형 16비트 PCM(Pulse-Code Modulation), 8비트 mu-law(u-law) 또는 기본 오디오의 형식으로 오디오를 생성할 수 있습니다. 

    자세한 정보는 [오디오 형식](/docs/services/text-to-speech/audio-formats.html)을 참조하십시오.

## WebSocket 인터페이스
{: #websocket}

서비스는 텍스트를 합성하는 데 사용할 수 있는 WebSocket 인터페이스를 제공합니다. 인터페이스는 최대 5KB의 입력 텍스트를 허용하는 단일 버전의 `/v1/synthesize` 메소드를 제공합니다. 합성될 텍스트, 사용될 음성 및 오디오의 형식을 지정합니다. 일반 텍스트 또는 SSML로 어노테이션을 작성하는 텍스트를 제공할 수 있습니다. 자세한 정보는 [WebSocket 인터페이스](/docs/services/text-to-speech/websockets.html)를 참조하십시오.

WebSocket 인터페이스는 오디오의 특정 위치를 식별하도록 SSML `<mark>` 요소의 사용을 지원합니다. 입력 텍스트의 모든 단어에 대한 단어 시간 지정 정보도 요청할 수 있습니다. 자세한 정보는 [단어 시간 지정 가져오기](/docs/services/text-to-speech/word-timing.html)를 참조하십시오.

## 사용자 정의 인터페이스
{: #customization}

서비스에는 음성 합성 중에 사용할 사용자 정의 음성 모델을 작성하는 데 사용할 수 있는 사용자 정의 인터페이스가 포함됩니다. 사용자 정의 음성 모델은 특정 언어를 위한 단어 및 변환의 사전을 제공합니다. 각 단어/변환 쌍은 단어가 입력 텍스트에 표시될 때 발음하는 방법을 서비스에게 알려줍니다. 

사용자 정의 음성 모델을 사용하여 서비스의 일반 발음 규칙으로 불완전한 발음이 생성될 수 있는 특이한 단어에 대한 애플리케이션별 변환을 작성할 수 있습니다. 표준 IPA(International Phonetic Alphabet) 표시 또는 자체 {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation(SPR)에서 단어/변환 쌍에 대한 사용자 정의 항목을 정의할 수 있습니다. 

예를 들어, 애플리케이션에는 정기적으로 외국어의 어원, 개인 또는 지리 이름 및 약어 또는 두문자어를 비롯한 특수 용어가 표시될 수 있습니다. 사용자 정의를 사용하여 이러한 용어를 발음하는 방식을 서비스에 알려주는 변환을 정의할 수 있습니다. 자세한 정보는 [사용자 정의 이해](/docs/services/text-to-speech/custom-intro.html)를 참조하십시오.

사용자 정의 인터페이스는 베타 릴리스입니다.
{: note}

## CORS 지원
{: #cors}

서비스는 CORS(Cross-Origin Resource Sharing)를 지원합니다. CORS를 사용하여 웹 페이지는 외부 도메인에서 직접 리소스를 요청할 수 있습니다. CORS는 이러한 요청이 발생하지 못하도록 하는 동일한 근원의 보안 정책을 우회합니다. 서비스가 CORS를 지원하기 때문에 웹 페이지는 페이지를 호스팅하는 웹 서버를 통해 요청을 전달하지 않고 서비스와 직접 통신할 수 있습니다. 

예를 들어, {{site.data.keyword.cloud}}의 서버에서 로드되는 웹 페이지가 {{site.data.keyword.cloud_notm}} 서버를 우회하여 사용자 정의 API를 직접 호출할 수 있습니다. 자세한 정보는 [enable-cors.org ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://enable-cors.org/){: new_window}를 참조하십시오.

## Software Development Kits 사용
{: #sdks}

{{site.data.keyword.texttospeechshort}} 서비스에서 음성 애플리케이션 개발을 단순화하는 데 SDK를 사용할 수 있습니다. 다수의 인기 있는 프로그래밍 언어 및 플랫폼에서 {{site.data.keyword.ibmwatson}} SDK를 사용할 수 있습니다. 

-   GitHub에서 SDK의 전체 목록 및 링크를 사용하는 데 대한 정보는 [SDK 사용](/docs/services/watson/getting-started-sdks.html)을 참조하십시오.
-   {{site.data.keyword.texttospeechshort}} 서비스에 적합한 Node, Java, Python, Ruby 및 Go SDK의 모든 메소드에 대한 자세한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/text-to-speech){: new_window}를 참조하십시오.

## 애플리케이션 개발에 대해 자세히 알아보기
{: #learn}

{{site.data.keyword.watson}} 서비스 및 {{site.data.keyword.cloud_notm}} 관련 작업에 대한 자세한 정보는 다음 항목을 참조하십시오.

-   {{site.data.keyword.watson}} 서비스 및 {{site.data.keyword.cloud_notm}} 관련 작업에 대한 소개는 [{{site.data.keyword.watson}} 및 {{site.data.keyword.cloud_notm}} 시작하기](/docs/services/watson/index.html)를 참조하십시오.
-   모든 새 서비스 인스턴스는 인증을 위해 {{site.data.keyword.cloud_notm}} Identity and Access Management(IAM)를 사용합니다. 이전 서비스 인스턴스는 인증을 위해 기존 Cloud Foundry 서비스 인증 정보에서 `{username}` 및 `{password}`를 계속 사용할 수 있습니다. 서비스 인증에 대한 자세한 정보는 릴리스 정보의 [2018년 10월 30일 서비스 업데이트](/docs/services/text-to-speech/release-notes.html#October2018)를 참조하십시오.
-   모든 {{site.data.keyword.watson}} 서비스에 대해 수행되는 기본 요청 로깅의 제어에 대한 자세한 정보는 [{{site.data.keyword.watson}} 서비스에 대한 요청 로깅 제어](/docs/services/watson/getting-started-logging.html)를 참조하십시오.
