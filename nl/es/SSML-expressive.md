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

# SSML expresivo
{: #expressive}

De forma predeterminada, el servicio {{site.data.keyword.texttospeechfull}} sintetiza el texto en un estilo declarativo neutro. El servicio amplía SSML con un elemento `<express-as>` que crea expresividad convirtiendo el texto en voz sintetizada en varios estilos de habla. Este elemento es análogo al elemento SSML `<say-as>`, que especifica la normalización de texto para el texto con formato, como por ejemplo fechas, horas y números.
{: shortdesc}

## Soporte de idiomas
{: #languages-expressive}

El servicio da soporte a la expresividad sólo para la voz de Allison en inglés de EE.UU. (`en-US_AllisonVoice`). La expresividad no está soportada para la voz `en-US_AllisonV2Voice`. Si se utiliza el elemento con una voz no soportada, se devuelve un error.

## Elemento express-as

Puede aplicar el elemento `<express-as>` a todo el cuerpo del texto, a una oración o a un fragmento, como por ejemplo una frase o una palabra. El elemento acepta un atributo obligatorio, `type`, que describe el tipo de expresión que se debe utilizar para el texto especificado: `GoodNews`, `Apology` o `Uncertainty`.

### GoodNews
{: #goodnews}

`GoodNews` expresa un mensaje positivo y optimista.

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

`Apology` expresa un mensaje de disculpa.

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

`Uncertainty` transmite un mensaje incierto e interrogativo.

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

## Ejemplos expresivos

En los siguientes ejemplos se muestra el uso de las tres formas de expresividad en el atributo `text` del método `POST /v1/synthesize`. El texto a sintetizar se encuentra dentro del alcance del elemento SSML raíz `<speak>`.

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
