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

# Wissenschaftlicher Hintergrund des Service
{: #science}

Der {{site.data.keyword.texttospeechshort}}-Service ist ein konkatenatives System, das sich auf eine Inventarisierung akustischer Einheiten aus einem umfangreichen Synthesekorpus stützt, um Sprachausgabe für beliebigen Eingabetext zu erzeugen. Er basiert auf der folgenden Prozesskette. Diese Prozesse erleichtern eine effiziente Echtzeitsuche unter den inventarisierten Einheiten, auf die eine Nachverarbeitung der Einheiten folgt.
{: shortdesc}

-   **Akustisches Modell** - Dieses Modell besteht aus einer Entscheidungsstruktur, die für die Generierung der möglichen Einheiten für die Suche zuständig ist. Für jeden Laut in einer synthetisch zu erstellenden Lautfolge berücksichtigt das Modell den Laut im Kontext des vorangehenden und des folgenden Lautes. Anschließend erzeugt es eine Reihe von akustischen Einheiten, die von der Suche hinsichtlich ihrer Eignung ausgewertet werden. Dieser Schritt verringert effizient die Komplexität der Suche, da sie nur auf diejenigen Einheiten beschränkt wird, die einige kontextbezogene Kriterien erfüllen, und alle anderen Einheiten nicht berücksichtigt.
-   **Zielmodelle für Prosodie** - Diese Modelle bestehen aus DRNNs (Deep Recurrent Neural Networks). Die Modelle sind für die Generierung von Zielwerten für prosodische Aspekte der Sprache zuständig (z. B. Dauer und Satzmelodie), deren Grundlage eine Folge von linguistischen Merkmalen ist, die aus dem Eingabetext extrahiert wurden. Diese Liste umfasst Attribute wie die Wortart, die lexikalische Betonung, Prominenz auf Wortebene und Positionsmerkmale (z. B. die Position der Silbe oder des Wortes innerhalb des Satzes). Die Zielmodelle für die Prosodie unterstützen die Ausrichtung der Suche auf solche Einheiten, von denen die durch das Modell vorgegebenen Kriterien für die Prosodie erfüllt werden.
-   **Suche** - Ausgehend von der Liste der Kandidaten, die durch das akustische Modell und die Zielprosodie zurückgegeben werden, fährt dieses Modell einen Viterbi-Suchvorgang durch. Die Suche extrahiert eine Sequenz akustischer Einheiten, die eine Kostenfunktion minimiert, von der der Aufwand sowohl für die Verkettung als auch für das Ziel berücksichtigt wird. Infolgedessen werden akustische Artefakte minimiert, die aus der Verknüpfung von zwei Einheiten entstehen, und das Modul versucht, sich an die durch die Zielmodelle für die Prosodie vorgeschlagene Zielprosodie anzunähern. Dieser Suchvorgang favorisiert außerdem zusammenhängende Blöcke im Synthesekorpus, um solche Artefakte weiter zu reduzieren.
-   **Generierung der Signalform** - Nachdem die Suche die optimale Sequenz von Einheiten zurückgegeben hat, generiert das System mithilfe von PSOLA (Pitch Synchronous Overlap and Add) zeit- und domänengebunden die Ausgabesignalform. PSOLA ist ein Verfahren zur Verarbeitung digitaler Signale, das für die Sprachverarbeitung eingesetzt wird. Es wird insbesondere für die Sprachsynthese genutzt. Mit diesem Verfahren können die Tonhöhe und Dauer eines Sprachsignals geändert sowie die Einheiten, die durch die Suche zurückgegeben werden, nahtlos überblendet werden.

    Für alle linguistischen Funktionen in den obigen Back-End-Prozessen nutzt der Service ein Textverarbeitungs-Front-End, um den Text syntaktisch zu analysieren, bevor aus dem Text synthetisch Sprache in einem Audioformat erstellt wird. Das Front-End bereinigt den Text von allen Formatierungsartefakten wie beispielsweise HTML-Tags. Anschließend bereitet es mithilfe einer proprietären Programmiersprache, die durch sprachabhängige linguistische Regeln gesteuert wird, den Text vor und generiert Aussprachevarianten. Dieses Modul normalisiert sprachabhängige Funktionen des Textes wie z. B. Datumsangaben, Uhrzeiten, Zahlen und Währungswerte. Beispielsweise setzt es Abkürzungen mithilfe eines Wörterverzeichnisses in die Langform um und formuliert anhand von Regeln für Ordinal- und Kardinalzahlen numerische Werte aus.

    Für einige Wörter gibt es mehrere mögliche Aussprachevarianten, weshalb das Textverarbeitung-Front-End zur Laufzeit eine einzige, kanonische Aussprache erzeugt. Diese Strategie bildet möglicherweise nicht die Aussprache ab, die bei der Aufzeichnung des Audiokorpus vom Sprecher verwendet wurde. Der Service erweitert somit eine potenzielle Gruppe von Aussprachevarianten durch alternative Formen, die in einem Wörterverzeichnis für alternative Grundformen inventarisiert sind. Er ermöglicht der Suche die Auswahl von Formen, die im Hinblick auf Problemstellungen und Vorgaben für Tonhöhe, Dauer und Kontiguität Kosten verringern. Dieser Algorithmus erleichtert die Auswahl von längeren zusammenhängenden Blöcken aus dem Datenbestand, was im synthetisch erstellten Ergebnis zu einem optimalen Sprechfluss führt.

Die synthetische Erstellung von Sprache aus Text ist grundsätzlich ein komplexes Feld; jede Erläuterung des Service erfordert daher eine tiefer gehende Erklärung, als von dieser kurzen Zusammenfassung geboten werden kann. Weitere Informationen zu der wissenschaftlichen Forschung, die hinter dem Service steht, enthalten die Dokumente, die im Abschnitt [Referenzinformationen zur Forschung](/docs/services/text-to-speech/references.html) aufgeführt sind.
