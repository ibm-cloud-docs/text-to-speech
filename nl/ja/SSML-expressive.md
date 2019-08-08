---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-21"

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

# 感情表出 SSML
{: #expressive}

デフォルトでは、{{site.data.keyword.texttospeechfull}} サービスは、テキストから感情表現のない叙述的なスタイルの音声を合成します。 このサービスでは、感情を表出できる `<express-as>` 要素を追加して SSML を拡張しています。この要素は、テキストからさまざまな発話スタイルの音声を合成できます。 この要素は、フォーマットを持つテキスト (日付、時刻、数値) の正規化を指定する SSML 要素 `<say-as>` に似ています。
{: shortdesc}

## 言語サポート
{: #languages-expressive}

サービスで感情表出がサポートされるのは、標準米国英語 Allison 音声 (`en-US_AllisonVoice`) のみです。ニューラル `en-US_AllisonV3Voice` 音声では、感情表出はサポートされません。サポートされない音声でこの要素を使用すると、エラーが返されます。

## express-as 要素
{: #ssml-express-as}

`<express-as>` 要素は、テキストの本文全体、文、またはフラグメント (句や単語など) に適用できます。 この要素は、1 つの必須属性 `type` を取ります。この属性は、指定したテキストで使用する感情表出のタイプ `GoodNews` (朗報)、`Apology` (謝罪)、または `Uncertainty` (不安) を表します。

### GoodNews
{: #goodnews}

`GoodNews`。肯定的で明るいメッセージを表します。

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

`Apology`。後悔のメッセージを表します。

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

`Uncertainty`。確信のない疑問メッセージを伝えます。

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

## 感情表出の例

`POST /v1/synthesize` メソッドの `text` 属性で 3 つのすべての感情表出形式を使用する例を以下に示します。 合成するテキストは、SSML のルート要素 `<speak>` の範囲内にあります。

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
