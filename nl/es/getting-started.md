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

# Guía de aprendizaje de iniciación
{: #gettingStarted}

El servicio {{site.data.keyword.texttospeechfull}} convierte el texto escrito en una voz que suena natural para proporcionar funciones de síntesis de voz para aplicaciones. Esta guía de aprendizaje basada en curl puede ayudarle a comenzar rápidamente con el servicio. Los ejemplos muestran cómo llamar a los métodos `POST` y `GET /v1/synthesize` del servicio para solicitar una secuencia de audio.
{: shortdesc}

## Antes de empezar
{: #before-you-begin}

- {: hide-dashboard}  Cree una instancia del servicio:
    1.  {: hide-dashboard} Vaya a la página de [{{site.data.keyword.texttospeechshort}}](https://{DomainName}/catalog/services/text-to-speech){: external} en el catálogo de {{site.data.keyword.cloud_notm}}.
    1.  {: hide-dashboard} Regístrese para obtener una cuenta gratuita de {{site.data.keyword.cloud_notm}} o inicie sesión.
    1.  {: hide-dashboard} Pulse **Crear**.
-   Copie las credenciales para autenticarse en la instancia de servicio:
    1.  {: hide-dashboard} Desde la [Lista de recursos de {{site.data.keyword.cloud_notm}}](https://{DomainName}/resources){: external}, pulse la instancia de servicio de {{site.data.keyword.texttospeechshort}} para ir a la página del panel de control del servicio {{site.data.keyword.texttospeechshort}}.
    1.  En la página **Gestionar**, pulse **Mostrar** para visualizar las credenciales.
    1.  Copie los valores de `Clave de API` y `URL`.

### Utilización de los ejemplos de curl
{: #getting-started-curl}

En esta guía de aprendizaje se utiliza el mandato `curl` para llamar a métodos de la interfaz HTTP de servicio. Asegúrese de tener instalado el mandato `curl` en el sistema.

1.  Para comprobar si está instalado el mandato `curl`, ejecute el mandato siguiente en la línea de mandatos. Si en la salida se muestra que la versión de `curl` admite la capa de sockets seguros (SSL - SSL Secure Sockets Layer), estará listo para empezar a utilizar esta guía de aprendizaje.

    ```bash
    curl -V
    ```
    {: pre}

1.  Si es necesario, instale la versión de `curl` con la opción SSL habilitada para su sistema operativo desde [curl.haxx.se](https://curl.haxx.se/){: external}.

Omita las llaves de los ejemplos porque indican valores de variables.
{: tip}

## Paso 1: Sintetizar texto en inglés de Estados Unidos
{: #synthesizeEnglish}

Los mandatos siguientes utilizan el método `POST /v1/synthesize` para sintetizar la entrada en inglés de Estados Unidos a archivos de audio en dos formatos diferentes. Las dos solicitudes utilizan la voz predeterminado para inglés de Estados Unidos, `en-US_MichaelVoice`.

1.  Emita el mandato siguiente para sintetizar la serie de caracteres "hello world" y producir un archivo WAV denominado `hello_world.wav`.
    -   {: hide-dashboard} Sustituya `{apikey}` y `{url}` por su clave de API y su URL.

    *Usuario de Windows:* sustituya la barra inclinada invertida (``\`) al final de cada línea por un acento circunflejo (``^`). Asegúrese de que no haya espacios finales.
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

1.  Emita el mandato siguiente para sintetizar el mismo texto pero generando un archivo Ogg (el formato predeterminado) denominado `hello_world.ogg`.
    -   {: hide-dashboard} Sustituya `{apikey}` y `{url}` por su clave de API y su URL.

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

Puede utilizar un navegador u otras herramientas para reproducir los archivos de audio que se generan con los ejemplos de esta guía de aprendizaje. Para obtener más información, consulte [Reproducir un archivo de audio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats#formatsPlay).
{: note}

## Paso 2: Sintetizar texto en español
{: #synthesizeSpanish}

En el mandato siguiente se utiliza el método `GET /v1/synthesize` para sintetizar entrada en español a un archivo de audio.

1.  Emita el mandato siguiente para sintetizar la serie de caracteres "hola mundo" y producir un archivo WAV denominado `hola_mundo.wav`. El texto de entrada está codificado como URL. El método incluye los parámetros de consulta `accept` para especificar el formato de audio y `voice` para especificar una voz en español, `es-ES_EnriqueVoice`.
    -   {: hide-dashboard} Sustituya `{apikey}` y `{url}` por su clave de API y su URL.

    ```bash
    curl -X GET -u "apikey:{apikey}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## Pasos siguientes

-   Obtenga más información acerca de la interfaz HTTP del servicio en [La interfaz HTTP](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP).
-   Obtenga información acerca de la interfaz WebSocket del servicio en [La interfaz WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).
-   Obtenga información detallada acerca de los métodos de la interfaz de servicio en la publicación [Consulta de API](https://{DomainName}/apidocs/text-to-speech){: external}.
