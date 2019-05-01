---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-21"

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

# HTTP 인터페이스
{: #usingHTTP}

{{site.data.keyword.texttospeechfull}} 서비스의 HTTP REST 인터페이스를 사용하여 문자-음성 변환을 합성하기 위해 `GET` 또는 `POST /v1/synthesize` 메소드를 호출합니다. 합성될 텍스트와 음성화된 오디오의 음성 및 형식을 지정합니다. 요청에 사용될 사용자 정의 음성 모델을 지정할 수도 있습니다.
{: shortdesc}

HTTP 인터페이스에 대한 자세한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/text-to-speech){: new_window}를 참조하십시오.

## 텍스트-오디오 변환 합성
{: #synthesize}

텍스트-오디오 변환을 합성하려면 서비스의 `/v1/synthesize` 메소드의 두 가지 버전 중 하나를 호출합니다. 

-   `GET /v1/synthesize` 메소드는 필수 `text` 조회 매개변수로 합성될 텍스트를 허용합니다. 최대 요청 크기는 8KB이며 입력 텍스트(지정하는 임의의 SSML)와 URL 및 헤더가 포함됩니다. 
-   `POST /v1/synthesize` 메소드는 필수 요청 본문에서 JSON 구성으로 합성될 텍스트를 허용합니다. 최대 요청 크기는 8KB(URL 및 헤더용) 및 5KB(요청의 본문에 전송된 입력 텍스트용)입니다. 5KB 제한에는 지정하는 SSML이 포함됩니다. 

`/v1/synthesize` 메소드의 두 가지 버전에는 다음 매개변수가 공통적으로 포함됩니다. 

<table>
  <caption>표 1. <code>/v1/synthesize</code> 메소드의
    매개변수</caption>
  <tr>
    <th style="text-align:left; width:18%">매개변수</th>
    <th style="text-align:center; width:12%">유형</th>
    <th style="text-align:center; width:12%">데이터 유형</th>
    <th style="text-align:left">설명</th>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>선택사항</em></td>
    <td style="text-align:center">조회</td>
    <td style="text-align:center">문자열</td>
    <td>
      서비스가 오디오를 리턴하는 요청된 오디오 형식 또는 MIME 유형을
      지정합니다. HTTP <code>Accept</code> 요청 헤더로 이 값을
      지정할 수도 있습니다. `accept` 조회 매개변수에 대한 인수를
      URL로 인코딩합니다. 자세한 정보는
      [오디오 형식](/docs/services/text-to-speech/audio-formats.html)을 참조하십시오.
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>선택사항</em></td>
    <td style="text-align:center">조회</td>
    <td style="text-align:center">문자열</td>
    <td>
      텍스트가 오디오에서 음성화될 음성을
      지정합니다. <code>/v1/voices</code> 메소드를 사용하여 지원되는
      음성의 현재 목록을 가져오십시오. 기본 음성은
      <code>en-US_MichaelVoice</code>입니다. 자세한 정보는
      [언어 및 음성](/docs/services/text-to-speech/voices.html)을 참조하십시오.
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>선택사항</em></td>
    <td style="text-align:center">조회</td>
    <td style="text-align:center">문자열</td>
    <td>
      합성에 사용될 사용자 정의 음성 모델에 대한 GUID(Globally Unique
      Identifier)를 지정합니다. 지정된 사용자 정의 음성 모델은 합성에 사용될 음성의
      언어와 일치하는 경우에만 작동되도록 보장됩니다. 사용자 정의 ID를 포함하는 경우
      모델의 소유자에 대한 서비스 인증 정보를 사용하여 메소드를 호출해야
      합니다. 사용자 정의가 없는 지정된 음성을 사용하려면 매개변수를
      생략하십시오. 자세한 정보는
      [사용자 정의 이해](/docs/services/text-to-speech/custom-intro.html)를 참조하십시오.
    </td>
  </tr>
</table>

합성 요청에 따라 모든 {{site.data.keyword.watson}} 서비스에 사용 가능한 다음 요청 헤더도 사용할 수 있습니다. 

-   `X-Watson-Learning-Opt-Out`은 서비스가 향후 사용자를 위해 서비스를 개선하도록 요청 및 응답 데이터를 로깅하는지 여부를 표시합니다. IBM이 일반 서비스 개선을 위해 데이터에 액세스하지 못하도록 하려면 매개변수에 <code>true</code>를 지정하십시오. 자세한 정보는 [{{site.data.keyword.watson}} 서비스에 대한 요청 로깅 제어](/docs/services/watson/getting-started-logging.html)를 참조하십시오.
-   `X-Watson-Metadata`는 고객 ID를 요청으로 전달된 데이터와 연관시킵니다. 자세한 정보는 [정보 보안](/docs/services/text-to-speech/information-security.html)을 참조하십시오.

`/v1/synthesize` 메소드에 대한 입력의 일부로 올바르지 않은 조회 매개변수 또는 JSON 필드를 지정하는 경우 서비스는 올바르지 않은 각 인수를 설명하고 나열하는 `Warnings` 응답 헤더를 리턴합니다. 경고가 발생하지만 요청이 성공합니다.
{: note}

## 입력 텍스트 지정
{: #input}

`GET` 및 `POST /v1/synthesize` 메소드는 일반 입력 텍스트 또는 SSML로 어노테이션을 작성하는 텍스트를 허용합니다. 두 가지 버전은 주로 합성될 텍스트를 지정하는 방법에 따라 달라집니다. 

-   `GET /v1/synthesize` 메소드는 `text` 조회 매개변수로 지정되는 입력 텍스트를 허용합니다. 일반 텍스트 또는 SSML로 입력을 지정하며, 둘 모두 URL 인코딩이어야 합니다. 
-   `POST /v1/synthesize` 메소드는 요청의 본문에서 입력 텍스트를 허용합니다. 일반 텍스트 또는 SSML을 캡슐화하는 다음과 같은 단순 JSON 구조를 사용하여 입력을 지정합니다. `Content-Type` 헤더에 `application/json` 값도 지정해야 합니다. 

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

`GET` 및 `POST` 메소드가 동등한 기능을 제공하지만 항상 `POST` 메소드를 사용하여 입력 텍스트를 서비스에 전달하는 것이 더욱 안전합니다. `POST` 요청은 요청의 본문에서 입력을 전달하고, `GET` 요청은 URL에서 데이터를 노출합니다. 

## SSML 입력 지정
{: #ssml-http}

SSML(Speech Synthesis Markup Language)은 {{site.data.keyword.texttospeechshort}} 서비스와 같은 음성 합성 애플리케이션을 위해 텍스트의 어노테이션을 제공하도록 설계된 XML 기반 마크업 언어입니다. SSML 요소 및 속성을 사용하여 합성과 생성되는 오디오 출력을 더욱 강력하게 제어할 수 있습니다. 

입력 텍스트의 어노테이션을 작성하기 위해 SSML을 사용하는 데 대한 자세한 정보는 [SSML 사용](/docs/services/text-to-speech/SSML.html)을 참조하십시오. 문서에는 서비스에서 지원되는 SSML 요소 및 속성이 나열되어 있습니다. 또한 서비스의 표현 및 음성 변환 확장기능도 문서화합니다. 

## XML 제어 문자 이스케이프
{: #escape}

XML 기반 SSML 어노테이션이 포함된 입력 텍스트를 제출할 수 있으므로 SSML이 올바르며 제대로 구성되어 있는지 확인하기 위해 서비스는 모든 입력을 유효성 검증합니다. 그러므로 입력에 SSML이 포함되는지 여부에 관계 없이 입력 텍스트에 표시되는 모든 XML 제어 문서를 이스케이프해야 합니다. 표시되는 문자 대신 표 2의 동등한 이스케이프 문자열 또는 문자 인코딩을 사용하십시오. 

<table style="width:80%">
  <caption>표 2. XML 제어 문자 이스케이프</caption>
  <tr>
    <th style="text-align:center; vertical-align:bottom; width:40%">문자</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">이스케이프 문자열</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">문자 인코딩</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>&quot;</code><br/>(큰따옴표)</td>
    <td style="text-align:center"><code>&amp;quot;</code></td>
    <td style="text-align:center"><code>&amp;#34;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>'</code><br/>(어퍼스트로피 또는 작은따옴표)</td>
    <td style="text-align:center"><code>&amp;apos;</code></td>
    <td style="text-align:center"><code>&amp;#39;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&amp;</code><br/>(앰퍼샌드)</td>
    <td style="text-align:center"><code>&amp;amp;</code></td>
    <td style="text-align:center"><code>&amp;#38;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&lt;</code><br/>(왼쪽 꺾쇠괄호)</td>
    <td style="text-align:center"><code>&amp;lt;</code></td>
    <td style="text-align:center"><code>&amp;#60;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&gt;</code><br/>(오른쪽 꺾쇠괄호)</td>
    <td style="text-align:center"><code>&amp;gt;</code></td>
    <td style="text-align:center"><code>&amp;#62;</code></td>
  </tr>
</table>

서비스가 입력 텍스트를 유효성 검증하는 방법에 대한 자세한 정보는 [SSML 유효성 검증](/docs/services/text-to-speech/SSML.html#errors)을 참조하십시오.

## 입력 텍스트 예
{: #httpExamples}

다음 예에서는 HTTP 인터페이스의 두 메소드를 사용하여 입력 텍스트를 지정하는 방법을 보여줍니다. XML 제어 문자를 이스케이프하는 방법도 보여줍니다. 예에는 가독성을 위한 행 바꾸기가 포함됩니다. 실제 입력에는 행 바꾸기를 포함하지 *마십시오*. 

### GET 요청이 포함된 입력 예
{: #getExamples}

다음 예에서는 `GET /v1/synthesize` 메소드의 `text` 조회 매개변수를 사용하여 URL 인코딩 입력을 전달합니다. 

-   일반 텍스트 입력:

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   SSML 입력:

    ```
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3C
    break%20time=%225s%22/%3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another
    %20sentence.%3C/s%3E%3Cs%3EFinally,%20this%20is%20the%20last%20sentence.
    %3C/s%3E%3C/p%3E%22
    ```
    {: codeblock}

### POST 요청이 포함된 입력 예
{: #postExamples}

다음 예에서는 `POST /v1/synthesize` 메소드의 본문에서 입력을 전달합니다. 

-   일반 텍스트 입력:

    ```javascript
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   SSML 입력:

    ```javascript
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/>
        paragraph.</s><s>Here is another sentence.</s><s>Finally, this is
        the last sentence.</s></p>"
    }
    ```
    {: codeblock}

### XML 제어 문자가 포함된 입력 예
{: #xmlExamples}

다음 예는 두 가지 문장을 `POST /v1/synthesize` 메소드에 전송합니다. 예에서는 임베디드 XML 문자를 올바르게 이스케이프합니다. 

```
"What have I learned?" he asked. "Everything!"
```
{: codeblock}

-   일반 텍스트 입력:

    ```javascript
    {
      "text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
    }
    ```
    {: codeblock}

-   SSML 입력:

    ```javascript
    {
      "text": "<s>&quot;What have I learned?&quot; he asked.
        &quot;<express-as type=\"GoodNews\">Everything!</express-as>&quot;</s>"
    }
    ```
    {: codeblock}
