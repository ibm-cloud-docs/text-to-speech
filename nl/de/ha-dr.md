---

copyright:
  years: 2019
lastupdated: "2019-03-19"

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

# Hochverfügbarkeit und Disaster-Recovery
{: #ha-dr}

Der {{site.data.keyword.texttospeechfull}}-Service ist an jedem {{site.data.keyword.cloud_notm}}-Standort (z. B. Dallas oder Washington, DC) hoch verfügbar. Die mögliche Disaster-Recovery für einen gesamten Standort setzt jedoch Planung und  Vorbereitung voraus.
{: shortdesc}

Sie müssen selbst dafür sorgen, dass Sie Ihre Konfiguration, Ihre Anpassung und Ihre Nutzung des Service kennen. Sie sind ebenfalls dafür verantwortlich, alle Vorbereitungen für die erneute Erstellung einer Instanz des Service an einem neuen Standort und für die Wiederherstellung Ihrer Daten an einem beliebigen Standort zu treffen.

## Hochverfügbarkeit
{: #high-availability}

Der {{site.data.keyword.texttospeechshort}}-Service unterstützt eine Hochverfügbarkeit ohne Single Point of Failure. Er erzielt die Hochverfügbarkeit automatisch und transparent durch die von {{site.data.keyword.cloud_notm}} bereitgestellte Funktion für Regionen mit mehreren Zonen (Multi-Zone Region, MZR).

{{site.data.keyword.cloud_notm}} ermöglicht an einem einzigen Standort mehrere Zonen ohne einen gemeinsamen Single Point of Failure. Darüber hinaus wird ein automatischer Lastausgleich unter den Zonen innerhalb einer Region zur Verfügung gestellt.

## Disaster-Recovery
{: #disaster-recovery}

Die Disaster-Recovery kann problematisch sein, falls an einem {{site.data.keyword.cloud_notm}}-Standort ein erheblicher Fehler auftritt, der auch einen möglichen Datenverlust einschließt. Da Regionen mit mehreren Zonen nicht standortübergreifend verfügbar sind, müssen Sie warten, bis {{site.data.keyword.IBM_notm}} einen Standort wieder in den Onlinestatus versetzt, falls die Verfügbarkeit des Standortes unterbrochen wird. Wenn der Fehler die zugrunde liegenden Datenservices beeinträchtigt, müssen Sie außerdem warten, bis {{site.data.keyword.IBM_notm}} diese Datenservices wiederhergestellt hat.

Bei einem katastrophalen Fehler ist {{site.data.keyword.IBM_notm}} möglicherweise nicht in der Lage, Daten aus Datenbanksicherungen wiederherzustellen. In diesem Fall müssen Sie Ihre Daten wiederherstellen, um die Serviceinstanz wieder in den aktuellen Zustand zu versetzen. Die Daten können Sie an demselben oder oder an einem anderen Standort wiederherstellen.

Beim {{site.data.keyword.texttospeechshort}}-Service werden nur Daten für angepasste Sprechmodelle in {{site.data.keyword.cloud_notm}} gespeichert. Für Ihren Disaster-Recovery-Plan müssen Sie auch Ihre angepassten Sprechmodelle kennen, aufbewahren und auf eine Wiederherstellung vorbereiten.

### Angepasste Sprechmodelle sichern
{: #disaster-recovery-backup}

Bewahren Sie die folgenden Informationen zu Ihren angepassten Sprechmodellen und deren angepassten Einträgen auf:

-   Liste aller angepassten Sprechmodelle und ihrer Definitionen. So können Sie Informationen zu Ihren angepassten Modellen auflisten:
    -   Verwenden Sie die Methode `GET /v1/customizations`, um Informationen zu allen angepassten Modellen aufzulisten. Weitere Informationen hierzu finden Sie unter [Alle angepassten Modelle abfragen](/docs/services/text-to-speech/custom-models.html#cuModelsQueryAll).
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}`, um Informationen zu einem angegebenen angepassten Modell aufzulisten. Weitere Informationen hierzu finden Sie unter [Angepasstes Modell abfragen](/docs/services/text-to-speech/custom-models.html#cuModelsQuery).
-   Informationen zu allen angepassten Einträgen (Paare aus Wort und Umsetzung) in Ihren angepassten Sprechmodellen:
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}/words`, um Informationen zu allen Paaren aus Wort und Umsetzung aus einem angepassten Modell aufzulisten. Weitere Informationen hierzu finden Sie unter [Alle Wörter aus einem angepassten Modell abfragen](/docs/services/text-to-speech/custom-entries.html#cuWordsQueryModel).
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}/words/{word}`, um Informationen zu einem bestimmten Paar aus Wort und Umsetzung aus einem angepassten Modell aufzulisten. Weitere Informationen hierzu finden Sie unter [Einzelnes Wort aus einem angepassten Modell abfragen](/docs/services/text-to-speech/custom-entries.html#cuWordQueryModel).

Es hat sich bewährt, diese Informationen in einem Format aufzubewahren, das die erneute Erstellung Ihrer angepassten Sprechmodelle bei einem Fehler möglich macht. Wenn Sie die Informationen zu Ihren angepassten Modellen und angepassten Einträgen aktiv verwalten und im Voraus die im folgenden Abschnitt aufgeführten Aufrufe vorbereiten, können Sie die Wiederherstellung so schnell wie möglich durchführen.

### Angepasste Sprechmodelle wiederherstellen
{: #disaster-recovery-restore}

Falls eine Disaster-Recovery erforderlich werden sollte, können Sie Ihre angepassten Sprechmodelle und deren angepassten Einträge mithilfe der Sicherungsinformationen erneut erstellen:

1.  Verwenden Sie für die erneute Erstellung Ihrer angepassten Sprechmodelle die Methode `POST /v1/customizations`. Weitere Informationen hierzu finden Sie im Abschnitt [Angepasstes Modell erstellen](/docs/services/text-to-speech/custom-models.html#cuModelsCreate).
1.  Verwenden Sie zum Hinzufügen mehrerer Paare aus Wort und Umsetzung zu Ihren angepassten Sprechmodellen die Methode `POST /v1/customizations/{customization_id}/words`. Weitere Informationen hierzu finden Sie unter [Mehrere Wörter zu einem angepassten Modell hinzufügen](/docs/services/text-to-speech/custom-entries.html#cuWordsAdd).
1.  Verwenden Sie zum Hinzufügen eines einzelnen Paares aus Wort und Umsetzung zu Ihren angepassten Sprechmodellen die Methode `POST /v1/customizations/{customization_id}/words/{word}`. Weitere Informationen hierzu finden Sie unter [Einzelnes Wort zu einem angepassten Modell hinzufügen](/docs/services/text-to-speech/custom-entries.html#cuWordAdd).

Alle angepassten Einträge können Sie auf einmal, in Gruppen oder einzeln nacheinander hinzufügen.
