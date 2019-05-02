---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-14"

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# Tutoriel d'initiation 
{: #gettingStarted}

Le service {{site.data.keyword.texttospeechfull}} convertit le texte écrit en discours naturel pour offrir des fonctionnalités de synthèse vocale aux applications. Ce tutoriel basé sur curl peut vous aider à utiliser rapidement le service. Les exemples vous montrent comment appeler les méthodes `POST` et `GET /v1/synthesize` du service pour demander un flux audio.
{: shortdesc}

Le tutoriel utilise les clés d'API {{site.data.keyword.cloud}} Cloud Identity and Access Management (IAM) pour l'authentification. Les anciennes instances de service peuvent continuer à utiliser les `{username}` et `{password}` de leurs données d'identification de service Cloud Foundry existantes pour l'authentification. Authentifiez-vous en utilisant l'approche qui convient à votre instance de service. Pour plus d'informations sur l'utilisation de l'authentification IAM par le service, voir la [mise à jour du service du 30 octobre 2018](/docs/services/text-to-speech/release-notes.html#October2018) dans les notes sur l'édition.
{: important}

## Avant de commencer
{: #before-you-begin}

- {: hide-dashboard}  Créez une instance du service :
    1.  {: hide-dashboard} Accédez à la page [{{site.data.keyword.texttospeechshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/text-to-speech){: new_window} du catalogue {{site.data.keyword.cloud_notm}}.
    1.  {: hide-dashboard} Inscrivez-vous pour un compte {{site.data.keyword.cloud_notm}} gratuit ou connectez-vous.
    1.  {: hide-dashboard} Cliquez sur **Create**. 
-   Copiez les données d'identification pour vous authentifier à votre instance de service :
    1.  {: hide-dashboard} Dans le [tableau de bord {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/dashboard/apps){: new_window}, cliquez sur votre instance de service {{site.data.keyword.texttospeechshort}} pour accéder à la page du tableau de bord du service {{site.data.keyword.texttospeechshort}}.
    1.  Sur la page **Manage**, cliquez sur **Show** pour afficher vos données d'identification.
    1.  Copiez les valeurs des zones `API Key` et `URL`.
-   Vérifiez que vous disposez de la commande `curl`.
    -   Les exemples utilisent la commande `curl` pour appeler des méthodes de l'interface HTTP. Installez la version de votre système d'exploitation à partir du site [curl.haxx.se ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://curl.haxx.se/){: new_window}. Installez la version qui prend en charge le protocole SSL (Secure Sockets Layer). Veillez à inclure le fichier binaire installé indiqué dans votre variable d'environnement `PATH`.

Lorsque vous entrez une commande, remplacez `{apikey}` et `{url} `par votre clé d’API et votre URL. Omettez les accolades de la commande car elles indiquent une valeur de variable. Une valeur réelle ressemble à l'exemple suivant :
{: hide-dashboard}

```bash
curl -X POST -u "apikey:L_HALhLVIksh1b73l97LSs6R_3gLo4xkujAaxm7i-b9x"
. . .
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```
{:pre}
{: hide-dashboard}

Vous pouvez utiliser un navigateur ou d’autres outils pour lire les fichiers audio générés par les exemples de ce tutoriel. Pour plus d'informations, voir [Lecture d'un fichier audio](/docs/services/text-to-speech/audio-formats.html#formatsPlay).
{: note}

## Etape 1 : Synthétiser du texte en anglais américain 
{: #synthesizeEnglish}

Les commandes suivantes utilisent la méthode `POST /v1/synthesize` pour synthétiser l’entrée en anglais américain en fichiers audio dans deux formats différents. Les deux demandes utilisent la voix anglo-américaine par défaut, `en-US_MichaelVoice`.

1.  Exécutez la commande suivante pour synthétiser la chaîne "hello world" et générer un fichier WAV nommé `hello_world.wav`.
    -   {: hide-dashboard} Remplacez `{apikey}` et `{url}` par votre clé d'API et votre URL.

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

1.  Exécutez la commande suivante pour synthétiser le même texte mais générer un fichier Ogg (format par défaut) nommé `hello_world.ogg`.
    -   {: hide-dashboard} Remplacez `{apikey}` et `{url}` par votre clé d'API et votre URL.

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

## Etape 2 : Synthétiser du texte en espagnol 
{: #synthesizeSpanish}

La commande suivante utilise la méthode `GET /v1/synthesize` pour synthétiser l’entrée en espagnol dans un fichier audio. 

1.  Exécutez la commande suivante pour synthétiser la chaîne "hola mundo" et générer un fichier WAV nommé `hola_mundo.wav`. Le texte en entrée est codé dans l'URL. La méthode comprend les paramètres de requête `accept` permettant de spécifier le format audio et `voice` indiquant une voix espagnole, `es-ES_EnriqueVoice`.
    -   {: hide-dashboard} Remplacez `{apikey}` et `{url}` par votre clé d'API et votre URL.

    ```bash
    curl -X GET -u "apikey:{apikey}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## Etapes suivantes

-   En savoir plus sur l'interface HTTP du service dans [Interface HTTP](/docs/services/text-to-speech/http.html).
-   En savoir plus sur l'interface WebSocket du service dans [Interface WebSocket](/docs/services/text-to-speech/websockets.html).
-   Obtenez des informations détaillées sur les méthodes de l'interface du service dans la [référence de l'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/text-to-speech){: new_window}.
