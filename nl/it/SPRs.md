---

copyright:
  years: 2019
lastupdated: "2019-06-11"

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

# Utilizzo di IBM SPR
{: #sprs}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} supporta sia la notazione IPA (International Phonetic Alphabet - Alfabeto fonetico internazionale) standard che {{site.data.keyword.IBM}} SPR (Symbolic Phonetic Representation) per rappresentare i suoni linguistici. SPR è una codifica fonetica che rappresenta la pronuncia di una parola, i suoni che compongono la parola, in che modo i suoni vengono sillabati e su quali sillabe viene applicata una forza maggiore (stress). SPR costituisce una rappresentazione alternativa a IPA.
{: shortdesc}

Le seguenti sezioni introducono la notazione {{site.data.keyword.IBM_notm}} SPR. Poiché IPA è una notazione standard, la documentazione non fornisce informazioni sull'uso di base per IPA. Per una breve guida all'uso, consulta [Utilizzo di IPA](#ipa).

## Introduzione a IBM SPR
{: #introduction-SPRs}

Una pronuncia SPR viene definita [l'elemento phoneme](/docs/services/text-to-speech-data?topic=text-to-speech-data-elements#phoneme_element) di SSML (Speech Synthesis Markup Language). È composto da una sequenza di simboli consentiti per una determinata lingua racchiusa tra virgolette. I simboli definiscono in che modo viene pronunciata la parola racchiusa nell'elemento `<phoneme>`. L'attributo `alphabet` dell'elemento ha il valore `ibm` per indicare che la pronuncia è definita in SPR e l'attributo `ph` definisce la pronuncia. Di seguito vengono riportati esempi della notazione SPR valida per le parole *through* e *shocking* nella lingua inglese americano:

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

Nelle definizioni, un simbolo `.` (punto) indica l'inizio di una nuova sillaba, le cifre `1` e `0` indicano il livello di stress delle sillabe e le lettere rappresentano suoni specifici della lingua inglese americano. Una voce SPR che non è conforme alla specifica richiesta, non è valida.

## Sillabazione

Puoi utilizzare un simbolo `.` (punto) per contrassegnare l'inizio di ogni sillaba. Tuttavia, per preservare la fonetica valida di una lingua, il servizio può scegliere di non rispettare i punti in alcuni casi (ad esempio, se la sillabazione viene applicata in una posizione errata o innaturale per una lingua). In generale, nei casi in cui l'utente può indicare una preferenza valida per la sillabazione o per un altro aspetto della pronuncia di una parola, il servizio rispetta tali richieste.

## Accento (stress) sulla sillaba

Puoi utilizzare i simboli presenti nella seguente tabella per contrassegnare l'accento (stress) su una sillaba per la pronuncia. {{site.data.keyword.IBM_notm}} ti consiglia di indicare l'accento principale per le pronunce in SPR o IPA. Tuttavia, indicare l'accento sulla sillaba è facoltativo per entrambi i formati; il servizio determina dove utilizzare l'accento se non lo indichi tu.

<table style="width:80%">
  <caption>Tabella 1. Accento (stress) sulla sillaba</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Simbolo IBM SPR
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Simbolo IPA
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Unicode IPA
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Significato
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      1
    </td>
    <td style="text-align:center">
      <code>&#712;</code>
    </td>
    <td style="text-align:center">
      02C8
    </td>
    <td>
      Accento (stress) principale
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      2
    </td>
    <td style="text-align:center">
      <code>&#716;</code>
    </td>
    <td style="text-align:center">
      02CC
    </td>
    <td>
      Accento (stress) secondario
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      0
    </td>
    <td style="text-align:center">Nessun simbolo</td>
    <td style="text-align:center">Nessun valore</td>
    <td>
      Nessun accento (stress)
    </td>
  </tr>
</table>

**Note:**

-   In IPA per il francese, i simboli di accento sulle sillabe vengono ignorati. In SPR per il francese, l'accento sulla sillaba non viene ignorato; se specificato, deve precedere immediatamente la vocale della sillaba. In SPR, l'accento sulla sillaba per il francese è molto più rigido che per le altre lingue; si verifica un errore se il simbolo dell'accento si trova in una posizione non valida.
-   In SPR per lo spagnolo e l'italiano, puoi specificare solo `1` (accento principale). Si verifica un errore se ne specifichi uno secondario o se non ne specifichi affatto.
-   In SPR per il giapponese, sono supportati solo `1` (accento principale) e `0` (nessun accento). Si verifica un errore se ne specifichi uno secondario.

Devi posizionare un contrassegno di accento all'interno di una sillabazione ma sempre alla sinistra della vocale della sillaba. Puoi posizionare un contrassegno in qualsiasi punto alla sinistra della vocale accentata. Ad esempio, ognuno dei seguenti esempi SPR posiziona l'accento principale sulla vocale corretta della parola *construction*:

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

## Simboli dei suoni fonetici

Ogni lingua utilizza il suo inventario di simboli SPR per rappresentare i suoni fonetici di tale lingua. Le regole riportate di seguito si applicano alla specifica di un simbolo SPR:

-   Le lettere sono sensibili al maiuscolo/minuscolo, quindi `e` e `E`, ad esempio, rappresentano due suoni diversi.
-   I simboli di due e tre caratteri devono essere racchiusi tra virgolette singole; ad esempio, il simbolo `aj` nella parola in tedesco *heim*: `"h'aj'm"`.
-   Il servizio considera non valida qualsiasi definizione SPR che contenga simboli fonetici non consentiti in una lingua.

Tieni in considerazione anche quanto segue quando definisci la pronuncia di una parola in formato SPR:

-   I suoni di ogni lingua hanno schemi di distribuzione specifici all'interno di tale lingua. Ad esempio, in tutti i dialetti dell'inglese, il suono `G` in *sing* (`".1sIG"`) non si trova all'inizio di una parola. Altri suoni dell'inglese americano che hanno una distribuzione particolarmente poco diffusa sono l'occlusiva glottidale (`?`), la vibrante (`F`) e la nasale sillabica (`N`). Se immetti un simbolo sonoro in un contesto in cui normalmente non viene utilizzato, il discorso risultante potrebbe suonare innaturale.
-   Il servizio {{site.data.keyword.texttospeechshort}} applica una serie sofisticata di regole linguistiche al suo input in modo che rifletta i processi in base ai quali i suoni cambiano in contesti specifici nel linguaggio naturale. Ad esempio, nell'inglese americano, il suono `t` della parola *write* (`".1r1Yt"`) viene pronunciato come una vibrante (`F`) in *writer* (`".1rY.0FR"`). L'input SPR subisce queste modifiche proprio come fa il testo ordinario di input. In questo esempio, se immetti `".1rY.0tR"` o `".1rY.0FR"`, non influisce sul discorso generato.

## Utilizzo di IPA
{: #ipa}

Le informazioni riportate di seguito si applicano per gestire la pronuncia nella notazione IPA:

-   Utilizza solo i simboli IPA documentati. Quando vengono elencati diversi simboli IPA (o combinazioni di simboli) per un simbolo SPR, sono tutti equivalenti al singolo simbolo SPR. In questo caso, il servizio tratta tutti questi simboli IPA allo stesso modo e non si rende conto delle differenze sottili o regionali che il sistema IPA intende descrivere.
-   Puoi anche specificare le pronunce IPA come valori Unicode IPA. Le tabelle specifiche della lingua elencate nella seguente sezione documentano sia i simboli IPA che i loro valori Unicode IPA equivalenti. Per una pronuncia di esempio che utilizza i valori Unicode IPA, vedi [L'elemento phoneme](/docs/services/text-to-speech-data?topic=text-to-speech-data-elements#phoneme_element).

Per ulteriori informazioni, consulta quanto segue:

-   Per ulteriori informazioni su IPA, vedi [International Phonetic Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}.
-   Per ulteriori informazioni sui simboli fonetici per Unicode, vedi [Phonetic symbols in Unicode](https://wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: external}.

## Lingue supportate
{: #supportedLanguages}

Le seguenti pagine documentano i simboli SPR, i simboli IPA e i valori Unicode IPA equivalenti per ogni lingua. Mostrano esempi di ogni simbolo nelle parole della lingua. A causa delle differenze dialettali, gli esempi potrebbero non corrispondere sempre alla tua pronuncia.

-   [Simboli per il portoghese brasiliano](/docs/services/text-to-speech-data?topic=text-to-speech-data-ptSymbols)
-   [Simboli per l'inglese britannico](/docs/services/text-to-speech-data?topic=text-to-speech-data-gbSymbols)
-   [Simboli per il francese](/docs/services/text-to-speech-data?topic=text-to-speech-data-frSymbols)
-   [Simboli per il tedesco](/docs/services/text-to-speech-data?topic=text-to-speech-data-deSymbols)
-   [Simboli per l'italiano](/docs/services/text-to-speech-data?topic=text-to-speech-data-itSymbols)
-   [Simboli per il giapponese](/docs/services/text-to-speech-data?topic=text-to-speech-data-jaSymbols)
-   [Simboli per lo spagnolo](/docs/services/text-to-speech-data?topic=text-to-speech-data-esSymbols)
-   [Simboli per l'inglese americano](/docs/services/text-to-speech-data?topic=text-to-speech-data-usSymbols)
