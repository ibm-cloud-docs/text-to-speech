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

# Expressive SSML
{: #expressive}

By default, the {{site.data.keyword.texttospeechfull}} service synthesizes text in a neutral declarative style. The service extends SSML with an `<express-as>` element that produces expressiveness by converting text to synthesized speech in various speaking styles. The element is analogous to the SSML element `<say-as>`, which specifies text normalization for formatted text such as dates, times, and numbers.
{: shortdesc}

## Language support
{: #languages-expressive}

The service supports expressiveness only for the US English Allison voice (`en-US_AllisonVoice`). Expressiveness is not supported with the `en-US_AllisonV2Voice` voice. Using the element with an unsupported voice returns an error.

## The express-as element

You can apply the `<express-as>` element to the entire body of the text, a sentence, or a fragment such as a phrase or word. The element accepts one required attribute, `type`, which describes the type of expression to use for the specified text: `GoodNews`, `Apology`, or `Uncertainty`.

### GoodNews
{: #goodnews}

`GoodNews` expresses a positive, upbeat message.

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

`Apology` expresses a message of regret.

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

`Uncertainty` conveys an uncertain, interrogative message.

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

## Expressive examples

The following examples demonstrate the use of all three forms of expressiveness in the `text` attribute of the `POST /v1/synthesize` method. The text to be synthesized is located within the span of the SSML root `<speak>` element.

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
