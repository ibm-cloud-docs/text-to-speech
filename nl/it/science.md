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

# La scienza alla base del servizio
{: #science}

Il servizio {{site.data.keyword.texttospeechshort}} è un sistema concatenativo che si basa su un inventario di unità acustiche derivanti da un corpus di sintesi di grandi dimensioni per produrre il discorso di output per il testo di input arbitrario. Si basa sulle seguenti pipeline dei processi. Questi processi facilitano una ricerca in tempo reale ed efficiente in questo inventario di unità seguita da una post-elaborazione delle unità.
{: shortdesc}

-   **Modello acustico** - Questo modello è composto da una struttura ad albero delle decisioni responsabile della generazione di unità candidate per la ricerca. Per ciascuno dei telefoni presenti in una sequenza di telefoni da sintetizzare, il modello considera il telefono nel contesto di due telefoni, quello precedente e quello successivo. Produce quindi una serie di unità acustiche che la ricerca valuta per l'idoneità. Questo passo riduce in modo efficace la complessità della ricerca restringendola a quelle unità che soddisfano alcuni criteri contestuali ed eliminando tutte le altre. 
-   **Modelli finali di prosodia** - Questo modelli sono composti da reti neurali ricorrenti profonde (Deep Recurrent Neural Networks - RNN). I modelli sono responsabili della generazione dei valori finali per gli aspetti prosodici del discorso (ad esempio durata e intonazione), data una sequenza di caratteristiche linguistiche estratte dal testo di input. Questo elenco include attributi come ad esempio una parte del discorso, lo stress lessicale, l'importanza del livello di parole e le caratteristiche di posizionamento (ad esempio, la posizione della sillaba o della parola nella frase). I modelli finali di prosodia ti aiutano a guidare la ricerca verso quelle unità che soddisfano i criteri prosodici previsti da questo modello. 
-   **Ricerca** - Dato l'elenco dei candidati restituiti dal modello acustico e dalla prosodia finale, questo modulo esegue una ricerca Viterbi. La ricerca estrae una sequenza delle unità acustiche che riduce una funzione di costo che considera sia i costi di concatenazione che finali. Di conseguenza, le risorse udibili provenienti dall'unione di due unità sono ridotte al minimo e il modulo tenta di approssimarsi alla prosodia finale suggerita dai modelli finali di prosodia. Questa ricerca favorisce anche i blocchi contigui nel corpus di sintesi per ridurre ulteriormente tali risorse. 
-   **Generazione di waveform** - Quando la ricerca restituisce la sequenza ottimale di unità, il sistema utilizza PSOLA (Pitch Synchronous Overlap and Add - Sovrapposizione e aggiunta a toni sincroni) del dominio del tempo per generare un waveform di output. PSOLA è una tecnica di elaborazione del segnale digitale che viene utilizzata per l'elaborazione di un discorso. Nello specifico, viene utilizzata per la sintesi vocale. Può modificare il tono e la durata di un segnale vocale e combinare le unità restituite dalla ricerca senza soluzione di continuità. 

    Per tutte le caratteristiche linguistiche nei processi di backend precedenti, il servizio utilizza un frontend di elaborazione del testo per analizzare il testo prima di sintetizzarlo in formato audio. Il frontend ripulisce il testo dalle risorse di formattazione come le tag HTML. Utilizza quindi una lingua proprietaria guidata da regole linguistiche che dipendono dalla lingua per preparare il testo e generare la pronuncia. Questo modulo normalizza le funzioni che dipendono dalla lingua del testo come date, ore, numeri e valuta. Ad esempio, esegue l'espansione abbreviata da un dizionario e da un'espansione numerica dalle regole per i numeri ordinali e cardinali. 

    Per alcune parole si possono utilizzare più pronunce, quindi il frontend di elaborazione del testo produce innanzitutto una singola pronuncia canonica nel runtime. Questo approccio potrebbe non riflettere la pronuncia che l'oratore ha utilizzato quando è stato registrato il corpus audio. Di conseguenza, il servizio amplia una serie candidata di pronunce con forme alternative archiviate in un dizionario di base alternativo. Consente alla ricerca di scegliere i formati che riducono il costo in termini di problemi e limitazioni di tono, durata e contiguità. Questo algoritmo facilita la selezione di blocchi contigui più lunghi provenienti dal dataset, ottenendo un flusso ottimale del discorso nel risultato sintetizzato. 

L'argomento della sintetizzazione del testo in voce è intrinsecamente complesso e qualsiasi spiegazione del servizio richiede una profondità esplicativa maggiore di quanto questo breve riepilogo possa contenere. Per ulteriori informazioni sulla ricerca scientifica alla base del servizio, consulta i documenti elencati in [Riferimenti di ricerca](/docs/services/text-to-speech/references.html).
