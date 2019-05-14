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

# SSML für Expressivität
{: #expressive}

Der {{site.data.keyword.texttospeechfull}}-Service erstellt aus Text standardmäßig synthetisch Sprache in einem neutralen und deklarativen Stil. Der Service erweitert SSML durch ein Element `<express-as>`, das durch die Konvertierung von synthetisch erstellter Sprache in verschiedene Sprechstile Expressivität erzeugt. Das Element ist analog zum SSML-Element `<say-as>`, mit dem die Textnormalisierung für formatierten Text wie Datums- und Zeitangaben oder Zahlen angegeben wird.
{: shortdesc}

## Sprachunterstützung
{: #languages-expressive}

Die Expressivität wird vom Service nur bei der Stimme 'Allison' für amerikanisches Englisch unterstützt (`en-US_AllisonVoice`). Bei der Stimme `en-US_AllisonV2Voice` wird die Expressivität nicht unterstützt. Die Verwendung des Elements bei einer nicht unterstützten Stimme gibt einen Fehler zurück.

## Element 'express-as'

Sie können das Element `<express-as>` auf den gesamten Text, einen Satz oder ein Fragment wie einen Ausdruck oder ein Wort anwenden. Das Element akzeptiert nur ein einziges erforderliches Attribut namens `type`, das den Typ der Expressivität beschreibt, die für den angegebenen Text verwendet werden soll: `GoodNews` (= gute Neuigkeiten), `Apology` (= Entschuldigung) oder `Uncertainty` (= Unsicherheit).

### GoodNews
{: #goodnews}

Der Attributwert `GoodNews` drückt eine positive und fröhliche Nachricht aus.

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

### Entschuldigung
{: #apology}

Der Attributwert `Apology` drückt eine bedauernde Mitteilung aus.

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

### Unsicherheit
{: #uncertainty}

Der Attributwert `Uncertainty` drückt eine unsichere und fragende Mitteilung aus.

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

## Beispiele für Expressivität

Die folgenden Beispiele veranschaulichen die Verwendung aller drei Formen von Expressivität im Attribut `text` der Methode `POST /v1/synthesize`. Der Text, aus dem synthetisch Sprache erstellt werden soll, befindet sich im Bereich des Elements `<speak>`.

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
