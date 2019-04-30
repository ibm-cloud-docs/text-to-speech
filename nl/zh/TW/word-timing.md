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

# 取得字組計時
{: #timing}

WebSocket 介面提供與 HTTP `GET` 和 `POST /v1/synthesize` 方法相同的功能。您也可以使用 WebSocket 介面，取得特定位置的計時資訊，或輸入之所有字組的計時資訊：
{: shortdesc}

-   將 SSML `<mark>` 元素併入輸入文字中，以識別在音訊中標記出現的時間。
-   指定 JSON 文字訊息的 `timings` 參數，以取得輸入文字之所有字串的計時資訊。

計時資訊有助於合成音訊及輸入文字。例如，您可以利用合成語音的內容來協調機器人的手勢。

日文輸入文字不支援 `timings` 參數。
{: note}

## 服務如何傳回字組計時
{: #timingHow}

若要傳回標記或字組計時資訊，服務會對獨立二進位及文字串流進行多工來建構其回應：

-   對於每個 `<mark`> 元素，服務都會傳回一則 JSON 文字訊息。每則訊息都會指出標示出現的確切時間，而這些時間來自合成音訊的開頭。
-   對於所有字串的字組計時，服務會傳回一則以上的 JSON 文字訊息。每則訊息都包含一個字組陣列，以及其來自合成音訊開頭的開始和結束時間。

服務傳送的二進位和文字串流是獨立的。因此，服務不太控制遞送的音訊區塊數目，以及使用者何時接收文字和音訊訊息。例如，如果音訊的合成速度比壓縮速度更快，則所有文字訊息可能會在有任何音訊之前送達。

實際上，服務可以傳送任意數目的音訊區塊，包括每則文字訊息前後的多個音訊區塊。單一二進位區塊也可以包含標記或字組計時資訊前後的音訊資料。

不過，包含計時資訊的文字訊息一律會在包含對應音訊的二進位區塊之前送達。此外，音訊訊息一律會按順序送達，讓您可以從二進位結果建構文字的精確音訊合成。

## 指定 SSML 標記
{: #mark}

選用的 SSML `<mark>` 元素是一個空白標籤，可將標記放置在要合成的文字中。在 `<mark>` 元素之前的所有文字都已完成合成時，即會通知用戶端。

此元素接受單一 `name` 屬性，此屬性會指定用來唯一識別標記的字串。名稱必須以英數字元開頭。服務會傳回名稱以及來自合成音訊開頭的標記出現時間。您可以在輸入文字中包括任意數目的標記。

JavaScript 程式碼的下列 Snippet 包括 `<mark>` 元素的實例，其名稱為 `here`：

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

當它完成合成標記前面的文字時，服務會傳送一則文字訊息，用於識別標記的名稱，以及標記出現在音訊的時間（以秒為單位）：

```javascript
{
  "marks": [
    ["here", 0.5019387755102041]
  ]
}
```
{: codeblock}

包含計時資訊的文字訊息一律會在包含標記位置的音訊區塊之前送達。

## 要求所有字組的字組計時
{: #timingRequest}

您傳遞至要求服務之 JSON 物件的選用 `timings` 參數，會針對輸入文字的所有字串傳回計時資訊。此便利性讓您不需要針對輸入的每個字組指定 SSML `<mark>` 元素。傳遞包括字串 `words` 的陣列，以要求字組計時。傳遞空陣列或省略參數，則不接收計時資訊。

服務會透過 WebSocket 連線傳回字組計時，此方式與針對個別 `<mark>` 元素傳回計時資訊的方式相同。它會傳回一則以上的 JSON 文字訊息。每則訊息都包含一個字組陣列，以及其來自合成音訊開頭的開始和結束時間（以秒為單位）。例如，下列範例要求字組計時資訊：

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

在回應中，服務可以傳回下列文字訊息：

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

回應只是範例。服務可以傳回一則以上的文字訊息，其中隨附輸入的計時資訊。此外，這些訊息可能會穿插包含二進位音訊區塊的回應。然而，包含字組計時資訊的文字訊息一律會在包含該字組的音訊區塊之前送達。

### 純文字的計時
{: #timingText}

服務的合成處理程序涉及文字正規化步驟，用於拼出數字、日期、時間、貨幣金額、字首語及縮寫。結果對應於如何說出這類字串。例如，字串 *$200* 會說成三個字：*two*、*hundred* 及 *dollars*。因為字組計時資訊用來合成音訊與輸入文字，所以服務會傳回對應於未正規化之輸入拼字的計時資訊。

例如，考量下列輸入文字：

```
The coldest recorded temperature is -89.2 degrees Celsius in Antarctica on July 21, 1983!
```
{: codeblock}

服務會傳回下列字串的音訊計時：

"*The*"、"*coldest*"、"*recorded*"、"*temperature*"、"*is*"、"*-89.2*"、"*degrees*"、"*Celsius*"、"*in*"、"*Antarctica*"、"*on*"、"*July*"、"*21,*"、"*1983!*"

雖然 "*-89.2*" 在音訊中會說成五個個別的字（*minus*、*eighty*、*nine*、*point*、*two*），但是文字訊息會提供字串的計時資訊，作為具有 *minus* 開始時間及 *two* 結束時間的單一單位。

如前一個範例所述，未正規化的字串也可以包含標點符號。服務包括的標點符號位在與計時一起傳回之文字訊息中的字組前面或後面。例如，字串 "*21,*" 及 "*1983!*" 包括服務在其文字訊息中傳回的標點符號。雖然標點符號會導致無聲，但是字組的音訊計時*不* 包括該無聲。

例如，考量包含下列條件式陳述式的輸入文字：

```
If it is sunny, I will go to the beach.
```
{: codeblock}

服務會針對輸入的所有字串傳回計時資訊，包括 "*sunny,*" 及 "*beach.*"，這兩者結束於產生無聲的標點符號。然而 "*sunny,*" 的計時資訊不包括逗點產生的無聲，而 "*beach.*" 的計時資訊也不包括句點的無聲。此資訊只會反映說出字串的計時。

### SSML 文字的計時
{: #timingSSML}

當服務合成純文字時，它會傳回所有輸入字元，但在其字組計時回應中作為字串一部分的空格除外。SSML 並非如此，因為部分 SSML 元素不會產生音訊。下列清單彙總了可能會影響字組計時資訊的 SSML 元素：

-   `<say-as>` 指出如何在正規化步驟中處理以開始和結束 `<say-as>` 標籤括住的文字。這些屬性指定如何說出內嵌的文字。下列範例指出如何說出日期：

    ```xml
    The baby was born on <say-as interpret-as="date" format="mdy">3/4/2016</say-as>.
    ```
    {: codeblock}

    服務會傳回下列字串的計時資訊："*The*"、"*baby*"、"*was*"、"*born*"、"*on*"、"*3/4/2016.*"。服務會將字串 "*3/4/2016*" 正規化為 "*march fourth two thousand sixteen*"。字串的字組計時資訊反映 "*march*" 的開始時間及 "*sixteen*" 的結束時間。

    下列範例指出將拼出字組 `Hello`：

    ```xml
    <say-as interpret-as="letters">Hello</say-as>.
    ```
    {: codeblock}

    服務會傳回字串 "*Hello.*" 的計時資訊。服務會在正規化步驟期間逐字母拼出字組。回應中的字組計時資訊反映字母 "*h*" 的開始時間及字母 "*o*" 的結束時間。
-   `<phoneme>` 會針對以開始和結束 `<phoneme>` 標籤括住的文字提供發音。然而，文字和結束標籤兩者都是選用的。下列範例包含內嵌的文字和結束標籤：

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme> was ripe.
    ```
    {: codeblock}

    服務會傳回下列字串的計時資訊："*The*"、"*tomato*"、"*was*"、"*ripe.*"

    反之，下列範例提供沒有內嵌文字也沒有結束標籤的單運算元 `<phoneme>` 元素：

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo"/> was ripe.
    ```
    {: codeblock}

    在此情況下，服務會傳回下列字串的計時資訊："*The*"、"*&lt;phoneme&gt;*"、"*was*"、"*ripe.*"
-   `<sub>` 會將已包含在元素的 `alias` 屬性中的文字，替換為在說出音訊中以開始和結束 `<sub>` 標籤括住的文字。例如，下列輸入包括單一 `<sub>` 標籤：

    ```xml
    I work at <sub alias="International Business Machines">IBM</sub>.
    ```
    {: codeblock}

    服務會產生下列字串的計時資訊："*I*"、"*work*"、"*at*"、"*{{site.data.keyword.IBM_notm}}.*"。服務會將字串 "*{{site.data.keyword.IBM_notm}}*" 正規化為 "*International Business Machines*"。字串的計時資訊反映 "*International*" 的開始時間及 "*Machines*" 的結束時間。
-   `<break>` 會在說出的文字中插入一個 pause。服務會將字組計時中產生的無聲，反映為 `<break>` 元素前面字組的結束時間與元素後面字組的開始時間之間的間隙。
- `<paragraph>`（或 `<p>`）可將無聲新增至音訊。服務不會傳回無聲的計時資訊。
- `<sentence>`（或 `<s>`）可將無聲新增至音訊。服務不會傳回無聲的計時資訊。

清單中未提及的 SSML 元素不會影響字組計時資訊。如需 SSML 支援服務的相關資訊，請參閱[使用 SSML](/docs/services/text-to-speech/SSML.html)。

## 具有 mark 元素的範例
{: #timingExample}

下列範例顯示用戶端與服務之間的簡單 WebSocket 階段作業。這些範例著重於交換資料，而不是開啟連線。用戶端會傳送一則文字訊息，其中包括兩個名為 `SIMPLE` 及 `EXAMPLE` 的 `<mark>` 元素，而且它要求以 WAV 格式傳回音訊：

```javascript
{
  "text": "This is a <mark name=\"SIMPLE\"/>simple <mark name=\"EXAMPLE\"/> example.",
  "accept": "audio/wav"
}
```
{: codeblock}

服務會先傳送一則訊息，以確認音訊格式。然後，會傳送多則訊息與結果。服務無法保證它傳送至用戶端的音訊區塊數，或遞送文字和音訊訊息的順序。

下列是兩種可能的回應。在每一種情況下，服務都會傳送兩則文字訊息，用於識別二進位串流中標記的位置。但它會傳送任意數目的二進位訊息，其中包含音訊。標記的計時資訊一律會在包含標記位置的音訊區塊之前送達。

### 第一個回應範例

在第一個回應範例中，文字訊息會穿插多則音訊訊息。

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

### 第二個回應範例

在第二個回應範例中，文字訊息會在所有音訊訊息之前送達。

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
