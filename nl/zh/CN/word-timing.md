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

# 获取词计时
{: #timing}

WebSocket 接口提供的功能与 HTTP `GET` 和 `POST /v1/synthesize` 方法相同。除此之外，您还可以使用 WebSocket 接口来获取特定位置或输入中所有词的计时信息：
{: shortdesc}

-   在输入文本中包含 SSML `<mark>` 元素，可确定音频中遇到标记时的时间。
-   在 JSON 文本消息中指定 `timings` 参数，可获取输入文本中所有字符串的计时信息。

计时信息对于同步音频和输入文本非常有用。例如，可以使用合成语音的内容来协调机器人的手势。

日语输入文本不支持 `timings` 参数。
{: note}

## 服务如何返回词计时
{: #timingHow}

要返回标记或词计时信息，服务会多路复用独立二进制流和文本流以构造其响应：

-   对于每个 `<mark>` 元素，服务会返回一条 JSON 格式文本消息。每条消息指示从合成音频开头起，遇到 mark 时的确切时间。
-   对于所有字符串的词计时，服务会返回一条或多条 JSON 文本消息。每条消息都包含词的数组，以及从合成音频开头起，这些词的开始时间和结束时间。

服务发送的二进制流和文本流是独立的。因此，服务对其传递的音频块数，以及对用户接收文本和音频消息的时间几乎没有控制权。例如，如果音频合成速度比压缩速度更快，那么所有文本消息可能都会先于任何音频到达。

实际上，服务可以发送任意数量的音频块，包括在每个文本消息之前和之后发送多个音频块。还可以使单个二进制块包含位于 mark 或词的计时信息之前和之后的音频数据。

但是，包含计时信息的文本消息始终会先于包含相应音频的二进制块到达。此外，音频消息始终按顺序到达，以便您可以通过二进制结果来构造文本的准确音频合成。

## 指定 SSML mark
{: #mark}

可选的 SSML `<mark>` 元素是一个空标记，用于在要合成的文本中放入标记。在合成了 `<mark>` 元素前面的所有文本后，系统会通知客户机。

此元素接受单个 `name` 属性，用于指定唯一标识 mark 的字符串。名称必须以字母数字字符开头。服务会将名称与从合成音频开头起，遇到 mark 时的时间一起返回。可以在输入文本中包含任意数量的 mark。

以下 JavaScript 代码片段包含 `<mark>` 元素的实例，其中 name 为 `here`：

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

完成对 mark 前面的文本的合成时，服务会发送一条文本消息，其中指明 mark 的名称以及在音频中遇到该 mark 的时间（以秒为单位）：

```javascript
{
  "marks": [
    ["here", 0.5019387755102041]
  ]
}
```
{: codeblock}

包含计时信息的文本消息始终会先于包含 mark 位置的音频块到达。

## 请求所有词的词计时
{: #timingRequest}

针对请求传递给服务的 JSON 对象的可选 `timings` 参数会返回输入文本中所有字符串的计时信息。通过此便利的功能，即无需为输入中的每个词指定 SSML `<mark>` 元素。请传递包含字符串 `words` 的数组来请求词计时。传递空数组或省略该参数时，不会收到任何计时信息。

服务通过 WebSocket 连接返回词计时的方式，与返回各个 `<mark>` 元素的计时信息的方式相同。服务会返回一条或多条 JSON 文本消息。每条消息都包含词的数组，以及从合成音频开头起，这些词的开始时间和结束时间（以秒为单位）。例如，以下示例将请求词计时信息：

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

在响应中，服务可以返回以下文本消息：

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

该响应仅仅是示例。服务可能会返回一条或多条文本消息，其中包含输入的计时信息。此外，消息还可能与包含二进制音频块的响应交错在一起。但是，包含词计时信息的文本消息始终会先于包含该词的音频块到达。

### 纯文本计时
{: #timingText}

服务的合成过程涉及文本规范化步骤，在此步骤中会拼读数字、日期、时间、金额、首字母缩略词和缩写。结果对应于如何读此类字符串。例如，字符串 *$200* 会读作三个词：*two*、*hundred* 和 *dollars*。由于词计时信息用于将音频与输入文本同步，因此服务会返回对应于输入的非规范化拼读的计时信息。

例如，假设有以下输入文本：

```
The coldest recorded temperature is -89.2 degrees Celsius in Antarctica on July 21, 1983!
```
{: codeblock}

服务将返回以下字符串的音频计时：

"*The*"、"*coldest*"、"*recorded*"、"*temperature*"、"*is*"、"*-89.2*"、"*degrees*"、"*Celsius*"、"*in*"、"*Antarctica*"、"*on*"、"*July*"、"*21,*"、"*1983!*"

虽然 "*-89.2*" 在音频中读作 5 个独立的词（*minus*、*eighty*、*nine*、*point* 和 *two*），但文本消息将此字符串作为一个单元提供其计时信息，开始时间为读 *minus* 的时间，结束时间为读 *two* 的时间。

与先前示例中一样，非规范化的字符串还可能包含标点。服务在其返回的文本消息中会包含词前面或后面的标点以及计时。例如，服务在其文本消息中返回的字符串 "*21,*" 和 "*1983!*" 包含标点。虽然标点会生成静默，但该词的音频计时*不会*包含该静默时间。

例如，假设输入文本包含以下条件语句：

```
If it is sunny, I will go to the beach.
```
{: codeblock}

服务会返回输入中所有字符串的计时信息，包括 "*sunny,*" 和 "*beach.*"，这两个字符串都以标点结尾，会生成静默。但是 "*sunny,*" 的计时信息不包含逗号生成的静默，"*beach.*" 的计时信息不包含句点生成的静默。这些信息仅反映所读字符串的计时。

### SSML 文本计时
{: #timingSSML}

服务合成纯文本时，会返回除空格以外的所有输入字符，以作为词计时响应中字符串的一部分。但对于 SSML 却并非如此，因为某些 SSML 元素不会生成音频。以下列表概述了可能影响词计时信息的 SSML 元素：

-   `<say-as>` 用于指示如何在规范化步骤中处理开始和结束 `<say-as>` 标记之间所含的文本。各属性指定如何读嵌入文本。以下示例指示如何读日期：

    ```xml
    The baby was born on <say-as interpret-as="date" format="mdy">3/4/2016</say-as>.
    ```
    {: codeblock}

    服务会返回以下字符串的计时信息："*The*"、"*baby*"、"*was*"、"*born*"、"*on*" 和 "*3/4/2016.*"。服务会将字符串 "*3/4/2016*" 规范化为 "*march fourth two thousand sixteen*"。该字符串的词计时信息反映的开始时间是读 "*march*" 的时间，结束时间是读 "*sixteen*" 的时间。

    以下示例指示要拼读词 `Hello`：

    ```xml
    <say-as interpret-as="letters">Hello</say-as>.
    ```
    {: codeblock}

    服务会返回字符串 "*Hello.*" 的计时信息. 服务在规范化步骤中，将逐字母拼读该词。响应中的词计时信息反映的开始时间是读字母 "*h*" 的时间，结束时间是读字母 "*o*" 的时间。
-   `<phoneme>` 用于对开始和结束 `<phoneme>` 标记之间所含的文本提供发音。但文本和结束标记都是可选的。以下示例包括嵌入文本和结束标记：

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme> was ripe.
    ```
    {: codeblock}

    服务会返回以下字符串的计时信息："*The*"、"*tomato*"、"*was*" 和 "*ripe.*"

    与上例不同，以下示例提供了一元 `<phoneme>` 元素，不包含嵌入文本和结束标记：

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo"/> was ripe.
    ```
    {: codeblock}

    在本例中，服务将返回以下字符串的计时信息："*The*"、"*&lt;phoneme&gt;*"、"*was*" 和 "*ripe.*"
-   `<sub>` 用于将元素的 `alias` 属性中包含的文本，替换为在语音音频中开始和结束 `<sub>` 标记之间所含的文本。例如，以下输入包含单个 `<sub>` 标记：

    ```xml
    I work at <sub alias="International Business Machines">IBM</sub>.
    ```
    {: codeblock}

    服务会生成以下字符串的计时信息："*I*"、"*work*"、"*at*" 和 "*{{site.data.keyword.IBM_notm}}.*". 服务会将字符串 "*{{site.data.keyword.IBM_notm}}*" 规范化为 "*International Business Machines*"。该字符串的词计时信息反映的开始时间是读 "*International*" 的时间，结束时间是读 "*Machines*" 的时间。
-   `<break>` 用于在语音文本中插入停顿。服务将词计时中生成的静默反映为在 `<break>` 元素之前词的结束时间与该元素之后词的开始时间之间的间隔。
- `<paragraph>`（或 `<p>`）可以在音频中插入静默。服务不会返回静默的计时信息。
- `<sentence>`（或 `<s>`）可以在音频中插入静默。服务不会返回静默的计时信息。

列表中未提及的 SSML 元素不会影响词计时信息。有关服务对 SSML 的支持的更多信息，请参阅[使用 SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml)。

## 使用 mark 元素的示例
{: #timingExample}

以下示例说明了客户机与服务之间的简单 WebSocket 会话。这些示例侧重于数据交换，而不是打开连接。客户机发送了包含两个 `<mark>` 元素（名为 `SIMPLE` 和 `EXAMPLE`）的文本消息，并请求返回 WAV 格式的音频：

```javascript
{
  "text": "This is a <mark name=\"SIMPLE\"/>simple <mark name=\"EXAMPLE\"/> example.",
  "accept": "audio/wav"
}
```
{: codeblock}

服务首先会发送消息来确认音频格式。然后，会发送包含结果的多条消息。服务无法保证发送给客户机的音频块数，也无法保证传递文本和音频消息的顺序。

因此，以下两种响应都是可能的。无论生成哪种响应，服务都会发送两条文本消息，用于标识 mark 在二进制流中的位置。但是，服务会发送任意数量的包含音频的二进制消息。mark 的计时信息始终会先于包含 mark 位置的音频块到达。

### 第一个示例响应

在第一个示例响应中，文本消息与多条音频消息交错在一起。

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

### 第二个示例响应

在第二个示例响应中，文本消息先于任何音频消息到达。

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
