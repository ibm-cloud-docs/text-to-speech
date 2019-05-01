---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-14"

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# 튜토리얼 시작하기
{: #gettingStarted}

{{site.data.keyword.texttospeechfull}} 서비스는 작성된 텍스트를 자연어 음성으로 변환하여 애플리케이션에 필요한 음성 합성 기능을 제공합니다. 이 curl 기반 튜토리얼은 서비스를 빠르게 시작하는 데 도움을 줍니다. 예에서는 오디오 스트림을 요청하기 위해 서비스의 `POST` 및 `GET /v1/synthesize` 메소드를 호출하는 방법을 보여줍니다.
{: shortdesc}

튜토리얼에서는 인증을 위해 {{site.data.keyword.cloud}} Identity and Access Management(IAM) API 키를 사용합니다. 이전 서비스 인스턴스는 인증을 위해 기존 Cloud Foundry 서비스 인증 정보에서 `{username}` 및 `{password}`를 계속 사용할 수 있습니다. 서비스 인스턴스에 적합한 방식을 사용하여 인증하십시오. 서비스의 IAM 인증 사용에 대한 자세한 정보는 릴리스 정보의 [2018년 10월 30일 서비스 업데이트](/docs/services/text-to-speech/release-notes.html#October2018)를 참조하십시오.
{: important}

## 시작하기 전에
{: #before-you-begin}

- {: hide-dashboard}  다음과 같이 서비스의 인스턴스를 작성하십시오. 
    1.  {: hide-dashboard} {{site.data.keyword.cloud_notm}} 카탈로그에서 [{{site.data.keyword.texttospeechshort}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/text-to-speech){: new_window} 페이지로 이동하십시오. 
    1.  {: hide-dashboard} 무료 {{site.data.keyword.cloud_notm}} 계정에 가입하거나 로그인하십시오. 
    1.  {: hide-dashboard} **작성**을 클릭하십시오.
-   인증할 인증 정보를 서비스 인스턴스에 복사하십시오. 
    1.  {: hide-dashboard} [{{site.data.keyword.cloud_notm}} 대시보드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/dashboard/apps){: new_window}에서 {{site.data.keyword.texttospeechshort}} 서비스 대시보드를 클릭하여 {{site.data.keyword.texttospeechshort}} 서비스 대시보드 페이지로 이동하십시오. 
    1.  **관리** 페이지에서 **표시**를 클릭하여 인증 정보를 보십시오. 
    1.  `API Key` 및 `URL` 값을 복사하십시오. 
-   `curl` 명령이 있는지 확인하십시오. 
    -   예에서는 `curl` 명령을 사용하여 HTTP 인터페이스의 메소드를 호출합니다. [curl.haxx.se ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://curl.haxx.se/){: new_window}에서 운영 체제의 버전을 설치하십시오. SSL(Secure Sockets Layer) 프로토콜을 지원하는 버전을 설치하십시오. `PATH` 환경 변수에 설치된 바이너리 파일이 포함되어 있는지 확인하십시오. 

명령 입력 시 `{apikey}` 및 `{url}`을 실제 API 키 및 URL로 대체하십시오. 명령에서 변수 값을 표시하는 중괄호를 생략하십시오. 실제 값은 다음 예와 유사합니다.
{: hide-dashboard}

```bash
curl -X POST -u "apikey:L_HALhLVIksh1b73l97LSs6R_3gLo4xkujAaxm7i-b9x"
. . .
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```
{:pre}
{: hide-dashboard}

브라우저 또는 기타 도구를 사용하여 이 튜토리얼의 예를 통해 생성된 오디오 파일을 재생할 수 있습니다. 자세한 정보는 [오디오 파일 재생](/docs/services/text-to-speech/audio-formats.html#formatsPlay)을 참조하십시오.
{: note}

## 1단계: 미국 영어로 된 텍스트 합성
{: #synthesizeEnglish}

다음 명령에서는 `POST /v1/synthesize` 메소드를 사용하여 두 가지 다른 형식으로 미국 영어 입력을 오디오 파일로 합성합니다. 두 요청에서는 기본적으로 미국 영어 음성(`en-US_MichaelVoice`)을 사용합니다.

1.  다음 명령을 실행하여 문자열 "hello world"를 합성하고 `hello_world.wav`라는 이름으로 WAV 파일을 생성하십시오. 
    -   {: hide-dashboard} `{apikey}` 및 `{url}`을 API 키 및 URL로 대체하십시오. 

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

1.  다음 명령을 실행하여 동일한 텍스트를 합성하지만 `hello_world.ogg`라는 Ogg 파일(기본 형식)을 생성하십시오. 
    -   {: hide-dashboard} `{apikey}` 및 `{url}`을 API 키 및 URL로 대체하십시오. 

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

## 2단계: 스페인어로 된 텍스트 합성
{: #synthesizeSpanish}

다음 명령에서는 `GET /v1/synthesize` 메소드를 사용하여 스페인어 입력을 오디오 파일로 합성합니다. 

1.  다음 명령을 실행하여 문자열 "hola mundo"를 합성하고 `hola_mundo.wav`라는 이름으로 WAV 파일을 생성하십시오. 입력 텍스트는 URL 인코딩입니다. 메소드는 조회 매개변수 `accept`를 포함하여 오디오 형식을 지정하고 `voice`를 포함하여 스페인어 음성(`es-ES_EnriqueVoice`)을 지정합니다. 
    -   {: hide-dashboard} `{apikey}` 및 `{url}`을 API 키 및 URL로 대체하십시오. 

    ```bash
    curl -X GET -u "apikey:{apikey}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## 다음 단계

-   [HTTP 인터페이스](/docs/services/text-to-speech/http.html)에서 서비스의 HTTP 인터페이스에 대해 알아보십시오. 
-   [WebSocket 인터페이스](/docs/services/text-to-speech/websockets.html)에서 서비스의 WebSocket 인터페이스에 대해 알아보십시오.
-   [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/text-to-speech){: new_window}에서 서비스 인터페이스의 메소드에 대해 자세히 알아보십시오. 
