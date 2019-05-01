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

# Informazioni sulla personalizzazione
{: #customIntro}

Quando sintetizzi il testo con {{site.data.keyword.texttospeechfull}}, il servizio applica regole di pronuncia dipendenti dalla lingua. Il servizio applica le regole per convertire l'ortografia ordinaria (ortografica) di ogni parola in una forma fonetica. La forma fonetica di una parola utilizza i simboli fonemi per definire come viene pronunciata la parola. Questi simboli sono le unità distinte del suono che distinguono le parole in una lingua, le sillabazioni e i segni di accento delle sillabe.
{: shortdesc}

Le regole di pronuncia regolare del servizio funzionano bene per le parole comuni. Tuttavia, possono produrre risultati imperfetti per parole inusuali. Tali parole includono termini speciali con origini straniere, nomi personali o geografici e abbreviazioni o acronimi. Se il lessico della tua applicazione include parole come queste, puoi utilizzare l'interfaccia di personalizzazione per specificare in che modo il servizio pronuncia tali parole.

L'interfaccia di personalizzazione è una funzionalità beta disponibile per tutte le lingue.
{: note}

## Come funziona la personalizzazione
{: #ciHow}

L'interfaccia di personalizzazione del servizio {{site.data.keyword.texttospeechshort}} crea un dizionario di parole e delle relative traduzioni per una lingua specifica. Questo dizionario viene definito come *modello vocale personalizzato* o semplicemente modello personalizzato. Ogni voce personalizzata in un modello vocale personalizzato è composta da una coppia di *parola*/*traduzione*. La traduzione di una parola indica al servizio come pronunciare la parola quando si presenta nel testo di input.

L'interfaccia di personalizzazione fornisce dei metodi per creare e gestire i tuoi modelli vocali personalizzati, che il servizio memorizza in modo permanente. Dopo aver creato un modello personalizzato, puoi utilizzarlo durante la sintesi con qualsiasi versione del metodo `/v1/synthesize`. Quando il servizio sintetizza il testo di input, determina la pronuncia delle parole presenti nel modello personalizzato applicando le loro traduzioni direttamente o indirettamente.

Puoi specificare la traduzione di una parola in un modello vocale personalizzato sotto forma di *traduzione di suoni simili* o di *traduzione fonetica*. Puoi utilizzare entrambi i metodi per le voci nello stesso modello personalizzato e puoi combinare i due metodi all'interno della stessa traduzione. Alle voci personalizzate si applicano una serie di regole e linee guida. Per ulteriori informazioni, vedi [Regole per la creazione di voci personalizzate](/docs/services/text-to-speech/custom-rules.html).

## Traduzione di suoni simili
{: #soundsLike}

La *traduzione di suoni simili* utilizza le regole di pronuncia regolare del servizio per rappresentare indirettamente la pronuncia di una parola di destinazione. Una traduzione di suoni simili è formata dalle pronunce regolari di una o più parole. Il servizio sostituisce innanzitutto la traduzione specificata per qualsiasi ricorrenza della parola riportata nel testo di input. Quindi applica le regole di pronuncia regolare alla traduzione, convertendola nella sua rappresentazione fonetica per ottenere la pronuncia.

Ad esempio, le regole di pronuncia regolare del servizio traducono correttamente molte abbreviazioni e acronimi comuni. Il servizio pronuncia l'abbreviazione *cm* come *centimeter*. Le abbreviazioni meno comuni vengono pronunciate lettera per lettera. Ad esempio, il servizio pronuncia la stringa *Str* (un'abbreviazione di *street*) come *S T R*, con ogni lettera pronunciata singolarmente. Puoi utilizzare il metodo di suoni simili per specificare la traduzione *street* per la stringa *Str*.

Un altro esempio di acronimo è la parola *IEEE*, che sta per Institute of Electrical and Electronic Engineers. Per impostazione predefinita, il servizio pronuncia questo acronimo come *I E E E*. Ma l'acronimo viene comunemente pronunciato *I triple E*, che puoi facilmente definire usando la semplice traduzione di suoni simili *I triple E*. Se la parola *IEEE* viene riportata nel tuo modello personalizzato con questa traduzione, il servizio sostituisce ogni ricorrenza della parola con la traduzione. Quindi, applica le regole di pronuncia regolare alle singole parole *I*, *triple* e *E* per fornire le pronuncia comune.

Puoi applicare il metodo di suoni simili a più di semplici abbreviazioni e acronimi. Funziona altrettanto bene per parole complesse o inusuali. Ad esempio, la seguente coppia di traduzioni di suoni simili fornisce pronunce corrette per le parole inusuali che vengono gestite in modo imperfetto dalle regole di pronuncia regolare del servizio. Trovare traduzioni appropriate per tali parole può essere più impegnativo rispetto alle semplici abbreviazioni. Le seguenti traduzioni utilizzano le regole di pronuncia regolare per modificare l'ortografia delle parole.

<table style="width:35%">
  <caption>Tabella 1. Traduzioni di suoni simili di esempio</caption>
  <tr>
    <th style="text-align:left">Parola</th>
    <th style="text-align:left">Traduzione</th>
  </tr>
  <tr>
    <td>ayurvedic</td>
    <td>aayervedic</td>
  </tr>
  <tr>
    <td>gastroenteritis</td>
    <td>gastro enteritis</td>
  </tr>
</table>

Come mostrano questi esempi, lo sviluppo di traduzioni di suoni simili può essere più un processo di prova ed errore anziché un processo costituito da formule prestabilite. In tale processo, crei una traduzione candidata in base alla tua intuizione ed esperienza con il servizio. Quindi sintetizzi la parola per la traduzione candidata come testo di input e ascolti l'audio risultante. Se sei soddisfatto con la pronuncia, puoi utilizzare la traduzione nel tuo modello personalizzato; altrimenti modifichi la traduzione e la verifichi di nuovo.

## Traduzione fonetica
{: #phonetic}

Il metodo di suoni simili è un modo relativamente semplice e utile per ottenere una pronuncia. Tuttavia, non è sempre possibile sviluppare traduzioni di suoni simili. L'alternativa diretta, il metodo fonetico, potrebbe sembrare più complicata e dispendiosa in termini di tempo, ma può ottenere la pronuncia di qualsiasi parola.

La *traduzione fonetica* specifica una pronuncia in termini di simboli fonemi, segni di accento delle sillabe e sillabazioni facoltative che sovrascrivono le regole di pronuncia regolare del servizio. Puoi specificare la traduzione fonetica in uno dei seguenti formati:

-   La rappresentazione IPA (International Phonetic Alphabet) standard
-   La rappresentazione {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation) proprietaria

In entrambi i casi, specifica una traduzione utilizzando uno specifico formato di fonemi basato sul linguaggio SSML (Speech Synthesis Markup Language). SSML è un linguaggio di markup basato su XML che fornisce annotazioni di testo per le applicazioni di sintesi vocale. Specifica la traduzione fonetica per una parola utilizzando l'elemento SSML `<phoneme>`:

<pre><code>&lt;phoneme alphabet="{ipa | ibm}" ph="{translation}"&gt;&lt;/phoneme&gt;</code></pre>

L'attributo `alphabet` specifica il tipo di rappresentazione fonetica: `ipa` o `ibm`. L'attributo `ph` specifica la stringa di traduzione fonetica.

Ad esempio, considera la parola `trinitroglycerin`. Le regole di pronuncia regolare del servizio producono una pronuncia che differisce da quella comunemente usata da chimici e medici. La pronuncia corretta può essere ottenuta con una traduzione fonetica.

<table style="width:35%">
  <caption>Tabella 2. Traduzioni fonetiche di esempio</caption>
  <tr>
    <th style="text-align:left">Alfabeto</th>
    <th style="text-align:left">Traduzione</th>
  </tr>
  <tr>
    <td>IPA</td>
    <td>t&#633;a&#618;n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n</td>
  </tr>
  <tr>
    <td>SPR</td>
    <td>trYn1YtrxglIsxrXn</td>
  </tr>
</table>

In questi esempi, la stringa di traduzione fonetica è composta da simboli fonemi e da un singolo segno di accento principale. Il segno di accento principale è rappresentato da <code>&#712;</code> in IPA e da `1` in SPR. In entrambi i casi, è posizionato appena prima del simbolo per la vocale accentata. Sebbene gli esempi non lo mostrino, in una traduzione fonetica puoi anche specificare sillabazioni e posizioni di accento secondario. Questi elementi non sono obbligatori e normalmente non sono necessari per ottenere una pronuncia. Come con le traduzioni di suoni simili, puoi comporre una traduzione fonetica da più stringhe delimitate da spazi.

Puoi anche specificare le traduzioni IPA come valori Unicode IPA. Per ulteriori informazioni, vedi [Utilizzo di IBM SPR](/docs/services/text-to-speech/SPRs.html) e le tabelle specifiche per le lingue nelle pagine a cui si fa riferimento in [Lingue supportate](/docs/services/text-to-speech/SPRs.html#supportedLanguages). Per una traduzione di esempio che utilizza i valori Unicode IPA, vedi [L'elemento phoneme](/docs/services/text-to-speech/SSML-elements.html#phoneme_element).
{: note}

### Utilizzo di una traduzione fonetica esistente
{: #phoneticMethod}

A meno che tu non sia un esperto di fonologia, la composizione di traduzioni fonetiche non è un'attività semplice. È sempre più facile modificare una traduzione fonetica esistente piuttosto che comporla da zero. Per aiutarti a creare traduzioni fonetiche, l'API del servizio include un metodo `GET /v1/pronunciation`. Il metodo restituisce la rappresentazione IPA o SPR generata dalle regole di pronuncia regolare del servizio per una parola in una lingua specificata. Puoi anche richiedere la pronuncia di una parola da un modello vocale personalizzato specificato per visualizzare la traduzione nella lingua di quel modello.

Puoi utilizzare il metodo `/GET v/1/pronunciation` per ottenere una traduzione fonetica iniziale per una parola. Puoi quindi modificare la traduzione per ottenere la pronuncia che desideri. Con il metodo di suoni simili, segui un processo di prova ed errore. Inoltri la tua traduzione candidata al servizio, sintetizzi la parola come testo di input, ascolti l'audio risultante e modifichi la traduzione candidata. Puoi ripetere il processo finché non sei soddisfatto della pronuncia.

Per ulteriori informazioni, vedi [Esecuzione di query di una parola da una lingua](/docs/services/text-to-speech/custom-entries.html#cuWordsQueryLanguage).

### Ulteriori informazioni sulla traduzione fonetica
{: #phoneticInfo}

Le seguenti risorse forniscono informazioni sulla traduzione fonetica:

-   Per ulteriori informazioni sull'utilizzo di SSML e del suo elemento `<phoneme>`, vedi [Utilizzo di SSML](/docs/services/text-to-speech/SSML.html).
-   Per ulteriori informazioni sulla specifica delle traduzioni SPR e dei loro simboli IPA equivalenti, vedi [Utilizzo di IBM SPR](/docs/services/text-to-speech/SPRs.html).
-   Per ulteriori informazioni sull'utilizzo dei simboli IPA e per campioni audio dei simboli, consulta le fonti sul web. Puoi trovare una discussione introduttiva dettagliata all'indirizzo [en.wikipedia.org/wiki/International_Phonetic_Alphabet ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet){: new_window}.

## Traduzione combinata di suoni simili e fonetica

Puoi combinare i metodi di suoni simili e fonetico nella stessa traduzione. Questa funzione può ridurre il lavoro che è coinvolto nella composizione di una traduzione.

Ad esempio, supponiamo che tu abbia utilizzato il metodo di suoni simili per ottenere una parte di una parola pronunciata in modo soddisfacente. Ma ora devi ottimizzare i restanti elementi della parola. Puoi utilizzare il metodo fonetico per specificare gli aspetti difficili della parola. Il seguente esempio applica la traduzione combinata alla parola `trinitroglycerin`:

<pre><code>try&lt;phoneme alphabet="ipa" ph="n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n"&gt;&lt;/phoneme&gt;</code></pre>
