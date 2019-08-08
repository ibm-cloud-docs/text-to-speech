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

# Angepasste Sprechmodelle erstellen und verwalten
{: #customModels}

Wenn Sie mit einem angepassten Modell arbeiten wollen, müssen Sie das Modell zunächst erstellen. Nachdem Sie das Modell erstellt haben, können Sie es verwalten, indem Sie seine Metadaten und Einträge abfragen oder aktualisieren bzw. das Modell löschen, wenn Sie es nicht mehr benötigen. In diesem Abschnitt können Sie sich vor dem Einstieg über die allgemeine Verwendung von angepassten Modellen informieren.
{: shortdesc}

## Hinweise zur Verwendung
{: #customGuidelines}

Beachten Sie bei der Arbeit mit der Anpassungsschnittstelle die folgenden Richtlinien.

### Eigentumsrecht an angepassten Sprechmodellen
{: #customOwner}

Eigner eines angepassten Sprechmodells ist die Instanz des {{site.data.keyword.texttospeechshort}}-Service, deren Berechtigungsnachweise zur Erstellung des Modells verwendet wurden. Bei jeder Arbeit mit dem angepassten Modell müssen Sie die Berechtigungsnachweise für diese Serviceinstanz mit Methoden der Anpassungsschnittstelle verwenden.

Alle für dieselbe Instanz des {{site.data.keyword.texttospeechshort}}-Service angeforderten Berechtigungsnachweise nutzen gemeinsam den Zugriff auf alle angepassten Modelle, die für die Serviceinstanz erstellt werden. Um den Zugriff auf ein angepasstes Modell einzuschränken, erstellen Sie eine separate Instanz des Service und verwenden Sie ausschließlich die Berechtigungsnachweise für diesen Service, um das Modell zu erstellen und mit ihm zu arbeiten. Berechtigungsnachweise für andere Services haben keinen Einfluss auf das angepasste Modell.

Ein Vorteil der gemeinsamen Nutzung des Eigentumsrechts durch mehrere Berechtigungsnachweise besteht darin, dass Sie beispielsweise eine Reihe von Berechtigungsnachweisen stornieren können, falls diese beeinträchtigt werden. Anschließend können Sie neue Berechtigungsnachweise für die gleiche Serviceinstanz erstellen und trotzdem das Eigentumsrecht an angepassten Modellen und den Zugriff auf angepasste Modelle verwalten, die mit den ursprünglichen Berechtigungsnachweisen erstellt wurden.

### Protokollierung von Anforderungen und Datenschutz
{: #customLogging}

Wie der Service die Anforderungsprotokollierung für Aufrufe der Anpassungsschnittstelle abwickelt, ist von der Anforderung abhängig:

-   Der Service protokolliert *keine* Daten (Wörter und Umsetzungen), die zum Erstellen von angepassten Sprechmodellen verwendet werden. Wenn Sie die Anpassungsschnittstelle verwenden, um die Wörter und Umsetzungen in einem angepassten Modell zu verwalten, müssen Sie nicht den Anforderungsheader `X-Watson-Learning-Opt-Out` festlegen. Ihre Trainingsdaten werden in keinem Fall verwendet, um die Grundmodelle des Service zu verbessern.
-   Der Service *protokolliert* Daten, wenn ein angepasstes Modell im Zusammenhang mit einer Anforderung für die synthetische Erstellung genutzt wird. Wenn Sie die Protokollierung von Syntheseanforderungen verhindern wollen, müssen Sie den Anforderungsheader `X-Watson-Learning-Opt-Out` auf `true` setzen.

Weitere Informationen enthält der Abschnitt [Anforderungsprotokollierung für {{site.data.keyword.watson}}-Services steuern](/docs/services/watson?topic=watson-gs-logging-overview).

### Informationssicherheit
{: #customSecurity}

Der Service ermöglicht Ihnen die Zuordnung einer Kunden-ID zu Daten, die für angepasste Sprechmodelle hinzugefügt oder aktualisiert werden. Sie können eine Kunden-ID zu angepassten Wörtern zuordnen, indem Sie den Header `X-Watson-Metadata` mit den folgenden Methoden übergeben:

-   `POST /v1/customizations/{customization_id}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word}`

Bei Bedarf können Sie dann die Daten, die der Kunden-ID zugeordnet sind, mit der Methode `DELETE /v1/user_data` löschen. Weitere Informationen finden Sie unter [Informationssicherheit](/docs/services/text-to-speech?topic=text-to-speech-information-security).

## Angepasstes Modell erstellen
{: #cuModelsCreate}

Zum Erstellen eines neuen angepassten Modells verwenden Sie die Methode `POST /v1/customizations`. Bei seiner erstmaligen Erstellung ist ein neues Modell immer leer. Sie müssen andere Methoden verwenden, um es mit Paaren aus Wort und Umsetzung zu füllen. Eigner des neuen angepassten Modells ist die Serviceinstanz, deren Serviceberechtigungsnachweise zur Erstellung des Modells verwendet werden. Weitere Informationen finden Sie unter [Eigentumsrecht an angepassten Sprechmodellen](#customOwner).

Mit dem Hauptteil der Anforderung übergeben Sie die folgenden Attribute als JSON-Objekt.

<table>
  <caption>Tabelle 1. Parameter der Methode <code>POST /v1/customizations</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parameter</th>
    <th style="text-align:center; width:12%">Datentyp</th>
    <th style="text-align:left">Beschreibung</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>Erforderlich</em></td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Ein benutzerdefinierter Name für das neue angepasste Modell. Mit dem
      Namen wird das Modell zur leichteren Identifizierung gekennzeichnet. Der
      Name muss unter allen angepassten Modellen, deren Eigner Sie sind,
      eindeutig sein.
    </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>      Optional
    </em></td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Eine ID für die Sprache des angepassten Modells. Der Standardwert
      ist <code>en-US</code> für amerikanisches Englisch. Das benutzerdefinierte Modell kann mit einer beliebigen (standardmäßigen oder neuronalen) Sprache verwendet werden, das in der angegebenen Sprache verfügbar ist.     </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>      Optional
    </em></td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Eine Beschreibung des neuen Modells. Eine Beschreibung ist
      zwar optional, wird aber dringend empfohlen.
    </td>
  </tr>
</table>

Der folgende Beispielbefehl `curl` erstellt ein neues angepasstes Modell namens `curl Test`. Der Header `Content-Type` gibt `application/json` als Eingabetyp an.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test\", \"language\":\"en-US\", \"description\":\"Customization test via curl\"}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

Die Methode gibt ein JSON-Objekt zurück, das eine global eindeutige ID (GUID) für das neue Modell enthält. Die GUID wird im Parameter `customization_id` bei Aufrufen für den Zugriff auf das Modell verwendet, beispielsweise zum Abfragen, Ändern und Verwenden des Modells und seiner Wörter.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

## Angepasstes Modell abfragen
{: #cuModelsQuery}

Mit der Methode `GET /v1/customizations/{customization_id}` können Sie Informationen zu einem vorhandenen angepassten Modell abfragen. Dies ist die direkteste Möglichkeit, um alle Informationen zu einem Modell anzuzeigen (sowohl seine Metadaten als auch die in ihm enthaltenen Paare aus Wort und Umsetzung).

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

Die Methode gibt ihre Ergebnisse als JSON-Objekt mit dem folgenden Format zurück:

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T18:12:31.743Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T18:12:31.743Z",
  "words": []
}
```
{: codeblock}

Neben den Informationen, die bei der Erstellung des Modells eingegeben wurden, enthält die Ausgabe die Berechtigungsnachweise für den Eigner des Modells, die Sprache des Modells und die Zeitpunkte für die Erstellung sowie die letzte Änderung des Modells. Da das Modell seit seiner Erstellung nicht geändert wurde, sind die beiden Zeitangaben im Beispiel identisch.

Die Ausgabe enthält außerdem ein Array namens `words`, in dem die angepassten Einträge des Modells aufgelistet sind. Da das Modell noch aktualisiert werden muss, ist das Array im Beispiel leer.

## Alle angepassten Modelle abfragen
{: #cuModelsQueryAll}

Mit der Methode `GET /v1/customizations` können Sie Informationen zu allen angepassten Modellen anzeigen, deren Eigner Sie sind:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

Die Methode gibt für jedes angepasste Modell, dessen Eigner der anfordernde Benutzer ist, ein Objekt in einem JSON-Array zurück. Die Berechtigungsnachweise des Eigners sind im Feld `owner` angegeben.

```javascript
{
  "customizations": [
    {
      "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T19:15:17.926Z",
      "name": "curl Test",
      "language": "en-US",
      "description": "Customization test via curl",
      "last_modified": "2016-07-15T19:15:17.926Z"
    },
    {
      "customization_id": "63f5807f-a4f2-5766-914e-7abb1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T18:12:31.743Z",
      "name": "curl Test Two",
      "language": "en-US",
      "description": "Second customization test via curl",
      "last_modified": "2016-07-15T18:23:50.912Z"
    }
  ]
}
```
{: codeblock}

Die Zeitangaben bei `created` und `last_modified` für das erste Modell sind identisch, weil es noch aktualisiert werden muss. Bei dem zweiten Modell sind die Zeitangaben unterschiedlich, woraus hervorgeht, dass das Modell nach seiner erstmaligen Erstellung geändert wurde. Die für die Modelle definierten angepassten Einträge sind in den Informationen nicht enthalten.

## Angepasstes Modell aktualisieren
{: #cuModelsUpdate}

Mit der Methode `POST /v1/customizations/{customization_id}` können Sie Informationen zu einem angepassten Modell aktualisieren. Die Aktualisierungen geben Sie in Form eines JSON-Objekts an. Mit dieser Methode können Sie nicht nur den Namen und die Beschreibung des Modells ändern, sondern auch Paare aus Wort und Umsetzung im Modell hinzufügen oder ändern. Die Sprache eines Modells kann nach seiner Erstellung nicht mehr geändert werden.

Im folgenden Beispiel werden der Name und die Beschreibung eines angepassten Modells aktualisiert. Mit dem Parameter `words` wird ein leeres JSON-Array gesendet; dies gibt an, dass die Einträge des Modells nicht geändert werden sollen.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test Update\", \"description\":\"Customization test update via curl\", \"words\":[]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

Weitere Informationen zum Aktualisieren der Wörter in einem Modell finden Sie im Abschnitt [Mehrere Wörter zu einem angepassten Modell hinzufügen](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsAdd).

## Angepasstes Modell löschen
{: #cuModelsDelete}

Mit der Methode `DELETE /v1/customizations/{customization_id}` können Sie ein angepasstes Modell löschen, das Sie nicht mehr benötigen. Verwenden Sie diese Methode nur, wenn Sie ganz sicher sind, dass Sie das Modell nicht mehr verwenden müssen, weil das Modell mit dieser Methode dauerhaft gelöscht wird.

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}
