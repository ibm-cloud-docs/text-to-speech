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

# 표현 SSML
{: #expressive}

기본적으로 {{site.data.keyword.texttospeechfull}} 서비스는 중립 선언 방식으로 텍스트를 합성합니다. 서비스는 다양한 말하기 방식으로 합성된 발음으로 텍스트를 변환하여 표현성을 생성하는 `<express-as>` 요소로 SSML을 확장합니다. 이 요소는 날짜, 시간 및 숫자와 같은 형식화된 텍스트에 대해 텍스트 정규화를 지정하는 SSML 요소인 `<say-as>`와 유사합니다.
{: shortdesc}

## 언어 지원
{: #languages-expressive}

서비스는 미국 영어의 Allison 음성(`en-US_AllisonVoice`)에만 표현성을 지원합니다. 표현성은 `en-US_AllisonV2Voice` 음성으로 지원되지 않습니다. 지원되지 않는 음성으로 요소를 사용하면 오류가 리턴됩니다. 

## express-as 요소

`<express-as>` 요소를 텍스트, 문장 또는 단어나 단편의 전체 본문(예: 구문 또는 단어)에 적용할 수 있습니다. 요소는 지정된 텍스트에 사용할 표현식의 유형(`GoodNews`, `Apology` 또는 `Uncertainty`)에 대해 설명하는 하나의 필수 속성인 `type`을 허용합니다. 

### GoodNews
{: #goodnews}

`GoodNews`는 긍정적이고 활기찬 메시지를 표시합니다. 

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

`Apology`는 후회의 메시지를 표시합니다. 

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

`Uncertainty`는 불확실하고 의문의 메시지를 전달합니다. 

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

## 표현 예

다음 예에서는 `POST /v1/synthesize` 메소드의 `text` 속성에서 세 가지 다른 양식의 표현성을 보여줍니다. 합성될 텍스트는 SSML 루트 `<speak>` 요소의 범위 내에 위치합니다.

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
