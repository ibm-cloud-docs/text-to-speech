---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-04"

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

# Informationssicherheit
{: #information-security}

{{site.data.keyword.IBM}} hat sich dazu verpflichtet, seinen Kunden und Partnern innovative Lösungen für Datenschutz, Sicherheit und Governance zu bieten.
{: shortdesc}

Kunden sind selbst für die Einhaltung der geltenden Gesetze und Bestimmungen verantwortlich, was auch die Datenschutzgrundverordnung (DSGVO) der Europäischen Union beinhaltet. Kunden sollten sich von kompetenter juristischer Stelle zu Inhalt und Auslegung aller relevanten Gesetze und Vorschriften beraten lassen, die ihre Geschäftstätigkeit und die von ihnen eventuell einzuleitenden Maßnahmen zur Einhaltung dieser Gesetze und Vorschriften betreffen.
{: important}

Die in dieser Dokumentation beschriebenen Produkte, Services und Leistungsmerkmale sind möglicherweise nicht für alle Kundensituationen geeignet und nur eingeschränkt verfügbar. {{site.data.keyword.IBM_notm}} erteilt keine Rechts-, Steuer- oder Auditberatung und gibt keine Garantie bezüglich der Konformität von IBM Produkten oder Services mit den geltenden Gesetzen und Vorschriften.

Falls Sie für die erstellten {{site.data.keyword.cloud}} {{site.data.keyword.watson}}-Ressourcen Unterstützung hinsichtlich der DSGVO benötigen, ziehen Sie Folgendes hinzu:

-   Lesen Sie für Ressourcen, die in der Europäischen Union (EU) erstellt werden, den Abschnitt [Unterstützung für {{site.data.keyword.cloud_notm}}-Ressourcen anfordern, die in der Europäischen Union erstellt werden](/docs/services/watson?topic=watson-gdpr-sar#request-EU).
-   Lesen Sie für Ressourcen, die außerhalb der EU erstellt werden, den Abschnitt [Unterstützung für Ressourcen anfordern, die außerhalb der Europäischen Union erstellt werden](/docs/services/watson?topic=watson-gdpr-sar#request-non-EU).

## Datenschutz-Grundverordnung der Europäischen Union (DSGVO)
{: #gdpr}

{{site.data.keyword.IBM_notm}} hat sich dazu verpflichtet, seinen Kunden und Partnern innovative Lösungen für Datenschutz, Sicherheit und Governance zu bieten und sie bei der Einhaltung der DSGVO zu unterstützen.

Weitere Informationen zu den eigenen Maßnahmen von {{site.data.keyword.IBM_notm}} für die Einhaltung der DSGVO sowie zu den Leistungsmerkmalen und Angeboten, die Ihnen dabei helfen, die Einhaltung der DSGVO vorzubereiten, finden Sie [hier](http://www.ibm.com/gdpr){: external}.

## Daten im Text to Speech-Service kennzeichnen und löschen
{: #gdpr-text-to-speech}

Beim {{site.data.keyword.texttospeechfull}}-Service können Sie alle Daten löschen, die mit Sprachsyntheseanforderungen und angepassten Sprechmodellen verbunden sind. Zum Löschen der Daten müssen Sie Folgendes ausführen:

1.  Ordnen Sie mit dem Header `X-Watson-Metadata` eine Kunden-ID zu Daten zu, die durch eine Anforderung an den Service übergeben werden; entsprechende Informationen finden Sie unter [Kunden-ID angeben](#specify-customer-id).
1.  Verwenden Sie die Methode `DELETE /v1/user_data`, um alle Daten zu löschen, die einer bestimmten Kunden-ID zugeordnet sind; Näheres hierzu enthält der Abschnitt [Daten löschen](#delete-pi).

Standardmäßig wird den Daten keine Kunden-ID zugeordnet.

Experimentelle und Beta-Funktionen sind nicht für die Verwendung in einer Produktionsumgebung gedacht; beim Kennzeichnen und Löschen von Daten kann ihre erwartungsgemäße Funktionsweise daher nicht garantiert werden. Experimentelle und Beta-Funktionen sollten nicht bei der Implementierung einer Lösung verwendet werden, die das Kennzeichnen und Löschen von Daten erforderlich macht.
{: note}

### Kunden-ID angeben
{: #specify-customer-id}

Um Daten eine Kunden-ID zuzuordnen, nehmen Sie den Header `X-Watson-Metadata` in die Anforderung auf, mit der die Informationen übergeben werden. Als Argument des Headers übergeben Sie die Zeichenfolge `customer_id={id}`. Im folgenden Beispiel wird die Kunden-ID `my_ID` den Daten zugeordnet, die mit einer Anforderung `POST /v1/synthesize` übergeben werden:

```bash
curl -X POST -u "apikey:{apikey}"
--header "X-Watson-Metadata: customer_id=my_ID"
--header "Content-Type: application/json"
--header "Accept: audio/wav"
--data "{\"text\":\"hello world\"}"
--output hello_world.wav
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```

Mit Ausnahme des Semikolons (`;`) und des Gleichheitszeichens (`=`) können Sie in einer Kunden-ID jedes beliebige Zeichen verwenden. Geben Sie für die Kunden-ID eine zufällige oder allgemeine Zeichenfolge an; verwenden Sie keine erkennbar persönlichen Angaben wie beispielsweise eine E-Mail-Adresse oder eine Twitter-ID. Sie können bei unterschiedlichen Anforderungen verschiedene Kunden-IDs angeben. Eine Kunden-ID, die Sie angeben, ist der Instanz des Service zugeordnet, dessen Berechtigungsnachweise mit der Anforderung verwendet werden. Nur Berechtigungsnachweise für diese Instanz des Service können Daten löschen, die der ID zugeordnet sind.

Verwenden Sie den Header `X-Watson-Metadata` bei den folgenden Methoden:

-   HTTP-Anforderungen:
    -   `POST /v1/synthesize`
    -   `GET /v1/synthesize`

    Die Kunden-ID wird den Daten zugeordnet, die mit der Anforderung gesendet werden.

-   WebSocket-Anforderungen:
    -   `/v1/synthesize`

    Geben Sie hierbei die Kunden-ID mit dem Abfrageparameter `x-watson-metadata` an, damit die ID den Daten zugeordnet wird, die mit der Anforderung gesendet werden. Sie müssen das Argument für den Abfrageparameter als URL codieren, z. B. `customer_id%3dmy_ID`.

-   Anforderungen zum Hinzufügen von Wörtern zu angepassten Sprechmodellen:
    -   `POST /v1/customizations/{customization_id}`
    -   `POST /v1/customizations/{customization_id}/words`
    -   `PUT /v1/customizations/{customization_id}/words/{word}`

    Die Kunden-ID wird hier den angepassten Wörtern zugeordnet, die durch die Anforderung hinzugefügt oder aktualisiert werden.

### Daten löschen
{: #delete-pi}

Mit der Methode `DELETE /v1/user_data` können Sie alle Daten löschen, die einer Kunden-ID zugeordnet sind. Hierzu übergeben Sie mit der Anforderung die Zeichenfolge `customer_id={id}` als Abfrageparameter. Im folgenden Beispiel werden alle Daten für die Kunden-ID `my_ID`gelöscht:

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/user_data?customer_id=my_ID"
```

Die Methode `/v1/user_data` löscht alle Daten, die der angegebenen Kunden-ID zugeordnet sind. Hierbei ist es unerheblich, mit welcher Methode die Informationen hinzugefügt wurden. Falls der Kunden-ID keine Daten zugeordnet sind, ist die Methode wirkungslos. Sie müssen die Anforderung mit Berechtigungsnachweisen für dieselbe Instanz des Service ausgeben, die auch verwendet wurde, um den Daten die Kunden-ID zuzuordnen.
