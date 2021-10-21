---

copyright:
  years: 2019, 2021
lastupdated: "2021-10-19"

keywords: text to speech release notes,text to speech for IBM cloud pak for data release notes

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}
{: #release-notes-data}

![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}} only**

The following features and changes were included for each release and update of installed or on-premises instances of {{site.data.keyword.texttospeechfull}} for {{site.data.keyword.icp4dfull_notm}}. The information includes known limitations. Unless otherwise noted, all changes are compatible with earlier releases and are automatically and transparently available to all new and existing applications.
{: shortdesc}

For information about releases and updates for {{site.data.keyword.cloud_notm}}, see [Release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}](/docs/text-to-speech?topic=text-to-speech-release-notes).
{: note}

## Known limitations
{: #limitations-data}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} has the following known limitation:

-   **30 August 2019:** When you specify the `audio/ogg;codecs=opus` audio format, you can optionally specify a sampling rate other than the default 48,000 Hz. However, while the service accepts `48000`, `24000`, `16000`, `12000`, or `8000` as a valid sampling rate, it currently disregards a specified value and always returns the audio with a sampling rate of 48 kHz.

## 1 October 2021 (Version 1.1.x)
{: #text-to-speech-data-1october2021}

Version 1.1.x is out of service
:   {{site.data.keyword.texttospeechshort}} and {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.x went out of service on 30 September 2021. As of 1 October 2021, the documentation for version 1.1.x is no longer available. For more information, see [Software withdrawal and support discontinuance](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/9/899/ENUSLP21-0099/index.html&request_locale=en){: external}.

## 29 July 2021 (Version 4.0.0)
{: #text-to-speech-data-29july2021}

Version 4.0.0 is available
:   {{site.data.keyword.texttospeechfull}} for {{site.data.keyword.icp4dfull}} version 4.0.0 is now available.  Installation and administration of the service include many changes. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.x and Red Hat OpenShift version 4.6. For more information about installing and managing the service, see [Installing {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}](/docs/text-to-speech?topic=text-to-speech-speech-install-data).

Enhanced neural voices
:   To optimize the overall quality of voice synthesis, all available voices are now *enhanced neural voices*. Enhanced neural voices, which include the string `V3` in their names, are now available for Brazilian Portuguese, United Kingdom and United States English, French, German, Italian, Japanese, and Spanish (all dialects).

    Enhanced neural voices support the use of both IPA and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) with the SSML `<phoneme>` element. Enhanced neural voices also achieve a slightly higher degree of natural-sounding speech. For more information, see

    -   [Supported languages and voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices)
    -   [Neural voice technology](/docs/text-to-speech?topic=text-to-speech-voices#neural-voices)

New Canadian French voice
:   The service now supports Canadian French with the enhanced neural voice `fr-CA_LouiseV3Voice`. The Canadian French voice supports customization and is generally available (GA) for production use.

    -   To hear a sample of the new voice, see [Supported languages and voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices).
    -   For more information about the phonetic symbols and Unicode values that are available for the Canadian French language, see [French (Canadian) symbols](/docs/text-to-speech?topic=text-to-speech-caSymbols).

New Tune by Example feature
:   The new Tune by Example feature lets you control how specified text is spoken by the service. The feature is beta functionality that is supported only for US English custom models and voices. The feature has two components:

    -   *Custom prompts* include the written text that is to be spoken and recorded audio that speaks the text as you want to hear it. The audio specifies the intonation, cadence, and stress of the synthesized text. The prompt can emphasize different syllables or words, introduce pauses, and generally make the synthesized audio sound more natural and appropriate for its context.
    -   *Speaker models* provide enrollment audio for a user who speaks one or more prompts. A speaker model provides an audio sample of a user's voice. The service trains itself on the voice, which can help it to produce higher-quality prompts for that speaker.

    You specify a custom prompt with a speech synthesis request to indicate how the service's voice is to pronounce the text. To specify a prompt, you use the SSML extension `<ibm:prompt id="{prompt_id}"/>`. The synthesized audio duplicates the prosody of the prompt.

    For more information about using the Tune by Example feature, see the following topics:

    -   [Understanding Tune by Example](/docs/text-to-speech?topic=text-to-speech-tbe-intro)
    -   [Rules for creating custom prompts and speaker models](/docs/text-to-speech?topic=text-to-speech-tbe-rules)
    -   [Creating a custom prompt](/docs/text-to-speech?topic=text-to-speech-tbe-create)
    -   [Using a custom prompt for speech synthesis](/docs/text-to-speech?topic=text-to-speech-tbe-use)
    -   [Managing custom prompts](/docs/text-to-speech?topic=text-to-speech-tbe-custom-prompts)
    -   [Managing speaker models](/docs/text-to-speech?topic=text-to-speech-tbe-speaker-models)

    The service includes eight new methods for working with the Tune by Example feature. The descriptions of the new methods that follow provide links to their entries in the API & SDK reference.

    -   The service includes four methods for working with custom prompts:

        -   [Add a custom prompt](https://{DomainName}/apidocs/text-to-speech/text-to-speech#addcustomprompt){: external}: `POST /v1/customizations/{customization_id}/prompts/{prompt_id}`
        -   [List custom prompts](https://{DomainName}/apidocs/text-to-speech/text-to-speech#listcustomprompts){: external}: `GET /v1/customizations/{customization_id}/prompts`
        -   [Get a custom prompt](https://{DomainName}/apidocs/text-to-speech/text-to-speech#getcustomprompt){: external}: `GET /v1/customizations/{customization_id}/prompts/{prompt_id}`
        -   [Delete a custom prompt](https://{DomainName}/apidocs/text-to-speech/text-to-speech#deletecustomprompt){: external}: `DELETE /v1/customizations/{customization_id}/prompts/{prompt_id}`

    -   The service includes four methods for working with speaker models:

        -   [Create a speaker model](https://{DomainName}/apidocs/text-to-speech/text-to-speech#createspeakermodel){: external}: `POST /v1/speakers`
        -   [List speaker models](https://{DomainName}/apidocs/text-to-speech/text-to-speech#listspeakermodels){: external}: `GET /v1/speakers`
        -   [Get a speaker model](https://{DomainName}/apidocs/text-to-speech/text-to-speech#getspeakermodel){: external}: `GET /v1/speakers/{speaker_id}`
        -   [Delete a speaker model](https://{DomainName}/apidocs/text-to-speech/text-to-speech#deletespeakermodel){: external}: `DELETE /v1/speakers/{speaker_id}`

Unified {{site.data.keyword.texttospeechshort}} documentation
:   The documentation for {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} is now combined with the documentation for managed instances of the {{site.data.keyword.texttospeechshort}} service that are hosted on {{site.data.keyword.cloud_notm}}. This is true of both the guide and reference documentation for the two forms of the service. Links to the formerly separate version of the {{site.data.keyword.icp4dfull_notm}} documentation for the service redirect to the unified documentation.

    For more information about identifying information that pertains to only one version of the product, see [About {{site.data.keyword.texttospeechshort}}](/docs/text-to-speech?topic=text-to-speech-about#about-version).

Version 1.1.x is going out of service
:   {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.x go out of service on **30 September 2021**. You must upgrade to a later version of the services on {{site.data.keyword.icp4dfull_notm}} before that date. As of 1 October 2021, the documentation for version 1.1.4 will no longer be available.

## 12 April 2021 (Version 1.2.1)
{: #text-to-speech-data-12april2021}

Addition to `speech-override.yaml` file
:   The minimal `speech-override.yaml` file includes an extra definition, `dockerRegistryPrefix`:

    ```yaml
    global:
      dockerRegistryPrefix: "{Registry}"
      image:
        pullSecret: "{Registry_pull_secret}"
    ```
    {: codeblock}

    `{Registry}` is the path for the internal Docker registry. It must be `image-registry.openshift-image-registry.svc:5000/{namespace}`, where `{namespace}` is the namespace in which {{site.data.keyword.icp4dfull}} is installed, normally `zen`. For more information, see [The speech-override.yaml file](/docs/text-to-speech?topic=text-to-speech-speech-override-12#speech-override-file-12).

## 9 April 2021 (Version 1.2.1)
{: #text-to-speech-data-9april2021}

Support for modifying installed models and voices
:   The Speech services let you add or remove installed models and voices for version 1.2 or 1.2.1 of the services. For more information, see [Modifying the installed models and voices](/docs/text-to-speech?topic=text-to-speech-speech-cluster-12#speech-cluster-models-voices-12).

## 26 March 2021 (Version 1.2.1)
{: #text-to-speech-data-26march2021}

Version 1.2.1 is available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.2.1 is now available. Versions 1.2 and 1.2.1 use the same version 1.2 documentation and installation instructions. Version 1.2.1 supports installation on Red Hat OpenShift version 4.6 in addition to versions 4.5 and 3.11.

New installation instructions
:   For both clusters connected to the internet and air-gapped clusters, the installation instructions include the following steps:
    -   Use the `oc label` command to set up required labels for the namespace where {{site.data.keyword.icp4dfull_notm}} is installed.
    -   Use the `oc project` command to ensure that you are pointing at the correct OpenShift project.
    -   Use the `cpd-cli install` command to install an EnterpriseDB PostgreSQL server that is used by the Speech services.

    You perform these steps before you install the Speech services. For more information, see [Installing the {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} service](https://www.ibm.com/support/knowledgecenter/SSQNUZ_3.5.0/svc-speech/stt-svc-install.html){: external}.

New uninstallation instructions
:   A step was added to the procedure for uninstalling the Speech services to clean up all of the resources from the installation. For more information, see [Uninstalling {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/knowledgecenter/SSQNUZ_3.5.0/svc-text/tts-svc-uninstall.html){: external}.

Entitled registry for PostgreSQL datastore
:   The entitled registry path from which the service pulls images for the PostgreSQL datastore has changed. The registry location changed from `cp.icr.io/cp/watson-speech` to `cp.icr.io/cp/cpd`. This change is transparent to users.

Secrets for Minio and PostgreSQL datastores
:   The Minio and PostgreSQL datastores require the following hard-coded values for their secrets:
    -   For *Minio*, use `minio`.
    -   For *PostgreSQL*, use `user-provided-postgressql`.

    You cannot use your own values for these secrets. The secrets must be created before you install the Speech services.

Deletions from `speech-override.yaml` file
:   The following entries have been removed from the `speech-override.yaml` file. They were added to work around a problem that has now been fixed.

    ```yaml
    sttRuntime:
      images:
        miniomc:
          tag:
            1.0.5
    sttAMPatcher:
      images:
        miniomc:
          tag:
            1.0.5
    ttsRuntime:
      images:
        miniomc:
          tag:
            1.0.5
    ```
    {: codeblock}

    The abbreviated `speech-override.yaml` file has generally been reduced further by fine-tuning its contents to the essential elements. The updated version of the file appears in the following sections:
    -   [Creating an override file for {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} installation](https://www.ibm.com/support/knowledgecenter/SSQNUZ_3.5.0/svc-speech/stt-svc-override.html){: external}
    -   [Using the override file](/docs/text-to-speech?topic=text-to-speech-speech-override-12)

    You can download a complete version of the [speech-override.yaml](https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/cpd-version-12/speech-override.yaml){: external} file. The complete version includes all of the detailed elements described in [Using the override file](/docs/text-to-speech?topic=text-to-speech-speech-override-12).

## 9 December 2020 (Version 1.2)
{: #text-to-speech-data-9december2020}

Version 1.2 is available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.2 is now available. Installation and administration of the service include many changes. This version supports {{site.data.keyword.icp4dfull_notm}} versions 3.5 and 3.0.1, and Red Hat OpenShift versions 4.5 and 3.11. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} version 1.2](/docs/text-to-speech?topic=text-to-speech-speech-install-12).

New voices
:   The service now offers three new voices:
    -   UK English: `en-GB_CharlotteV3Voice` and `en-GB_JamesV3Voice`
    -   French: `fr-FR_NicolasV3Voice`

    The service also offers an improved version of the existing UK voice, `en-KateV3Voice`. For more information about all supported languages and voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

Defect fix for `<prosody>` element for Japanese
:   **Defect fix:** For the `ja-JP_EmiV3Voice` voice, the service now correctly parses SSML input text that includes a prosody rate specification. Previously, the following use of the `<prosody>` element worked properly:

    `<speak>成功する/繁栄する</speak>`

    But the following use of the rate attribute with the `<prosody>` element caused the service to read and speak the embedded SSML notation:

    `<speak rate="fast">成功する/繁栄する</speak>`

    The service now correctly parses and applies the `rate` attribute of the `<prosody>` element for Japanese input.

## 4 September 2020 (Version 1.1.4)
{: #text-to-speech-data-4september2020}

Customization interface is generally available
:   The customization interface is now generally available. Customization is no longer beta functionality. You can use the customization interface to specify how the service pronounces unusual words that occur in your input text by creating language-specific custom dictionaries. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

## 15 July 2020 (Version 1.1.4)
{: #text-to-speech-data-15july2020}

Red Hat OpenShift version 4.3 is going out of service
:   {{site.data.keyword.icp4dfull_notm}} 3.0.1 is deprecating support for Red Hat OpenShift 4.3 on 1 September 2020. Red Hat OpenShift 4.3 is going out of service on **22 October 2020**. {{site.data.keyword.icp4dfull_notm}} is introducing support for Red Hat OpenShift 4.5. {{site.data.keyword.icp4dfull_notm}} is recommending that clients upgrade to Red Hat OpenShift 4.5 before 22 October 2020. IBM Support will work with any customers who already installed {{site.data.keyword.icp4dfull_notm}} 3.0.1 on Red Hat OpenShift 4.3. New customers who want to install on Red Hat OpenShift 4.x are instructed to install Red Hat OpenShift 4.5.

## 19 June 2020 (Version 1.1.4)
{: #text-to-speech-data-19june2020}

Version 1.1.4 is available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.4 is now available. Installation and administration of the service include many changes. This version supports {{site.data.keyword.icp4dfull_notm}} versions 2.5 and 3.0.1, and Red Hat OpenShift versions 3.11 and 4.3. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} version 1.1.4](/docs/text-to-speech?topic=text-to-speech-speech-install).

New neural voices
:   The service now supports five new neural voices:

    -   US English: `en-US_EmilyV3Voice`, `en-US_HenryV3Voice`, `en-US_KevinV3Voice`, and `en-US_OliviaV3Voice`
    -   German: `de-DE_ErikaV3Voice`

    These new voices have the same capabilities for customization and SSML as all existing voices. For more information, see [Supported languages and voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices).

Support for SSML `digits` attribute of `<say-as>` element for Japanese
:   The service now supports the `digits` attribute of the SSML `<say-as>` element with its Japanese voice.  For more information, see [The `<say-as>` element](/docs/text-to-speech?topic=text-to-speech-elements#say-as_element).

Simplified backup and restore procedures
:   The backup and restore procedures are greatly simplified. They now back up data from the datastores, so you no longer need to re-create the operations you have run. For more information, see [Backing up and restoring your data](/docs/text-to-speech?topic=text-to-speech-speech-backup).

## 28 February 2020 (Version 1.1.3)
{: #text-to-speech-data-28february2020}

Version 1.1.3 is available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.3 is now available.

## 27 November 2019 (Version 1.1.2)
{: #text-to-speech-data-27november2019}

Version 1.1.2 is available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.2 is now available.

## 30 August 2019 (Version 1.0.1)
{: #text-to-speech-data-30august2019}

Version 1.0.1 is available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.0.1 is now available. The service now works with {{site.data.keyword.icp4dfull_notm}} 2.1.0.1. The service now supports installing {{site.data.keyword.icp4dfull_notm}} with Red Hat OpenShift.

New Japanese neural voice
:   The service now offers the neural Japanese voice `ja-JP_EmiV3Voice`. For more information, see [Supported languages and voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices).

FISMA support
:   Federal Information Security Management Act (FISMA) support is now available for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}. The service is FISMA High Ready.

## 28 June 2019 (Version 1.0.0)
{: #text-to-speech-data-28june2019}

Version 1.0.0 is available
:   Version 1.0.0, the initial release of the service, is now available. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} is based on the {{site.data.keyword.texttospeechfull}} service on the public {{site.data.keyword.cloud_notm}}. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} differs from the public {{site.data.keyword.texttospeechshort}} service in the following ways. You might find this information helpful if you are already familiar with the {{site.data.keyword.texttospeechshort}} service on the public {{site.data.keyword.cloud_notm}}.

    -   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} uses access tokens for authentication. For more information, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.
    -   The endpoints for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} are specific to your {{site.data.keyword.icp4dfull_notm}} cluster. For more information, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.
    -   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} supports only neural voices. It does not support standard (concatenative) voices. The neural voices do not support the SSML `<express-as>` and `<voice-transformation>` elements.
    -   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} does not perform any request logging. You do not need to use the `X-Watson-Learning-Opt-Out` request header.
    -   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} does not support Watson tokens. You cannot use the `X-Watson-Authorization-Token` request header to authenticate with the service.
