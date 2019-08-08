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

# HTTP-Schnittstelle
{: #usingHTTP}

Um mit der HTTP-REST-Schnittstelle des {{site.data.keyword.texttospeechfull}}-Service synthetisch Sprache aus Text zu erstellen, rufen Sie die Methode `GET` oder `POST /v1/synthesize` auf. Sie geben den Text an, aus dem synthetisch Sprache erstellt werden soll, sowie die Stimme und das Format für die gesprochene Audioausgabe. Sie können auch ein angepasstes Sprechmodell angeben, das für die Anforderung verwendet werden soll.
{: shortdesc}

Weitere Informationen zur HTTP-Schnittstelle enthält die [API-Referenz](https://{DomainName}/apidocs/text-to-speech){: external}.

## Audioausgabe synthetisch aus Text erstellen
{: #synthesize}

Um aus Text synthetisch eine Audioausgabe zu erstellen, rufen Sie eine der beiden Versionen für die Methode `/v1/synthesize` des Service auf:

-   Die Methode `GET /v1/synthesize` akzeptiert den Text, aus dem synthetisch Audioausgabe erstellt werden soll, als erforderlichen Abfrageparameter `text`. Die maximale Größe der Anforderung beträgt 8 KB, was den Eingabetext, den gegebenenfalls angegebenen SSML-Code sowie die URL und die Header beinhaltet.
-   Die Methode `POST /v1/synthesize` akzeptiert den Text, aus dem synthetisch Audioausgabe erstellt werden soll, als JSON-Konstrukt im erforderlichen Hauptteil der Anforderung. Die maximale Größe der Anforderung beträgt 8 KB für die URL und Header und 5 KB für den Eingabetext, der im Hauptteil der Anforderung gesendet wird. Die Begrenzung von 5 KB bezieht jeden gegebenenfalls angegebenen SSML-Code ein.

Bei den beiden Versionen der Methode `/v1/synthesize` werden die folgenden Parameter einheitlich verwendet:

<table>
  <caption>Tabelle 1. Parameter der Methoden <code>/v1/synthesize</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parameter</th>
    <th style="text-align:center; width:12%">Typ</th>
    <th style="text-align:center; width:12%">Datentyp</th>
    <th style="text-align:left">Beschreibung</th>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>      Optional
    </em></td>
    <td style="text-align:center">Abfrage</td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Gibt das angeforderte Audioformat oder den MIME-Typ an, in dem der
      Service die Audiodaten zurückgeben soll. Diesen Wert können Sie auch im
      HTTP-Anforderungsheader <code>Accept</code> angeben. Codieren Sie das
      Argument für den Abfrageparameter `accept` als URL. Weitere Informationen finden Sie unter [Audioformate](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>      Optional
    </em></td>
    <td style="text-align:center">Abfrage</td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Gibt die Stimme an, von der der Text in der Audioausgabe
      gesprochen werden soll. Mit der Methode <code>/v1/voices</code>
      können Sie die aktuelle Liste der unterstützten Stimmen
      abrufen. Die Standardstimme ist <code>en-US_MichaelVoice</code>. Weitere Informationen finden Sie unter
      [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>      Optional
    </em></td>
    <td style="text-align:center">Abfrage</td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Gibt eine GUID (global eindeutige ID) für ein angepasstes Sprechmodell
      an, das für die Synthese verwendet werden soll. Ein angegebenes
      angepasstes Sprechmodell funktioniert nur dann, wenn es mit der Sprache
      der Stimme übereinstimmt, die für die Synthese verwendet wird. Wenn Sie eine Anpassungs-ID angeben, müssen Sie die Anforderung mit den Berechtigungsnachweisen für die Instanz des Service ausführen, der Eigner des angepassten Modells ist. Lassen Sie
      den Parameter weg, um die angegebene Stimme ohne Anpassung zu verwenden. Weitere Informationen enthält der Abschnitt
      [Wissenswertes
      über die Anpassung](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
    </td>
  </tr>
</table>

Zusammen mit einer Anforderung für die synthetische Erstellung können Sie auch die folgenden Anforderungsheader verwenden, die für alle {{site.data.keyword.watson}}-Services verfügbar sind:

-   Der Header `X-Watson-Learning-Opt-Out` gibt an, ob der Service Anforderungs- und Antwortdaten protokolliert, um den Service für künftige Benutzer zu verbessern. Wenn Sie verhindern möchten, dass IBM zur allgemeinen Serviceverbesserung auf Ihre Daten zugreift, geben Sie den Wert <code>true</code> für den Parameter an. Weitere Informationen enthält der Abschnitt [Anforderungsprotokollierung für {{site.data.keyword.watson}}-Services steuern](/docs/services/watson?topic=watson-gs-logging-overview).
-   Der Header `X-Watson-Metadata` ordnet die Daten, die mit einer Anforderung übergeben werden, einer Kunden-ID zu. Weitere Informationen finden Sie unter [Informationssicherheit](/docs/services/text-to-speech?topic=text-to-speech-information-security).

Falls die Eingabe für die Methode `/v1/synthesize` einen ungültigen Abfrageparameter oder ein ungültiges JSON-Feld enthält, gibt der Service einen Antwortheader namens `Warnings` zurück, in dem jedes ungültige Argument beschrieben und aufgeführt ist. Die Anforderung wird ungeachtet der Warnungen erfolgreich ausgeführt.
{: note}

## Eingabetext angeben
{: #input}

Beide Methoden `GET` und `POST /v1/synthesize` akzeptieren als Eingabe einfachen Text oder Text, der mit SSML annotiert ist. Die beiden Versionen unterscheiden sich in erster Linie dadurch, wie Sie den Text angeben, aus dem synthetisch Sprache erstellt werden soll:

-   Die Methode `GET /v1/synthesize` akzeptiert Eingabetext, der durch den Abfrageparameter `text` angegeben wird. Die Eingabe geben Sie als einfachen Text oder als SSML-Text an, jeweils in URL-Codierung.
-   Die Methode `POST /v1/synthesize` akzeptiert Eingabetext im Hauptteil der Anforderung. Den Eingabetext geben Sie mit dem folgenden einfachen JSON-Konstrukt an, das einfachen Text oder SSML-Text kapselt. Außerdem müssen Sie den Wert `application/json` für den Header `Content-Type` angeben.

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

Die Methoden `GET` und `POST` bieten zwar eine äquivalente Funktionalität, die Übergabe von Eingabetext an den Service mit der Methode `POST` bietet jedoch immer eine größere Sicherheit. Eine `POST`-Anforderung übergibt Eingabe im Hauptteil der Anforderung, wohingegen die Daten bei einer `GET`-Anforderung in der URL offengelegt werden.

## SSML-Eingabe angeben
{: #ssml-http}

SSML (Speech Synthesis Markup Language) ist eine XML-basierte Markup-Sprache, die zur Bereitstellung von Annotationen bei Text für Sprachsyntheseanwendungen wie dem {{site.data.keyword.texttospeechshort}}-Service konzipiert ist. Mithilfe der SSML-Elemente und ihrer Attribute können Sie die Synthese und die resultierende Audioausgabe stärker steuern.

Weitere Informationen zum Annotieren von Eingabetext mit SSML enthält der Abschnitt [SSML verwenden](/docs/services/text-to-speech?topic=text-to-speech-ssml). In der Dokumentation sind die vom Service unterstützten SSML-Elemente und -Attribute aufgeführt. Außerdem sind dort die Erweiterungen des Service für die Expressivität und die Stimmenumwandlung dokumentiert.

## XML-Steuerzeichen mit Escapezeichen versehen
{: #escape}

Da Sie Eingabetext übergeben können, der XML-basierte SSML-Annotationen enthält, validiert der Service die gesamte Eingabe, um sicherzustellen, dass alle SSML-Angaben gültig und korrekt formatiert sind. Aus diesem Grund müssen Sie alle im Eingabetext vorhandenen XML-Steuerzeichen mit Escapezeichen versehen, und zwar unabhängig davon, ob die Eingabe SSML enthält. Verwenden Sie anstelle der angegebenen Zeichen die äquivalenten Escapezeichenfolgen oder Zeichencodierungen, die in Tabelle 2 aufgeführt sind.

<table style="width:80%">
  <caption>Tabelle 2. Escapezeichen für XML-Steuerzeichen</caption>
  <tr>
    <th style="text-align:center; vertical-align:bottom; width:40%">Zeichen</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">Escapezeichenfolgen</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">Zeichencodierung</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>&quot;</code><br/>(doppelte Anführungszeichen)</td>
    <td style="text-align:center"><code>&amp;quot;</code></td>
    <td style="text-align:center"><code>&amp;#34;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>'</code><br/>(Hochkomma oder einfaches Anführungszeichen)</td>
    <td style="text-align:center"><code>&amp;apos;</code></td>
    <td style="text-align:center"><code>&amp;#39;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&amp;</code><br/>(Et-Zeichen)</td>
    <td style="text-align:center"><code>&amp;amp;</code></td>
    <td style="text-align:center"><code>&amp;#38;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&lt;</code><br/>(linke spitze Klammer)</td>
    <td style="text-align:center"><code>&amp;lt;</code></td>
    <td style="text-align:center"><code>&amp;#60;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&gt;</code><br/>(rechte spitze Klammer)</td>
    <td style="text-align:center"><code>&amp;gt;</code></td>
    <td style="text-align:center"><code>&amp;#62;</code></td>
  </tr>
</table>

Weitere Informationen zur Validierung von Eingabetext durch den Service finden Sie unter [SSML-Validierung](/docs/services/text-to-speech?topic=text-to-speech-ssml#errors).

## Beispiele für Eingabetext
{: #httpExamples}

Die folgenden Beispiele zeigen, wie Eingabetext mit einer der beiden Methoden der HTTP-Schnittstelle angegeben wird. Sie veranschaulichen außerdem, wie XML-Steuerzeichen mit Escapezeichen versehen werden. Zur besseren Lesbarkeit enthalten die Beispiele Zeilenumbrüche. Nehmen Sie in den tatsächlichen Eingabetext *keine* Zeilenumbrüche auf.

### Beispieleingabe mit GET-Anforderung
{: #getExamples}

Die folgenden Beispiele übergeben eine URL-codierte Eingabe mit dem Abfrageparameter `text` der Methode `GET /v1/synthesize`:

-   Einfacher Eingabetext:

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   SSML-Eingabetext:

    ```
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3C
    break%20time=%225s%22/%3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another
    %20sentence.%3C/s%3E%3Cs%3EFinally,%20this%20is%20the%20last%20sentence.
    %3C/s%3E%3C/p%3E%22
    ```
    {: codeblock}

### Beispieleingabe mit POST-Anforderung
{: #postExamples}

Die folgenden Beispiele übergeben eine Eingabe im Hauptteil der Methode `POST /v1/synthesize`:

-   Einfacher Eingabetext:

    ```javascript
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   SSML-Eingabetext:

    ```javascript
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/>
        paragraph.</s><s>Here is another sentence.</s><s>Finally, this is
        the last sentence.</s></p>"
    }
    ```
    {: codeblock}

### Beispieleingabe mit XML-Steuerzeichen
{: #xmlExamples}

Die folgenden Beispiele senden zwei Sätze an die Methode `POST /v1/synthesize`. In den Beispielen sind die eingebetteten XML-Zeichen ordnungsgemäß mit Escapezeichen versehen.

```
"What have I learned?" he asked. "Everything!"
```
{: codeblock}

-   Einfacher Eingabetext:

    ```javascript
    {
      "text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
    }
    ```
    {: codeblock}

-   SSML-Eingabetext:

    ```javascript
    {
      "text": "<s>&quot;What have I learned?&quot; he asked.
        &quot;<express-as type=\"GoodNews\">Everything!</express-as>&quot;</s>"
    }
    ```
    {: codeblock}
