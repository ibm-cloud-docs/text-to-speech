---

copyright:
  years: 2019, 2022
lastupdated: "2022-02-25"

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

## 23 February 2022 (Version 4.0.6)
{: #text-to-speech-data-23february2022}

Version 4.0.6 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.0.6 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.x and Red Hat OpenShift versions 4.6 and 4.8. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

All neural voices are now deprecated for {{site.data.keyword.icp4dfull_notm}}
:   The neural voices that were available with {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} are now deprecated. The neural voices continue to be available to users of {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}. Only the enhanced neural voices continue to be available to users of {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}.

    All voices for the following languages are now deprecated for {{site.data.keyword.icp4dfull_notm}}:
    -   Arabic
    -   Chinese (Mandarin)
    -   Czech
    -   Dutch (Belgian)
    -   Dutch (Netherlands)
    -   English (Australian)
    -   Korean
    -   Swedish

    Existing users of these voices can continue to use them for now, but the voices will be removed entirely in a future release. These voices can no longer be installed by new users and have been removed from the installation documentation for {{site.data.keyword.icp4dfull_notm}}. The `voiceType` property has been removed from the Speech services custom resource.

    For more information, see
    -   [Supported languages and voices](https://test.cloud.ibm.com/docs/text-to-speech?topic=text-to-speech-voices#language-voices)
    -   [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}

Updates to import/export scripts
:   The `import_export.sh` and `transfer_ownership.sh` scripts have been updated. These scripts are used to import and export data between clusters, back up and restore data, and migrate data from version 3.5 to version 4.0.x. The scripts have been modified and improved as follows:
    -   The `transfer_ownership.sh` script now requires a `-c` option to be included on the command line before the `<custom_resource_name>` argument.
    -   The `transfer_ownership.sh` script now requires a `-v <version>` option and argument to indicate the version to which ownership of resources is being transferred. Specify `35` for version 3.5 or `40` for version 4.0.x.
    -   The `transfer_ownership.sh` script now requires a `-p` option to be included on the command line before the `<postgres_auth_secret_name>` argument.
    -   The `<postgres_auth_secret_name>` argument provides the Kubernetes secret that is used to authenticate to the PostgreSQL datastore to which you are transferring ownership. You can omit the authentication secret if is the same as the default value (`<custom-resource-name>-postgres-auth-secret` for version 4.0.x, `user-provided-postgressql` for version 3.5). You must provide the secret if it is different from the default value.
    -   Both scripts now include a `-h` (`--help`) option to display information about the script and its usage.

    For more information, see
    -   [Administering {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-administering-watson-text){: external}, specifically *Importing and exporting data* and *Backing up and restoring data*.
    -   [Upgrading {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-upgrading-watson-text){: external}, specifically *Migrating data from {{site.data.keyword.icp4dfull_notm}} Version 3.5*.

Updated recommendation for OpenShift Container Storage
:   Starting with Speech services version 4.0.6, the recommended storage class for OpenShift Container Storage is `ocs-storagecluster-ceph-rbd`.
    -   If you are installing Speech services 4.0.6 or upgrading to Speech services 4.0.6 from IBM Cloud Pak for Data version 3.5, specify the `ocs-storagecluster-ceph-rbd` storage class during installation or upgrade.
    -   If you are upgrading to Speech services 4.0.6 from a previous refresh of Cloud Pak for Data version 4.0, continue to use `ocs-storagecluster-cephfs`. You cannot change the storage that is used in an existing deployment.

    The value is specified with the `storageClass` property in the Speech services custom resource:

    ```yaml
    ################
    # Storage class
    ################
      storageClass: "ocs-storagecluster-ceph-rbd"
    ```
    {: codeblock}

    The Speech services work with either version of OpenShift Container Storage. The newly recommended version has more restrictive access permissions. For more information, see
    -    [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}
    -   [Upgrading {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-upgrading-watson-text){: external}

## 2 February 2022
{: #text-to-speech-data-2february2022}

Defect fixes for SSML documentation
:   **Defect fixes:** The SSML documentation was updated to correct the following errors:
    -   The examples of the `<break>` element are now correct. The element is unary, as now shown in the examples. The previous examples included open and close tags with embedded text. The embedded text was not spoken by the service. For more information, see [The `<break>` element](/docs/text-to-speech?topic=text-to-speech-elements#break_element).
    -   The service supports Speech Synthesis Markup Language (SSML) version 1.1. All references and examples now use the correct version. The documentation previously referred to version 1.0.

## 31 January 2022 (Version 4.0.5)
{: #text-to-speech-data-31january2022}

Version 4.0.5 has been updated
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.0.5 has been updated to address installation issues. The case package version is now 4.0.6. Use this package instead of the version 4.0.5 package. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

Important: Extra steps for mirrored installation are no longer necessary
:   *Important:* The [26 January 2022 release notes](#text-to-speech-data-26january2022) included important notes for the following steps:

    -   Additional step for performing a mirrored installation of Minio datastore
    -   Additional steps for performing a mirrored installation of new next-generation models

    These additional steps are no longer needed. The case package has been updated to correct the installation issues.

## 26 January 2022 (Version 4.0.5)
{: #text-to-speech-data-26january2022}

Version 4.0.5 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.0.5 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.x and Red Hat OpenShift versions 4.6 and 4.8. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

Important: Additional step for performing a mirrored installation of Minio datastore
:   **Important:** These steps are no longer needed if you install case package 4.0.6. For more information, see [28 January 2022 (Version 4.0.5)](#text-to-speech-data-28january2022).

    If you are performing a mirrored installation (for example, in an air-gapped environment), you need to perform an additional step *before* completing either of the following steps:

    -   Step 7 [Mirroring the images to the private container registry](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=registry-mirroring-images-bastion-node#reference_g4h_z1q_tpb__mirror-to-target){: external} of *Mirroring images with a bastion model*
    -   Step 8 [Mirroring the images to the intermediary container registry](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=registry-mirroring-images-intermediary-container#preinstall_container_registry_air_gapped__mirror-to-target){: external} of *Mirroring images with an intermediary container registry*

    This step is mandatory to copy the necessary images for the Minio datastore:

    ```sh
    echo 'cp.icr.io,cp/opencontent-minio-client,1.1.4,sha256:7b4cf5e47a0455cfa7ca9ab246b80916e4dccbc1483b3e0f276fb7b0ab3e5c60,IMAGE,linux,x86_64,"",0,CASE,"",""' \
    >> $CASE_PATH/ibm-watson-speech-4.0.5-images.csv
    ```
    {: codeblock}

    Failure to perform this step will cause installation errors for both {{site.data.keyword.texttospeechshort}} and {{site.data.keyword.speechtotextshort}}.

License Server is now automatically installed
:   The Speech services operator now automatically installs the required License Server when it installs the Speech services. You no longer need to install the License Server from the {{site.data.keyword.icp4dfull_notm}} foundational services, and you no longer need to use additional YAML content to create an OperandRequest with the necessary bindings.

Removal of steps specific to PostgreSQL EnterpriseDB server
:   The previous version of the documentation included steps for the PostgreSQL EnterpriseDB server that were specific to the Speech services. These steps were documented in the topics *Upgrading {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} (Version 4.0)* and *Uninstalling {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}*. These additional steps are no longer necessary and have been removed from the documentation.

Security vulnerabilities addressed
:   The following security vulnerabilities associated with Apache Log4j have been addressed:
    -   [Security Bulletin: Vulnerability in Apache Log4j may affect IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2021-4104)](https://www.ibm.com/support/pages/node/6551170){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to denial of service and arbitrary code execution due to Apache Log4j (CVE-2021-45105 and CVE-2021-45046)](https://www.ibm.com/support/pages/node/6551168){: external}
    -   [Security Bulletin: Vulnerability in Apache Log4j may affect IBM Watson Speech Services Cartridge for {{site.data.keyword.icp4dfull_notm}} (CVE-2021-4428)](https://www.ibm.com/support/pages/node/6536732){: external} (this vulnerability was fixed with Speech services version 4.0.4)

RabbitMQ datastore is now used only by the `sttAysnc` component
:   The RabbitMQ datastore was previously used by components of both Speech services, {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}}. It now handles non-persistent message queuing for the Speech to Text asynchronous HTTP component (`sttAsync`) only. It is used only if the `sttAsync` component is installed and enabled.

New Belgian Dutch and Czech neural voices
:   Two new neural voices are now available:
    -   *Belgian Dutch:* A new male Belgian Dutch (Flemish) voice, `nl-BE_BramVoice`. For more information about the IPA symbols for the language, see [Dutch (Belgian) symbols](/docs/text-to-speech?topic=text-to-speech-beSymbols).
    -   *Czech:* A new language, Czech, with a new female voice, `cs-CZ_AlenaVoice`. For more information about the IPA symbols for the language, see [Czech symbols](/docs/text-to-speech?topic=text-to-speech-csSymbols).

    You can install the new voices along with all neural voices by setting the `voiceType` property of the custom resource to `neuralVoices`.
    -   For more information about using the custom resource to install voices, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.
    -   For more information about all available languages and voices, see [Using languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

Defect fixes for SSML documentation
:   **Defect fixes:** The SSML documentation was updated to correct the following errors:
    -   The examples of the `<break>` element are now correct. The element is unary, as now shown in the examples. The previous examples included open and close tags with embedded text. The embedded text was not spoken by the service. For more information, see [The `<break>` element](/docs/text-to-speech?topic=text-to-speech-elements#break_element).
    -   The service supports Speech Synthesis Markup Language (SSML) version 1.1. All references and examples now use the correct version. The documentation previously referred to version 1.0.

## 20 December 2021 (Version 4.0.4)
{: #text-to-speech-data-20december2021}

Version 4.0.4 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.0.4 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.x and Red Hat OpenShift versions 4.6 and 4.8. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

Important: Changes to properties for disabling the storage and logging of user data
:   **Important:** The names of the properties of the Speech services custom resource that specify whether user data is stored and logged have changed. The custom resource formerly contained the following properties:

    ```yaml
    #################
    # Anonymize logs
    #################
      sttRuntime:
        anonymizeLogs: "false"  # If true, disables storage and logging of user data
      sttAMPatcher:
        anonymizeLogs: "false"  # If true, disables storage and logging of user data
      ttsRuntime:
        anonymizeLogs: "false"  # If true, disables storage and logging of user data
    ```
    {: codeblock}

    These properties are now named as follows:

    ```yaml
    ###################################
    # Storage and logging of user data
    ###################################
      sttRuntime:
        skipAudioAndResultLogging: "false"  # If true, disables storage and logging of user data
      sttAMPatcher:
        skipAudioAndResultLogging: "false"  # If true, disables storage and logging of user data
      ttsRuntime:
        skipAudioAndResultLogging: "false"  # If true, disables storage and logging of user data
    ```
    {: codeblock}

    If you already set these properties in your custom resource to change the default value of `false` to `true`, you need to edit your custom resource. You must manually change the names of the properties to the new values and save the updated custom resource. For more information, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

Important: Changes to properties of PostgreSQL secrets object
:   **Important:** When you install the Speech services, an object that contains a randomly generated password for the PostgreSQL datastore is created by default. You can choose instead to specify the password manually. If you do, the properties of the YAML file for the secrets object have changed. For more information, see the topic about managing your datastores in [Administering {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-administering-watson-text){: external}.

Important: PostgreSQL pods do not start with EnterpriseDB version 1.10 operator
:   **Important:** With {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.0.3, PostgreSQL pods based on the EnterpriseDB version 1.10 operator can fail to start. This prevents the Speech services from starting. A workaround exists for this problem. If your Speech services fail to start, see [PostgreSQL pods do not start with EnterpriseDB version 1.10 operator](https://www.ibm.com/support/pages/node/6525340){: external} for information about diagnosing and resolving the problem.

    This problem is fixed in {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.0.4.

New support for IBM Spectrum Scale Container Native storage class
:   Since version 4.0.3, the Speech services support the IBM Spectrum® Scale Container Native storage class. To use IBM Spectrum Scale, specify `"ibm-spectrum-scale-sc"` for the `storageClass` property of the Speech services custom resource. For more information, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

Interaction of Speech services with MinIO datastore during installation
:   The Speech services runtime components, `sttRuntime` and `ttsRuntime`, cannot start until the models and voices for the services are fully uploaded into the MinIO datastore. During installation, the services might fail and automatically restart themselves one or more times until upload of the models and voices is complete. They then start properly. No user action is required.

Defect fix for upgrade documentation
:   **Defect fix:** Documentation for upgrading the Speech services to new versions of {{site.data.keyword.icp4dfull_notm}} version 4.0.x included incorrect references in some commands. These references are now correct:
    -   The strings `watsonSpeechToTextStatus` and `watsonTextToSpeechStatus` have been changed to `speechStatus` in both cases.
    -   The strings `status.watsonSpeechToTextVersion` and `status.watsonTextToSpeechVersion` have been changed to `.spec.version` in both cases.

    For more information, see [Upgrading {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-upgrading-watson-text){: external}.

Defect fixes for SSML and speech synthesis
:   **Defect fixes:** The following defects for the Speech Synthesis Markup Language (SSML) and speech synthesis were fixed with this release:

    -   The `pitch` attribute of the `<prosody>` element is now applied to all specified text. Previously, the pitch change was not always applied to the first word of the affected text. Also, the documentation now includes additional guidance about specifying a `pitch` value. For more information, see [The `pitch` attribute](/docs/text-to-speech?topic=text-to-speech-elements#prosody-pitch).
    -   Speech synthesis of Japanese text now speaks the audio more slowly. Previously, the synthesized speech was being spoken too quickly. If you find that synthesis of Japanese text is still spoken too quickly for your application, use the `rate` attribute of the SSML `<prosody>` element to control the rate of speech. For more information, see [The `rate` attribute](/docs/text-to-speech?topic=text-to-speech-elements#prosody-rate).
    -   Neural voices now parse the escaped apostrophe character (`&apos;`) properly. Previously, some neural voices were not interpreting the character properly.

## 20 December 2021 (Version 1.2.x)
{: #text-to-speech-data-20december2021-12}

Important: You can no longer install {{site.data.keyword.texttospeechshort}} version 1.2.x on {{site.data.keyword.icp4dfull_notm}} version 3.5
:   **Important:** You can no longer perform new installations of {{site.data.keyword.texttospeechshort}} version 1.2.x on {{site.data.keyword.icp4dfull_notm}} version 3.5. You can install only {{site.data.keyword.texttospeechshort}} version 4.0.x on {{site.data.keyword.icp4dfull_notm}} version 4.x. For more information, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

    The Speech services for {{site.data.keyword.icp4dfull_notm}} version 3.5 reach their End of Support date on 30 April 2022. You are encouraged to upgrade to the latest version 4.0.x release of the services at your earliest convenience. For more information, see [Upgrading {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-upgrading-watson-text){: external}.

## 30 November 2021 (Version 4.0.3)
{: #text-to-speech-data-30november2021}

Version 4.0.3 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.0.3 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.x and Red Hat OpenShift versions 4.6 and 4.8. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

License Server now a mandatory prerequisite
:   You must now install the License Server from the {{site.data.keyword.icp4dfull_notm}} foundational services. You must install the License Server by using the YAML content that is provided to create an OperandRequest with the necessary bindings. You must also install the License Service in the same namespace as the service (operand), which is also where {{site.data.keyword.icp4dfull_notm}} is installed. For more information, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

New support for in-place upgrade
:   The service now supports in-place, operator-based upgrade from version 4.0.0 to version 4.0.3. Moving from {{site.data.keyword.icp4dfull_notm}} version 3.5 to version 4.0.3 continues to require use of migration utilities. For more information, see [Upgrading {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-upgrading-watson-text){: external}.

EDB PostgreSQL operator and license installation changes
:   Installation, upgrade, and uninstallation for the Enterprise DB PostgreSQL operator and license have changed:
    -   Instructions for installing the EDB PostgreSQL operator and license are now included with the {{site.data.keyword.icp4dfull_notm}} foundational services. The instructions for installing the Speech services have been updated accordingly. For more information, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.
    -   Instructions for upgrading from {{site.data.keyword.texttospeechshort}} version 4.0.0 to 4.0.3 include instructions for uninstalling the previous EDB PostgreSQL operator and license and reinstalling them with the {{site.data.keyword.icp4dfull_notm}} foundational services. For more information, see [Upgrading {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-upgrading-watson-text){: external}.
    -   Instructions for uninstalling the Speech services now include steps for removing the EDB PostgreSQL operator and license that were previously installed with  {{site.data.keyword.texttospeechshort}}. For more information, see [Uninstalling {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-uninstalling-watson-text){: external}.

New guidance for scaling up your installation
:   The service now provides updated guidance about scaling up your installation. The information includes specifying the number of pods and the maximum number of concurrent sessions for enhanced neural or neural voices. For more information, see [Administering {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-administering-watson-text){: external}.

Command-line updates to import and export utilities
:   The commands that are used with the import and export utilities for the Speech services include new options and arguments. The import and export utilities are also the foundation for backing up and restoring the services and for migrating from {{site.data.keyword.icp4dfull_notm}} version 3.5 to version 4.0.3. For more information about using the utilities, see

    -   [Administering {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-administering-watson-text){: external}
    -   [Upgrading {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-upgrading-watson-text){: external}

New property for managing concurrency and speech synthesis
:   The new `global.ttsVoiceMarginalCPU` property manages the tradeoff between concurrency and speech synthesis speed. The default value of 400 offers a reasonable balance for most customers and maintains real-time synthesis. For information about modifying this value to suit your needs, contact IBM Support.

New support for neural voices
:   All neural voices that are currently available for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}} are now also available for installation on {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}. The following languages and voices are now available:

    -   *Arabic:* `ar-MS_OmarVoice`
    -   *Chinese (Mandarin):* `zh-CN_LiNaVoice`, `zh-CN_WangWeiVoice`, and `zh-CN_ZhangJingVoice`
    -   *Dutch (Belgian):* `nl-BE_AdeleVoice`
    -   *Dutch (Netherlands):* `nl-NL_EmmaVoice` and `nl-NL_LiamVoice`
    -   *English (Australian):* `en-AU_CraigVoice`, `en-AU_MadisonVoice`, and `en-AU_SteveVoice`
    -   *Korean:* `ko-KR_HyunjunVoice`, `ko-KR_SiWooVoice`, `ko-KR_YoungmiVoice`, and `ko-KR_YunaVoice`
    -   *Swedish:* `sv-SE_IngridVoice`

    For more information about all available languages and voices, see [Using languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

Installing voices
:   You can install either the enhanced neural voices or the neural voices. You can install only one of the two types of voices. When you install the service, you use the `voiceType` property of the custom resource to indicate the voices that are to be installed:

    -   Specify `enhancedNeuralVoices` to install the enhanced neural voices. You must then specify the individual enhanced neural voices that are to be installed. By default, only `en-US_AllisonV3Voice`, `en-US_LisaV3Voice`, and `en-US_MichaelV3Voice` are installed. You can choose to install these default voices, these and other voices, or just other voices. Only the voices that you install are available.
    -   Specify `neuralVoices` to install the neural voices. All of the neural voices are installed and available. You cannot refine the list of installed voices.

    For more information about using the custom resource to install voices, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

Specifying a voice for speech synthesis
:   Both the HTTP `POST` and `GET /v1/synthesize` methods, as well as the WebSocket `/v1/synthesize` method, accept an optional `voice` query parameter that you use to specify the voice that is to be used for speech synthesis. If you omit the `voice` parameter, the service uses a default voice, which depends on the version of the service that you are using:

    -   ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}}** The service always uses the US English `en-US_MichaelV3Voice` by default.
    -   ![Cloud Pak for Data only](images/cloud-pak.png) **{{site.data.keyword.icp4dfull}}** The default voice depends on the voices that you installed:

        -   *If you installed the enhanced neural voices,* the service uses the US English `en-US_MichaelV3Voice` by default. If that voice is not installed, you must specify a voice.
        -   *If you installed the neural voices,* the service always uses the Australian English `en-AU_MadisonVoice` by default.

    For more information, see [Specifying a voice for speech synthesis](/docs/text-to-speech?topic=text-to-speech-voices#specify-voice).

Specifying a language for a custom model
:   You use the `POST /v1/customizations` method to create a custom model. The method includes a `language` parameter that you use to identify the language of the new custom model.

    -   *If you installed the enhanced neural voices,* the `language` parameter is optional. By default, the service uses the `en-US` identifier for the language.
    -   *If you installed the neural voices,* the `language` parameter is required. You must specify the language for the custom model in the indicated format (for example, `en-AU` for Australian English).

    For more information about specifying a language when you create a custom model, see [Creating a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsCreate).

Defect fix for Spanish enhanced neural voices
:   **Defect fix:** For the Castilian Spanish (`es-ES_EnriqueV3Voice` and `es-ES_LauraV3Voice`), Latin American Spanish (`es-LA_SofiaV3Voice`), and North American Spanish (`es-US_SofiaV3Voice`) voices, questions of all types now use the correct intonation. The voices previously did not use the correct intonation for some questions, instead pronouncing them like statements.

Defect fix for multitenancy documentation
:   The {{site.data.keyword.icp4dfull_notm}} topic [Multitenancy support](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=planning-multitenancy-support){: external} incorrectly stated that the Speech services do not support multitenancy. The topic has been updated to state that the Speech services support the following operations:

    -   Install the service in separate projects
    -   Install the service multiple times in the same project
    -   Install the service once and deploy multiple instances in the same project

    The documentation that is specific to the Speech services correctly stated the multitenancy support.

## 1 October 2021 (Version 1.1.x)
{: #text-to-speech-data-1october2021}

Version 1.1.x is out of service
:   {{site.data.keyword.texttospeechshort}} and {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.x went out of service on 30 September 2021. As of 1 October 2021, the documentation for version 1.1.x is no longer available. For more information, see [Software withdrawal and support discontinuance](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/9/899/ENUSLP21-0099/index.html&request_locale=en){: external}.

## 29 July 2021 (Version 4.0.0)
{: #text-to-speech-data-29july2021}

Version 4.0.0 is available
:   {{site.data.keyword.texttospeechfull}} for {{site.data.keyword.icp4dfull}} version 4.0.0 is now available. Installation and administration of the service include many changes. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.x and Red Hat OpenShift version 4.6. For more information about installing and managing the service, see [Installing {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}](/docs/text-to-speech?topic=text-to-speech-speech-install-data).

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
    -   Use the `cpd-cli install` command to install an Enterprise DB PostgreSQL server that is used by the Speech services.

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

    ```xml
    <speak>成功する/繁栄する</speak>
    ```
    {: codeblock}

    But the following use of the rate attribute with the `<prosody>` element caused the service to read and speak the embedded SSML notation:

    ```xml
    <speak>
      <prosody rate="fast">成功する/繁栄する</prosody>
    </speak>
    ```
    {: codeblock}

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
