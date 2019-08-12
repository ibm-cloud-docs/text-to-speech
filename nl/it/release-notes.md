---

copyright:
  years: 2019
lastupdated: "2019-06-24"

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

# Note sulla release
{: #release-notes}

Sono disponibili le seguenti versioni di {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}. Le informazioni includono le nuove versioni e le modifiche di ogni versione del prodotto e tutte le limitazioni note.
{: shortdesc}

## Limitazioni note
{: #limitations}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} ha le seguenti limitazioni note:

-   La voce in giapponese neurale `ja-JP_EmiV3Voice` non è ancora disponibile. Il supporto è in fase di sviluppo e sarà disponibile a breve.

### Versione 1.0.0 (giugno 2019)
{: #v100}

La release iniziale del servizio. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} si basa sul servizio {{site.data.keyword.texttospeechfull}} su {{site.data.keyword.cloud_notm}} pubblico. Per ulteriori informazioni sul servizio pubblico, vedi [Informazioni su {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}.

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} è diverso dal servizio {{site.data.keyword.texttospeechshort}} pubblico nei seguenti modi. Potresti trovare queste informazioni utili se hai già familiarità con il servizio {{site.data.keyword.texttospeechshort}} su {{site.data.keyword.cloud_notm}} pubblico.

-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} utilizza i token di accesso per l'autenticazione. Per ulteriori informazioni, vedi [Effettuare le richieste al servizio](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) e il [Riferimento API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   Gli endpoint per {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} sono specifici per il tuo cluster {{site.data.keyword.icp4dfull_notm}}. Per ulteriori informazioni, vedi [Effettuare le richieste al servizio](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) e il [Riferimento API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} supporta solo le voci neurali. Non supporta le voci standard (concatenative). Le voci neurali non supportano gli elementi `<express-as>` e `<voice-transformation>` SSML.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} non esegue alcuna registrazione della richiesta. Non hai bisogno di utilizzare l'intestazione della richiesta `X-Watson-Learning-Opt-Out`.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} non supporta i token Watson. Non puoi utilizzare l'intestazione della richiesta `X-Watson-Authorization-Token` per l'autenticazione con il servizio.
