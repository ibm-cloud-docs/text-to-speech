---

copyright:
  years: 2019
lastupdated: "2019-06-23"

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

# Elementi SSML
{: #elements}

Con {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}, puoi utilizzare la maggior parte degli elementi SSML (Speech Synthesis Markup Language) per controllare la sintesi del tuo testo. Gli elementi sono disponibili per tutte le lingue supportate. La seguente tabella riepiloga il supporto del servizio per gli attributi e gli elementi SSML.

-   *Completo* indica che il servizio supporta completamente l'elemento o l'attributo con le sue interfacce HTTP e WebSocket.
-   *Parziale* indica che il servizio non supporta tutti gli aspetti dell'elemento o dell'attributo. Indica anche che il servizio supporta l'elemento o l'attributo solamente con una delle sue interfacce oppure che l'elemento o l'attributo non è supportato con tutte le voci.
-   *Nessuno* indica che il servizio non supporta l'elemento o l'attributo.

Per ulteriori informazioni su un elemento o su un attributo, vedi la sua descrizione. Dove indicato, il supporto per alcuni attributi e valori è leggermente diverso dalla specifica SSML. Per ulteriori informazioni, vedi [W3C Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/speech-synthesis/){: external}.

<table>
  <caption>Tabella 1. Elementi SSML</caption>
  <tr>
    <th style="text-align:left; width:30%">Elemento o attributo</th>
    <th style="text-align:center; width:12%">Supporto</th>
    <th style="text-align:left; width:46%; padding-left:75px">Elemento o attributo</th>
    <th style="text-align:center; width:12%">Supporto</th>
  </tr>
  <tr>
    <td>[Audio](#audio_element)</td>
    <td style="text-align:center">Nessuno</td>
    <td style="padding-left:75px">[Say-as](#say-as_element)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td>[Break](#break_element)</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:100px">[cardinal](#sayAsCardinal)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td>[Desc](#desc_element)</td>
    <td style="text-align:center">Nessuno</td>
    <td style="padding-left:100px">[date](#sayAsDate)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td>[Emphasis](#emphasis_element)</td>
    <td style="text-align:center">Nessuno</td>
    <td style="padding-left:100px">[digits](#sayAsDigits)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td>[Lexicon](#lexicon_element)</td>
    <td style="text-align:center">Nessuno</td>
    <td style="padding-left:100px">[letters](#sayAsLetters)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td>[Mark](#mark_element)</td>
    <td style="text-align:center">Parziale</td>
    <td style="padding-left:100px">[number](#sayAsNumber)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td>[Meta](#mm_element)</td>
    <td style="text-align:center">Nessuno</td>
    <td style="padding-left:125px">cardinal</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td>[Metadata](#mm_element)</td>
    <td style="text-align:center">Nessuno</td>
    <td style="padding-left:125px">ordinal</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td>[Paragraph](#ps_element)</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:125px">telephone</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td>[Phoneme](#phoneme_element)</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:150px">punctuation</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:100px">[ordinal](#sayAsOrdinal)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:100px">[vxml:boolean](#vxml-boolean)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td>[Prosody](#prosody_element)</td>
    <td style="text-align:center">Parziale</td>
    <td style="padding-left:100px">[vxml:currency](#vxml-currency)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td style="padding-left:25px">contour</td>
    <td style="text-align:center">Nessuno</td>
    <td style="padding-left:100px">[vxml:date](#vxml-date)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td style="padding-left:25px">duration</td>
    <td style="text-align:center">Nessuno</td>
    <td style="padding-left:100px">[vxml:digits](#vxml-digits)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[pitch](#prosody-pitch)</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:100px">[vxml:phone](#vxml-phone)</td>
    <td style="text-align:center">Parziale</td>
  </tr>
  <tr>
    <td style="padding-left:25px">range</td>
    <td style="text-align:center">Nessuno</td>
    <td style="padding-left:75px">[Sentence](#ps_element)</td>
    <td style="text-align:center">Completo</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[rate](#prosody-rate)</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:75px">[Speak](#speak_element)</td>
    <td style="text-align:center">Completo</td>
  </tr>
  <tr>
    <td style="padding-left:25px">volume</td>
    <td style="text-align:center">Nessuno</td>
    <td style="padding-left:75px">[Sub](#sub_element)</td>
    <td style="text-align:center">Completo</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td style="padding-left:75px">[Voice](#voice_element)</td>
    <td style="text-align:center">Nessuno</td>
  </tr>
</table>

## L'elemento audio
{: #audio_element}

Questo elemento `<audio>` inserisce gli elementi registrati nell'audio generato dal servizio. Non è supportato.

## L'elemento break
{: #break_element}

L'elemento`<break>` inserisce una pausa nel testo pronunciato. Presenta i seguenti attributi facoltativi:

-   `strength` specifica la lunghezza della pausa in termini di variazione dei valori di intensità:
    -   `none` elimina l'interruzione che potrebbe altrimenti essere eseguita durante l'elaborazione.
    -   `x-weak`, `weak`, `medium`, `strong` o `x-strong` inseriscono interruzioni che diventano sempre più potenti.
-   `time` specifica la lunghezza della pausa in termini di secondi o millisecondi. I formati di valore validi sono `{integer}s` per i secondi o `{integer}ms` per i millisecondi.

```xml
<speak version="1.0">
  Different sized <break strength="none">no pause</break>
  Different sized <break strength="x-weak">x-weak pause</break>
  Different sized <break strength="weak">weak pause</break>
  Different sized <break strength="medium">medium pause</break>
  Different sized <break strength="strong">strong pause</break>
  Different sized <break strength="x-strong">x-strong pause</break>
  Different sized <break time="1s">one-second pause</break>
  Different sized <break time="1500ms">1500-millisecond pause</break>
</speak>
```
{: codeblock}

## L'elemento desc
{: #desc_element}

L'elemento `<desc>` può essere utilizzato solo all'interno di un elemento `<audio>`. Poiché l'elemento `<audio>` non è supportato, non lo è nemmeno l'elemento `<desc>`.

## L'elemento emphasis
{: #emphasis_element}

L'elemento `<emphasis>` richiede che il testo racchiuso tra elementi di codice venga pronunciato con enfasi. Non è supportato.

## L'elemento lexicon
{: #lexicon_element}

Questo elemento `<lexicon>` introduce dizionari di pronuncia per il documento SSML fornito. Non è supportato.

Puoi utilizzare l'interfaccia di personalizzazione del servizio per definire un dizionario di voci personalizzate (coppie di parole/traduzioni) da utilizzare durante la sintesi vocale. Per ulteriori informazioni, vedi
      [Informazioni sulla personalizzazione](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).

## L'elemento mark
{: #mark_element}

L'elemento `<mark>` è supportato solo dall'interfaccia WebSocket del servizio, non dalla sua interfaccia HTTP che ignora l'elemento. Per ulteriori informazioni, vedi [Specifica di un contrassegno SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing#mark).
{: note}

L'elemento `<mark>` è un elemento vuoto che inserisce un contrassegno nel testo da sintetizzare. Il client viene informato quando tutto il testo che precede l'elemento `<mark>` è stato sintetizzato. L'elemento accetta un singolo attributo `name` che specifica una stringa che identifica in modo univoco il contrassegno; il nome deve iniziare con un carattere alfanumerico. Il nome viene restituito insieme al tempo in cui si presenta il contrassegno nell'audio sintetizzato.

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

## Gli elementi meta e metadata
{: #mm_element}

Gli elementi `<meta>` e `<metadata>` sono contenitori in cui puoi inserire le informazioni relative al documento. Non sono supportati.

## Gli elementi paragraph e sentence
{: #ps_element}

Gli elementi `<paragraph>` (o `<p>`) e `<sentence>` (o `<s>`) sono elementi facoltativi che possono essere utilizzati per fornire suggerimenti sulla struttura del testo. Se il testo che è racchiuso in un elemento `<paragraph>` o `<sentence>` non termina con carattere di punteggiatura di fine frase (come un punto), il servizio aggiunge una pausa più lunga del normale all'audio sintetizzato.

L'unico attributo valido per l'elemento è `xml:lang`, che consente di passare da una lingua all'altra. L'attributo non è supportato.

```xml
<speak version="1.0">
  <paragraph>
    <sentence>Text within a sentence element.</sentence>
    <s>More text in another sentence.</s>
  </paragraph>
</speak>
```
{: codeblock}

## L'elemento phoneme
{: #phoneme_element}

L'elemento `<phoneme>` fornisce una pronuncia fonetica per il testo racchiuso tra elementi di codice. L'ortografia fonetica rappresenta il suono di una parola, in che modo viene sillabato e su quali sillabe viene utilizzato l'accento (stress). L'elemento ha due attributi:

-   `alphabet` è un attributo facoltativo che specifica la fonologia da utilizzare. Gli alfabeti supportati sono:
    -   IPA (International Phonetic Alphabet - Alfabeto fonetico internazionale) standard: `alphabet="ipa"`
    -   {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation): `alphabet="ibm"`

    Se non viene specificato alcun alfabeto, il servizio utilizza IBM SPR per impostazione predefinita.
-   `ph` è un attributo obbligatorio che fornisce la pronuncia nell'alfabeto indicato. Gli esempi riportati di seguito mostrano la pronuncia della parola *tomato* in entrambi i formati:

    -   Formato IPA:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   Formato IPA con simboli Unicode:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   Formato IBM SPR:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

Per ulteriori informazioni sull'utilizzo delle notazioni SPR e IPA con l'elemento `<phoneme>`, vedi [Utilizzo di IBM SPR](/docs/services/text-to-speech-data?topic=text-to-speech-data-sprs).

## L'elemento prosody
{: #prosody_element}

L'elemento `<prosody>` controlla il tono e la velocità di pronuncia del testo. Tutti gli attributi sono facoltativi, ma si verifica un errore se non ne viene specificato nessuno. La specifica SSML consente quattro attributi che il servizio non supporta: `volume`, `contour`, `range` e `duration`. Il servizio supporta gli attributi `pitch` e `rate`.

### L'attributo pitch
{: #prosody-pitch}

L'attributo `pitch` modifica il tono di riferimento per il testo all'interno dell'elemento. I valori accettati sono:

-   Un numero seguito dalla designazione `Hz` (Hertz): il tono di riferimento viene trasposto (in alto o in basso) nel valore specificato.
-   Un valore di modifica relativa (in semitoni): un numero che causa un cambiamento assoluto dal riferimento corrente. Il numero è preceduto dal simbolo `+` (un incremento) o dal simbolo `-` (un decremento) ed è seguito da `st` (semitoni), ad esempio, `+5st`.
-   Una modifica relativa in percentuale: un numero che causa un cambiamento relativo dal riferimento corrente. Il numero è preceduto dal simbolo `+` (un incremento) o dal simbolo `-` (un decremento) ed è seguito da `%` (segno di percentuale), ad esempio, `-10%`.
-   Una delle sei parole chiave riportate di seguito che modificano il tono con i valori predefiniti corrispondenti:
    -   `default` utilizza il tono di riferimento predefinito del servizio.
    -   `x-low` abbassa il riferimento del tono di 12 semitoni.
    -   `low` abbassa il riferimento del tono di sei semitoni.
    -   `medium` produce lo stesso comportamento di `default`.
    -   `high` alza il riferimento del tono di sei semitoni.
    -   `x-high` alza il riferimento del tono di 12 semitoni.

    ```xml
    <speak version="1.0">
      <prosody pitch="150Hz">Transpose pitch to 150 Hz</prosody>
      <prosody pitch="-20Hz">Lower pitch by 20 Hz from baseline</prosody>
      <prosody pitch="+20Hz">Increase pitch by 20 Hz from baseline</prosody>
      <prosody pitch="-12st">Lower pitch by 12 semitones from baseline</prosody>
      <prosody pitch="+12st">Increase pitch by 12 semitones from baseline</prosody>
      <prosody pitch="x-low">Lower pitch by 12 semitones from baseline</prosody>
    </speak>
    ```
    {: codeblock}

### L'attributo rate
{: #prosody-rate}

L'attributo `rate` indica un cambiamento nella velocità di pronuncia del testo all'interno dell'elemento. La velocità viene specificata in termini di parole al minuto; se la velocità di pronuncia è di 50 parole al minuto, `rate` è uguale a `50`. Quando `rate` è impostato su un numero positivo, l'implementazione non è conforme alla specifica dell'attributo prosody rate W3C corrente. Inoltre, il servizio supporta i cambiamenti relativi in percentuale (ad esempio, `+15%`) ma non i cambiamenti relativi del valore (ad esempio, `+15`). I valori accettati sono:

-   Un incremento o un decremento relativo in percentuale: `+10%`.
-   Un numero di parole al minuto come un numero positivo: `75`.
-   `default` utilizza la velocità predefinita del servizio.
-   `x-slow` riduce la velocità del 50 percento.
-   `slow` riduce la velocità del 25 percento.
-   `medium` produce lo stesso comportamento di `default`.
-   `fast` aumenta la velocità del 25 percento.
-   `x-fast` aumenta la velocità del 50 percento.

```xml
<speak version="1.0">
  <prosody rate="slow">Decrease speaking rate by 25%</prosody>
  <prosody rate="50">Set speaking rate at 50 words per minute</prosody>
  <prosody rate="+5%">Increase speaking rate by 5 percent</prosody>
</speak>
```
{: codeblock}

## L'elemento say-as
{: #say-as_element}

L'elemento `<say-as>` è supportato solo parzialmente per la maggior parte delle lingue. Per le lingue diverse dall'inglese americano, di norma il servizio supporta solo gli attributi `digits` e `letters` dell'elemento.
{: note}

L'elemento `<say-as>` fornisce informazioni sul tipo di testo contenuto all'interno dell'elemento e specifica il livello di dettaglio per eseguire il rendering del testo. L'elemento ha un attributo obbligatorio, `interpret-as`, che indica in che modo deve essere interpretato il testo racchiuso tra elementi di codice. Ha due attributi facoltativi, `format` e `detail`, utilizzati solo con particolari valori all'interno dell'attributo `interpret-as`, come illustrato nei seguenti esempi.

Di seguito vengono riportati i valori accettabili per l'attributo `interpret-as` e gli esempi di ciascuno di essi.

### cardinal
{: #sayAsCardinal}

Il valore `cardinal` esprime il numero cardinale per il valore numerico all'interno dell'elemento. I seguenti esempi specificano *Super Bowl forty-nine*. Il primo è superfluo dal momento che non modifica il comportamento predefinito del servizio.

```xml
<speak version="1.0">
  Super Bowl <say-as interpret-as="cardinal">49</say-as>
  Super Bowl <say-as interpret-as="cardinal">XLIX</say-as>
</speak>
```
{: codeblock}

### date
{: #sayAsDate}

Il valore `date` esprime la data all'interno dell'elemento in base al formato fornito nell'attributo `format` associato. L'attributo `format` è obbligatorio per il valore `date`. Se non è presente alcun `format`, il servizio tenterà ancora di pronunciare la data. I seguenti esempi esprimono le date indicate nei formati specificati, dove `d`, `m` e `y` rappresentano giorno, mese e anno.

```xml
<speak version="1.0">
  <say-as interpret-as="date" format="mdy">12/17/2005</say-as>
  <say-as interpret-as="date" format="ymd">2005/12/17</say-as>
  <say-as interpret-as="date" format="dmy">17/12/2005</say-as>
  <say-as interpret-as="date" format="ydm">2005/17/12</say-as>
  <say-as interpret-as="date" format="my">12/2005</say-as>
  <say-as interpret-as="date" format="md">12/17</say-as>
  <say-as interpret-as="date" format="ym">2005/12</say-as>
</speak>
```
{: codeblock}

### digits
{: #sayAsDigits}

Il valore `digits` esprime le cifre nel numero all'interno dell'elemento. Il seguente esempio esprime le singole cifre *123456*.

```xml
<speak version="1.0">
  <say-as interpret-as="digits">123456</say-as>
</speak>
```
{: codeblock}

### letters
{: #sayAsLetters}

Il valore `letters` specifica i caratteri nella parola all'interno dell'elemento. Il seguente esempio specifica le lettere della parola *hello*.

```xml
<speak version="1.0">
  <say-as interpret-as="letters">Hello</say-as>
</speak>
```
{: codeblock}

### number
{: #sayAsNumber}

Il valore `number` offre un'alternativa ai valori `cardinal` e `ordinal`. Puoi utilizzare l'attributo `format` facoltativo per indicare come deve essere interpretata una serie di numeri. Il primo esempio omette l'attributo `format` per pronunciare il numero come un valore cardinale. Il secondo esempio specifica esplicitamente che il numero deve essere pronunciato come un valore `cardinal`. Il terzo esempio specifica che il numero deve essere pronunciato come un valore `ordinal`.

```xml
<speak version="1.0">
  <say-as interpret-as="number">123456</say-as>
  <say-as interpret-as="number" format="cardinal">123456</say-as>
  <say-as interpret-as="number" format="ordinal">123456</say-as>
</speak>
```
{: codeblock}

Puoi anche specificare il valore `telephone` per l'attributo `format`. Gli esempi mostrano due diversi modi di pronunciare una serie di numeri come un numero di telefono. Per pronunciare i numeri con la punteggiatura inclusa, specifica il valore `punctuation` per l'attributo `detail` facoltativo.

```xml
<speak version="1.0">
  <say-as interpret-as="number" format="telephone">555-555-5555</say-as>
  <say-as interpret-as="number" format="telephone" detail="punctuation">555-555-5555</say-as>
</speak>
```
{: codeblock}

### ordinal
{: #sayAsOrdinal}

Il valore `ordinal` esprime il valore ordinale per la cifra all'interno dell'elemento. I seguenti esempi specificano *second first*.

```xml
<speak version="1.0">
  <say-as interpret-as="ordinal">2</say-as>
  <say-as interpret-as="ordinal">1</say-as>
</speak>
```
{: codeblock}

### vxml:boolean
{: #vxml-boolean}

Il valore `vxml:boolean` esprime *yes* o *no* a seconda del valore `true` o `false` all'interno dell'elemento.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:boolean">true</say-as>
  <say-as interpret-as="vxml:boolean">false</say-as>
</speak>
```
{: codeblock}

### vxml:currency
{: #vxml-currency}

Il valore `vxml:currency` viene utilizzato per controllare la sintesi dei valori monetari. La stringa deve essere scritta nel formato `UUUmm.nn`, dove `UUU` è l'indicatore di valuta a tre caratteri specificato dallo standard ISO 4217 e `mm.nn` è la quantità. Il seguente esempio specifica *forty-five dollars and thirty cents*.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.30</say-as>
</speak>
```
{: codeblock}

Se il numero specificato include più di due posizioni decimali, la quantità viene sintetizzata come un numero decimale seguito dall'indicatore della valuta. Se l'indicatore di valuta a tre cifre non è presente, la quantità viene sintetizzata solamente come un numero decimale e il tipo di valuta non viene pronunciato. Il seguente esempio specifica *forty-five point three two nine US dollars*.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.329</say-as>
</speak>
```
{: codeblock}

### vxml:date
{: #vxml-date}

Il valore `vxml:date` funziona come il valore `date`, ma il formato è predefinito come `YYYYMMDD`. Se un valore di giorno, mese o anno è sconosciuto oppure se non vuoi che venga pronunciato, sostituisci il valore con un `?` (punto interrogativo). Il secondo e il terzo esempio includono punti interrogativi.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:date">20050720</say-as>
  <say-as interpret-as="vxml:date">????0720</say-as>
  <say-as interpret-as="vxml:date">200507??</say-as>
</speak>
```
{: codeblock}

### vxml:digits
{: #vxml-digits}

Il valore `vxml:digits` fornisce la stessa funzione del valore `digits`.

### vxml:phone
{: #vxml-phone}

Il valore `vxml:phone` esprime un numero di telefono che contiene sia cifre che punteggiatura. Equivale a utilizzare il valore `number` e a specificare `telephone` per l'attributo `format` e `punctuation` per l'attributo `detail`.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:phone">555-555-5555</say-as>
</speak>
```
{: codeblock}

## L'elemento speak
{: #speak_element}

L'elemento `<speak>` è l'elemento root dei documenti SSML. Gli attributi validi sono:

-   `version` è un attributo obbligatorio che specifica la specifica SSML. Il valore accettato è `1.0`.
-   `xml:lang` non è richiesto dal servizio. Ometti l'attributo quando utilizzi questo elemento.
-   `xml:base` non ha alcun effetto.

```xml
<speak version="1.0">
  The text to be spoken.
</speak>
```
{: codeblock}

## L'elemento sub
{: #sub_element}

L'elemento `<sub>` indica che il testo specificato dall'attributo `alias` deve sostituire il testo racchiuso all'interno dell'elemento quando viene sintetizzato il discorso. L'attributo `alias` è l'unico attributo dell'elemento ed è obbligatorio.

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

## L'elemento voice
{: #voice_element}

Questo elemento `<voice>` richiede un cambiamento nella voce. Non è supportato.
