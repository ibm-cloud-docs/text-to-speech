---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-09"

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

# WebSocket 인터페이스
{: #usingWebSocket}

{{site.data.keyword.texttospeechfull}} 서비스의 WebSocket 인터페이스로 문자-음성 변환을 합성하려면 먼저 `/v1/synthesize` 메소드를 호출하여 서비스와의 연결을 설정해야 합니다. 그런 다음 연결을 통해 JSON 텍스트 메시지로서 합성할 텍스트를 서비스로 전송해야 합니다. 서비스가 요청 처리를 완료하면 자동으로 WebSocket 연결을 닫습니다.
{: shortdesc}

합성 요청 및 응답 주기에는 다음 단계가 포함되어 있습니다. 

1.  [연결을 여십시오](#WSopen).
1.  [입력 텍스트를 전송하십시오](#WSsend).
1.  [응답을 수신하십시오](#WSreceive).

WebSocket 인터페이스는 HTTP 인터페이스의 `GET` 및 `POST /v1/synthesize` 메소드와 동일한 입력을 허용하고 이 메소드와 동일한 결과를 생성합니다. 그러나 WebSocket 인터페이스는 오디오에서 사용자 지정 마커의 위치를 식별하도록 SSML `<mark>` 요소의 사용을 지원합니다. 또한 입력 텍스트의 모든 문자열에 대한 시간 지정 정보도 리턴할 수 있습니다. 자세한 정보는 [단어 시간 지정 가져오기](/docs/services/text-to-speech/word-timing.html)를 참조하십시오.

다음에 나오는 코드 예의 스니펫은 JavaScript에서 작성되고 HTML5 WebSocket API를 기반으로 합니다. WebSocket 프로토콜에 대한 자세한 정보는 IETF(Internet Engineering Task Force) [RFC(Request for Comment) 6455 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://tools.ietf.org/html/rfc6455){: new_window}를 참조하십시오.
{: note}

## 연결 열기
{: #WSopen}

WSS(WebSocket Secure) 프로토콜을 통해 `/v1/synthesize` 메소드를 호출하여 서비스에 대한 연결을 엽니다. 메소드는 다음 엔드포인트에서 사용 가능합니다. 

```
wss://{host_name}/text-to-speech/api/v1/synthesize
```
{: codeblock}

여기서 `{host_name}`은 애플리케이션이 호스트되는 위치입니다. 

-   달라스: `stream.watsonplatform.net`(다음 예에서는 이 호스트 이름을 사용함)
-   프랑크푸르트: `stream-fra.watsonplatform.net`
-   시드니: `gateway-syd.watsonplatform.net`
-   워싱턴, DC: `gateway-wdc.watsonplatform.net`
-   도쿄: `gateway-tok.watsonplatform.net`
-   런던: `gateway-lon.watsonplatform.net`

WebSocket 클라이언트는 서비스와의 인증된 연결을 설정하기 위해 다음 조회 매개변수로 이 메소드를 호출합니다. IAM(Identity and Access Management) 인증을 사용하는 경우 `access_token` 조회 매개변수를 사용하십시오. Cloud Foundry 서비스 인증 정보를 사용하는 경우 `watson-token` 조회 매개변수를 사용하십시오. 

<table>
  <caption>표 1. <code>/v1/synthesize</code> 메소드의
    매개변수</caption>
  <tr>
    <th style="text-align:left; width:23%">매개변수</th>
    <th style="text-align:center; width:12%">데이터 유형</th>
    <th style="text-align:left">설명</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>access_token</code>
      <br/><em>선택사항</em></td>
    <td style="text-align:center">문자열</td>
    <td style="text-align:left">
      <em>IAM 인증을 사용하는 경우</em> 서비스로 인증하도록 유효한
      IAM 액세스 토큰을 전달하십시오. 호출로 API 키를 전달하는 대신
      IAM 액세스 토큰을 전달합니다. 액세스 토큰이 만료되기 전에
      사용해야 합니다. 액세스 토큰 가져오기에 대한 자세한 정보는
      [IAM 토큰으로 인증](/docs/services/watson/getting-started-iam.html)을
      참조하십시오.
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>watson-token</code>
      <br/><em>선택사항</em></td>
    <td style="text-align:center">문자열</td>
    <td style="text-align:left">
      <em>Cloud Foundry 서비스 인증 정보를 사용하는 경우</em> 서비스로
      인증하도록 유효한 {{site.data.keyword.watson}} 인증 토큰을
      전달합니다. 호출로 서비스 인증 정보를 전달하는 대신
      {{site.data.keyword.watson}} 토큰을 전달합니다.
      {{site.data.keyword.watson}} 토큰은 Cloud Foundry 서비스 인증 정보를
      기반으로 하며, HTTP 기본 인증을 위해 `username` 및 `password`를
      사용합니다. {{site.data.keyword.watson}} 토큰
      가져오기에 대한 자세한 정보는
      [{{site.data.keyword.watson}} 토큰](/docs/services/watson/getting-started-tokens.html)을 참조하십시오.
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>선택사항</em></td>
    <td style="text-align:center">문자열</td>
    <td>
      텍스트가 오디오에서 음성화될 음성을
      지정합니다. 기본 음성인 `en-US_MichaelVoice`를 사용하려면 매개변수를 생략하십시오.
      자세한 정보는
      [언어 및 음성](/docs/services/text-to-speech/voices.html)을 참조하십시오.
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>선택사항</em></td>
    <td style="text-align:center">문자열</td>
    <td>
      합성에 사용될 사용자 정의 음성 모델에 대한 GUID(Globally Unique
      Identifier)를 지정합니다. 사용자 정의 음성 모델은
      합성에 사용될 음성의 언어와 일치하는 경우에만
      작동되도록 보장됩니다. 사용자 정의 ID를 포함하는 경우 사용자 정의
      모델의 소유자에 대한 서비스 인증 정보를 사용하여 메소드를 호출해야
      합니다. 사용자 정의가 없는 지정된 음성을 사용하려면 매개변수를
      생략하십시오. 자세한 정보는
      [사용자 정의 이해](/docs/services/text-to-speech/custom-intro.html)를 참조하십시오.
    </td>
  </tr>
  <tr>
    <td><code>x-watson-learning-opt-out</code><br/><em>선택사항</em></td>
    <td style="text-align:center">부울</td>
    <td>
      서비스가 연결을 통해 전송되는 요청 및 결과를 로깅하는지 여부를
      표시합니다. IBM이 일반 서비스 개선을 위해 데이터에 액세스하지 못하도록
      하려면 매개변수에 <code>true</code>를 지정하십시오. 자세한
      정보는
      [Watson 서비스에 대한 요청 로깅 제어](/docs/services/watson/getting-started-logging.html)를 참조하십시오.
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>x-watson-metadata</code>
      <br/><em>선택사항</em></td>
    <td style="text-align:center">문자열</td>
    <td style="text-align:left">
      고객 ID를 연결을 통해 전달되는 데이터와
      연관시킵니다. 매개변수는
      <code>customer_id={id}</code> 인수를 허용합니다. 여기서, <code>id</code>는 무작위 문자열이거나
      데이터와 연관되는 일반 문자열입니다. 매개변수에 대한 인수를
      URL로 인코딩해야 합니다(예:
      `customer_id%3dmy_ID`). 기본적으로 고객 ID가 데이터와
      연관되지 않습니다. 자세한 정보는
      [정보 보안](/docs/services/text-to-speech/information-security.html)을 참조하십시오.
    </td>
  </tr>
</table>

다음 JavaScript 코드의 스니펫을 통해 서비스와의 연결이 열립니다. `/v1/synthesize` 메소드에 대한 호출이 `access_token` 조회 매개변수와 미국 영어 Allison 음성을 사용하도록 서비스에게 지시하는 `voice` 조회 매개변수를 전달합니다. 연결이 설정되면 이벤트 리스너(`onOpen`, `onClose` 등)는 서비스에서 이벤트를 응답하도록 정의됩니다. 

```javascript
var IAM_access_token = '{access_token}';
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&voice=en-US_AllisonVoice';

var websocket = new WebSocket(wsURI);
websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

## 입렉 텍스트 전송
{: #WSsend}

텍스트를 합성하기 위해 클라이언트는 다음 매개변수를 사용하여 단순 JSON 텍스트 메시지를 서비스에 전달합니다. 

<table>
  <caption>표 2. JSON 텍스트 메시지의 매개변수</caption>
  <tr>
    <th style="text-align:left; width:23%">매개변수</th>
    <th style="text-align:center; width:12%">데이터 유형</th>
    <th style="text-align:left">설명</th>
  </tr>
  <tr>
    <td><code>text</code><br/><em>필수</em></td>
    <td style="text-align:center">문자열</td>
    <td>
      합성될 텍스트를 제공합니다. 클라이언트는 일반 텍스트 또는
      SSML(Speech Synthesis Markup Language)로 어노테이션을 작성하는 텍스트를
      전달할 수 있습니다. 클라이언트는 요청에 따라 최대 5KB의 입력 텍스트를
      전달할 수 있습니다. 제한에는 지정하는 SSML이
      포함됩니다. 자세한 정보는
      [입력 텍스트 지정](/docs/services/text-to-speech/http.html#input) 및 다음 섹션을
      참조하십시오.<br/><br/>
      SSML 입력에는 <code>&lt;mark&gt;</code> 요소도 포함될 수 있습니다.
      자세한 정보는
      [SSML 표시 지정](/docs/services/text-to-speech/word-timing.html#mark)을 참조하십시오.
    </td>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>필수</em></td>
    <td style="text-align:center">문자열</td>
    <td>
      오디오의 요청된 형식(MIME 유형)을 지정합니다. 
      `*/*`를 사용하여 기본 오디오 형식인
      <code>audio/ogg;codecs=opus</code>를 요청하십시오. 자세한 정보는
      [오디오 형식](/docs/services/text-to-speech/audio-formats.html)을 참조하십시오.
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>선택사항</em></td>
    <td style="text-align:center">문자열[ ]</td>
    <td>
      서비스가 입력 텍스트의 모든 문자열에 대한 단어 시간 지정을
      리턴하도록 지정합니다. 서비스는 입력에 대한 각 토큰의 시작 시간 및
      종료 시간을 리턴합니다. 단어 시간 지정을 요청하기 위해 배열의
      단독 요소로 <code>words</code>를 지정합니다. 비어 있는 배열을
      지정하거나 매개변수를 생략하여 단어 시간 지정을 수신하지 않습니다.
      자세한 정보는
      [단어 시간 지정 가져오기](/docs/services/text-to-speech/word-timing.html#timing)를 참조하십시오. <em>일본어 입력 텍스트에 대해서는 지원되지 않습니다.</em>
    </td>
  </tr>
</table>

다음 JavaScript 코드의 스니펫은 입력 텍스트로 단순 "Hello world" 메시지를 전달하고 오디오에 대한 기본 형식을 요청합니다. 호출은 연결이 설정된 후에만 전송되도록 클라이언트에 대해 정의된 `onOpen` 함수에 포함되어 있습니다. 

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

서비스는 오디오 응답의 형식을 확인하는 텍스트 메시지를 전송하여 이 메시지에 응답합니다. 다음 응답은 기본 오디오 형식을 확인합니다. 

```javascript
{
  'binary_streams': [
    {
      content_type: 'audio/ogg;codecs=opus'
    }
  ]
}
```
{: codeblock}

## 응답 수신
{: #WSreceive}

오디오 형식을 확인한 후 서비스는 표시된 형식을 사용하여 데이터의 바이너리 스트림으로 합성된 오디오를 전송합니다. 서비스는 다음과 같은 경우 하나 이상의 텍스트 메시지로 시간 지정 정보를 전송합니다. 

-   입력 텍스트에는 하나 이상의 SSML `<mark>` 요소가 포함됩니다. 
-   요청에 따라 `timings` 매개변수를 지정합니다. 

서비스는 경고 또는 오류가 있는 텍스트 메시지를 전송할 수도 있습니다. 입력 텍스트 합성이 완료되면 서비스는 자동으로 WebSocket 연결을 닫습니다. 

클라이언트는 연결을 통해 수신된 오디오 결과에 서비스의 바이너리 응답을 추가해야 합니다. 오디오 결과에 응답하고, 오디오 결과를 표시하고, 애플리케이션의 사용을 위해 오디오 결과를 캡처하여 텍스트 메시지를 처리할 수 있습니다(예를 들어, 오디오 결과에 표시 위치가 포함된 경우). 다음 `onMessage` 함수의 단순 예는 서비스에서 수신된 텍스트 및 바이너리 메시지를 해당 유형을 기반으로 한 적절한 변수에 추가합니다. `onClose()` 함수가 실행되면 전체 오디오 스트림이 수신됩니다. 

```javascript
var messages;
var audioStream;

function onMessage(evt) {
  if (typeof evt.data === string) {
    messages += evt.data;
  } else {
    console.log('Received ' + evt.data.size() + ' binary bytes');
    audioStream += evt.data;
  }
}

function onClose(evt) {
  // The audio stream is complete.
}
```
{: codeblock}

## WebSocket 리턴 코드
{: #returnCodes}

서비스는 WebSocket 연결을 통해 리턴 코드를 클라이언트에 전송할 수 있습니다.

-   `1000`은 정상적인 연결의 닫기를 표시하며, 연결이 설정된 목적이 충족되었음을 의미합니다. 
-   `1002`는 서비스는 프로토콜 오류로 인해 연결을 닫는 중임을 표시합니다. 
-   `1006`은 연결이 비정상적으로 닫혔음을 표시합니다. 
-   `1009`는 프레임 크기가 4MB 한계를 초과했음을 표시합니다. 
-   `1011`은 서비스가 요청을 수행할 수 없는 예기치 않은 조건(예: 올바르지 않은 인수)이 발생했으므로 연결을 종료하는 중임을 표시합니다. 리턴 코드는 입력 텍스트가 너무 길었음을 표시할 수도 있습니다. 

소켓이 오류와 함께 종료되는 경우 서비스는 닫기 전에 클라이언트에게 `{"error": "Specific error message"}` 형식의 정보 메시지를 전송합니다. 서비스는 알 수 없는 매개변수에 대해 치명적이지 않은 경고 메시지를 전송할 수도 있습니다. 

## 오류 및 경고 메시지 예
{: #returnErrors}

다음 예는 오류 응답을 표시합니다. 여기에는 클라이언트의 `onClose` 콜백 메소드에서 JSON 텍스트 메시지 및 형식화된 메시지가 포함되어 있습니다. 형식화된 메시지는 연결이 닫히기 때문에 부울 `true`로 시작됩니다. 여기에는 닫힘의 원이 되는 WebSocket 오류 코드도 포함됩니다. 

-   이 예에는 `accept` 매개변수에 대해 올바르지 않은 인수에 대한 오류 메시지를 표시합니다. 

    ```javascript
    {
      "error": "Unsupported mimetype. Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   이 예에는 누락된 `text` 매개변수에 대한 오류 메시지가 포함됩니다. 

    ```javascript
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

다음 예에는 `invalid-parameter`라는 알 수 없는 매개변수에 대한 오류 메시지가 표시됩니다. 여기에는 연결이 경고로 닫히지 않았으므로 두 번째 메시지가 포함되지 않습니다. 

```javascript
{
  "warnings": "Unknown arguments: invalid-parameter."
}
```
{: codeblock}

WebSocket 리턴 코드에 대한 자세한 정보는 IETF(Internet Engineering Task Force) [RFC(Request for Comments) 6455 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://tools.ietf.org/html/rfc6455){: new_window}를 참조하십시오.
