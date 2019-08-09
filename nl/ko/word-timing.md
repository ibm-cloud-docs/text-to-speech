---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-04"

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

# 단어 시간 지정 가져오기
{: #timing}

WebSocket 인터페이스는 HTTP `GET` 및 `POST /v1/synthesize` 메소드와 동일한 기능을 제공합니다. WebSocket 인터페이스를 사용하여 특정 위치 또는 또는 모든 입력 단어에 대한 정보를 얻을 수 있습니다.
{: shortdesc}

-   입력 텍스트에 SSML `<mark>` 요소를 포함하여 오디오에서 마커가 표시되는 시간을 식별하십시오.
-   JSON 텍스트 메시지의 `timings` 매개변수를 지정하여 입력 텍스트의 모든 문자열에 대한 시간 지정 정보를 얻으십시오.

시간 지정 정보는 오디오 및 입력 텍스트를 동기화하는 데 유용합니다. 예를 들어, 합성된 음성의 컨텐츠로 로봇의 제스처를 조정할 수 있습니다.

`timings` 매개변수는 일본어 입력 텍스트에 대해 지원되지 않습니다.
{: note}

## 서비스가 단어 시간 지정을 리턴하는 방법
{: #timingHow}

표시 또는 단어 시간 지정 정보를 리턴하기 위해 서비스는 독립적인 바이너리 스트림 및 텍스트 스트림을 다중화하여 응답을 생성합니다.

-   각 `<mark`> 요소의 경우 서비스는 JSON 텍스트 메시지를 리턴합니다. 각 메시지에는 표시가 발생하는 합성된 오디오의 시작부터 정확한 시간에 표시합니다.
-   모든 문자열에 대한 단어 시간 지정의 경우 서비스는 하나 이상의 JSON 텍스트 메시지를 리턴합니다. 각 메시지에는 합성된 오디오의 시작부터 단어의 배열과 시작 시간 및 종료 시간이 포함됩니다.

서비스가 전송하는 바이너리 스트림 및 텍스트 스트림은 독립적입니다. 따라서 사용자가 텍스트 및 오디오 메시지를 수신하는 시간과 서비스가 제공하는 오디오 청크의 수를 제어할 수 없습니다. 예를 들어, 오디오가 압축되는 속도보다 빨리 합성되는 경우 모든 텍스트 메시지가 오디오 도착 전에 도착할 수 있습니다.

실제적으로 서비스는 각 텍스트 메시지 전후에 오디오의 다중 청크를 포함하여 임의의 오디오 청크 수를 전송할 수 있습니다. 단일 바이너리 청크는 표시 또는 단어에 대한 시간 지정 정보가 앞뒤에 모두 오는 오디오 데이터를 포함할 수도 있습니다.

그러나 시간 지정 정보가 포함된 텍스트 메시지는 항상 해당 오디오가 포함된 바이너리 청크 전에 도착합니다. 또한 오디오 메시지는 바이너리 결과에서 텍스트의 정확한 오디오 합성을 구성할 수 있도록 항상 순서대로 도착합니다.

## SSML 표시 지정
{: #mark}

선택적인 SSML `<mark>` 요소는 마커를 합성될 텍스트에 배치하는 비어 있는 태그입니다. `<mark>` 요소 앞에 오는 모든 텍스트가 합성되면 클라이언트에게 알립니다.

요소는 표시를 고유하게 식별하는 문자열을 지정하는 단일 `name` 속성을 허용합니다. 이름은 영숫자 문자로 시작해야 합니다. 서비스는 표시가 합성된 오디오의 시작부터 발생하는 시간과 함께 이름을 리턴합니다. 입력 텍스트에 원하는 수의 표시를 포함할 수 있습니다.

다음 JavaScript 코드의 스니펫에는 이름이  `here`인 `<mark>` 요소가 포함됩니다.

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello <mark name="here"/> world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

표시가 앞에 오는 텍스트의 합성을 완료하면 서비스는 표시가 오디오에서 발생하는 시간(초) 및 표시의 이름을 식별하는 텍스트 메시지를 전송합니다.

```javascript
{
  "marks": [
    ["here", 0.5019387755102041]
  ]
}
```
{: codeblock}

시간 지정 정보가 포함된 텍스트 메시지는 항상 표시의 위치가 포함된 오디오 청크 전에 도착합니다.

## 모든 단어에 대한 단어 시간 지정 요청
{: #timingRequest}

요청을 위해 서비스에 전달하는 JSON 오브젝트의 선택적인 `timings` 매개변수는 입력 텍스트의 모든 문자열에 대한 시간 지정 정보를 리턴합니다. 따라서 입력 단어마다 SSML `<mark>` 요소를 지정하지 않아도 됩니다. 문자열 `words`가 포함된 배열을 전달하여 단어 시간 지정을 요청합니다. 비어 있는 배열을 지정하거나 매개변수를 생략하여 단어 시간 지정 정보를 수신하지 않습니다.

서비스는 개별 `<mark>` 요소에 대한 시간 지정 정보를 리턴하는 방식과 동일하게 WebSocket 연결을 통해 단어 시간 지정을 리턴합니다. 이는 하나 이상의 JSON 텍스트 메시지를 리턴합니다. 각 메시지에는 합성된 오디오의 시작부터 단어의 배열과 시작 시간(초) 및 종료 시간(초)이 포함됩니다. 예를 들어, 다음 예에서는 단어 시간 지정 정보를 요청합니다.

```javascript
function onOpen(evt) {
  var message = {
    text: 'I have a pet bird.',
    accept: '*/*',
    timings: ['words']
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

응답으로 서비스는 다음 텍스트 메시지를 리턴할 수 있습니다.

```javascript
{
  "words": [
    ["I", [0.0690258394023930, 0.1655782733012873]]
    ["have", [0.1655789302434486, 0.3722901056092351]]
    ["a", [0.3722906798320199, 0.4012192331086645]]
  ]
}
{
  "words": [
    ["pet", [0.4012195492838347, 0.5798213856109801]]
    ["bird.", [0.5798218710823425, 0.7440360383928273]]
  ]
}
```
{: codeblock}

응답은 예일 뿐입니다. 서비스는 입력에 대한 시간 지정 정보가 포함된 하나 이상의 텍스트 메시지를 리턴할 수 있습니다. 또한 메시지는 오디오의 바이너리 청크가 포함된 응답에 배치될 수 있습니다. 그러나 단어에 대한 시간 지정 정보가 포함된 텍스트 메시지는 항상 해당 단어가 포함된 오디오 청크 전에 도착합니다.

### 일반 텍스트에 대한 시간 지정
{: #timingText}

서비스의 합성 프로세스에는 숫자, 날짜, 시간, 통화, 약어 및 두문자어의 철자를 발음하는 텍스트 정규화 단계가 포함됩니다. 결과는 이 문자열이 음성화되는 방법과 일치합니다. 예를 들어, 문자열 *$200*은 *two*, *hundred* 및 *dollars*의 세 개의 단어로 음성화됩니다. 단어 시간 지정 정보가 오디오를 입력 텍스트와 동기화하는 데 사용되므로 서비스는 정규화되지 않은 입력의 철자에 해당하는 시간 지정 정보를 리턴합니다.

예를 들어, 다음 입력 텍스트를 고려하십시오.

```
The coldest recorded temperature is -89.2 degrees Celsius in Antarctica on July 21, 1983!
```
{: codeblock}

서비스는 다음 문자열의 오디오 시간 지정을 리턴합니다.

"*The*", "*coldest*", "*recorded*", "*temperature*", "*is*", "*-89.2*", "*degrees*", "*Celsius*", "*in*", "*Antarctica*", "*on*", "*July*", "*21,*", "*1983!*"

"*-89.2*"가 다섯 개의 개별 단어(*minus*, *eighty*, *nine*, *point*, *two*)로 오디오에 음성화되긴 하지만 *minus*의 시작 시간 및 *two*의 종료 시간이 포함된 단일 단위로 문자열에 대한 시간 지정 정보를 제공합니다.

이전 예에서와 같이 정규화되지 않은 문자열에는 구두점도 포함될 수 있습니다. 서비스에는 시간 지정과 함께 리턴되는 텍스트 메시지에서 단어 앞뒤에 오는 구두점이 포함됩니다. 예를 들어, 문자열 "*21,*" 및 "*1983!*"에는 서비스가 텍스트 메시지에 리턴하는 마침표가 포함됩니다. 구두점으로 인해 정적이 발생되긴 하지만 단어에 대한 오디오 시간 지정에는 해당 정적이 포함되지 *않습니다*.

예를 들어, 다음 조건문이 포함된 입력 텍스트를 고려하십시오.

```
If it is sunny, I will go to the beach.
```
{: codeblock}

서비스는 둘 모두 정적이 생성되는 구두점으로 끝나는 "*sunny,*" 및 "*beach.*"를 포함하여 모든 입력 문자열에 대한 시간 지정 정보를 리턴합니다. 그러나 "*sunny,*"에 대한 시간 지정 정보에는 쉼표로 생성되는 정적이 포함되지 않으며 발생하는 정적이 "*beach.*"에 대한 시간 지정 정보에는 마침표에 대한 정적이 포함되지 않습니다. 정보는 음성화된 문자열의 시간 지정만 반영합니다.

### SSML 텍스트에 대한 시간 지정
{: #timingSSML}

서비스가 일반 텍스트를 합성하는 경우 단어 시간 지정 응답에서 문자열의 일부로 공백을 제외한 모든 입력 문자를 리턴합니다. 일부 SSML 요소가 오디오를 생성하지 않으므로 SSML에는 해당되지 않습니다. 다음 목록에서는 단어 시간 지정 정보에 영향을 줄 수 있는 SSML 요소가 요약되어 있습니다.

-   `<say-as>`는 열기 및 닫기 `<say-as>` 태그 내에 있는 텍스트가 정규화 단계에서 처리되는 방식을 보여줍니다. 속성은 임베디드 텍스트가 음성화되는 방식을 지정합니다. 다음 예에서는 날짜가 음성화되는 방식을 표시합니다.

    ```xml
    The baby was born on <say-as interpret-as="date" format="mdy">3/4/2016</say-as>.
    ```
    {: codeblock}

    서비스는 "*The*", "*baby*", "*was*", "*born*", "*on*", "*3/4/2016.*"의 문자열에 대한 시간 지정 정보를 리턴합니다. 서비스는 문자열 "*3/4/2016*"을 "*march fourth two thousand sixteen*"으로 정규화합니다. 문자열에 대한 단어 시간 지정 정보는 "*march*"의 시작 시간과 "*sixteen*"의 종료 시간을 반영합니다.

    다음 예에서는 `Hello` 단어의 철자가 발음되는 것을 표시합니다.

    ```xml
    <say-as interpret-as="letters">Hello</say-as>.
    ```
    {: codeblock}

    서비스는 문자열 "*Hello.*"에 대한 시간 지정 정보를 리턴합니다. 정규화 단계 중에 단어 한자씩 철자를 발음합니다. 응답의 단어 시간 지정 정보는 "*h*" 문자의 시작 시간과 "*o*" 문자의 종료 시간을 반영합니다.
-   `<phoneme>`는 열기 및 닫기 `<phoneme>` 태그 내에 있는 텍스트의 발음을 제공합니다. 그러나 텍스트와 닫기 태그는 모두 선택사항입니다. 다음 예에는 임베디드 텍스트돠 닫기 텍스트가 포함되어 있습니다.

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme> was ripe.
    ```
    {: codeblock}

    서비스는 "*The*", "*tomato*", "*was*", "*ripe.*"의 문자열에 대한 시간 지정 정보를 리턴합니다.

    반대로, 다음 예에서는 임베드된 텍스트와 닫기 태그 없이 단항 `<phoneme>` 요소를 제공합니다.

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo"/> was ripe.
    ```
    {: codeblock}

    이 경우 서비스는 "*The*", "*&lt;phoneme&gt;*", "*was*", "*ripe.*"의 문자열에 대한 시간 지정 정보를 리턴합니다.
-   `<sub>`는 음성화된 오디오에서 열기 및 닫기 `<sub>` 태그 내에 있는 텍스트에 대해 요소의 `alias` 속성에 포함된 텍스트를 대체합니다. 예를 들어, 다음 입력에는 단일 `<sub>` 태그가 포함됩니다.

    ```xml
    I work at <sub alias="International Business Machines">IBM</sub>.
    ```
    {: codeblock}

    서비스는 "*I*", "*work*", "*at*", "*{{site.data.keyword.IBM_notm}}.*"의 문자열에 대한 시간 지정 정보를 생성합니다. 서비스는 문자열 "*{{site.data.keyword.IBM_notm}}*"을 "*International Business Machines*"로 정규화합니다. 문자열에 대한 시간 지정 정보는 "*International*"의 시작 시간과 "*Machines*"의 종료 시간을 반영합니다.
-   `<break>`는 일시정지를 음성화된 텍스트에 삽입합니다. 서비스는 `<break>` 요소 앞에 오는 단어의 종료 시간과 요소 뒤에 오는 단어의 시작 시간 간의 차이로 단어 시간 지정에서 발생하는 정적을 반영합니다.
- `<paragraph>`(또는 `<p>`)를 사용하면 정적을 오디오에 추가할 수 있습니다. 서비스는 정적에 대한 시간 지정 정보를 리턴하지 않습니다.
- `<sentence>`(또는 `<s>`)를 사용하면 정적을 오디오에 추가할 수 있습니다. 서비스는 정적에 대한 시간 지정 정보를 리턴하지 않습니다.

목록에 언급되지 않은 SSML 요소는 단어 시간 지정 정보에 영향을 주지 않습니다. SSML의 서비스 지원에 대한 자세한 정보는 [SSML 사용](/docs/services/text-to-speech?topic=text-to-speech-ssml)을 참조하십시오.

## 표시 요소가 포함된 예
{: #timingExample}

다음 예에서는 클라이언트와 서비스 간의 단순 WebSocket 세션을 보여줍니다. 예는 연결 열기가 아닌 데이터 교환에 중점을 둡니다. 클라이언트는 `SIMPLE` 및 `EXAMPLE`이라고 하는 두 개의 `<mark>` 요소가 포함된 텍스트 메시지를 전송하고 이는 오디오가 WAV 형식으로 리턴되도록 요청합니다.

```javascript
{
  "text": "This is a <mark name=\"SIMPLE\"/>simple <mark name=\"EXAMPLE\"/> example.",
  "accept": "audio/wav"
}
```
{: codeblock}

서비스는 먼저 메시지를 전송하여 오디오 형식을 확인합니다. 그런 다음 결과가 포함된 여러 개의 메시지를 전송합니다. 서비스는 클라이언트에 전송하는 오디오 청크의 수와 텍스트 및 오디오 메시지가 전달되는 순서를 보장할 수 없습니다.

다음 두 가지 응답이 사용 가능합니다. 각각의 경우, 서비스는 바이너리 스트림에서 표시의 위치를 식별하는 두 개의 텍스트 메시지를 전송합니다. 그러나 오디오가 포함된 임의의 바이너리 메시지 수를 전송합니다. 표시에 대한 시간 지정 정보는 항상 표시의 위치가 포함된 오디오 청크 전에 도착합니다.

### 첫 번째 응답 예

첫 번째 응답 예에서 텍스트 메시지는 여러 오디오 메시지에 배치됩니다.

```javascript
{
  "binary_streams": [
    {
      "content_type": "audio/wav"
    }
  ]
}
... one or more chunks of binary audio
    all audio precedes the SIMPLE mark ...
{
  "marks": [
    [
      "SIMPLE",
      0.7848991042702103
    ]
  ]
}
... one or more chunks of binary audio
    audio can precede and follow the SIMPLE mark
    all audio precedes the EXAMPLE mark ...
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... one or more chunks of binary audio
    audio can precede and follow the EXAMPLE mark ...
```
{: codeblock}

### 두 번째 응답 예

두 번째 응답 예에서 텍스트 메시지는 오디오 메시지 전에 도착합니다.

```javascript
{
  "binary_streams": [
    "content_type": "audio/wav"}
  ]
}
{
  "marks": [
    [
      "SIMPLE", 0.7848991042702103
    ]
  ]
}
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... one or more chunks of binary audio ...
```
{: codeblock}
