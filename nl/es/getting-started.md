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

# Guía de aprendizaje de iniciación
{: #gettingStarted}

El servicio {{site.data.keyword.texttospeechfull}} convierte el texto escrito en una voz que suena natural para proporcionar funciones de síntesis de voz para aplicaciones. Esta guía de aprendizaje basada en curl puede ayudarle a comenzar rápidamente con el servicio. Los ejemplos muestran cómo llamar a los métodos `POST` y `GET /v1/synthesize` del servicio para solicitar una secuencia de audio.
{: shortdesc}

La guía de aprendizaje utiliza las teclas de API de {{site.data.keyword.cloud}} Identity and Access Management (IAM) para la autenticación. Las instancias de servicio más antiguas pueden seguir utilizando `{username}` y `{password}` de sus credenciales de servicio de Cloud Foundry existentes para la autenticación. Realice la autenticación utilizando el método correcto para su instancia de servicio. Para obtener más información sobre el uso que hace el servicio de la autenticación de IAM, consulte la [actualización de servicio del 30 de octubre de 2018](/docs/services/text-to-speech/release-notes.html#October2018) en las notas del release.
{: important}

## Antes de empezar
{: #before-you-begin}

- {: hide-dashboard}  Cree una instancia del servicio:
    1.  {: hide-dashboard} Vaya a la página [{{site.data.keyword.texttospeechshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/text-to-speech){: new_window} en el catálogo de {{site.data.keyword.cloud_notm}}.
    1.  {: hide-dashboard} Regístrese para obtener una cuenta gratuita de {{site.data.keyword.cloud_notm}} o inicie sesión.
    1.  {: hide-dashboard} Pulse **Crear**.
-   Copie las credenciales para autenticarse en la instancia de servicio:
    1.  {: hide-dashboard} En el [panel de control de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/dashboard/apps){: new_window}, pulse en la instancia de servicio de {{site.data.keyword.texttospeechshort}} para ir a la página de panel de control del servicio {{site.data.keyword.texttospeechshort}}.
    1.  En la página **Gestionar**, pulse **Mostrar** para visualizar las credenciales.
    1.  Copie los valores de `Clave de API` y `URL`.
-   Asegúrese de tener el mandato `curl`.
    -   Los ejemplos utilizan el mandato `curl` para llamar a métodos de la interfaz HTTP. Instale la versión correspondiente a su sistema operativo desde [curl.haxx.se ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://curl.haxx.se/){: new_window}. Instale la versión que da soporte al protocolo SSL (Secure Sockets Layer). Asegúrese de incluir el archivo binario instalado en la variable de entorno `PATH`.

Cuando especifique un mandato, sustituya `{apikey}` y `{url}` por la clave de API y el URL reales. Omita las llaves, que indican un valor variable, en el mandato. Un valor real se asemeja al ejemplo siguiente:
{: hide-dashboard}

```bash
curl -X POST -u "apikey:L_HALhLVIksh1b73l97LSs6R_3gLo4xkujAaxm7i-b9x"
. . .
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```
{:pre}
{: hide-dashboard}

Puede utilizar un navegador u otras herramientas para reproducir los archivos de audio que se generan con los ejemplos de esta guía de aprendizaje. Para obtener más información, consulte [Reproducir un archivo de audio](/docs/services/text-to-speech/audio-formats.html#formatsPlay).
{: note}

## Paso 1: Sintetizar texto en inglés de Estados Unidos
{: #synthesizeEnglish}

Los mandatos siguientes utilizan el método `POST /v1/synthesize` para sintetizar la entrada en inglés de Estados Unidos a archivos de audio en dos formatos diferentes. Las dos solicitudes utilizan la voz predeterminado para inglés de Estados Unidos, `en-US_MichaelVoice`.

1.  Emita el mandato siguiente para sintetizar la serie de caracteres "hello world" y producir un archivo WAV denominado `hello_world.wav`.
    -   {: hide-dashboard} Sustituya `{apikey}` y `{url}` por su clave de API y su URL.

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

## Siguientes pasos

-   Obtenga más información acerca de la interfaz HTTP del servicio en [La interfaz HTTP](/docs/services/text-to-speech/http.html).
-   Obtenga información acerca de la interfaz WebSocket del servicio en [La interfaz WebSocket](/docs/services/text-to-speech/websockets.html).
-   Obtenga información detallada sobre los métodos de la interfaz del servicio en la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/text-to-speech){: new_window}.
