---

copyright:
  years: 2015, 2022
lastupdated: "2021-02-02"

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

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only.** Watch the following video for a visual summary of getting started with the {{site.data.keyword.texttospeechshort}} service.

![Getting started with the {{site.data.keyword.texttospeechshort}} service](https://video.ibm.com/embed/channel/23952663/video/text-to-speech-get-started){: video output="iframe" data-script="none" id="watsonmediaplayer" width="560" height="315" scrolling="no" allowfullscreen webkitallowfullscreen mozAllowFullScreen frameborder="0" style="border: 0 none transparent;"}

## Before you begin
{: #getting-started-before-you-begin}

### {{site.data.keyword.cloud_notm}}
{: #getting-started-before-you-begin-cloud}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only**

-   Create an instance of the service: {: hide-dashboard}

    1.  Go to the [{{site.data.keyword.texttospeechshort}}](https://{DomainName}/catalog/services/text-to-speech){: external} page in the {{site.data.keyword.cloud_notm}} Catalog. {: hide-dashboard}
    1.  Sign up for a free {{site.data.keyword.cloud_notm}} account or log in. {: hide-dashboard}
    1.  Click **Create**. {: hide-dashboard}

-   Copy the credentials to authenticate to your service instance:

    1.  From the [{{site.data.keyword.cloud_notm}} Resource list](https://{DomainName}/resources){: external}, click on your {{site.data.keyword.texttospeechshort}} service instance to go to the {{site.data.keyword.texttospeechshort}} service dashboard page. {: hide-dashboard}
    1.  On the **Manage** page, click **Show Credentials** to view your credentials.
    1.  Copy the `API Key` and `URL` values.

### {{site.data.keyword.icp4dfull_notm}}
{: #getting-started-before-you-begin-icpd}

![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}} only**

1.  Provision an instance of {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}. For more information about provisioning, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} version 1.2](/docs/text-to-speech?topic=text-to-speech-speech-install-12).
1.  From the {{site.data.keyword.icp4dfull_notm}} web client menu, choose **My Instances**.
1.  Click the {{site.data.keyword.texttospeechshort}} instance to open the overview page.
1.  Copy the `{token}` and `{URL}` values.

### Using the curl examples
{: #getting-started-curl}

This tutorial uses the `curl` command to call methods of the service's HTTP interface. Make sure that you have the `curl` command installed on your system.

1.  To test whether `curl` is installed, run the following command on the command line. If the output lists the `curl` version that supports Secure Sockets Layer (SSL), you are set for the tutorial.

    ```bash
    curl -V
    ```
    {: pre}

1.  If necessary, install the version of `curl` with SSL enabled for your operating system from [curl.haxx.se](https://curl.haxx.se/){: external}.

### Tips
{: #getting-started-tips}

-   Omit the braces (`{ }`) from the examples. They indicate variable values.
-   *Windows users,* replace the backslash (`\`) at the end of each line with a caret (`^`). Make sure there are no trailing spaces.
-   You can use a browser or other tools to play the audio files that are produced by the examples in this tutorial. For more information, see [Playing an audio file](/docs/text-to-speech?topic=text-to-speech-audio-formats#formats-play).

## Synthesize text in US English
{: #getting-started-synthesize-english}
{: step}

The following command use the `POST /v1/synthesize` method to synthesize US English input to audio. The request uses the voice `en-US_MichaelV3Voice`. It produces audio in the WAV format.

1.  Issue the following command to synthesize the string "hello world". The request produces a WAV file that is named `hello_world.wav`.

    ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}}**

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

    ![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}}**

    -   Replace `{token}` with the access token for your service instance.
    -   Replace `{url}` with the URL for your service instance.

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

    ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}}**

    -   Replace `{apikey}` and `{url}` with your API key and URL. {: hide-dashboard}

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize?voice=en-US_AllisonV3Voice"
    ```
    {: pre}

    ![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}}**

    -   Replace `{token}` with the access token for your service instance.
    -   Replace `{url}` with the URL for your service instance.

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

    ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}}**

    -   Replace `{apikey}` and `{url}` with your API key and URL. {: hide-dashboard}

    ```bash
    curl -X GET -u "apikey:{apikey}" \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueV3Voice"
    ```
    {: pre}

    ![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}}**

    -   Replace `{token}` with the access token for your service instance.
    -   Replace `{url}` with the URL for your service instance.

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
