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

# SSML di espressività
{: #expressive}

Per impostazione predefinita, il servizio {{site.data.keyword.texttospeechfull}} sintetizza il testo in uno stile enunciativo neutrale. Il servizio estende SSML con un elemento `<express-as>` che produce espressività convertendo il testo nel discorso sintetizzato in diversi stili di pronuncia. L'elemento è analogo all'elemento `<say-as>` SSML che specifica la normalizzazione del testo per il testo formattato come le date, le ore e i numeri.
{: shortdesc}

## Supporto linguistico
{: #languages-expressive}

Il servizio supporta l'espressività solo per la voce in inglese americano Allison (`en-US_AllisonVoice`). L'espressività non è supportata con la voce `en-US_AllisonV2Voice`. L'utilizzo dell'elemento con una voce non supportata restituisce un errore. 

## L'elemento express-as

Puoi applicare l'elemento `<express-as>` all'intero corpo del testo, a un periodo o a un frammento come ad esempio una frase o una parola. L'elemento accetta un attributo obbligatorio, `type`, che descrive il tipo di espressione da utilizzare per il testo specificato: `GoodNews`, `Apology` o `Uncertainty`.

### GoodNews
{: #goodnews}

`GoodNews` esprime un messaggio positivo, ottimistico. 

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

`Apology` esprime un messaggio di rammarico. 

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

`Uncertainty` trasmette un messaggio incerto, interrogativo. 

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

## Esempi di espressività

I seguenti esempi dimostrano l'utilizzo di tutte e tre le forme di espressività nell'attributo `text` del metodo `POST /v1/synthesize`. Il testo da sintetizzare si trova all'interno dell'estensione dell'elemento `<speak>` root SSML.

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
