---

copyright:
  years: 2019
lastupdated: "2019-07-08"

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

# La scienza alla base del servizio
{: #science}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} si basa su una tecnologia di voce neurale per sintetizzare un discorso di qualità umana dal testo di input. Le voci neurali producono un discorso nitido e chiaro, con una qualità audio dal suono molto naturale e fluido.
{: shortdesc}

Il servizio analizza prima il testo di input per determinare il contenuto desiderato. Utilizza un modello acustico che consiste in una struttura ad albero delle decisioni per generare le unità candidate per la sintesi. Per ciascuno dei telefoni presenti in una sequenza di telefoni da sintetizzare, il modello considera il telefono nel contesto di due telefoni, quello precedente e quello successivo. Produce quindi una serie di unità acustiche di cui viene valutata l'idoneità. Questo passo riduce la complessità della ricerca restringendola a quelle unità che soddisfano alcuni criteri contestuali ed eliminando tutte le altre. 

Il servizio utilizza quindi tre DNN (Deep Neural Network) per prevedere le caratteristiche acustiche (spettrali) del discorso e codificare l'audio risultante: 

-   Previsione della prosodia 
-   Previsione della caratteristica acustica 
-   Vocoder neurale 

Durante la sintesi, le DNN prevedono la durata tonale e fonemica (prosodia), la struttura spettrale e la forma d'onda del discorso. Ad esempio, il modulo di previsione della prosodia genera dei valori di destinazione per le caratteristiche linguistiche estratte dal testo di input. Le caratteristiche includono attributi quali la parte del discorso, l'accento lessicale, la prominenza a livello delle parole e le caratteristiche posizionali quali la posizione della sillaba o della parola nella frase. 

Le DNN sono addestrate sul discorso umano naturale per prevedere le caratteristiche acustiche dell'audio. Questo approccio modulare presenta il vantaggio di consentire un addestramento facile e veloce, così come il controllo indipendente di ciascun componente. Una volta addestrate, le reti di base possono essere adattate a nuove voci o nuovi stili di pronuncia per finalità di consolidamento del marchio e di personalizzazione. 

Per ulteriori informazioni sulla tecnologia vocale neurale del servizio, vedi 

-   Il post del blog [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external} 
-   L'articolo di ricerca [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external} 

L'argomento della sintetizzazione del testo in voce è intrinsecamente complesso. Per ulteriori informazioni sulla ricerca scientifica alla base della tecnologia vocale del servizio, consulta i documenti elencati in [Riferimenti di ricerca](/docs/services/text-to-speech-data?topic=text-to-speech-data-references).
