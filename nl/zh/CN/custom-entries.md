---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-24"

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

# 创建和管理定制条目
{: #customWords}

定制模型存在后，下一步是以词/转换项对的格式添加定制条目，以定义指定的词在合成期间如何发音。这些定义会覆盖服务的缺省常规发音规则。可以一次添加和查询一个或多个词的转换项，并且可以删除不再需要的各个词。熟悉定制接口后，可以一次性处理多个词，这比逐词处理要方便得多。对于拥有定制模型的服务实例，您必须使用该实例的凭证，才能利用需要其定制标识的任何方法。
{: shortdesc}

## 向定制模型添加单个词
{: #cuWordAdd}

要向定制模型添加单个词/转换项对，请使用 `PUT /v1/customizations/{customization_id}/words/{word}` 方法。可在此方法的 URL 中指定要添加的词。通过单个 `translation` 属性提供词的转换项作为 JSON 对象。向模型中已存在的词添加新的转换项会覆盖该词的现有转换项。

可以使用近似读音方法或拼音方法（或这两者的组合）来提供转换项。对于拼音转换项，可以使用国际音标 (IPA) 或 {{site.data.keyword.IBM_notm}} 符号拼音表示法 (SPR) 格式。以下示例使用不同的方法将词 `IEEE` 的等效转换项添加到定制模型。

-   **近似读音：**对于此示例，近似读音方法是最简单的方法：

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"I triple E\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **拼音 IPA：**IPA 需要使用 `<phoneme>` 元素，其中 `alphabet` 属性设置为 `ipa`，`ph` 属性以 IPA 格式进行定义：

    <pre><code class="language-bash">  curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#712;a&#618;.t&#633;&#712;&#616;p&#601;l.&#712;i\\\"&gt;&lt;/phoneme&gt;\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"</code></pre>

-   **拼音 {{site.data.keyword.IBM_notm}} SPR：**SPR 使用 `<phoneme>` 元素，其中 `alphabet` 属性设置为 `ibm`，`ph` 属性以 SPR 格式进行定义：

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

## 向定制模型添加多个词
{: #cuWordsAdd}

要一次向定制模型添加一个或多个词，请使用 `POST /v1/customizations/{customization_id}/words` 方法。指定要作为词/转换项对的 JSON 数组添加到定制模型的条目。以下示例向定制模型添加了词 `NCAA` 和 `iPhone` 的常见近似读音转换项：

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

在请求主体中发送的 JSON 内容等同于以下内容：

```javascript
{
  "words": [
    {"word":"NCAA", "translation":"N C double A"},
    {"word":"iPhone", "translation":"I phone"}
  ]
}
```
{: codeblock}

如[更新定制模型](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsUpdate)中所述，还可以使用 `POST /v1/customizations/{customization_id}` 方法向定制模型添加词。以下示例使用此方法来添加与先前示例相同的两个词；但不对模型的元数据进行任何更改。除了 URL 外，这两种方法完全相同。

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

## 向日语定制模型添加词
{: #cuJapaneseAdd}

在日语定制模型中创建词的条目时，额外注意事项和额外的 `part_of_speech` 字段适用；有关更多信息，请参阅[使用日语条目](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes)。指定日语定制条目的词性，如下所示：

-   对于 `PUT /v1/customizations/{customization_id}/words/{word}` 方法，传递以下格式的 JSON 对象：

    ```javascript
    {
      "translation": "value",
      "part_of_speech": "value"
    }
    ```
    {: codeblock}

-   对于 `POST /v1/customizations/{customization_id}/words` 和 `POST customizations/{customization_id}` 方法，请传递类似于以下内容的 JSON 对象：

    ```javascript
    {
      "words": [
        {
          "word": "value",
          "translation": "value",
          "part_of_speech": "value"
        }
        . . .
      ]
    }
    ```
    {: codeblock}

`PUT /v1/customizations/{customization_id}/words/{word}` 方法的以下示例将 `NY` 的 URL 编码的双字节字符串转换为名词 (`Mesi`) <code>&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;</code>（英语中的 `New York`）。如果未定义此定制转换项，那么字符串将被读成 `enu wai`。

-   **近似读音：**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **拼音 IPA：**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#626;&#623;&#720;&#106;&#111;&#720;&#107;&#623;\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **拼音 {{site.data.keyword.IBM_notm}} SPR：**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

## 在定制模型中查询单个词
{: #cuWordQueryModel}

要在定制模型中查询单个词的转换项，请使用 `GET /v1/customizations/{customization_id}/words/{word}` 方法。可在此方法的 URL 中指定该词。转换项将按照定制模型（近似读音或拼音）中所定义的内容返回。

以下示例在定制模型中查询词 `IEEE` 的转换项：

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

如果该词在模型中有近似读音转换项，那么示例会返回以下 JSON 输出：

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

## 查询定制模型中的所有词
{: #cuWordsQueryModel}

要查看在定制模型中定义的所有词的转换项，请使用 `GET /v1/customizations/{customization_id}/words` 方法。以下示例使用此方法列出定制模型中的条目，该模型包含三个词的近似读音转换项：

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

此方法返回具有以下数据的 JSON 数组。对于日语定制模型，输出会包含各个词的词性。

```javascript
{
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

如[查询定制模型](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery)中所述，您还可以使用 `GET /v1/customizations/{customization_id}` 方法来查看定制模型的元数据和词：

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

此方法返回以下格式的 JSON 输出。由于此示例和上一个示例指定的定制模型相同，因此两个示例的输出中的词数组完全相同。

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T19:15:17.926Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T19:46:01.387Z",
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

## 查询某种语言的词
{: #cuWordsQueryLanguage}

要查询词的发音，请使用 `GET /v1/pronunciation` 方法。指定声音以获取该声音在该语言中的发音。缺省情况下，此方法会返回基于服务的常规发音规则的发音，但您还可以请求针对指定定制声音模型的发音。此方法包括四个查询参数，可用于指定要返回的信息：

-   必需的 `text` 参数指定要返回其发音的词。
-   可选的 `voice` 参数允许指定发音所用的语言。您可指定其中一个声音模型（例如，`en-US_LisaVoice`）以指示所需的语言；同一语言（例如，`en-US`）的所有声音都会返回相同的发音。缺省情况下，将返回美国英语的发音。
-   可选的 `format` 参数允许指定发音的拼音格式：`ipa` 或 `ibm`。缺省情况下，发音以 IPA 格式返回。
-   可选的 `customization_id` 参数允许指定要为其返回发音的定制声音模型。如果未在指定的声音模型中定义该词，那么服务将返回模型所用语言的缺省发音。省略该参数可查看未进行任何定制的指定声音的转换项。不要同时指定声音和定制声音模型。

此方法非常有用，因为它允许您查询任何语言的词，并且此方法无需定制标识，因此对您可以查看的词没有限制。在编写新词的拼音转换项时，此方法会特别有用；您可以将其用于获取现有词的发音，然后将其用作新转换项的基础，这比从头开始创建转换项要方便得多。

以下示例将以缺省 IPA 格式获取词 `IEEE` 的发音。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=IEEE"
```
{: pre}

<pre><code data-copy="false" class="language-javascript">{
  "pronunciation": ".&#712;a&#618; .&#712;i .&#712;i .&#712;i"
}</code></pre>

以下示例将输入词 `IEEE` 的近似读音转换项，并获取 {{site.data.keyword.IBM_notm}} SPR 格式的拼音等效项。获取近似读音转换项的拼音发音是一种特别有趣的编写拼音转换项的方法。在以下示例中，对词的空格进行了 URL 编码。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=i%20triple%20e&format=ibm"
```
{: pre}

```javascript
{
  "pronunciation": "1Y.tr1Ipxl.1i"
}
```
{: codeblock}

## 从定制模型中删除词
{: #cuWordDelete}

要从定制模型中删除词，请使用 `DELETE /v1/customizations/{customization_id}/words/{word}` 方法。可在此方法的 URL 中指定要删除的词。只能删除单个词；不能使用一个方法来删除多个词。

以下示例将从指定的定制模型中删除词 `IEEE`：

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}
