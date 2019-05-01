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

# SSML per la trasformazione della voce
{: #transformation}

Il servizio {{site.data.keyword.texttospeechfull}}, come la maggior parte dei sistemi di sintesi vocale, può esprimersi solo con un numero limitato di voci. Inoltre, alcune lingue offrono solo una o due voci. Per espandere la gamma di possibili voci, il servizio estende SSML con un elemento `<voice-transformation>`. Puoi utilizzare questo elemento per realizzare voci virtuali diverse controllando gli aspetti di una voce predefinita. Le applicazioni della funzione includono:
{: shortdesc}

-   *Dare un'altra intonazione a una voce.* Vuoi che l'intonazione della voce sia leggermente diversa in generale o per una specifica applicazione. 
-   *Personalizzazione della voce.* Vuoi utilizzare una voce particolare per differenziare le tue applicazioni. 
-   *Applicazioni multiruolo.* Hai bisogno di più voci per rappresentare persone diverse. 

Puoi applicare l'elemento `<voice-transformation>` all'intero corpo del testo, a un periodo o a una parola o un frammento. L'elemento accetta un attributo obbligatorio, `type`, che descrive il tipo di trasformazione della voce da applicare al testo specificato. Puoi applicare una trasformazione integrata oppure creare una trasformazione personalizzata basata su diversi aspetti della voce. 

## Supporto linguistico
{: #languages-transformation}

Il servizio supporta la trasformazione della voce solo per le seguenti voci in inglese americano:

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

La trasformazione della voce non è supportata con `V2`, le versioni basate su DNN di queste voci (ad esempio, `en-US_AllisonV2Voice`). L'utilizzo dell'elemento con una voce non supportata restituisce un errore. 

## Trasformazioni integrate

Le trasformazioni integrate applicano modifiche preconfigurate agli attributi di una voce. Pensa a loro come a voci virtuali rese disponibili dal servizio. Il servizio offre due trasformazioni integrate. Per utilizzarle, specifica il nome sensibile al maiuscolo/minuscolo della trasformazione integrata con l'attributo `type`:

-   `Young` dà alla voce un'intonazione più giovanile. 
-   `Soft` rende la voce più morbida. 

Puoi applicare l'attributo `strength` facoltativo alla voce integrata per controllare in che misura il servizio applica la trasformazione. Pensa al valore come a un fattore di fusione che il servizio applica alla voce originale. L'attributo accetta un valore compreso nell'intervallo da 0 a 100 percento. Se specifichi `0%` la voce rimane inalterata; se specifichi `100%` ottieni la misura completa della trasformazione. Se ometti l'attributo, l'intensità predefinita è `100%`.

Il servizio ignora gli attributi per le trasformazioni personalizzate quando utilizzi una trasformazione integrata.
{: note}

## Esempi di trasformazione integrata

I seguenti esempi applicano le due trasformazioni integrate alla stessa frase con intensità diverse: 

```xml
<voice-transformation type="Young" strength="80%">
  Could you provide us with new information?
</voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Could you provide us with new information?
</voice-transformation>
```
{: codeblock}

## Trasformazioni personalizzate

Le trasformazioni personalizzate ti danno un maggiore controllo sui diversi aspetti della trasformazione della voce. Per utilizzare una trasformazione personalizzata, specifica `Custom` per l'attributo `type`. Puoi quindi utilizzare uno o più degli attributi facoltativi riportati di seguito per controllare la trasformazione. 

<table>
  <caption>Tabella 1. Attributi della trasformazione personalizzata</caption>
  <tr>
    <th style="width:15%; text-align:left">Attributo</th>
    <th style="width:25%; text-align:center">Intervallo</th>
    <th style="text-align:left">Descrizione</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Modifica relativa normalizzata del livello medio di intonazione
      entro i limiti di sicurezza. L'attributo controlla il livello di
      tono medio percepito. Viene preso in prestito dall'attributo
      <code>pitch</code> dell'elemento
      <code>&lt;prosody&gt;</code> SSML. Contribuisce al
      cambiamento dell'identità dell'oratore percepito.
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-narrow</code>, <code>narrow</code>, <code>default</code>,
      <code>wide</code>, <code>x-wide</code>]</td>
    <td>
      Modifica relativa normalizzata dell'intervallo dinamico di intonazione
      entro i limiti di sicurezza. L'aumento o la riduzione della gamma dei
      toni rende lo stile del discorso più o meno espressivo. L'attributo
      viene preso in prestito dall'attributo <code>range</code>
      dell'elemento <code>&lt;prosody&gt;</code> SSML.</td>
  </tr>
  <tr>
    <td><code>glottal_tension</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Modifica relativa normalizzata della tensione glottidale entro i limiti
      di sicurezza. L'aumento o la riduzione della tensione glottidale viene
      percepita come una qualità di riproduzione vocale più tesa o morbida. Un
      valore positivo potrebbe produrre un ronzio che puoi alleviare
      aumentando il valore dell'attributo <code>breathiness</code>. Un valore
      negativo viene percepito come un suono più arioso e generalmente più piacevole.
    </td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Modifica relativa normalizzata del livello percepito del rumore di
      aspirazione entro i limiti di sicurezza. I valori estremi potrebbero
      produrre un discorso rumoroso (per breathiness positivo) o un ronzio
      (per breathiness negativo). Utilizza questo attributo per compensare
      il ronzio o il rumore supplementare prodotto come effetto collaterale
      degli altri attributi.
    </td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-slow</code>, <code>slow</code>, <code>default</code>,
      <code>fast</code>, <code>x-fast</code>]</td>
    <td>
      Modifica relativa normalizzata della velocità di pronuncia entro i limiti di sicurezza.
      L'aumento o la riduzione della velocità rende il discorso più veloce o più lento.
      Una velocità positiva (più veloce) rende la gamma di toni percepiti più ampia
      e una velocità negativa (più lenta) riduce la gamma di toni percepiti.
      L'attributo viene preso in prestito dall'attributo <code>rate</code>
      dell'elemento <code>&lt;prosody&gt;</code> SSML.</td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>,
      <code>Breeze</code>]</td>
    <td>
      Il nome sensibile al maiuscolo/minuscolo di una delle trasformazioni del
      tratto vocale integrate: <code>Sunrise</code> oppure <code>Breeze</code>.
      I nomi sono simbolici. Fai esperimenti con i timbri per capire come
      influiscono sulla trasformazione della voce. L'attributo contribuisce
      al cambiamento dell'identità dell'oratore percepito.
    </td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0%, 100%]</td>
    <td>
      La misura della trasformazione del tratto vocale <code>timbre</code>:
      <code>0%</code> annulla la trasformazione; <code>100%</code>
      rappresenta l'applicazione completa della trasformazione. L'attributo
      quantifica la differenza tra la voce trasformata e quella
      originale. Consente la fusione del timbro selezionato con quello
      della voce originale. Anche a valori di misura moderati del timbro,
      l'attributo <code>timbre</code> contribuisce al cambiamento
      dell'identità dell'operatore percepito.
    </td>
  </tr>
