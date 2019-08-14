---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-03"

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

## Avant de commencer
{: #before-you-begin}

- {: hide-dashboard}  Créez une instance du service :
    1.  {: hide-dashboard} Accédez à la page [{{site.data.keyword.texttospeechshort}}](https://{DomainName}/catalog/services/text-to-speech){: external} du catalogue {{site.data.keyword.cloud_notm}}.
    1.  {: hide-dashboard} Inscrivez-vous pour un compte {{site.data.keyword.cloud_notm}} gratuit ou connectez-vous.
    1.  {: hide-dashboard} Cliquez sur **Create**.
-   Copiez les données d'identification pour vous authentifier à votre instance de service :
    1.  {: hide-dashboard} Depuis la [liste des ressources {{site.data.keyword.cloud_notm}}](https://{DomainName}/resources){: external}, cliquez sur votre instance de service {{site.data.keyword.texttospeechshort}} pour accéder à la page du tableau de bord du service {{site.data.keyword.texttospeechshort}}.
    1.  Sur la page **Manage**, cliquez sur **Show** pour afficher vos données d'identification.
    1.  Copiez les valeurs des zones `API Key` et `URL`.

### Utilisation des exemples curl
{: #getting-started-curl}

Ce tutoriel utilise la commande `curl` pour appeler des méthodes de l'interface HTTP du service. Vérifiez que vous disposez de la commande `curl` installée sur votre système.

1.  Pour tester si `curl` est installée, exécutez la commande suivante sur la ligne de commande. Si la sortie indique la version `curl` qui prend en charge SSL (Secure Sockets Layer), vous êtes prêt pour le tutoriel.

    ```bash
    curl -V
    ```
    {: pre}

1.  Si nécessaire, installez la version de `curl` avec SSL activé pour votre système d'exploitation depuis [curl.haxx.se](https://curl.haxx.se/){: external}.

Omettez les accolades des exemples. Elles indiquent des valeurs de variable.
{: tip}

## Etape 1 : Synthétiser du texte en anglais américain
{: #synthesizeEnglish}

Les commandes suivantes utilisent la méthode `POST /v1/synthesize` pour synthétiser l’entrée en anglais américain en fichiers audio dans deux formats différents. Les deux demandes utilisent la voix anglo-américaine par défaut, `en-US_MichaelVoice`.

1.  Exécutez la commande suivante pour synthétiser la chaîne "hello world" et générer un fichier WAV nommé `hello_world.wav`.
    -   {: hide-dashboard} Remplacez `{apikey}` et `{url}` par votre clé d'API et votre URL.

    *Utilisateurs Windows,* remplacez la barre oblique inversée (``\`) à la fin de chaque ligne par un caret (``^`). Vérifiez qu'il n'y a aucun espace de fin.
    {: tip}

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

Vous pouvez utiliser un navigateur ou d’autres outils pour lire les fichiers audio générés par les exemples de ce tutoriel. Pour plus d'informations, voir [Lecture d'un fichier audio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats#formatsPlay).
{: note}

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

-   En savoir plus sur l'interface HTTP du service dans [Interface HTTP](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP).
-   En savoir plus sur l'interface WebSocket du service dans [Interface WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).
-   Obtenez des informations détaillées sur les méthodes de l'interface du service dans [IBM Cloud API Docs / Text to Speech](https://{DomainName}/apidocs/text-to-speech){: external}.
