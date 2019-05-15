---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28"

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

# Sprachen und Stimmen
{: #voices}

Der {{site.data.keyword.texttospeechfull}}-Service unterstützt eine Vielzahl von Sprachen, Stimmen und Dialekten. Für jede Sprache bietet der Service mindestens eine Männer- oder Frauenstimme, manchmal auch beides. Jede Stimme verwendet den geeigneten Tonfall und die passende Satzmelodie für ihren Dialekt.
{: shortdesc}

## Unterstützte Sprachen und Stimmen
{: #languageVoices}

In Tabelle 1 sind die für jede Sprache und jeden Dialekt verfügbaren Stimmen einschließlich des Geschlechts aufgeführt. Falls Sie den optionalen Parameter `voice` in einer Anforderung weglassen, verwendet der Service standardmäßig die Stimme `en-US_MichaelVoice`. Im Abschnitt [Technologien der Sprachsynthese](#technologiesVoices) erfahren Sie, warum der Service von manchen Stimmen zwei Versionen anbietet.

Ein Problem bei der Bereitstellung der `V2`-Stimmen verursacht gegenwärtig Hintergrundgeräusche bei der synthetisch erstellten Sprache. Weitere Informationen enthält der Abschnitt [Bekannte Einschränkungen](/docs/services/text-to-speech/release-notes.html#limitations).
{: note}

<table style="width:90%">
  <caption>Tabelle 1. Unterstützte Sprachen und Stimmen</caption>
  <tr>
    <th style="text-align:left">Sprache</th>
    <th style="text-align:center">Stimme</th>
    <th style="text-align:center">Geschlecht</th>
  </tr>
  <tr>
    <td style="text-align:left">Brasilianisches Portugiesisch</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Kastilisches Spanisch</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Französisch</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Deutsch</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code><br/>
      <code>de-DE_BirgitV2Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code><br/>
      <code>de-DE_DieterV2Voice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
  <tr>
    <td style="text-align:left">Italienisch</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code><br/>
      <code>it-IT_FrancescaV2Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Japanisch</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Lateinamerikanisches Spanisch</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Nordamerikanisches Spanisch</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Britisches Englisch</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Amerikanisches Englisch</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code><br/>
      <code>en-US_AllisonV2Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaVoice</code><br/>
      <code>en-US_LisaV2Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code><br/>
      <code>en-US_MichaelV2Voice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
</table>

Die Stimmen `es-LA_SofiaVoice` und `es-US_SofiaVoice` sind im Wesentlichen identisch. Der größte Unterschied besteht in der Interpretation eines Dollarzeichens ($) durch die beiden Stimmen. Die lateinamerikanische Version verwendet den Begriff *pesos*, während die nordamerikanische Version den Begriff *d&oacute;lares* verwendet. Darüber hinaus kann es einige geringere Unterschiede zwischen den beiden Stimmen geben.
{: note}

### Technologien der Sprachsynthese
{: #technologiesVoices}

Der Service stellt bei einigen Stimmen zwei Versionen zur Verfügung, z. B. `en-US_AllisonVoice` und `en-US_AllisonV2Voice`. Der Hauptunterschied zwischen den beiden Versionen beruht auf der Technologie, die der Service für die synthetische Erstellung von Sprache verwendet:

-   Die *konkatenative Synthese* setzt Segmente (oder Einheiten) von aufgezeichneter Sprache zusammen, um die angeforderte Audioausgabe zu generieren. Die hierbei generierte Audioausgabe klingt klarer, bisweilen führen die Verkettungspunkte der aufgezeichneten Segmente jedoch zu Verzerrungen in der Sprache.

    Stimmen, deren Namen die Zeichenfolge `V2` nicht enthalten
    (z. B. `en-US_AllisonVoice`) basieren auf der
    konkatenativen Synthese.
-   Die *Deep-Learning-Synthese* verwendet DNN (Deep Neural Network), um aus dem angegebenen Text synthetisch Sprache zu erstellen. Statt aufgezeichnete Tonsegmente miteinander zu verketten, stützt sich dieser Ansatz auf maschinelles Lernen, um ein DNN anhand von aufgezeichneten Sprachdaten zu trainieren. Die auch 'DNN-basiert' genannte Deep-Learning-Synthese erzeugt Audioausgabe mit einem natürlicheren Satzrhytmus und einer konsistenteren Gesamtqualität.

    Stimmen, deren Namen die Zeichenfolge `V2` enthalten (z. B. `en-US_AllisonV2Voice`) sind neuere Stimmen, die die DNN-basierte Synthese verwenden.

Sie müssen mit den neuen Stimmen experimentieren, bevor Sie sie für Ihre Anwendung übernehmen. Die beiden Technologien erzeugen Audioausgabe mit unterschiedlicher Signalqualität, weshalb die neuen Stimmen möglicherweise nicht für alle Anwendungen die bessere Wahl sind. Außerdem werden die folgenden SSML-Elemente bzw. -Attribute von den DNN-basierten Stimmen nicht unterstützt:

-   Attribut `volume` des Elements `<prosody>`
-   Element `<express-as>`
-   Element `<voice-transformation>`

Falls Ihre Anwendung diese Elemente verwendet, nutzen Sie weiterhin die Stimmen, die auf der konkatenativen Synthese basieren.

### Stimmenanpassung
{: #customizeVoice}

Bei der synthetischen Erstellung von Sprache aus Text wendet der Service sprachenabhängige Ausspracheregeln an, um die normale Schreibweise eines Wortes in eine phonetische Schreibweise zu konvertieren. Bei gängigen Wörtern funktionieren die Ausspracheregeln des Service gut, jedoch kann es bei unüblichen Wörtern wie beispielsweise Begriffen fremdsprachlichen Ursprungs, Personennamen sowie Abkürzungen oder Akronymen zu mangelhaften Ergebnissen kommen.

Falls das Wörterbuch Ihrer Anwendung solche Wörter enthält, können Sie mit der Anpassungsschnittstelle angeben, wie sie vom Service ausgesprochen werden sollen. Weitere Informationen enthält der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech/custom-intro.html).

## Stimme angeben
{: #specifyVoice}

Sowohl die HTTP-Methoden `GET` und `POST /v1/synthesize` als auch die WebSocket-Methode `/v1/synthesize` akzeptieren einen optionalen Abfrageparameter `voice`, mit dem die Stimme für die synthetisch erstellte Audioausgabe angegeben wird. Weitere Informationen enthalten die Abschnitte [HTTP-Schnittstelle](/docs/services/text-to-speech/http.html) und [WebSocket-Schnittstelle](/docs/services/text-to-speech/websockets.html).

Der Service legt dem Verständnis der Sprache für den Eingabetext die angegebene Stimme zugrunde. Achten Sie darauf, eine Stimme anzugeben, die mit der Sprache des Eingabetextes übereinstimmt. Falls Sie beispielsweise die Stimme für Französisch (`fr-FR_ReneeVoice`) angeben, geht der Service davon aus, dass der Eingabetext in Französisch geschrieben ist. Wenn Sie Text übergeben, der nicht in der Sprache der Stimme geschrieben ist (z. B. englischer Text für die französische Stimme), liefert der Service möglicherweise keine sinnvollen Ergebnisse.

## Alle verfügbaren Stimmen auflisten
{: #listVoices}

Die Methode `GET /v1/voices` listet Informationen zu allen verfügbaren Stimmen auf. Sie verwendet keine Argumente und gibt ein JSON-Array namens `voices` zurück. Das Array enthält für jede Stimme ein separates Objekt.

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaVoice",
      "language": "en-US",
      "gender": "female",
      "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
      "description": "Lisa: American English female voice.",
      "customizable": true,
      "supported_features": {
        "voice_transformation": true,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

Die Felder der Objekte 'voice' liefern die folgenden Informationen:

-   Das Feld `name` gibt eine ID für die Stimme an (z. B. `en-US_LisaVoice`). Geben Sie diesen Wert für den Parameter `voice` der Methode `/v1/synthesize` an.
-   Das Feld `language` gibt die Sprache und die Region der Sprache an (z. B. `en-US`).
-   Das Feld `gender` gibt an, ob es sich um eine Männerstimme (`male`) oder um eine Frauenstimme (`female`) handelt.
-   Das Feld `url` gibt die URL für die Stimme an.
-   Das Feld `description` bietet eine Kurzbeschreibung der Stimme.
-   Das Feld `customizable` enthält einen booleschen Wert dafür, ob die Stimme mit der Anpassungsschnittstelle des Service angepasst werden kann. (Dieses Feld, das dieselben Informationen wie das Feld `custom_pronunciation` bereitstellt, wird aus Gründen der Abwärtskompatibilität beibehalten.)
-   Das Feld `supported_features` beschreibt die zusätzlichen Servicefunktionen, die von der Stimme unterstützt werden:
    -   Der boolesche Wert für `voice_transformation` gibt an, ob die Stimme mit dem SSML-Element `<voice-transformation>` umgewandelt werden kann.
    -   Der boolesche Wert für `custom_pronunciation` gibt an, ob die Stimme mit der Anpassungsschnittstelle des Service angepasst werden kann.

## Bestimmte Stimme auflisten
{: #listVoice}

Die Methode `GET /v1/voices` listet Informationen zu einer bestimmten Stimme auf. Sie akzeptiert zwei Parameter.

<table>
  <caption>Tabelle 2. Parameter der Methode <code>voices</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parameter</th>
    <th style="text-align:center; width:12%">Typ</th>
    <th style="text-align:center; width:12%">Datentyp</th>
    <th style="text-align:left">Beschreibung</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Erforderlich</em></td>
    <td style="text-align:center">Pfad</td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Gibt die Stimme an, für die Informationen zurückgegeben werden sollen. Sie
      geben eine Stimme durch ihren Namen an (z. B. <code>en-US_LisaVoice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Optional</em></td>
    <td style="text-align:center">Abfrage</td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Stellt die GUID (global eindeutige ID) eines angepassten Sprechmodells
      bereit, das für die angegebene Stimme definiert ist. Falls Sie
      eine Anpassungs-ID einbeziehen, müssen Sie die Methode mit den
      Serviceberechtigungsnachweisen für den Eigner des angepassten Modells
      aufrufen.</td>
  </tr>
</table>

Wenn Sie den Parameter `customization_id` nicht angeben, gibt die Methode die JSON-Ausgabe für die angegebene Stimme zurück; diese ist identisch mit den Informationen, die für eine Stimme durch die Methode `GET /v1/voices` zurückgegeben werden. Falls Sie einen Wert für `customization_id` angeben, enthält die Ausgabe ein Feld `customization`, in dem Informationen zum angegebenen angepassten Sprechmodell bereitgestellt werden.

```javascript
{
  "name": "en-US_LisaVoice",
  "language": "en-US",
  "gender": "female",
  "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
  "description": "Lisa: American English female voice.",
  "customizable": true,
  "supported_features": {
    "voice_transformation": true,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

Die Attribute des zusätzlichen Feldes `customization` liefern Informationen wie beispielsweise die GUID, den Namen, die Sprache und die Beschreibung des angepassten Sprechmodells. Außerdem zeigen sie die Serviceberechtigungsnachweise des Modelleigners, das Datum und die Uhrzeit für die Erstellung des Modells sowie das Datum und die Uhrzeit für die letzte Änderung des Modells.