</table>

### Utilizzo degli intervalli
{: #ranges}

Gli intervalli numerici dei diversi attributi indicano in che misura l'attributo influisce sulla voce. Ad esempio, l'attributo `rate` ha un intervallo da -100% a 100%:

-   Un valore di `100%` non significa che la voce diventa più veloce del 100% . Significa che il servizio aumenta la velocità della voce al valore massimo consentito per tale voce. 
-   Un valore di `-100%` significa che il servizio utilizza la velocità minima consentita per la voce. 
-   Un valore di `0%` rappresenta il livello intrinseco dell'attributo per la voce; la voce rimane invariata. 

### Utilizzo dei valori letterali
{: #literals}

Per praticità, molti degli attributi definiscono anche valori letterali che puoi utilizzare al posto delle percentuali. Il significato di questi valori è diverso dai valori utilizzati dall'elemento `<prosody>` SSML. L'elemento `<voice-transformation>` utilizza una scala coerente tra i suoi attributi. 

-   `x-low`, `x-slow` e `x-narrow` sono uguali a un valore di `-100%`.
-   `low`, `slow` e `narrow` sono uguali a un valore di `-50%`.
-   `default` è uguale a un valore di `0%`, il valore predefinito per tale attributo e voce. 
-   `high`, `fast` e `wide` sono uguali a un valore di `+50%`.
-   `x-high`, `x-fast` e `x-wide` sono uguali a un valore di `+100%`.

### Linee guida di utilizzo
{: #guidelines}

Utilizza le seguenti linee guida e informazioni di avvertenza: 

-   Per la personalizzazione della voce o le applicazioni multiruolo, utilizza gli attributi `timbre`, `pitch` e `glottal_tension` per cambiare l'identità dell'oratore percepito. Puoi utilizzare combinazioni di questi tre attributi per creare voci virtuali. Considera una voce virtuale come un punto nello spazio multidimensionale che viene realizzato dal timbro, dal tono e dalla tensione glottidale specificati. Combinazioni diverse degli attributi producono voci virtuali diverse. 
-   Puoi utilizzare gli attributi `pitch_range`, `breathiness` e `rate` per aggiungere intonazione a una voce virtuale. Altri utenti possono scegliere gli stessi attributi o attributi simili, quindi il servizio non può garantire l'unicità della tua voce virtuale. 
-   Tieni presente i seguenti potenziali effetti collaterali dell'applicazione degli attributi: 
    -   Tensione glottidale elevata, tono elevato e velocità bassa possono causare il ronzio. Aumenta la respirazione per mitigare l'effetto. 
    -   La tensione glottidale estremamente bassa può produrre un discorso rumoroso. Riduci la respirazione per ridurre il rumore. 
    -   L'aumento o la riduzione della gamma di toni e della velocità a valori estremi contemporaneamente può rendere innaturale un discorso. 
-   Come osservato, alcuni degli attributi vengono presi in prestito dall'elemento `<prosody>` SSML. Per ulteriori informazioni, vedi [L'elemento prosody](/docs/services/text-to-speech/SSML-elements.html#prosody_element). Per abilitare un buon controllo della prosodia di una voce virtuale, puoi: 
    -   Nidificare gli elementi `<prosody>` all'interno degli elementi `<voice-transformation>`.
    -   Nidificare gli elementi `<voice-transformation>` all'interno degli elementi `<prosody>`.

    *Non puoi* nidificare gli elementi `<voice-transformation>`.

## Esempi di trasformazione personalizzata

I seguenti esempi applicano attributi diversi per dimostrare le possibili applicazioni della trasformazione personalizzata. Il primo esempio riduce la tensione glottidale per rendere la voce più morbida. Aumenta anche la gamma di toni e la velocità in modo moderato per introdurre uno stile di pronuncia più dinamico. 

```xml
<voice-transformation type="Custom" glottal_tension="-50%"
  pitch_range="30%" rate="10%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

Il secondo esempio utilizza la tensione glottidale massima, il tono massimo e la velocità minima. Combinazioni di questo tipo generalmente non sono vantaggiose e possono produrre un ronzio. L'esempio mitiga questo effetto aumentando la respirazione. 

```xml
<voice-transformation type="Custom" glottal_tension="100%" pitch="100%"
  rate="-100%" breathiness="60%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

I due prossimi esempi cambiano l'identità dell'oratore percepito applicando il timbro. La voce viene alterata controllando la misura della fusione e cambiando il livello del tono. Il primo esempio utilizza la misura di timbro predefinita, 100%.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="40%">
  Do you have more information?
</voice-transformation>

<voice-transformation type="Custom" timbre="Breeze" timbre_extent="30%"
  pitch="-30%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

L'esempio finale utilizza più attributi per trasformare la voce. L'esempio utilizza la misura di timbro predefinita e omette la respirazione. 

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="-30%"
  pitch_range="80%" rate="60%" glottal_tension="-80%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}
