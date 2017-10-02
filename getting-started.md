---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Getting started tutorial
{: #gettingStarted}

The {{site.data.keyword.texttospeechfull}} service converts written text to natural-sounding speech to provide speech-synthesis capabilities for applications. This cURL-based tutorial can help you get started quickly with the service. The examples show you how to call the service's `POST` and `GET /v1/synthesize` methods to request an audio stream.
{: shortdesc}

> **Note:** The examples use cURL to call methods of the HTTP interface. You can install the version of cURL for your operating system from [curl.haxx.se ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://curl.haxx.se/){: new_window}. You must install the version that supports the Secure Sockets Layer (SSL) protocol. Make sure to include the installed binary file on your `PATH` environment variable.

## Step 1: Log in, create the service, and get your credentials

If you already know the credentials for your {{site.data.keyword.texttospeechshort}} service instance, skip this step.
{: tip}

1.  Go to the [{{site.data.keyword.texttospeechshort}} service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/catalog/services/text-to-speech/){: new_window} and either sign up for a free Bluemix account or log in.
1.  After you log in, enter `text-to-speech-tutorial` in the **Service name field** of the {{site.data.keyword.texttospeechshort}} page. Click **Create**.
1.  Copy your credentials:
    1.  Click **Service credentials**.
    1.  Click **View credentials** under **Actions**.
    1.  Copy the `username` and `password` values.

## Step 2: Synthesize text in US English
{: #synthesizeEnglish}

The following commands use the `POST /v1/synthesize` method to synthesize US English input to audio files in two different formats. Both requests use the default US English voice, `en-US-MichaelVoice`.

1.  Issue the following command to synthesize the string "hello world" and produce a WAV file named `hello_world.wav`.
    -   Replace `{username}` and `{password}` with your service credentials from the previous step.

    ```bash
    curl -X POST -u {username}:{password} \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
    ```
    {: pre}

1.  Issue the following command to synthesize the same text but to produce an Ogg file named `hello_world.ogg`, the default format.
    -   Replace `{username}` and `{password}` with your service credentials.

    ```bash
    curl -X POST -u {username}:{password} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
    ```
    {: pre}

## Step 3: Synthesize text in Spanish
{: #synthesizeSpanish}

The following command uses the `GET /v1/synthesize` method to synthesize Spanish input to an audio file.

1.  Issue the following command to synthesize the string "hola mundo" and produce a WAV file named `hola_mundo.wav`. The input text is URL-encoded. The method includes the query parameters `accept` to specify the audio format and `voice` to specify a Spanish voice, `es-ES-EnriqueVoice`.
    -   Replace `{username}` and `{password}` with your service credentials.

    ```bash
    curl -X GET -u {username}:{password} \
    --output hola_mundo.wav \
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?accept=audio/wav&text=hola%20mundo&voice=es-ES_EnriqueVoice"
    ```
    {: pre}

## Next steps

-   For more information about using the service's interface, see [The HTTP REST interface](/docs/services/text-to-speech/http.html).
-   For detailed information about the methods of the service's interface, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/){: new_window}.
-   Interact with the API in the [API explorer ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-api-explorer.mybluemix.net/apis/text-to-speech-v1){: new_window}.
