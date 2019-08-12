---

copyright:
  years: 2019
lastupdated: "2018-06-04"

subcollection: text-to-speech-data

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

# Regole per la creazione di voci personalizzate
{: #rules}

Per popolare un modello personalizzato con voci personalizzate (coppie di parole/traduzioni), si applicano le seguenti regole e linee guida.

## Numero massimo di voci personalizzate

Un singolo modello personalizzato non può includere più di 20.000 voci personalizzate.

## Codifica dei caratteri

Il servizio accetta la codifica dei caratteri ASCII e UTF-8 per le voci di *parola* e *traduzione*. Per le traduzioni, utilizza la codifica ASCII per le notazioni SPR e la codifica UTF-8 per le notazioni IPA.

## Spazio vuoto

Una *parola* non può includere spazi vuoti. Il servizio utilizza lo spazio vuoto per delineare le singole parole nel testo di input.

## Sensibilità alle maiuscole/minuscole

Una *parola* è sensibile al maiuscolo/minuscolo. Ad esempio, supponiamo che un modello personalizzato contenga la voce `{word='Sun', translation='Sunday'}`. Il servizio applica la sua pronuncia predefinita alla parola `sun` ma la traduzione personalizzata alla parola `Sun`, poiché solo quest'ultima ha una lettera maiuscola iniziale.


## Sensibilità al contesto

Le pronunce di alcune parole sono sensibili al contesto. Ad esempio, considera la seguente frase di input di esempio:

```
St. Anthony lives on Henry St.
```
{: codeblock}

Le regole di pronuncia predefinite del servizio sintetizzano correttamente questo testo come

```
Saint Anthony lives on Henry Street
```
{: codeblock}

Tuttavia, se sovrascrivi le regole di pronuncia predefinite per la stringa `St.` per tradurla come `saint`, il servizio non può più pronunciare la parola in base al contesto. L'applicazione di un modello vocale personalizzato che include tale traduzione fa sì che il servizio pronunci la frase di input precedente come

```
Saint Anthony lives on Henry saint
```
{: codeblock}

Considera questi casi quando sviluppi coppie di parole/traduzioni.

## Punti finali

Il servizio applica una parola da un modello personalizzato solo a quelle stringhe nel testo di input che corrispondono esattamente alla parola. Un punto `.` finale nell'immissione di una parola cambia il modo in cui la parola viene sintetizzata:

-   *Una parola che non ha un punto finale* può contenere praticamente qualsiasi carattere. I caratteri includono lettere, cifre, segni di punteggiatura (diversi da un punto finale), simboli diversi da lettere (come %, &amp; e @), virgolette, parentesi, parentesi quadre e così via. La sua *traduzione* può includere qualsiasi input legale per il servizio, inclusi lo spazio vuoto e una rappresentazione fonetica in formato SSML.
-   *Una parola che ha un punto finale* può contenere solo lettere, punti e apostrofi interni (non come primo o ultimo carattere). La *traduzione* della parola può contenere solo parole normali con ortografia ordinaria separate da spazio vuoto o trattini. Non può contenere una rappresentazione fonetica.

Un esempio di parola con un punto finale è "`div.`". Supponiamo che un modello personalizzato includa la voce `{word='div.', translation='division'}`. Il servizio non applica la traduzione alla stringa "`div`" perché non include un punto finale e pertanto non corrisponde alla voce.

## Utilizzo delle voci IBM SPR
{: #sprNotes}

La rappresentazione SPR (Symbolic Phonetic Representation ) è un formato proprietario, dipendente dalla lingua sviluppato da {{site.data.keyword.IBM_notm}} per specificare la pronuncia di una parola. Per ogni lingua supportata, SPR include un alfabeto fonema, simboli per le sillabazioni e simboli per i livelli di accento lessicale. Le seguenti regole di base si applicano alla creazione di voci SPR:

-   La pronuncia predefinita che l'interfaccia di personalizzazione restituisce per una parola inizia con una <code>&#96;</code> (virgoletta aperta) ed è racchiusa tra `[]` (parentesi quadre). Ad esempio, l'interfaccia restituisce la seguente pronuncia per la parola `tomato`:

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    Ometti la virgoletta aperta e le parentesi quadre quando specifichi la traduzione di una parola con i metodi dell'interfaccia di personalizzazione.
-   Puoi utilizzare un punto per indicare l'inizio di una sillaba in una traduzione, ma i punti sono facoltativi e non influiscono sulla pronuncia della parola. Vengono riportati nella pronuncia di una parola solo se li includi nella traduzione della parola. Non utilizzare gli spazi per indicare le sillabazioni.
-   {{site.data.keyword.IBM_notm}} ti consiglia di precedere la vocale che ha l'accento principale per una parola con un simbolo `1`, sebbene non sia strettamente necessario. Il servizio determina dove si presenta l'accento se non lo indichi tu. Puoi anche utilizzare un simbolo `2` per indicare la posizione di ogni accento secondario, ma anche l'utilizzo dei simboli `2` è facoltativo. Vengono riportati nella pronuncia di una parola solo se li includi nella traduzione della parola.

Per ulteriori informazioni sull'utilizzo di SPR, vedi [Utilizzo di IBM SPR](/docs/services/text-to-speech-data?topic=text-to-speech-data-sprs).

## Utilizzo di voci in giapponese
{: #jaNotes}

Per la creazione di voci per le parole in un modello vocale personalizzato in giapponese, si applicano ulteriori regole e un campo `part_of_speech`:

-   Una traduzione di suoni simili può contenere solo caratteri *Katakana*. I caratteri *Kanji* e *Hiragana* non sono consentiti.
-   Quando crei una traduzione (suoni simili o fonetica) per una parola, puoi anche specificare un campo `part_of_speech` facoltativo per identificare la parte del discorso della parola. Il servizio utilizza la parte del discorso per produrre l'intonazione corretta per la parola. Per un elenco completo, vedi [Parti del discorso in giapponese](#partsOfSpeech).
-   Per ogni parola puoi creare solo una singola voce e puoi specificare solo una singola parte del discorso. Non puoi creare più voci con parti del discorso diverse (ad esempio, sostantivo e verbo) per la stessa parola. L'aggiunta di una traduzione per una parola che esiste in un modello sovrascrive la traduzione esistente della parola, compresa la sua parte di discorso.
-   Il servizio applica la parola corrispondente più lunga tra le coppie di parole/traduzioni definite per un modello vocale personalizzato. Ad esempio, considera le seguenti tre voci per un modello personalizzato.

    <pre><code>{
      "words": [
        {
          "word": "&#65326;&#65337;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65326;&#65337;&#65315;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65337;&#65315;",
          "translation": "&#12520;&#12467;&#12495;&#12510;&#12481;&#12517;&#12540;&#12459;&#12460;&#12452;",
          "part_of_speech": "Mesi"
        }
      ]
    }</code></pre>

    Con queste voci, supponiamo che il servizio riceva il seguente testo di input: <code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>. In questo caso, il servizio fa corrispondere la parola <code>&#65326;&#65337;&#65315;</code> perché <code>&#65326;&#65337;&#65315;</code> è più lungo di <code>&#65326;&#65337;</code> e perché <code>&#65326;&#65337;&#65315;</code> corrisponde prima di <code>&#65337;&#65315;</code>.

### Parti del discorso in giapponese
{: #partsOfSpeech}

La seguente tabella elenca le parti del discorso supportate per le voci personalizzate in giapponese. Per ulteriori informazioni sulla specifica della parte del discorso per una voce personalizzata in giapponese, vedi [Aggiunta di parole a un modello personalizzato in giapponese](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuJapaneseAdd).

<table style="width:75%">
  <caption>Tabella 1. Parti del discorso in giapponese</caption>
  <tr>
    <th style="text-align:center">Argomento <code>part_of_speech</code></th>
    <th style="text-align:center; width:35%">Significato in giapponese</th>
    <th style="text-align:center; width:35%">Significato in inglese</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>Josi</code></td>
    <td style="text-align:center"><em>Joshi</em></td>
    <td style="text-align:center">Participio</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Mesi</code></td>
    <td style="text-align:center"><em>Meishi</em></td>
    <td style="text-align:center">Sostantivo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kigo</code></td>
    <td style="text-align:center"><em>Kigou</em></td>
    <td style="text-align:center">Simbolo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Gobi</code></td>
    <td style="text-align:center"><em>Gobi</em></td>
    <td style="text-align:center">Inflessione</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Dosi</code></td>
    <td style="text-align:center"><em>Doushi</em></td>
    <td style="text-align:center">Verbo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Jodo</code></td>
    <td style="text-align:center"><em>Jodoushi</em></td>
    <td style="text-align:center">Verbo ausiliare</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Koyu</code></td>
    <td style="text-align:center"><em>Koyuumeishi</em></td>
    <td style="text-align:center">Nome proprio</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stbi</code></td>
    <td style="text-align:center"><em>Setsubiji</em></td>
    <td style="text-align:center">Suffisso</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Suji</code></td>
    <td style="text-align:center"><em>Suuji</em></td>
    <td style="text-align:center">Numerale</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kedo</code></td>
    <td style="text-align:center"><em>Keiyodoushi</em></td>
    <td style="text-align:center">Verbo aggettivale</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Fuku</code></td>
    <td style="text-align:center"><em>Fukishi</em></td>
    <td style="text-align:center">Avverbio</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Keyo</code></td>
    <td style="text-align:center"><em>Keiyoshi</em></td>
    <td style="text-align:center">Verbo aggettivale</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stto</code></td>
    <td style="text-align:center"><em>Settoji</em></td>
    <td style="text-align:center">Prefisso</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Reta</code></td>
    <td style="text-align:center"><em>Rentaishi</em></td>
    <td style="text-align:center">Determinante</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stzo</code></td>
    <td style="text-align:center"><em>Setsuzokushi</em></td>
    <td style="text-align:center">Congiunzione</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kato</code></td>
    <td style="text-align:center"><em>Kantoushi</em></td>
    <td style="text-align:center">Interiezione</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Hoka</code></td>
    <td style="text-align:center"><em>Hoka</em></td>
    <td style="text-align:center">Altro</td>
  </tr>
</table>
