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

# Worttakt abrufen
{: #timing}

Die WebSocket-Schnittstelle bietet dieselbe Funktionalität wie die HTTP-Methoden `GET` und `POST /v1/synthesize`. Mit der WebSocket-Schnittstelle können Sie darüber hinaus Taktinformationen für bestimmte Positionen oder für alle Wörter der Eingabe erhalten.
{: shortdesc}

-   Beziehen Sie das SSML-Element `<mark>` in den Eingabetext ein, um den Zeitpunkt anzugeben, an der die Markierung in der Audioausgabe vorkommt.
-   Geben Sie den Parameter `timings` einer JSON-Textnachricht an, um Taktinformationen für alle Zeichenfolgen des Eingabetextes zu erhalten.

Taktinformationen sind bei der Synchronisierung der Audioausgabe mit dem Eingabetext von Nutzen. Beispielsweise können Sie die Gesten eines Roboters mit dem Inhalt der synthetisch erstellten Sprache koordinieren.

Bei Eingabetext in Japanisch wird der Parameter `timings` nicht unterstützt.
{: note}

## Rückgabe des Worttakts durch den Service
{: #timingHow}

Zur Rückgabe von Markierungs- oder Worttaktinformationen führt der Service ein Multiplexing von unabhängigen binären Datenströmen und Textdatenströmen durch, um seine Antwort zu erstellen:

-   Für jedes Element `<mark>` gibt der Service eine JSON-Textnachricht zurück. In jeder Nachricht ist der genaue Zeitpunkt seit dem Beginn der synthetisch erstellten Audioausgabe angegeben, an dem die Markierung vorkommt.
-   Beim Worttakt für alle Zeichenfolgen gibt der Service eine oder mehrere JSON-Textnachrichten zurück. Jede Nachricht enthält ein Array von Wörtern und dessen Start- sowie Endzeitpunkt seit dem Beginn der synthetisch erstellten Audioausgabe.

Die vom Service gesendeten Binärdatenströme und Textdatenströme sind unabhängig. Der Service kann somit die Anzahl der von ihm gelieferten Audioblöcke und den Zeitpunkt für den Empfang der Text- und Audionachrichten durch den Benutzer nur wenig steuern. Falls beispielsweise die Audioausgabe schneller synthetisch erstellt wird, als sie komprimiert werden kann, treffen möglicherweise alle Textnachrichten ein, bevor eine der Audionachrichten empfangen wird.

In der Praxis bedeutet dies, dass der Service eine beliebige Anzahl von Audioblöcken senden kann, also auch mehrere Blöcke von Audiodaten vor und nach jeder Textnachricht. Außerdem kann es vorkommen, dass ein einzelner Binärblock Audiodaten enthält, die den Taktinformationen für eine Markierung oder ein Wort sowohl vorausgehen als auch folgen.

Die Textnachricht, in der die Taktinformationen enthalten sind, trifft jedoch stets vor dem Binärblock ein, der die entsprechende Audioausgabe enthält. Darüber hinaus treffen die Audionachrichten immer in der richtigen Reihenfolge ein, weshalb Sie aus den binären Ergebnissen eine präzise Audiosynthese des Textes erstellen können.

## SSML-Markierung angeben
{: #mark}

Das optionale SSML-Element `<mark>` ist ein leerer Tag, der eine Markierung in dem Text platziert, aus dem synthetisch Sprache erstellt werden soll. Der Client wird benachrichtigt, sobald aus dem gesamten Text, der dem Element `<mark>` vorangeht, synthetisch Sprache erstellt worden ist.

Das Element akzeptiert ein einziges Attribut `name`, in dem eine Zeichenfolge angegeben ist, die die Markierung eindeutig kennzeichnet. Der Name muss mit einem alphanumerischen Zeichen beginnen. Der Service gibt den Namen zusammen mit dem Zeitpunkt seit Beginn der synthetisch erstellten Audioausgabe zurück, an dem die Markierung vorkommt. Sie können eine beliebige Anzahl von Markierungen in den Eingabetext aufnehmen.

Das folgende Snippet aus JavaScript-Code enthält eine Instanz des Elements `<mark>` mit dem Namen `here`:

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

Sobald der Service die synthetische Erstellung von Sprache aus dem Text, der der Markierung vorausgeht, abgeschlossen hat, sendet er eine Textnachricht, in der der Name der Markierung sowie in Sekunden der Zeitpunkt angegeben ist, zu dem die Markierung in der Audioausgabe auftritt:

```javascript
{
  "marks": [
    ["here", 0.5019387755102041]
  ]
}
```
{: codeblock}

Die Textnachricht, in der die Taktinformationen enthalten sind, trifft stets vor dem Audioblock ein, der die Position der Markierung enthält.

## Worttakt für alle Wörter anfordern
{: #timingRequest}

Der optionale Parameter `timings` des JSON-Objekts, das Sie an den Service für eine Anforderung übergeben, gibt Taktinformationen für alle Zeichenfolgen des Eingabetextes zurück. Diese komfortable Option macht die Angabe des SSML-Elements `<mark>` für jedes Wort der Eingabe überflüssig. Übergeben Sie ein Array, das die Zeichenfolge `words` enthält, um den Worttakt anzufordern. Geben Sie ein leeres Array an oder lassen Sie den Parameter weg, damit keine Taktinformationen empfangen werden.

Der Service gibt den Worttakt über die WebSocket-Verbindung genauso wie Taktinformationen für einzelne Elemente `<mark>` zurück. Er gibt eine oder mehrere JSON-Textnachrichten zurück. Jede Nachricht enthält ein Array von Wörtern sowie in Sekunden dessen Start- und Endzeitpunkt seit dem Beginn der synthetisch erstellten Audioausgabe. Der folgende Code fordert beispielsweise Worttaktinformationen an:

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

Als Antwort kann der Service die folgenden Textnachrichten zurückgeben:

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

Die Antwort ist nur ein Beispiel. Der Service kann eine oder mehrere Textnachrichten mit Taktinformationen für die Eingabe zurückgeben. Zwischen den einzelnen Nachrichten können außerdem Antworten eintreffen, die Binärblöcke mit Audioausgabe enthalten. Die Textnachricht, in der die Taktinformationen für ein Wort enthalten sind, trifft jedoch immer vor dem Audioblock ein, der das Wort enthält.

### Takt für einfachen Text
{: #timingText}

Der Syntheseprozess des Service beinhaltet einen Schritt für die Textnormalisierung, bei dem Zahlen, Datumsangaben, Uhrzeiten, Geldbeträge, Akronyme und Abkürzungen ausformuliert werden. Die Ergebnisse entsprechen der zu verwendenden Aussprache für solche Zeichenfolgen. Die Zeichenfolge *$200* wird beispielsweise in drei Wörtern gesprochen: *two*, *hundred* und *dollars*. Da Worttaktinformationen zum Synchronisieren der Audioausgabe mit dem Eingabetext verwendet werden, gibt der Service Taktinformationen zurück, die der nicht normalisierten Schreibweise der Eingabe entsprechen.

Beispieleingabetext:

```
The coldest recorded temperature is -89.2 degrees Celsius in Antarctica on July 21, 1983!
```
{: codeblock}

Der Service gibt den Audiotakt für die folgenden Zeichenfolgen zurück:

"*The*", "*coldest*", "*recorded*", "*temperature*", "*is*", "*-89.2*", "*degrees*", "*Celsius*", "*in*", "*Antarctica*", "*on*", "*July*", "*21,*", "*1983!*"

Obwohl für "*-89.2*" in der Audioausgabe fünf separate Wörter gesprochen werden (*minus*, *eighty*, *nine*, *point*, *two*), stellt die Textnachricht Taktinformationen für die Zeichenfolge als gesamte Einheit mit dem Startzeitpunkt von *minus* und dem Endzeitpunkt von *two* bereit.

Wie im vorherigen Beispiel können nicht normalisierte Zeichenfolgen auch Interpunktionszeichen enthalten. Der Service bezieht die Interpunktion vor oder nach einem Wort in der Textnachricht ein, die er mit dem Takt zurückgibt. Die Zeichenfolgen "*21,*" und "*1983!*" enthalten beispielsweise eine Interpunktion, die der Service in seiner Textnachricht zurückgibt. Die Interpunktion führt zwar zu einer Sprechpause, aber der Audiotakt für das Wort enthält diese Sprechpause *nicht*.

Dies wird nachfolgend am Beispiel eines Eingabetextes erläutert, der die folgende bedingte Aussage enthält:

```
If it is sunny, I will go to the beach.
```
{: codeblock}

Der Service gibt Taktinformationen für alle Zeichenfolgen der Eingabe zurück, also auch für die Zeichenfolgen "*sunny,*" und "*beach.*", die beide mit einem Interpunktionszeichen enden, das eine Sprechpause erzeugt. Die Taktinformationen für "*sunny,*" enthalten jedoch nicht die durch das Komma entstehende Sprechpause; ebensowenig berücksichtigen die Taktinformationen für "*beach.*" die Sprechpause für den Punkt. Die Informationen bilden nur den Takt der gesprochenen Zeichenfolgen ab.

### Takt für SSML-Text
{: #timingSSML}

Wenn der Service aus einfachem Text synthetisch Sprache erstellt, gibt er mit Ausnahme von Leerzeichen alle Eingabezeichen der Eingabezeichenfolge in seiner Worttaktantwort zurück. Bei SSML gilt dies nicht, weil manche SSLM-Elemente keine Audioausgabe generieren. Die folgende Liste vermittelt Ihnen einen Überblick über SSML-Elemente, die sich auf Worttaktinformationen auswirken können:

-   Das Element `<say-as>` gibt an, wie der Text, der zwischen dem Anfangs- und dem Endtag `<say-as>` angegeben ist, im Normalisierungsschritt verarbeitet werden soll. Mit Attributen wird angegeben, wie der eingebettete Text zu sprechen ist. Das folgende Beispiel zeigt, wie das Datum gesprochen werden soll:

    ```xml
    The baby was born on <say-as interpret-as="date" format="mdy">3/4/2016</say-as>.
    ```
    {: codeblock}

    Der Service gibt Taktinformationen für die folgenden Zeichenfolgen zurück: "*The*", "*baby*", "*was*", "*born*", "*on*", "*3/4/2016.*" Er normalisiert die Zeichenfolge "*3/4/2016*" als "*march fourth two thousand sixteen*". Die Worttaktinformationen für die Zeichenfolge bilden den Startzeitpunkt von "*march*" und den Endzeitpunkt von "*sixteen*" ab.

    Im folgenden Beispiel ist angegeben, dass das Wort `Hello` buchstabiert werden soll:

    ```xml
    <say-as interpret-as="letters">Hello</say-as>.
    ```
    {: codeblock}

    Der Service gibt Taktinformationen für die Zeichenfolge "*Hello.*" zurück. Das Wort wird vom Service während des Normalisierungsschritts Buchstabe für Buchstabe gesprochen. Die Worttaktinformationen in der Antwort bilden den Startzeitpunkt des Buchstabens "*h*" und den Endzeitpunkt des Buchstabens "*o*" ab.
-   Das Element `<phoneme>` stellt eine Aussprache für den Text zwischen dem Anfangs- und dem Endtag `<phoneme>` bereit. Sowohl der Text als auch der Endtag sind optional. Das folgende Beispiel enthält eingebetteten Text und einen Endtag:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme> was ripe.
    ```
    {: codeblock}

    Der Service gibt Taktinformationen für die folgenden Zeichenfolgen zurück: "*The*", "*tomato*", "*was*", "*ripe.*"

    Im Gegensatz hierzu bietet das folgende Beispiel ein unitäres Element `<phoneme>` ohne eingebetteten Text und Endtag:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo"/> was ripe.
    ```
    {: codeblock}

    In diesem Fall gibt der Service Taktinformationen für die folgenden Zeichenfolgen zurück: "*The*", "*&lt;phoneme&gt;*", "*was*", "*ripe.*".
-   Das Element `sub` verwendet in der gesprochenen Audioausgabe den Text, der im Attribut `alias` des Elements angegeben ist, als Ersetzung für den Text zwischen dem Anfangs- und dem Endtag `sub`. Die folgende Eingabe enthält beispielsweise einen einzigen Tag `sub`:

    ```xml
    I work at <sub alias="International Business Machines">IBM</sub>.
    ```
    {: codeblock}

    Der Service erzeugt Taktinformationen für die folgenden Zeichenfolgen: "*I*", "*work*", "*at*", "*{{site.data.keyword.IBM_notm}}.*". Er normalisiert die Zeichenfolge "*{{site.data.keyword.IBM_notm}}*" als "*International Business Machines*". Die Taktinformationen für die Zeichenfolge bilden den Startzeitpunkt von "*International*" und den Endzeitpunkt von "*Machines*" ab.
-   Das Element `break` fügt eine Pause im gesprochenen Text ein. Der Service bildet die resultierende Sprechpause im Worttakt als Lücke zwischen dem Endzeitpunkt des Wortes vor dem Element `<break>` und dem Startzeitpunkt des Wortes nach dem Element ab.
- Das Element `paragraph` (oder `<p>`) kann eine Sprechpause zur Audioausgabe hinzufügen. Für die Sprechpause werden vom Service keine Taktinformationen zurückgegeben.
- Das Element `sentence` (oder `s`) kann eine Sprechpause zur Audioausgabe hinzufügen. Für die Sprechpause werden vom Service keine Taktinformationen zurückgegeben.

SSML-Elemente, die in der Liste nicht aufgeführt sind, haben keine Auswirkungen auf die Worttaktinformationen. Weitere Angaben über die Unterstützung des Service für SSML enthält der Abschnitt [SSML verwenden](/docs/services/text-to-speech?topic=text-to-speech-ssml).

## Beispiele mit Markierungselementen
{: #timingExample}

Die folgenden Beispiele zeigen eine einfache WebSocket-Sitzung zwischen einem Client und dem Service. In den Beispielen ist der Datenaustausch dargestellt, nicht der Verbindungsaufbau. Der Client sendet eine Textnachricht, die zwei Elemente `<mark>` namens `SIMPLE` und `EXAMPLE` enthält, und fordert die Audiorückgabe im WAV-Format an:

```javascript
{
  "text": "This is a <mark name=\"SIMPLE\"/>simple <mark name=\"EXAMPLE\"/> example.",
  "accept": "audio/wav"
}
```
{: codeblock}

Der Service sendet zunächst eine Nachricht, um das Audioformat zu bestätigen. Anschließend sendet er mehrere Nachrichten mit den Ergebnissen. Weder die Anzahl der vom Service an den Client gesendeten Audioblöcke noch die Reihenfolge bei der Übermittlung der Text- und Audionachrichten können vom Service garantiert werden.

Beide der folgenden Antworten sind möglich. In beiden Fällen sendet der Service zwei Textnachrichten, die die Positionen der Markierungen im Binärdatenstrom angeben. Er sendet jedoch eine beliebige Anzahl von Binärnachrichten, die die Audioausgabe enthalten. Die Taktinformationen für eine Markierung treffen stets vor dem Audioblock ein, der die Position der Markierung enthält.

### Erste Beispielantwort

In der ersten Beispielantwort werden zwischen den Textnachrichten mehrere Audionachrichten gesendet.

```javascript
{
  "binary_streams": [
    {
      "content_type": "audio/wav"
    }
  ]
}
... Einer oder mehrere Blöcke mit binärer Audioausgabe.
    Die gesamte Audioausgabe geht der Markierung SIMPLE voran. ...
{
  "marks": [
    [
      "SIMPLE",
      0.7848991042702103
    ]
  ]
}
... Einer oder mehrere Blöcke mit binärer Audioausgabe,
    die der Markierung SIMPLE vorangehen oder auf sie folgen kann.
    Die gesamte Audioausgabe geht der Markierung EXAMPLE voran. ...
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... Einer oder mehrere Blöcke mit binärer Audioausgabe,
    die der Markierung EXAMPLE vorangehen oder auf sie folgen kann. ...
```
{: codeblock}

### Zweite Beispielantwort

In der zweiten Beispielantwort treffen die Textnachrichten vor allen Audionachrichten ein.

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
... Einer oder mehrere Blöcke mit binärer Audioausgabe ...
```
{: codeblock}
