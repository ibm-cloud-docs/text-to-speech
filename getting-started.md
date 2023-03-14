---

copyright:
  years: 2015, 2023
lastupdated: "2023-03-09"

keywords: text to speech,IBM cloud,getting started,tutorial,synthesize audio,speech synthesis

subcollection: text-to-speech

content-type: tutorial
account-plan: lite
completion-time: 10m

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with {{site.data.keyword.texttospeechshort}}
{: #gettingStarted}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

The {{site.data.keyword.texttospeechfull}} service converts written text to natural-sounding speech to provide speech-synthesis capabilities for applications. This `curl`-based tutorial can help you get started quickly with the service. The examples show you how to call the service's `POST` and `GET /v1/synthesize` methods to request an audio stream.
{: shortdesc}

The tutorial uses the `curl` command-line utility to demonstrate REST API calls. For more information about `curl`, see [Using curl with Watson examples](/docs/watson?topic=watson-using-curl).
{: note}

[IBM Cloud]{: tag-ibm-cloud} Watch the following video for a visual summary of getting started with the {{site.data.keyword.texttospeechshort}} service.

![Getting started with the {{site.data.keyword.texttospeechshort}} service](https://video.ibm.com/embed/channel/23952663/video/text-to-speech-get-started){: video output="iframe" data-script="none" id="watsonmediaplayer" width="560" height="315" scrolling="no" allowfullscreen webkitallowfullscreen mozAllowFullScreen frameborder="0" style="border: 0 none transparent;"}

## Before you begin
{: #getting-started-before-you-begin}

### {{site.data.keyword.cloud_notm}}
{: #getting-started-before-you-begin-cloud}

[IBM Cloud]{: tag-ibm-cloud}

-   Create an instance of the service: {: hide-dashboard}

    1.  Go to the [{{site.data.keyword.texttospeechshort}}](https://{DomainName}/catalog/text-to-speech){: external} page in the {{site.data.keyword.cloud_notm}} catalog.
    1.  Sign up for a free {{site.data.keyword.cloud_notm}} account or log in.
    1.  Read and agree to the terms of the license agreement.
    1.  Click **Create**.

- Copy the credentials to authenticate to your service instance: {: hide-dashboard}

    1.  View the **Manage** page for the service instance:

        -   If you are on the **Getting started** page for your service instance, click the **Manage** entry in the list of topics.
        -   If you are on the **Resource list** page, expand the **AI / Machine Learning** grouping in the **Name** column, and click the name of your service instance.

    1.  On the **Manage** page, click **Show Credentials** in the **Credentials** box.
    1.  Copy the `API Key` and `URL` values for the service instance.

This tutorial uses an API key to authenticate. In production, use an IAM token. For more information see [Authenticating to IBM Cloud](/docs/watson?topic=watson-iam#gs-credential-cloud).
{: tip}

### {{site.data.keyword.icp4dfull_notm}}
{: #getting-started-before-you-begin-icpd}

[IBM Cloud Pak for Data]{: tag-cp4d}

The {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} must be installed and configured before beginning this tutorial. For more information, see [Watson Speech services on Cloud Pak for Data](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

1.  Create an instance of the service by using the web client, the API, or the command-line interface. For more information about creating a service instance, see [Creating a Watson Speech services instance](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=setup-creating-service-instance){: external}.
1.  Follow the instructions in *Creating a Watson Speech services instance* to obtain a Bearer token for the instance. This tutorial uses a Bearer token to authenticate to the service.

## Synthesize text in US English
{: #getting-started-synthesize-english}
{: step}

The following command use the `POST /v1/synthesize` method to synthesize US English input to audio. The request uses the voice `en-US_MichaelV3Voice`. It produces audio in the WAV format.

You can use a browser or other tools to play the audio files that are produced by the examples in this tutorial. For more information, see [Playing an audio file](/docs/text-to-speech?topic=text-to-speech-audio-formats#formats-play).
{: tip}

1.  Issue the following command to synthesize the string "hello world". The request produces a WAV file that is named `hello_world.wav`.

    [IBM Cloud]{: tag-ibm-cloud}

    -   Replace `{apikey}` and `{url}` with your API key and URL. {: hide-dashboard}

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize?voice=en-US_MichaelV3Voice"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    -   Replace `{token}` and `{url}` with the access token and URL for your service instance.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize?voice=en-US_MichaelV3Voice"
    ```
    {: pre}

## Use a different voice and audio format
{: #getting-started-different audio}
{: step}

The following command again uses the `POST /v1/synthesize` method to synthesize the same US English input to audio. But this request uses the voice `en-US_AllisonV3Voice` and explicitly requests audio in the default Ogg format.

1.  Issue the following command to synthesize the string "hello world" but with a different voice. The request produces an Ogg file that is named `hello_world.ogg`.

    [IBM Cloud]{: tag-ibm-cloud}

    -   Replace `{apikey}` and `{url}` with your API key and URL. {: hide-dashboard}

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize?voice=en-US_AllisonV3Voice"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    -   Replace `{token}` and `{url}` with the access token and URL for your service instance.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize?voice=en-US_AllisonV3Voice"
    ```
    {: pre}

## Synthesize text in Spanish
{: #getting-started-synthesize-spanish}
{: step}

The following command uses the `GET /v1/synthesize` method to synthesize Spanish input to an audio file. The `GET` method includes three query parameters: `accept` to specify the audio format, `text` to specify the input text for the audio, and `voice` to specify a Spanish voice. Because `accept` and `text` are passed as query parameters, the request is URL-encoded.

1.  Issue the following command to synthesize the string "hola mundo" and produce a WAV file that is named `hola_mundo.wav`.

    [IBM Cloud]{: tag-ibm-cloud}

    -   Replace `{apikey}` and `{url}` with your API key and URL. {: hide-dashboard}

    ```bash
    curl -X GET -u "apikey:{apikey}" \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueV3Voice"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    -   Replace `{token}` and `{url}` with the access token and URL for your service instance.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueV3Voice"
    ```
    {: pre}

## Next steps
{: #getting-started-next-steps}

-   To try an example application that accepts text and generates speech with different voices, see the [{{site.data.keyword.texttospeechshort}} demo](https://www.ibm.com/demos/live/tts-demo/self-service/home){: external}.
-   For more information about the service's interfaces and features, see [Service features](/docs/text-to-speech?topic=text-to-speech-service-features).
-   For more information about all methods of the service's interfaces, see the [API & SDK reference](/apidocs/text-to-speech){: external}.
