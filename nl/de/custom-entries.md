---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-07"

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

# Angepasste Einträge erstellen und verwalten
{: #customWords}

Nachdem ein angepasstes Modell erstellt wurde, besteht der nächste Schritt darin, angepasste Einträge als Paare aus Wort und Umsetzung hinzuzufügen. Hiermit wird definiert, wie angegebene Wörter während der synthetischen Erstellung auszusprechen sind. Die Definitionen setzen die normalen Standardausspracheregeln des Service außer Kraft. Sie können gleichzeitig Umsetzungen für eines oder mehrere Wörter hinzufügen und abfragen; außerdem können Sie einzelne Wörter löschen, die Sie nicht mehr benötigen. Wenn Sie erst einmal mit der Anpassungsschnittstelle vertraut sind, kann die gleichzeitige Bearbeitung mehrerer Wörter bequemer sein, als einzelne Wörter nacheinander separat zu bearbeiten. Damit Sie eine der Methoden nutzen können, die eine Anpassungs-ID erforderlich machen, müssen Sie die Serviceberechtigungsnachweise der Serviceinstanz verwenden, die Eigner des angepassten Modells ist.
{: shortdesc}

## Einzelnes Wort zu einem angepassten Modell hinzufügen
{: #cuWordAdd}

Zum Hinzufügen eines einzelnen Paares aus Wort und Umsetzung zu einem angepassten Modell verwenden Sie die Methode `PUT /v1/customizations/{customization_id}/words/{word}`. Das Wort, das hinzugefügt werden soll, geben Sie in der URL der Methode an. Die Umsetzung für das Wort stellen Sie als JSON-Objekt mit einem einzelnen Attribut `translation` bereit. Wenn Sie eine neue Umsetzung für ein Wort hinzufügen, das in einem Modell bereits vorhanden ist, wird die bestehende Umsetzung für das Wort überschrieben.

Zum Bereitstellen einer Umsetzung können Sie die gleich klingende oder die phonetische Methode (oder auch eine Kombination dieser beiden Methoden) verwenden. Für phonetische Umsetzungen können Sie entweder das Format IPA (International Phonetic Alphabet) oder das {{site.data.keyword.IBM_notm}} Format SPR (Symbolic Phonetic Representation) verwenden. In den folgenden Beispielen werden verschiedene Methoden verwendet, um äquivalente Umsetzungen für das Wort `IEEE` zu einem angepassten Modell hinzuzufügen.

-   **Gleich klingend:** Bei dem folgenden Beispiel ist die gleich klingende Methode die einfachste Lösung:

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"I triple E\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **Phonetisch mit IPA:** IPA erfordert die Verwendung des Elements `<phoneme>`, bei dem das Attribut `alphabet` auf `ipa` gesetzt und das Attribut `ph` im IPA-Format definiert ist:

    <pre><code class="language-bash">  curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#712;a&#618;.t&#633;&#712;&#616;p&#601;l.&#712;i\\\"&gt;&lt;/phoneme&gt;\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"</code></pre>

-   **Phonetisch mit {{site.data.keyword.IBM_notm}} SPR:** SPR verwendet das Element `<phoneme>`, bei dem das Attribut `alphabet` auf `ibm` gesetzt und das Attribut `ph` im SPR-Format definiert ist:

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

## Mehrere Wörter zu einem angepassten Modell hinzufügen
{: #cuWordsAdd}

Mit der Methode `POST /v1/customizations/{customization_id}/words` können Sie ein Wort oder gleichzeitig mehrere Wörter zu einem angepassten Modell hinzufügen. Die Einträge, die zum angepassten Modell hinzugefügt werden sollen, geben Sie als JSON-Array mit Paaren aus Wort und Umsetzung an. Im folgenden Beispiel werden gängige gleich klingende Umsetzungen für die Wörter `NCAA` und `iPhone` zu einem angepassten
Modell hinzugefügt:

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

Der JSON-Inhalt, der im Anforderungshauptteil gesendet wird, sieht hierbei folgendermaßen aus:

```javascript
{
  "words": [
    {"word":"NCAA", "translation":"N C double A"},
    {"word":"iPhone", "translation":"I phone"}
  ]
}
```
{: codeblock}

Wie bereits im Abschnitt [Angepasstes Modell aktualisieren](/docs/services/text-to-speech/custom-models.html#cuModelsUpdate) erläutert wurde, können Sie Wörter zu einem angepassten Modell auch mithilfe der Methode `POST /v1/customizations/{customization_id}` hinzufügen. Im folgenden Beispiel werden mit dieser Methode dieselben beiden Wörter wie im vorherigen Beispiel hinzugefügt; die Methode nimmt keine Änderungen an den Metadaten des Modells vor. Mit Ausnahme der URL sind beide Methoden identisch.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

## Wörter zu einem angepassten Modell für Japanisch hinzufügen
{: #cuJapaneseAdd}

Für die Erstellung von Einträgen für Wörter in einem angepassten Modell für Japanisch gibt es zusätzliche Hinweise sowie ein Feld `part_of_speech`. Weitere Informationen hierzu enthält der Abschnitt [Mit Einträgen in Japanisch arbeiten](/docs/services/text-to-speech/custom-rules.html#jaNotes). Die Wortart für einen angepassten Eintrag in Japanisch geben Sie folgendermaßen an:

-   Übergeben Sie für die Methode `PUT /v1/customizations/{customization_id}/words/{word}` ein JSON-Objekt mit dem folgenden Format:

    ```javascript
    {
      "translation": "wert",
      "part_of_speech": "wert"
    }
    ```
    {: codeblock}

-   Übergeben Sie für die Methoden `POST /v1/customizations/{customization_id}/words` und `POST customizations/{customization_id}` ein JSON-Objekt, das etwa wie folgt aussieht:

    ```javascript
    {
      "words": [
        {
          "word": "wert",
          "translation": "wert",
          "part_of_speech": "wert"
        }
        . . .
      ]
    }
    ```
    {: codeblock}

In den folgenden Beispielen für die Methode `PUT /v1/customizations/{customization_id}/words/{word}` wird die als URL codierte Doppelbytezeichenfolge für `NY` in das Substantiv (`Mesi`) <code>&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;</code> umgesetzt (in Englisch `New York`). Falls diese angepasste Umsetzung nicht definiert ist, wird die Zeichenfolge als `enu wai` gelesen.

-   **Gleich klingend:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **Phonetisch mit IPA:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#626;&#623;&#720;&#106;&#111;&#720;&#107;&#623;\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **Phonetisch mit {{site.data.keyword.IBM_notm}} SPR:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

## Einzelnes Wort aus einem angepassten Modell abfragen
{: #cuWordQueryModel}

Mit der Methode `GET /v1/customizations/{customization_id}/words/{word}` können Sie aus einem angepassten Modell die Umsetzung für ein einzelnes Wort abfragen. Das Wort geben Sie in der URL der Methode an. Die Umsetzung wird so zurückgegeben, wie sie im angepassten Modell definiert ist (also gleich klingend oder phonetisch).

Im folgenden Modell wird aus einem angepassten Modell die Umsetzung des Wortes `IEEE` abgefragt:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

Falls im Modell für das Wort eine gleich klingende Umsetzung vorhanden ist, wird beim Beispiel die folgende JSON-Ausgabe zurückgegeben:

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

## Alle Wörter aus einem angepassten Modell abfragen
{: #cuWordsQueryModel}

Mit der Methode `GET /v1/customizations/{customization_id}/words` können Sie die Umsetzungen für alle Wörter anzeigen, die in einem angepassten Modell definiert sind. Im folgenden Beispiel werden mit der Methode die Einträge aus einem angepassten Modell aufgelistet, das gleich klingende Umsetzungen für drei Wörter enthält:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

Die Methode gibt ein JSON-Array mit den folgenden Daten zurück. Bei angepassten Modellen für Japanisch enthält die Ausgabe die Wortart für einzelne Wörter.

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

Wie bereits im Abschnitt [Angepasstes Modell abfragen](/docs/services/text-to-speech/custom-models.html#cuModelsQuery) erläutert wurde, können Sie die Methode `GET /v1/customizations/{customization_id}` ebenfalls verwenden, um sowohl die Metadaten als auch die Wörter für ein angepasstes Modell anzuzeigen:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

Die Methode gibt eine JSON-Ausgabe im folgenden Format zurück. Weil in diesem Beispiel und im vorherigen Beispiel dasselbe angepasste Modell angegeben sind, ist das Array der Wörter in der Ausgabe identisch.

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

## Wort aus einer Sprache abfragen
{: #cuWordsQueryLanguage}

Mit der Methode `GET /v1/pronunciation` können Sie die Aussprache für ein Wort abfragen. Geben Sie eine Stimme an, um die Aussprache in der Sprache dieser Stimme zu erhalten. Die Methode gibt die Aussprache standardmäßig basierend auf den normalen Ausspracheregeln des Service zurück. Sie können jedoch auch die Aussprache für ein angegebenes angepasstes Sprechmodell anfordern. Die Methode umfasst vier Abfrageparameter, mit denen Sie die Informationen angeben können, die zurückgegeben werden sollen:

-   Der erforderliche Parameter `text` gibt das Wort an, dessen Aussprache zurückgegeben werden soll.
-   Mit dem optionalen Parameter `voice` können Sie die Sprache der Aussprache angeben. Zur Angabe der gewünschten Sprache geben Sie eines der Stimmenmodelle an (z. B. `en-US_LisaVoice`); alle Stimmen derselben Sprache (z. B. `en-US`) geben dieselbe Aussprache zurück. Standardmäßig wird die Aussprache für amerikanisches Englisch zurückgegeben.
-   Mit dem optionalen Parameter `format` können Sie das phonetische Format der Aussprache angeben, entweder `ipa` oder `ibm`. Standardmäßig wird die Aussprache im IPA-Format zurückgegeben.
-   Mit dem optionalen Parameter `customization_id` können Sie ein angepasstes Sprechmodell angeben, für das die Aussprache zurückgegeben werden soll. Falls das Wort im angegebenen Sprechmodell nicht definiert ist, gibt der Service die Standardaussprache für die Sprache des Modells zurück. Lassen Sie den Parameter weg, um die Umsetzung für die angegebene Stimme ohne Anpassung anzuzeigen. Geben Sie nicht gleichzeitig eine Stimme und ein angepasstes Sprechmodell an.

Diese Methode ist hilfreich, weil Sie mit ihr ein Wort aus einer beliebigen Sprache abfragen können und sie darüber hinaus keine Einschränkungen für die Wörter vorgibt, die Sie anzeigen können, da für die Methode keine Anpassungs-ID benötigt wird. Als besonders praktisch kann sie sich erweisen, wenn Sie eine phonetische Umsetzung für ein neues Wort erstellen. In diesem Fall können Sie mit der Methode die Aussprache für ein vorhandenes Wort anfordern und diese dann als Grundlage für Ihre neue Umsetzung verwenden, was weitaus komfortabler als die völlig neue Erstellung einer Umsetzung ist.

Im folgenden Beispiel wird die Aussprache für das Wort `IEEE` im Standardformat 'IPA' angefordert.

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=IEEE"
```
{: pre}

<pre><code data-copy="false" class="language-javascript">{
  "pronunciation": ".&#712;a&#618; .&#712;i .&#712;i .&#712;i"
}</code></pre>

Im folgenden Beispiel wird eine gleich klingende Umsetzung für das Wort `IEEE` eingegeben und das phonetische Äquivalent im {{site.data.keyword.IBM_notm}} Format SPR angefordert. Die Anforderung einer phonetischen Aussprache für eine gleich klingende Umsetzung ist ein besonders interessantes Verfahren zur Erstellung einer phonetischen Umsetzung. Die Leerzeichen des Wortes sind beim Beispiel als URL codiert.

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

## Wort aus einem angepassten Modell löschen
{: #cuWordDelete}

Mit der Methode `DELETE /v1/customizations/{customization_id}/words/{word}` können Sie ein Wort aus einem angepassten Modell löschen. Das Wort, das gelöscht werden soll, geben Sie in der URL der Methode an. Sie können ausschließlich einzelne Wörter löschen; das Löschen mehrerer Wörter mit einer einzigen Methode ist nicht möglich.

Im folgenden Beispiel wird das Wort `IEEE` aus dem angegebenen angepassten Modell gelöscht:

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}
