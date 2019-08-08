---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-08"

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

# Wissenschaftlicher Hintergrund des Service
{: #science}

Der {{site.data.keyword.texttospeechfull}} Service bietet Stimmen, die auf zwei Arten von Technologie basieren: [Neuronale Sprachtechnologie](#science-neural) und [Konkatenative Synthese](#science-concatenative). Beide Technologien erstellen synthetisch Sprache aus Eingabetext, aber sie verwenden verschiedene Ansätze, um eine Audioausgabe mit unterschiedlichen Eigenschaften zu produzieren. Neuronale Stimmen (`V3`) sind funktional erweiterte Versionen der ursprünglichen konkatenativen Stimmen des Service.
{: shortdesc}

Die synthetische Erstellung von Sprache aus Text ist grundsätzlich komplex. Weitere Informationen zu der wissenschaftlichen Forschung, die hinter der Service-Sprachtechnologie steht, enthalten die Dokumente, die im Abschnitt [Referenzinformationen zur Forschung](/docs/services/text-to-speech?topic=text-to-speech-references) aufgeführt sind.

## Neuronale Sprachtechnologie
{: #science-neural}

Die neuronale Sprachtechnologie synthetisiert Sprache in menschlicher Qualität aus Eingabetext. Der Service analysiert zunächst den Eingabetext, um den gewünschten Inhalt zu bestimmen. Wie bei seinen Verkettungsmodellen verwendet der Service ein akustisches Modell, das aus einem Entscheidungsbaum besteht, um Kandidateneinheiten für die Synthese zu generieren.

Für jeden Laut in einer synthetisch zu erstellenden Lautfolge berücksichtigt das Modell den Laut im Kontext des vorangehenden und des folgenden Lautes. Anschließend erzeugt es eine Reihe von akustischen Einheiten, die hinsichtlich ihrer Eignung ausgewertet werden. Dieser Schritt verringert die Komplexität der Suche, da sie nur auf diejenigen Einheiten beschränkt wird, die einige kontextbezogene Kriterien erfüllen, und alle anderen Einheiten nicht berücksichtigt.

Der Service nutzt dann drei Deep Neural Networks (DNNs), um die akustischen (spektralen) Eigenschaften der Sprache vorherzusagen und die resultierende Audioausgabe zu kodieren:

-   Prosodie-Vorhersage
-   Vorhersage für akustische Features
-   Neuronaler Vocodierer

Während der Synthese sagen die DNNs die Tonhöhe und die Phonemdauer (Satzrhythmus), die spektrale Struktur und die Signalform der Sprache voraus. Das Vorhersagemodul 'prosody' generiert beispielsweise Zielwerte für die linguistischen Features, die aus dem Eingabetext extrahiert werden. Zu den Features gehören Attribute wie die Wortart, die lexikalische Betonung, Prominenz auf Wortebene und Positionsmerkmale, z. B. die Position der Silbe oder des Wortes innerhalb des Satzes.

Die DNNs werden auf eine natürliche menschliche Sprache trainiert, um die akustischen Merkmale der Audioausgabe vorherzusagen. Dieser modulare Ansatz hat den Vorteil, ein schnelles und einfaches Training sowie eine unabhängige Steuerung der einzelnen Komponenten zu ermöglichen. Sobald die Basisnetze trainiert sind, können sie dann an neue Sprechstile oder Stimmen für Branding- und Personalisierungszwecke angepasst werden.

Neuronale Stimmen erzeugen Sprache, die klar klingt und eine sehr natürlich klingende und geschmeidige Tonqualität hat. Weitere Informationen über die neuronale Sprachtechnologie des Service finden Sie unter:

-   Blogbeitrag [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   Forschungspapier [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

## Konkatenative Synthese
{: #science-concatenative}

Die konkatenative Synthese basiert auf einem Inventar akustischer Einheiten aus einem großen Synthesekorpus, um Ausgangssprache für beliebigen Eingabetext zu erzeugen. Er basiert auf der folgenden Prozesskette. Diese Prozesse erleichtern eine effiziente Echtzeitsuche unter den inventarisierten Einheiten, auf die eine Nachverarbeitung der Einheiten folgt.

-   **Akustisches Modell** - Dieses Modell besteht aus einer Entscheidungsstruktur, die für die Generierung der möglichen Einheiten für die Suche zuständig ist. Für jeden Laut in einer synthetisch zu erstellenden Lautfolge berücksichtigt das Modell den Laut im Kontext des vorangehenden und des folgenden Lautes. Anschließend erzeugt es eine Reihe von akustischen Einheiten, die von der Suche hinsichtlich ihrer Eignung ausgewertet werden. Dieser Schritt verringert effizient die Komplexität der Suche, da sie nur auf diejenigen Einheiten beschränkt wird, die einige kontextbezogene Kriterien erfüllen, und alle anderen Einheiten nicht berücksichtigt.
-   **Zielmodelle für Prosodie** - Die Prosodie-Zielmodelle für einige Stimmen basieren auf DRNNs (Deep Recurrent Neural Networks). Bei anderen Stimmen basieren die Modelle auf Entscheidungsstrukturen, um die Prosodie zu bestimmen. In beiden Fällen sind die Modelle für die Generierung von Zielwerten für prosodische Aspekte der Sprache zuständig (z. B. Dauer und Satzmelodie), deren Grundlage eine Folge von linguistischen Merkmalen ist, die aus dem Eingabetext extrahiert wurden. Diese Liste umfasst Attribute wie die Wortart, die lexikalische Betonung, Prominenz auf Wortebene und Positionsmerkmale (z. B. die Position der Silbe oder des Wortes innerhalb des Satzes). Die Zielmodelle für die Prosodie unterstützen die Ausrichtung der Suche auf solche Einheiten, von denen die durch die Modelle vorgegebenen Kriterien für die Prosodie erfüllt werden.
-   **Suche** - Ausgehend von der Liste der Kandidaten, die durch das akustische Modell und die Zielprosodie zurückgegeben werden, fährt dieses Modell einen Viterbi-Suchvorgang durch. Die Suche extrahiert eine Sequenz akustischer Einheiten, die eine Kostenfunktion minimiert, von der der Aufwand sowohl für die Verkettung als auch für das Ziel berücksichtigt wird. Infolgedessen werden akustische Artefakte minimiert, die aus der Verknüpfung von zwei Einheiten entstehen, und das Modul versucht, sich an die durch die Zielmodelle für die Prosodie vorgeschlagene Zielprosodie anzunähern. Dieser Suchvorgang favorisiert außerdem zusammenhängende Blöcke im Synthesekorpus, um solche Artefakte weiter zu reduzieren.
-   **Generierung der Signalform** - Nachdem die Suche die optimale Sequenz von Einheiten zurückgegeben hat, generiert das System mithilfe von PSOLA (Pitch Synchronous Overlap and Add) zeit- und domänengebunden die Ausgabesignalform. PSOLA ist ein Verfahren zur Verarbeitung digitaler Signale, das für die Sprachverarbeitung eingesetzt wird. Es wird insbesondere für die Sprachsynthese genutzt. Mit diesem Verfahren können die Tonhöhe und Dauer eines Sprachsignals geändert sowie die Einheiten, die durch die Suche zurückgegeben werden, nahtlos überblendet werden.

    Für alle linguistischen Funktionen in den obigen Back-End-Prozessen nutzt der Service ein Textverarbeitungs-Front-End, um den Text syntaktisch zu analysieren, bevor aus dem Text synthetisch Sprache in einem Audioformat erstellt wird. Das Front-End bereinigt den Text von allen Formatierungsartefakten wie beispielsweise HTML-Tags. Anschließend bereitet es mithilfe einer proprietären Programmiersprache, die durch sprachabhängige linguistische Regeln gesteuert wird, den Text vor und generiert Aussprachevarianten. Dieses Modul normalisiert sprachabhängige Funktionen des Textes wie z. B. Datumsangaben, Uhrzeiten, Zahlen und Währungswerte. Beispielsweise setzt es Abkürzungen mithilfe eines Wörterverzeichnisses in die Langform um und formuliert anhand von Regeln für Ordinal- und Kardinalzahlen numerische Werte aus.

    Für einige Wörter gibt es mehrere mögliche Aussprachevarianten, weshalb das Textverarbeitung-Front-End zur Laufzeit eine einzige, kanonische Aussprache erzeugt. Diese Strategie bildet möglicherweise nicht die Aussprache ab, die bei der Aufzeichnung des Audiokorpus vom Sprecher verwendet wurde. Der Service erweitert somit eine potenzielle Gruppe von Aussprachevarianten durch alternative Formen, die in einem Wörterverzeichnis für alternative Grundformen inventarisiert sind. Er ermöglicht der Suche die Auswahl von Formen, die im Hinblick auf Problemstellungen und Vorgaben für Tonhöhe, Dauer und Kontiguität Kosten verringern. Dieser Algorithmus erleichtert die Auswahl von längeren zusammenhängenden Blöcken aus dem Datenbestand, was im synthetisch erstellten Ergebnis zu einem optimalen Sprechfluss führt.
