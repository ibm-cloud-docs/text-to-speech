---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-12"

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
{:download: .download}

# Getting started tutorial
{: #gettingStarted}

The {{site.data.keyword.texttospeechfull}} service converts written text to natural-sounding speech to provide speech-synthesis capabilities for applications. This cURL-based tutorial can help you get started quickly with the service. The examples show you how to call the service's `POST` and `GET /v1/synthesize` methods to request an audio stream.
{: shortdesc}

> **Important:** The tutorial uses service instance credentials to authenticate to the {{site.data.keyword.texttospeechshort}} service. In some regions, new service instances instead use {{site.data.keyword.Bluemix}} Identity and Access Management (IAM) tokens for authentication. Authenticate by using the approach that is right for your region and service instance.

For more information about where the service uses IAM access tokens and how to use them for authentication, see the June 12 and May 15 service updates in the [Release notes](/docs/services/text-to-speech/release-notes.html).

## Before you begin
{: #before-you-begin}

- {: download} If you're seeing this, you created your service instance. Now get your credentials.
- Create an instance of the service:
    1.  Go to the [{{site.data.keyword.texttospeechshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/services/text-to-speech){: new_window} page in the {{site.data.keyword.Bluemix_notm}} Catalog.
    1.  Sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in.
    1.  Click **Create**.
- Copy the credentials to authenticate to your service instance:
    1.  On the service dashboard, click the **Service credentials** tab.
    1.  Click **View credentials** under **Actions**.
    1.  Copy the `username`, `password`, and `url` values.
- Make sure that you have cURL:
    - The examples use cURL to call methods of the HTTP interface. Install the version for your operating system from [curl.haxx.se ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://curl.haxx.se/){: new_window}. Install the version that supports the Secure Sockets Layer (SSL) protocol. Make sure to include the installed binary file on your `PATH` environment variable.

## Step 1: Synthesize text in US English
{: #synthesizeEnglish}

The following commands use the `POST /v1/synthesize` method to synthesize US English input to audio files in two different formats. Both requests use the default US English voice, `en-US_MichaelVoice`.

1.  Issue the following command to synthesize the string "hello world" and produce a WAV file that is named `hello_world.wav`.
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

1.  Issue the following command to synthesize the same text but produce an Ogg file (the default format) that is named `hello_world.ogg`.
    -   Replace `{username}` and `{password}` with your service credentials.

    ```bash
    curl -X POST -u {username}:{password} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
    ```
    {: pre}

## Step 2: Synthesize text in Spanish
{: #synthesizeSpanish}

The following command uses the `GET /v1/synthesize` method to synthesize Spanish input to an audio file.

1.  Issue the following command to synthesize the string "hola mundo" and produce a WAV file that is named `hola_mundo.wav`. The input text is URL-encoded. The method includes the query parameters `accept` to specify the audio format and `voice` to specify a Spanish voice, `es-ES_EnriqueVoice`.
    -   Replace `{username}` and `{password}` with your service credentials.

    ```bash
    curl -X GET -u {username}:{password} \
    --output hola_mundo.wav \
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?accept=audio/wav&text=hola%20mundo&voice=es-ES_EnriqueVoice"
    ```
    {: pre}

## Next steps

-   Learn more about the service's HTTP interface in [The HTTP REST interface](/docs/services/text-to-speech/http.html).
-   Learn about the service's WebSocket interface in [The WebSocket interface](/docs/services/text-to-speech/websockets.html).
-   Get detailed information about the methods of the service's interface in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/){: new_window}.
-   Interact with the API in the [API explorer ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-api-explorer.ng.bluemix.net/apis/text-to-speech-v1){: new_window}.
