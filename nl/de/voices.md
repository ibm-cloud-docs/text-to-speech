---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-25"

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

# Sprachen und Stimmen
{: #voices}

Der {{site.data.keyword.texttospeechfull}}-Service unterstützt eine Vielzahl von Sprachen, Stimmen und Dialekten. Der Service bietet für jede Sprache mindestens eine Frauenstimme an. Für einige Sprachen bietet der Service mehrere Stimmen an, darunter sowohl Männer- als auch Frauenstimmen. Jede Stimme verwendet den geeigneten Tonfall und die passende Satzmelodie für ihren Dialekt.
{: shortdesc}

Die `V2`-Stimmen, die mit dem Service bisher verfügbar waren, werden nicht mehr verwendet. Wenn Sie eine `V2`-Stimme in Ihrer Anwendung verwenden, verwendet der Service stattdessen automatisch die entsprechende `V3`-Stimme.
{: note}

## Unterstützte Sprachen und Stimmen
{: #languageVoices}

In Tabelle 1 sind die für jede Sprache und jeden Dialekt verfügbaren Stimmen einschließlich des Typs und Geschlechts aufgeführt. Alle Stimmen sind sowohl als [Standardstimmen](#standardVoices) als auch als [neuronale Stimmen](#neuralVoices) verfügbar. Falls Sie den optionalen Parameter `voice` in einer Anforderung weglassen, verwendet der Service die Standardstimme `en-US_MichaelVoice`. 

<table style="width:100%">
  <caption>Tabelle 1. Unterstützte Sprachen und Stimmen</caption>
  <tr>
    <th style="text-align:left">Sprache</th>
    <th style="text-align:center">Typ</th>
    <th style="text-align:center">Stimme</th>
    <th style="text-align:center">Geschlecht</th>
  </tr>
  <tr>
    <td style="text-align:left">Brasilianisches Portugiesisch</td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Kastilisches Spanisch</td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Französisch</td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Deutsch</td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
  <tr>
    <td style="text-align:left">Italienisch</td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Japanisch</td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>ja-JP_EmiV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Lateinamerikanisches Spanisch</td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Nordamerikanisches Spanisch</td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Britisches Englisch</td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Amerikanisches Englisch</td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>en-US_LisaVoice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Standard</td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
</table>

Die Stimmen `es-LA_SofiaVoice` und `es-US_SofiaVoice` sind im Wesentlichen identisch. Der größte Unterschied besteht in der Interpretation eines Dollarzeichens ($) durch die beiden Stimmen. Die lateinamerikanische Version verwendet den Begriff *pesos*, während die nordamerikanische Version den Begriff *d&oacute;lares* verwendet. Darüber hinaus kann es einige geringere Unterschiede zwischen den beiden Stimmen geben.
{: note}

### Standardstimmen
{: #standardVoices}

Standardstimmen enthalten keine Versionszeichenfolge (`V3`) in ihrem Namen (z. B. `pt-BR_IsabelaVoice` und `en-US_AllisonVoice`). Standardstimmen verwenden eine konkatenative Synthese, um Segmente (oder Einheiten) der aufgezeichneten Sprache zusammenzusetzen, um die angeforderte Audioausgabe zu generieren. Die Verkettungspunkte der aufgezeichneten Segmente führen manchmal zu Sprachdiskontinuitäten, die die Qualität und Natürlichkeit der resultierenden Sprache reduzieren können.

### Neuronale Stimmen
{: #neuralVoices}

Neuronale Stimmen umfassen eine Versionszeichenfolge (`V3`) in ihrem Namen (z. B. `pt-BR_IsabelaV3Voice` und `en-US_AllisonV3Voice`). Statt Segmentauswahl und Verkettung nutzt die neuronale Sprachtechnologie mehrere Deep Neural Networks (DNNs), um die akustischen (spektralen) Merkmale der Sprache vorherzusagen. Die DNNs werden für eine natürliche menschliche Sprache trainiert und erzeugen die daraus resultierende Audioausgabe aus den vorhergesagten akustischen Merkmalen.

Während der Synthese sagen die DNNs die Tonhöhe und die Phonemdauer (Satzrhythmus), die spektrale Struktur und die Signalform der Sprache voraus. Neuronale Stimmen erzeugen Sprache, die klar klingt und eine sehr natürlich klingende und geschmeidige Tonqualität hat. So haben neuronale Stimmen eine größere Konsistenz in der Gesamtqualität als Standardstimmen.

Weitere Informationen über die neuronale Sprachtechnologie des Service finden Sie unter:

-   Blogbeitrag [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   Forschungspapier [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

Die neuronalen Stimmen unterstützen keine der folgenden SSML-Elemente oder -Attribute:

-   Attribut `volume` des Elements `<prosody>`
-   Element `<express-as>`
-   Element `<voice-transformation>`

Sie können jedoch feststellen, dass diese SSML-Funktionen bei der Verwendung der neuronalen Stimmen nicht mehr benötigt werden. Außerdem können Sie mithilfe des Elements `<prosody>` anstelle des Elements `<voice-transformation>` Tonhöhe- und Geschwindigkeitsänderungen an den neuronalen Stimmen vornehmen. Weitere Informationen enthält der Abschnitt [Element 'prosody'](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element).

### Stimmenanpassung
{: #customizeVoice}

Bei der synthetischen Erstellung von Sprache aus Text wendet der Service sprachenabhängige Ausspracheregeln an, um die normale Schreibweise eines Wortes in eine phonetische Schreibweise zu konvertieren. Bei gängigen Wörtern funktionieren die Ausspracheregeln des Service gut, jedoch kann es bei unüblichen Wörtern wie beispielsweise Begriffen fremdsprachlichen Ursprungs, Personennamen sowie Abkürzungen oder Akronymen zu mangelhaften Ergebnissen kommen.

Falls das Wörterbuch Ihrer Anwendung solche Wörter enthält, können Sie mit der Anpassungsschnittstelle angeben, wie sie vom Service ausgesprochen werden sollen. Weitere Informationen enthält der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

Sie erstellen ein benutzerdefiniertes Sprechmodell für eine bestimmte Sprache, nicht für eine bestimmte Stimme. So kann ein benutzerdefiniertes Modell für seine angegebene Sprache mit jeder Standardstimme oder neuronalen Stimme verwendet werden.

## Stimme angeben
{: #specifyVoice}

Sowohl die HTTP-Methoden `GET` und `POST /v1/synthesize` als auch die WebSocket-Methode `/v1/synthesize` akzeptieren einen optionalen Abfrageparameter `voice`, mit dem die Stimme für die synthetisch erstellte Audioausgabe angegeben wird. Weitere Informationen enthalten die Abschnitte [HTTP-Schnittstelle](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) und [WebSocket-Schnittstelle](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).

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
    <td><code>customization_id</code><br/><em>      Optional
    </em></td>
    <td style="text-align:center">Abfrage</td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Stellt die GUID (global eindeutige ID) eines angepassten Sprechmodells
      bereit, das für die Sprache der angegebenen Stimme definiert ist. Wenn Sie eine Anpassungs-ID angeben, müssen Sie die Anforderung mit den Berechtigungsnachweisen für die Instanz des Service ausführen, der Eigner des angepassten Modells ist. </td>
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

Die Attribute des zusätzlichen Feldes `customization` liefern Informationen wie beispielsweise die GUID, den Namen, die Sprache und die Beschreibung des angepassten Sprechmodells. Außerdem zeigen sie die Berechtigungsnachweise des Modelleigners, das Datum und die Uhrzeit für die Erstellung des Modells sowie das Datum und die Uhrzeit für die letzte Änderung des Modells.
