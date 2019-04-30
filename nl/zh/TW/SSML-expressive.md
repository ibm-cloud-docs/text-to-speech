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

# 表示 SSML
{: #expressive}

依預設，{{site.data.keyword.texttospeechfull}} 服務會以中性宣告樣式來合成文字。此服務會使用 `<express-as>` 元素來擴充 SSML，以各種說話樣式將文字轉換為合成語音來產生表示式。此元素類似於 SSML 元素 `<say-as>`，其會指定格式化文字（例如日期、時間及數字）的文字正規化。
{: shortdesc}

## 語言支援
{: #languages-expressive}

服務僅支援美式英文 Allison 語音 (`en-US_AllisonVoice`) 的表示式。不支援表示式與 `en-US_AllisonV2Voice` 語音搭配使用。使用元素與不受支援的語音搭配會傳回錯誤。

## express-as 元素

您可以將 `<express-as>` 元素套用至整個文字內文、句子，或詞組或字組這類的片段。此元素接受一個必要屬性 `type`，其說明要用於指定文字的表示式類型：`GoodNews`、`Apology` 或 `Uncertainty`。

### GoodNews
{: #goodnews}

`GoodNews` 表示正面的樂觀訊息。

```xml
<express-as type="GoodNews">
  I am pleased to inform you that your mortgage loan application was approved.
</express-as>

<express-as type="GoodNews">
  I have good news: I was able to reduce the payments on your monthly bill!
</express-as>

<express-as type="GoodNews">
  Congratulations on your engagement! You two are perfect for each other!
</express-as>

<express-as type="GoodNews">
  Wow, good job on your promotion! That&apos;s a really prestigious position!
</express-as>
```
{: codeblock}

### Apology
{: #apology}

`Apology` 表示遺憾訊息。

```xml
<express-as type="Apology">
  Unfortunately, the next flight doesn&apos;t leave for another five hours.
</express-as>

<express-as type="Apology">
  I am terribly sorry for the quality of service you have received.
</express-as>

<express-as type="Apology">
  Please forgive me for deleting your files. It was an accident.
</express-as>

<express-as type="Apology">
  Is there any way I can make this up to you?
</express-as>
```
{: codeblock}

### Uncertainty
{: #uncertainty}

`Uncertainty` 傳達不確定的疑問訊息。

```xml
<express-as type="Uncertainty">
  Could she still be in the office? She told me that she might leave early.
</express-as>

<express-as type="Uncertainty">
  Sorry, I think I misheard. Was that Friday or Saturday?
</express-as>

<express-as type="Uncertainty">
  Can you please explain it again? I&apos;m not sure I understand.
</express-as>

<express-as type="Uncertainty">
  I&apos;m sorry, but I didn&apos;t catch your name. Could you please repeat it?
</express-as>
```
{: codeblock}

## 表示範例

下列範例示範如何在 `POST /v1/synthesize` 方法的 `text` 屬性中使用這三種格式的表示式。要合成的文字位於 SSML 根 `<speak>` 元素的文字段內。

```xml
{
  "text": "<speak>
    I have been assigned to handle your order status request.
    <express-as type=\"Apology\">
      I am sorry to inform you that the items you requested are backordered.
      We apologize for the inconvenience.
    </express-as>
    <express-as type=\"Uncertainty\">
      We don&apos;t know when the items will become available. Maybe next week,
      but we are not sure at this time.
    </express-as>
    <express-as type=\"GoodNews\">
      But because we want you to be a satisfied customer, we are giving you
      a 50% discount on your order!
    </express-as>
  </speak>"
}
```
{: codeblock}
