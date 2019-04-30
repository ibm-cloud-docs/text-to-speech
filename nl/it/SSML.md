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

# Utilizzo di SSML
{: #ssml}

SSML (Speech Synthesis Markup Language) è un linguaggio di markup basato su XML che fornisce annotazioni di testo per le applicazioni di sintesi vocale. Si tratta di un suggerimento di W3C Voice-Browser Working Group che è stato adottato come linguaggio di markup standard per la sintesi vocale dalla specifica VoiceXML 2.0. SSML offre agli sviluppatori delle applicazioni per sintesi vocale un modo standard per controllare gli aspetti del processo di sintesi consentendo loro di specificare pronuncia, volume, tono, velocità e altri attributi tramite markup.
{: shortdesc}

Con il servizio {{site.data.keyword.texttospeechfull}}, puoi utilizzare SSML per controllare la sintesi del tuo testo con tutte le lingue supportate. Ciò include l'utilizzo dell'elemento `<phoneme>` SSML per definire la pronuncia di una parola in IPA (International Phonetic Alphabet) o in {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation). Il servizio si basa sull'elemento `<phoneme>` SSML per definire la traduzione fonetica di una parola con la sua interfaccia di personalizzazione; per ulteriori informazioni, vedi [Informazioni sulla personalizzazione](/docs/services/text-to-speech/custom-intro.html).

## Introduzione a SSML
{: #introduction-SSML}

SSML opera ampliando il testo semplice che viene passato a un sintetizzatore con una serie predefinita di elementi o tag. Innanzitutto, un parser XML separa il testo semplice di input dalle specifiche di markup. Le specifiche vengono poi elaborate e inviate come una serie di istruzioni in un formato che possa essere compreso dal sintetizzatore per produrre gli effetti desiderati. Affinché il parser XML esegua questo lavoro, è necessario che la markup sia ben formata; ad esempio, gli elementi devono essere chiusi e più elementi devono essere nidificati correttamente. Per un'introduzione ai concetti XML di base, vedi [w3schools.com/xml/xml_whatis.asp ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.w3schools.com/xml/xml_whatis.asp){: new_window}.

Un elemento SSML è qualsiasi cosa contenuta all'interno di una tag di apertura e della corrispondente tag di chiusura, incluse. Come mostrato nel seguente esempio, un elemento può contenere una combinazione di altri elementi (le tag possono essere nidificate) e testo. Inoltre, gli elementi possono richiedere o accettare facoltativamente attributi impostati su particolari valori. 

```xml
<tag1>
  <tag2 attributeName="attributeValue">
    ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

Un documento SSML legale completo è composto da un XML Prolog, che contiene informazioni come la codifica e lo schema in base al quale convalidare il documento SSML, seguito dal Root Element, `<speak>`. (Per ulteriori informazioni sulla struttura del Prolog, vedi [tizag.com/xmlTutorial/xmlprolog.php ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.tizag.com/xmlTutorial/xmlprolog.php){: new_window}.) All'interno dell'estensione dell'elemento `<speak>`, specifica il testo che deve essere sintetizzato, ampliato con altri elementi. 

```xml
<!-- The XML Prolog -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE speak PUBLIC "-//W3C//DTD SYNTHESIS 1.0//EN"
  "http://www.w3.org/TR/speech-synthesis/synthesis.dtd">

<!-- Root Element -->
<speak version="1.0" xmlns="www.w3.org/2001/10/synthesis"
  ... the body that contains text to be synthesized plus markup ...
</speak>
```
{: codeblock}

Il servizio supporta i frammenti SSML, che sono elementi SSML che non includono l'intestazione XML completa.

## Supporto SSML
{: #ssmlSupport}

Il servizio {{site.data.keyword.texttospeechshort}} basa il suo supporto su SSML Versione 1.0, consigliato da W3C il 7 settembre 2004. Per ulteriori informazioni sul suggerimento SSML di W3C, vedi [W3C Speech Synthesis Markup Language (SSML) Version 1.0 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.w3.org/TR/speech-synthesis/){: new_window}.

Per ulteriori informazioni sull'utilizzo di SSML con il servizio, consulta quanto segue: 

-   Per informazioni complete sul livello di supporto del servizio per tutti gli elementi SSML, vedi [Elementi SSML](/docs/services/text-to-speech/SSML-elements.html). Con poche eccezioni, il servizio implementa la maggior parte della specifica W3C, così come i frammenti SSML. 
-   Il servizio estende SSML con un elemento `<express-as>` che indica il modo in cui il testo deve essere espresso quando viene pronunciato (come buone notizie, come scuse o con incertezza). Il servizio supporta l'espressività solo per la voce in inglese americano Allison. Vedi [Utilizzo di SSML di espressività](/docs/services/text-to-speech/SSML-expressive.html).
-   Il servizio estende SSML con un elemento `<voice-transformation>` che espande la gamma di possibili voci consentendoti di controllare il tono, la gamma dei toni, la tensione glottidale, la respirazione, la velocità e il timbro del testo pronunciato. Il servizio offre anche due voci virtuali integrate, *Young* e *Soft*. Il servizio supporta la trasformazione della voce solo per le voci in inglese americano. Vedi [Utilizzo di SSML per la trasformazione della voce](/docs/services/text-to-speech/SSML-transformation.html).
-   L'interfaccia di personalizzazione del servizio supporta l'uso dell'elemento `<phoneme>` SSML per specificare l'ortografia fonetica utilizzata per pronunciare una parola. L'ortografia fonetica rappresenta il suono di una parola, in che modo viene sillabato e su quali sillabe viene utilizzato l'accento (stress). 
    -   Per informazioni sull'interfaccia di personalizzazione, vedi [Utilizzo della personalizzazione](/docs/services/text-to-speech/custom-intro.html).
    -   Per informazioni sui simboli validi che puoi utilizzare in una specifica IPA o {{site.data.keyword.IBM_notm}} SPR per qualsiasi lingua supportata, vedi [Utilizzo di IBM SPR](/docs/services/text-to-speech/SPRs.html).

## Convalida SSML
{: #errors}

Il servizio convalida tutti gli elementi SSML che inoltri in qualsiasi contenuto, come testo di input per la sintesi o come la definizione della traduzione di una parola per la personalizzazione. Il servizio non può determinare in anticipo se il testo inoltrato per la sintesi contiene elementi SSML. Di conseguenza, esegue la stessa convalida per tutto il testo di input, indipendentemente dal fatto che contenga SSML. 

-   *Tutto l'input SSML deve essere corretto e ben formato.* Il servizio ignora automaticamente gli elementi SSML non supportati. Il servizio sintetizza il testo contenuto all'interno di un elemento non supportato o di un elemento che utilizza caratteristiche non supportate; l'elemento viene semplicemente ignorato. 
-   *Il servizio riporta un codice di errore HTTP 400 per gli elementi non validi.* La risposta dell'errore include un messaggio descrittivo e la richiesta ha esito negativo. 

Nello specifico, il servizio restituisce un errore nei seguenti casi: 

-   *Elemento non valido.* Ad esempio, specifichi una tag in modo errato, ometti un attributo richiesto o includi una tag di apertura ma non quella di chiusura corrispondente. 
-   *Simbolo non valido.* L'attributo `ph` di un elemento `<phoneme>` include un simbolo IPA o SPR non supportato per la lingua specificata. 
-   *Nessuna vocale.* L'attributo `ph` di un elemento `<phoneme>` specifica la pronuncia di una parola che non contiene vocali. 
-   *La liaison in francese è in una posizione non valida.* Nell'attributo `ph` di un elemento `<phoneme>`, il carattere della liaison non segue una consonante oppure viene utilizzato al centro della pronuncia della parola. 
-   *Il simbolo giapponese `:` non precede una vocale.* Nell'attributo `ph` di un elemento `<phoneme>`, un carattere `:` non si trova prima di una vocale (forse con altri simboli in mezzo, ad esempio la sillabazione).
-   *Accento (stress) sulla sillaba non valido.* L'attributo `ph` di un elemento `<phoneme>` per un {{site.data.keyword.IBM_notm}} SPR include un accento (stress) sulla sillaba non valido. Per il francese, il simbolo dell'accento non precede immediatamente una vocale. Per lo spagnolo o l'italiano, viene utilizzato un accento secondario (`2`) o non ne viene utilizzato alcuno (`0`). Per il giapponese, viene utilizzato un simbolo di accento (stress) secondario (`2`).
-   *Uso non valido dell'elemento `<express-as>` o `<voice-transformation>` SSML.* Puoi utilizzare queste estensioni SSML solo con le voci in inglese americano specificate. 
-   *Uso non valido dell'elemento `<prosody>` SSML.* Non puoi utilizzare questo elemento con le voci `V2` basate su DNN (ad esempio, `en-US_AllisonV2Voice`).
-   *Caratteri di controllo XML senza escape.* Il testo di input stesso contiene un carattere <code>&quot;</code>, <code>&apos;</code>, `&`, `<` o `>` invece della stringa di escape e della codifica del carattere equivalente. Per ulteriori informazioni, vedi [Escape dei caratteri di controllo XML](/docs/services/text-to-speech/http.html#escape).
