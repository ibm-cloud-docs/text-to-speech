---

copyright:
  years: 2019, 2023
lastupdated: "2023-05-03"

keywords: text to speech release notes,text to speech for IBM cloud pak for data release notes

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}
{: #release-notes-data}

[IBM Cloud Pak for Data]{: tag-cp4d}

The following features and changes were included for each release and update of installed or on-premises instances of {{site.data.keyword.texttospeechfull}} for {{site.data.keyword.icp4dfull_notm}}. Unless otherwise noted, all changes are compatible with earlier releases and are automatically and transparently available to all new and existing applications.
{: shortdesc}

For information about known limitations of the service, see [Known limitations](/docs/text-to-speech?topic=text-to-speech-known-limitations).

For information about releases and updates of the service for {{site.data.keyword.cloud_notm}}, see [Release notes for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.cloud_notm}}](/docs/text-to-speech?topic=text-to-speech-release-notes).
{: note}

## 2 May 2023 (Version 4.6.5)
{: #text-to-speech-data-2may2023}

Version 4.6.5 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.6.5 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.6.x and Red Hat OpenShift versions 4.10 and 4.12. For more information, see [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

New Australian English expressive neural voices
:   The service now supports two new expressive neural voices for Australian English:
    -   `en-AU_HeidiExpressive`
    -   `en-AU_JackExpressive`

    Expressive neural voices offer natural-sounding speech that is exceptionally clear, crisp, and fluid. The new voices are generally available (GA) for production use. They support the use of both standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) phonetic symbols. For more information, see
    -   [Expressive neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-expressive)
    -   [English (Australian) symbols](/docs/text-to-speech?topic=text-to-speech-auSymbols-new)

New Korean enhanced neural voice
:   The service now supports a new enhanced neural voice for Korean: `ko-KR_JinV3Voice`. The new voice is generally available (GA) for production use. It supports the use of both standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) phonetic symbols. For more information, see
    -   [Enhanced neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-enhanced-neural)
    -   [Korean symbols](/docs/text-to-speech?topic=text-to-speech-koSymbols-new)

New beta Netherlands Dutch enhanced neural voice
:   The service now supports a new enhanced neural female voice for Netherlands Dutch: `nl-NL_MerelV3Voice`. It supports the use of both standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) phonetic symbols.

    The new voice is beta functionality pending completion of support for SSML. At its initial release, the voice does not support use of the following SSML-related functionality:
    -   The `<prosody>` element with any speech synthesis request
    -   The `rate_percentage` and `pitch_percentage` parameters with any speech synthesis request
    -   The `<mark>` element with a WebSocket speech synthesis request
    -   The `timings` parameter of the JSON text message with a WebSocket speech synthesis request

    For more information about the new voice, its support for IPA and SPR symbols, and migrating to the new voice from the deprecated Netherlands Dutch neural voices, see
    -   [Enhanced neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-enhanced-neural)
    -   [Dutch (Netherlands) symbols](/docs/text-to-speech?topic=text-to-speech-nlSymbols-new)

New environment variable for Speech services custom resource
:   The documentation now includes instructions to create an environment variable named `${CUSTOM_RESOURCE_SPEECH}`. You append the new variable to the `cpd_vars.sh` script, and source the script to use the variable in your environment. For more information, see *Information you need to complete this task* in [Installing Watson Speech services](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-installing){: external}, or refer to any of the upgrade topics for the Speech services.

Defect fix: French Canadian voice now handles numeric times properly
:   **Defect fix:** The French Canadian voices now pronounce times like `19:41` correctly. Previously, the voices were omitting elements of the time in the synthesized audio.

Defect fix: Japanese voice no longer inserts unexpected audio
:   **Defect fix:** The Japanese voice no longer inserts unexpected audio in speech synthesis results. Previously, additional audio was inserted in certain cases.

Defect fix: Update Korean phonetic symbols in documentation
:   **Defect fix:** In the documentation for Korean SPR symbols, two-character symbols for consonants are now enclosed in single quotes, making them a single symbol. Previously, they were shown as two separate symbols, without enclosing quotes. For more information, see [Consonants (Korean)](/docs/text-to-speech?topic=text-to-speech-koSymbols-new#koConsonants-new).

Documentation updates for IBM SPR symbols
:   The overview documentation for IBM SPR symbols has been updated to clarify the use of multi-character symbols. For more information, see [Speech sound symbols](/docs/text-to-speech?topic=text-to-speech-symbols#intro-SPRs-symbols)).

Security vulnerabilities addressed
:   The following security vulnerabilities have been fixed:
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Python (CVE-2020-10735)](https://www.ibm.com/support/pages/node/6988073){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to phishing attacks in Python (CVE-2021-28861)](https://www.ibm.com/support/pages/node/6988075){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Pypa Setuptools (CVE-2022-40897)](https://www.ibm.com/support/pages/node/6988077){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a sensitive information exposure in systemd (CVE-2022-4415)](https://www.ibm.com/support/pages/node/6988079){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Python (CVE-2022-45061)](https://www.ibm.com/support/pages/node/6988081){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in Libksba (CVE-2022-47629)](https://www.ibm.com/support/pages/node/6988083){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in GNU Tar (CVE-2022-48303)](https://www.ibm.com/support/pages/node/6988085){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in FasterXML jackson-databind (CVE-2022-42003)](https://www.ibm.com/support/pages/node/6988087){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in Perl (CVE-2020-10878)](https://www.ibm.com/support/pages/node/6988089){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security restrictions bypass in Apache Tomcat (CVE-2022-45143)](https://www.ibm.com/support/pages/node/6988091){: external}
    -   CVE-2020-10543: Publication of the security bulletin is pending.

## 29 March 2023 (Version 4.6.4)
{: #text-to-speech-data-29march2023}

Version 4.6.4 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.6.4 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.6.x and Red Hat OpenShift versions 4.10 and 4.12. For more information, see [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

Important: Back up your data before upgrading to version 4.6.3 or 4.6.4
:   **Important:** Before upgrading to Watson Speech services version 4.6.3 or 4.6.4, you must make a backup of your data. Preserve the backup in a safe location. For more information about backing up your Watson Speech services data, see *Backing up and restoring Watson Speech services data* in [Administering Watson Speech services](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-administering){: external}. That topic also includes information about restoring your data if that becomes necessary.

Defect fix: You can now change the installed models and voices with the advanced installation options
:   **Defect fix:** During installation, you can now specify different models or voices with the advanced installation options of the command-line interface. Previously, the service always installed the default models and voices. The limitation continues to apply for Watson Speech services versions 4.6.0, 4.6.2, and 4.6.3. For information about installing models and voices, see *Specifying additional installation options* in [Installing Watson Speech services](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-installing){: external}.

Setting load balancer timeouts
:   Watson Speech services require that you change the load balancer timeout settings for both the server and client to 300 seconds. These settings ensure that long-running speech recognition requests, those with long or difficult audio, have sufficient time to complete. For more information, see *Information you need to complete this task* in [Installing Watson Speech services](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-installing){: external}.

Documentation updates for IBM SPR symbols
:   The overview documentation for IBM SPR symbols has been updated to clarify the use of multi-character symbols. For more information, see [Speech sound symbols](/docs/text-to-speech?topic=text-to-speech-symbols#intro-SPRs-symbols).

Security vulnerabilities addressed
:   The following security vulnerabilities have been fixed:
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to cross-site scripting in GNOME libxml2 (CVE-2016-3709](https://www.ibm.com/support/pages/node/6967621){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in SQlite (CVE-2020-35525)](https://www.ibm.com/support/pages/node/6967623){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security restrictions bypass in Amazon AWS S3 Crypto SDK for GoLang (CVE-2020-8912)](https://www.ibm.com/support/pages/node/6967631){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to elevated system privileges in the Red Hat Build of OpenJDK (CVE-2021-20264)](https://www.ibm.com/support/pages/node/6967637){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to an arbitrary code execution in e2fsprogs (CVE-2022-1304)](https://www.ibm.com/support/pages/node/6967639){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to errors in TrustCor (CVE-2022-23491)](https://www.ibm.com/support/pages/node/6967641){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in GnuTLS (CVE-2022-2509)](https://www.ibm.com/support/pages/node/6967643){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to an arbitrary code execution in systemd (CVE-2022-2526)](https://www.ibm.com/support/pages/node/6967649){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to sensitive information exposure in AWS SDK for Go (CVE-2022-2582)](https://www.ibm.com/support/pages/node/6967651){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to denial of service in cURL libcurl (CVE-2022-32206)](https://www.ibm.com/support/pages/node/6967687){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a man-in-the-middle attack in cURL libcurl (CVE-2022-32208)](https://www.ibm.com/support/pages/node/6967655){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to spoofing attacks in GnuPG (CVE-2022-34903)](https://www.ibm.com/support/pages/node/6967657){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in SQLite (CVE-2022-35737)](https://www.ibm.com/support/pages/node/6967659){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in zlib (CVE-2022-37434)](https://www.ibm.com/support/pages/node/6967661){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in systemd (CVE-2022-3821)](https://www.ibm.com/support/pages/node/6967663){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to an arbitrary code execution in Gnome libxml2 (CVE-2022-40303)](https://www.ibm.com/support/pages/node/6967667){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to an arbitrary code execution in Gnome libxml2 (CVE-2022-40304)](https://www.ibm.com/support/pages/node/6967669){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Python Charmers Future (CVE-2022-40899)](https://www.ibm.com/support/pages/node/6967679){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security restrictions bypass in Golang Go (CVE-2022-41716)](https://www.ibm.com/support/pages/node/6967671){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Golang Go (CVE-2022-41717)](https://www.ibm.com/support/pages/node/6967677){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Freedesktop D-Bus (CVE-2022-42010)](https://www.ibm.com/support/pages/node/6967691){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Freedesktop D-Bus (CVE-2022-42011)](https://www.ibm.com/support/pages/node/6967693){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Freedesktop D-Bus (CVE-2022-42012)](https://www.ibm.com/support/pages/node/6967695){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in MIT krb5 (CVE-2022-42898)](https://www.ibm.com/support/pages/node/6967697){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in libexpat (CVE-2022-43680)](https://www.ibm.com/support/pages/node/6967699){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to an arbitrary commands execution in Python (CVE-2015-20107)](https://www.ibm.com/support/pages/node/6981849){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in SQlite (CVE-2020-35527)](https://www.ibm.com/support/pages/node/6981851){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security restrictions bypass in GNU Libtasn1 (CVE-2021-46848)](https://www.ibm.com/support/pages/node/6981853){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in Git (CVE-2022-23521)](https://www.ibm.com/support/pages/node/6981857){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in GnuPG Libksba (CVE-2022-3515)](https://www.ibm.com/support/pages/node/6981855){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to an arbitrary code execution in libexpat (CVE-2022-40674)](https://www.ibm.com/support/pages/node/6981859){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in Git (CVE-2022-41903)](https://www.ibm.com/support/pages/node/6981861){: external}

## 23 February 2023 (Version 4.6.3)
{: #text-to-speech-data-23february2023}

Version 4.6.3 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.6.3 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.6.x and Red Hat OpenShift version 4.10. Red Hat OpenShift version 4.8 is no longer supported. For more information, see [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

Known issue: You cannot change the installed models and voices with the advanced installation options
:   **Known issue:** You currently cannot specify different models or voices with the advanced installation options. The service always installs the default models and voices. For information about changing the models after installation, see *Updating models and voices for your Watson Speech services* in the *Administration* topic of [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

Known issue: Upgrade to version 4.6.3 can fail to complete
:   **Known issue:**  When upgrading to version 4.6.3, the MinIO backup job can fail to be deleted upon completion. If this happens, the solution is to delete the job, after which the upgrade proceeds normally. Perform the following steps to resolve the problem.

    1.  To determine whether the MinIO backup job remains undeleted, issue the following command:

        ```sh
        oc get job --namespace {${PROJECT_CPD_INSTANCE} | grep speech-cr-ibm-minio-backup
        ```
        {: pre}

        The MinIO job that is not deleted is identified by an entry of the following form:

        ```text
        speech-cr-ibm-minio-backup   1/1   3m25s   1d
        ```
        {: codeblock}

    1.  To delete the MinIO backup job, issue the following command:

        ```sh
        oc delete job speech-cr-ibm-minio-backup --namespace ${PROJECT_CPD_INSTANCE}
        ```
        {: pre}

    Once the backup job is deleted, upgrade continues and completes.

Additional information about working with service instances
:   The documentation now includes information about creating a service instance with the command-line interface (`cpl-cli`) and about managing service instances. For more information, see the following topics of [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}:
    -   *Creating a Watson Speech services instance* under *Post-installation setup*
    -   *Managing your Watson Speech services instances* under *Administering*

Defect fix: The beta Tune by Example is now available
:   **Defect fix:** The beta Tune by example feature is now available for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}. Previously, it was not possible to create speaker models. For more information about the feature, which is available for U.S. English voices only, see [Understanding Tune by Example](/docs/text-to-speech?topic=text-to-speech-tbe-intro).

Defect fix: Specifying large cardinal numbers with the `<say-as>` element no longer causes errors for English voices
:   **Defect fix:** You can now use the `<say-as>` element to pronounce large numbers as cardinal numbers. Previously, enclosing a large number in the `<say-as>` element with the attribute `interpret-as="cardinal"` could cause speech synthesis to fail for English voices. For example, `<say-as interpret-as="cardinal">3,200</say-as>` could cause the service to generate an error. For more information, see [cardinal](/docs/text-to-speech?topic=text-to-speech-elements#say-as-cardinal) in the topic *SSML elements*.

Defect fix: Homonyms and other words are now pronounced correctly by English voices
:   **Defect fix:** The service now pronounces homonyms and other words correctly based on their context in English text that is to be synthesized. Previously, words such as `advocate` and `wifi` could be pronounced incorrectly by English voices.

Security vulnerability addressed
:   The following security vulnerability has been fixed:
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to denial of service in Pypa Setuptools (CVE-2022-40897)](https://www.ibm.com/support/pages/node/6958142){: external}

## 30 January 2023 (Version 4.6.2)
{: #text-to-speech-data-30january2023}

Version 4.6.2 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.6.2 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.6.x and Red Hat OpenShift versions 4.8 and 4.10. For more information, see [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

The custom resource now includes a new `fileStorageClass` property
:   The custom resource for the Watson Speech services now includes a `fileStorageClass` property in addition to the existing `blockStorageClass` property. You specify both block and file storage classes when you install or upgrade a service. During upgrade from a previous version, the new property is added automatically to the custom resource by the `--file_storage_class` option on `cli manage apply-cr` command.

    For more information about the available block and file storage classes you use with each of the supported storage solutions, see the table of *Storage requirements* under *Information you need to complete this task* on the page "Installing Watson Speech services" in [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

Additional information about provisioning a service instance
:   The documentation now includes information about creating a service instance programmatically. It also includes examples of listing service instances and deleting a service instance. For more information, see *Creating a Watson Speech services instance* in the *Post-installation setup* documentation in [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

Server-side encryption is enabled for the MinIO datastore
:   The Speech services have now enabled server-side encryption for object storage in the MinIO datastore. No action is required on your part.

Change to audit webhooks
:  The Speech services have now removed the audit webhook dependency. The services now write audit events directly to the server. After upgrading to version 4.6.2, some webhook resources might remain until all services can remove the dependency. The remaining resources will be removed in a future release. No action is required on your part.

New US English expressive neural voices
:   The service offers four new expressive neural voices for US English:
    -   `en-US_AllisonExpressive`
    -   `en-US_EmmaExpressive`
    -   `en-US_LisaExpressive`
    -   `en-US_MichaelExpressive`

    Expressive neural voices offer natural-sounding speech that is exceptionally clear, crisp, and fluid. The new voices are generally available (GA) for production use. They support the use of both standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) phonetic symbols. For more information, see
    -   [Supported languages and voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-expressive)
    -   [Expressive neural voices](/docs/text-to-speech?topic=text-to-speech-voices#language-voices-expressive)

New speaking styles with expressive neural voices
:   The expressive neural voices determine the sentiment of the text from the context of its words and phrases. The speech that they produce, in addition to having a very conversational style, reflects the mood of the text. But you can embellish the voices' natural tendencies by indicating that all or some of the text is to emphasize one of the following speaking styles:
    -   **Cheerful** - Expresses happiness and good news.
    -   **Empathetic** - Expresses empathy or sympathy.
    -   **Neutral** - Expresses objectivity and evenness.
    -   **Uncertain** - Expresses confusion or uncertainty.

    For more information, see [Using speaking styles](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#syntheses-expressive-styles).

New interjection emphasis with expressive neural voices
:   With expressive neural voices, the service automatically detects a set of common interjections based on context. When it synthesizes these interjections, it gives them the natural emphasis that a human would use in normal conversation. For some of the interjections, you can use SSML to enable or disable their emphasis. For more information, see [Emphasizing interjections](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#emphasizing-interjections).

New word emphais with expressive neural voices
:   The expressive voices use a conversational style that naturally applies the correct intonation from context. But you can indicate that one or more words are to be given more or less emphasis. The change in stress can be indicated by an increase or decrease in pitch, timing, volume, or other acoustic attributes. For more information, see [Emphasizing words](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#emphasizing-words).

The service now enforces stricter SSML validation
:   The service now enforces stricter validation of input text that includes Speech Synthesis Markup Language (SSML) elements. Required elements of attributes must be specified with valid values. Otherwise, the request fails with a 400 error code. For more information about SSML validation and the requirements that marked-up text must meet, see [SSML validation](/docs/text-to-speech?topic=text-to-speech-ssml#ssml-errors).

Defect fix: The gender listed for the `en-US_MichaelExpressive` voice is now correct
:   **Defect fix:** When you list information about the available voices, the `gender` of the `en-US_MichaelExpressive` voice is now `male`. Previously, the voice's gender was mistakenly described as `female`. For more information, see [Listing information about voices](/docs/text-to-speech?topic=text-to-speech-voices-list).

Security vulnerabilities addressed
:   The following security vulnerabilities have been fixed:
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to issues in OpenSSL (CVE-2022-1434, CVE-2022-1343, CVE-2022-1292, CVE-2022-1473)](https://www.ibm.com/support/pages/node/6890819){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary command execution in OpenSSL (CVE-2022-2068)](https://www.ibm.com/support/pages/node/6890831){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in protobuf (CVE-2022-1941)](https://www.ibm.com/support/pages/node/6890835){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a buffer overflow in GNU glibc (CVE-2021-3999)](https://www.ibm.com/support/pages/node/6890837){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security bypass in GNU gzip (CVE-2022-1271)](https://www.ibm.com/support/pages/node/6890841){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Golang Go (CVE-2022-27664)](https://www.ibm.com/support/pages/node/6890843){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Golang Go (CVE-2022-2879)](https://www.ibm.com/support/pages/node/6909749){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to query parameter smuggling in Golang Go (CVE-2022-2880)](https://www.ibm.com/support/pages/node/6890847){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Golang Go (CVE-2022-32189)](https://www.ibm.com/support/pages/node/6890849){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Golang Go (CVE-2022-41715)](https://www.ibm.com/support/pages/node/6890851){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to information exposure in OpenSSL (CVE-2022-2097)](https://www.ibm.com/support/pages/node/6890853){: external}

## 30 November 2022 (Version 4.6.0)
{: #text-to-speech-data-30november2022}

Version 4.6.0 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.6.0 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.6.x and Red Hat OpenShift versions 4.8 and 4.10. For more information, see [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

Amazon Web Services (AWS) is now supported
:   {{site.data.keyword.watson}} Speech services for {{site.data.keyword.icp4dfull_notm}} are now supported on Amazon Web Services™ (AWS™). The services support Amazon Elastic Block Store, which you specify by setting the `blockStorageClass` property of the Speech services custom resource to `gp2-csi` or `gp3-csi`.

New storage classes are now supported
:   {{site.data.keyword.watson}} Speech services for {{site.data.keyword.icp4dfull_notm}} now support two additional storage classes:
    -   IBM Cloud Block Storage (`ibmc-block-gold`)
    -   NetApp Trident (`ontap-nas`)

    You specify the storage class with the `blockStorageClass` property of the Speech services custom resource. For more information about all supported storage classes, see the following topics in [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}:
    -   *Before you begin* in *Installing Watson Speech services*
    -   *Specifying a storage class* in *Using the Watson Speech services custom resource*

Known issue: Some Watson Speech services pods do not have annotations that are used for scheduling
:   **Known issue:** Some Watson Speech services pods are missing the `cloudpakInstanceId` annotation. If you use the {{site.data.keyword.icp4dfull_notm}} scheduling service, any Watson Speech services pods without the `cloudpakInstanceId` annotation are
    -   Scheduled by the default Kubernetes scheduler rather than the scheduling service
    -   Not included in the quota enforcement

Monitoring of the PostgreSQL datastore is now available
:   You can now enable monitoring of the PostgreSQL datastore to receive updates on its usage and status by the Watson Speech services. The events can be consumed by Prometheus monitoring software or whatever application you use for monitoring. By enabling monitoring for user-defined projects in addition to the default platform monitoring, you can monitor your own projects with the Red Hat® OpenShift® Container Platform monitoring stack. This capability includes an additional property, `spec.global.datastores.postgressql.enablePodMonitor`, in the Speech services custom resource.

    For more information, see the topic *Monitoring the PostgreSQL datastore for Watson Speech services* in the *Administering* section of [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

Defect fix: PostgreSQL datastore is no longer installed if only runtime microservices are enabled
:   **Defect fix:** The PostgreSQL datastore is no longer installed if only the runtime microservices are enabled. The datastore is now installed only if at least one of the `sttAsync`, `sttCustomization`, or `ttsCustomization` microservices is installed. PostgreSQL is not uninstalled if at a later date these microservices are disabled.

    Prior to version 4.6.0, PostgreSQL was always installed with the Speech services. If you are an existing customer who used only the runtime microservices of the Speech services prior to version 4.6.0, PostgreSQL remains installed but is not used. In this case, installation of PostgreSQL persists across upgrades.

    The MinIO datastore is always installed because the runtime microservices depend on it. The RabbitMQ datastore is installed only if the `sttAsync` microservice is installed.

    For more information, see *Datastore properties* in *Using the Watson Speech services custom resource* in [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.6.x?topic=services-watson-speech){: external}.

Defect fix: Creation of a Network Policy is no longer necessary for the PostgreSQL operator to monitor its operands
:   **Defect fix:** For version 4.6.0, it is not necessary to create a Network Policy to allow the PostgreSQL operator to monitor its operands, as described in the [10 November 2022 (Versions 4.0.x and 4.5.x)](#text-to-speech-data-10november2022) service update. As of version 4.6.0, the service handles this situation automatically.

New beta `rate_percentage` query parameter for controlling the global speaking rate
:   The service offers a new `rate_percentage` query parameter to modify the speaking rate for a speech synthesis request. The speaking rate is the speed at which the service speaks the text that it synthesizes into speech. A higher rate causes the text to be spoken more quickly; a lower rate causes the text to be spoken more slowly. The parameter changes the per-voice default rate for an entire request. For more information, see [Modifying the speaking rate](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-rate-percentage).

New beta `pitch_percentage` query parameter for controlling the global speaking pitch
:   The service offers a new `pitch_percentage` query parameter to modify the speaking pitch for a synthesis request. The speaking pitch represents the tone of the speech that the service synthesizes. It represents how high or low the tone of the voice is perceived by the listener. A higher pitch results in speech that is spoken at a higher tone and is perceived as a higher voice; a lower pitch results in speech that is spoken in a lower tone and is perceived as a lower voice. The parameter changes the per-voice default pitch for an entire request. For more information, see [Modifying the speaking pitch](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-pitch-percentage).

Defect fix: Custom word translations now accept commas in all cases
:   **Defect fix:** Word translations added to custom models now accept commas in all cases. Previously, a comma in a translation could occasionally cause the translation to fail to generate valid audio when used for speech syntheses. This problem was identified in US English custom models.

Defect fix: French synthesis of dates is now consistent
:   **Defect fix:** French synthesis no longer includes the article "le" before dates of the form "the *ordinal* of *month*." Previously, the article was included only for the first day of the month for French (for example, "the first of September," "le premier septembre").

Defect fix: Japanese synthesis is improved to handle long strings of input text
:   **Defect fix:** The service now correctly synthesizes Japanese requests that include long strings of characters. Previously, the service failed to properly synthesize very long strings of Japanese text.

Defect fix: Add rules for custom model naming documentation
:   **Defect fix:** The documentation now provides detailed rules for naming custom models. For more information, see
    -   [Creating a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsCreate)
    -   [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}

Security vulnerabilities addressed
:   The following security vulnerabilities have been fixed:
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a cross-configuration attack against OpenPGP (CVE-2021-40528)](https://www.ibm.com/support/pages/node/6843867){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in PCRE2 (CVE-2022-1586)](https://www.ibm.com/support/pages/node/6843869){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in Vim (CVE-2022-1621)](https://www.ibm.com/support/pages/node/6843871){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a buffer overflow in Vim (CVE-2022-1629)](https://www.ibm.com/support/pages/node/6843873){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in Vim (CVE-2022-1785, CVE-2022-1897, CVE-2022-1927)](https://www.ibm.com/support/pages/node/6843875){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security restrictions bypass in cURL libcurl (CVE-2022-22576)](https://www.ibm.com/support/pages/node/6843877){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to credential exposure in cURL libcurl (CVE-2022-27774)](https://www.ibm.com/support/pages/node/6843879){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to data information exposure in cURL libcurl (CVE-2022-27776)](https://www.ibm.com/support/pages/node/6843881){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security restrictions bypass in cURL libcurl (CVE-2022-27782)](https://www.ibm.com/support/pages/node/6843883){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in GNOME libxml2 (CVE-2022-29824)](https://www.ibm.com/support/pages/node/6843885){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a SQL injection in PostgreSQL (CVE-2022-31197)](https://www.ibm.com/support/pages/node/6843887){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in libexpat (CVE-2022-25313)](https://www.ibm.com/support/pages/node/6843889){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in libexpat (CVE-2022-25314)](https://www.ibm.com/support/pages/node/6843891){: external}

## 10 November 2022 (Versions 4.0.x and 4.5.x)
{: #text-to-speech-data-10november2022}

Known issue: Updated Network Policy needed for PostgreSQL operator
:   **Known issue:** For Speech services version 4.0.x (not including version 4.0.0) and 4.5.x, if the PostgreSQL operator and the Speech services are installed in different namespaces, the PostgreSQL operator is not able to monitor the PostgreSQL operands for the Speech services. The operator is prevented from monitoring the operands by the Network Policy that is in place for the Speech services.

    This problem does not prevent the PostgreSQL cluster from functioning properly. The cluster remains active and fully functional. However, the operator is not able to update the operands when you upgrade to new versions of the Speech services.

    The solution for the problem is to create an additional Network Policy for the PostgreSQL operator, as shown in the following steps. You can perform the steps regardless of whether the PostgreSQL operator is installed in the same namespace as the Speech services or in a different namespace.

    1.  Log in as an administrator of the Red Hat® OpenShift® project where the Speech services are installed.
    2.  Enter the following command to update the Network Policy for the Speech services:

        ```sh
        cat << EOF | oc apply -f -
        apiVersion: networking.k8s.io/v1
        kind: NetworkPolicy
        metadata:
          labels:
            app.kubernetes.io/component: stt
            app.kubernetes.io/instance: {{ <custom-resource-name> }}
            app.kubernetes.io/name: speech-to-text
            release: {{ <custom-resource-name> }}
          name: <custom-resource-name>-postgres-network-policy
          namespace: {{ <cpd-instance-namespace> }}
        spec:
          ingress:
          - from:
            - namespaceSelector: {}
              podSelector:
                matchLabels:
                  app.kubernetes.io/name: cloud-native-postgresql
        EOF
        ```
        {: pre}

        where
        -   `<custom-resource-name>` is the name of the Speech services custom resource. The recommended name for version 4.0.x is `speech-prod-cr`; the recommended name for version 4.5.x is `speech-cr`.
        -   `<cpd-instance-name>` is the name of the project (namespace) in which the Speech services are installed. The documentation uses the environment variable `${PROJECT_CPD_INSTANCE}` to identity the namespace.

    3.  To verify that the updated Network Policy allows the operator to monitor the operands and that the PostgreSQL cluster is in a healthy state, enter the following command, where `<custom-resource-name>` and `<cpd-instance-name>` are the values you used in the previous step:

        ```text
        oc -get cluster {{ <custom-resource-name> }}-postgres -n {{ <cpd-instance-namespace> }}
        ```
        {: codeblock}

        If the PostgreSQL cluster is functioning properly, the command produces output similar to the following:

        ```text
        NAME                 AGE   INSTANCES   READY   STATUS                     PRIMARY
        speech-cr-postgres   14d   3           3       Cluster in healthy state   speech-cr-postgres-1
        ```
        {: codeblock}

    These steps do not cause operator to update the operands to the latest versions. However, the operands are upgraded as expected when you next upgrade the Speech services software.

## 13 October 2022 (Version 4.5.3)
{: #text-to-speech-data-13october2022}

Version 4.5.3 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.5.3 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.5.x and Red Hat OpenShift versions 4.6, 4.8, and 4.10. For more information, see [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=services-watson-speech){: external}.

Audit events are available for the Speech services
:   The {{site.data.keyword.icp4dfull_notm}} Audit Logging Service generates and forwards audit events for both the {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}} services. The audit events match those that are available for [Activity Tracker](/docs/text-to-speech?topic=text-to-speech-at-events) with the public service. For more information, see [Audit events](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=2-audit-events){: external}.

You cannot uninstall individual Speech service components
:   The documentation now notes that you cannot uninstall individual service components (microservices) once they are installed. To remove any of the following components, you must uninstall the Watson Speech services in their entirety and reinstall only the components that you need: {{site.data.keyword.speechtotextshort}} runtime, {{site.data.keyword.speechtotextshort}} asynchronous HTTP, {{site.data.keyword.speechtotextshort}} customization, {{site.data.keyword.texttospeechshort}} runtime, and {{site.data.keyword.texttospeechshort}} customization. For more information about installing the Speech services, see [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=services-watson-speech){: external}.

New beta `spell_out_mode` parameter for German voices
:   To indicate how individual characters of a string are to be spelled out, you can now include the beta `spell_out_mode` query parameter with a synthesis request for a German voice. By default, the service spells out individual characters at the same rate at which it synthesizes text for a language. You can use the parameter to direct the service to spell out individual characters more slowly, in groups of one, two, or three characters. Use the parameter with the SSML `<say-as>` element to control how the characters of a string are synthesized. For more information, see [Specifying how strings are spelled out](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-spell-out-mode).

Known limitation with using the Ogg audio format with the Safari browser
:   By default, the service returns audio in the Ogg audio format with the Opus codec (`audio/ogg;codecs=opus`). However, the Ogg audio format is not supported with the Safari browser. If you are using the the {{site.data.keyword.texttospeechshort}} service with the Safari browser, you must specify a different format in which you want the service to return the audio.
    -   For more information about the available formats, see [Supported audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats#formats-supported).
    -   For more information about specifying a format, see [Specifying an audio format](/docs/text-to-speech?topic=text-to-speech-audio-formats#formats-specify).

Troubleshooting upgrade from version 4.0.x to version 4.5.x
:   When you upgrade the Speech services from version 4.0.x to version 4.5.x, you might encounter an issue where the PostgreSQL pods become stuck in the `Terminating` state. If this problem occurs during your upgrade, perform the following steps to resolve the problem. The information and steps are also documented in *Upgrading Watson Speech services from Version 4.0 to Version 4.5* in the *Upgrading* topic of [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=services-watson-speech){: external}.

    1.  Use the following command to identify pods that remain in the `Terminating` state:

    ```sh
    oc get pods -n ${PROJECT_CPD_INSTANCE} -o wide | awk {'print $1'}
    ```
    {: codeblock}

    1.  Use the following command to set the environment variable `pods` to include the list of pods that remain in the `Terminating` state:

    ```sh
    pods=$(oc get pods -n ${PROJECT_CPD_INSTANCE} -o wide | grep Terminating | awk {'print $1'})
    ```
    {: codeblock}

    1.  Use the following command to delete the stuck pods so that the upgrade process can continue:

    ```sh
    oc delete pod $pods -n ${PROJECT_CPD_INSTANCE} --force=true --grace-period=0
    ```
    {: codeblock}

Documentation updates for the SSML `<prosody>` element
:   The documentation for the SSML `<prosody>` element and its `pitch` and `rate` parameters has been improved and clarified. It also now includes a description of the differences between the service and the latest version of the SSML specification. For more information, see [The `<prosody>` element](/docs/text-to-speech?topic=text-to-speech-elements#prosody_element).

Security vulnerabilities addressed
:   The following security vulnerabilities have been fixed:
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a buffer over-read flaw in Linux Kernel (CVE-2020-28915)](https://www.ibm.com/support/pages/node/6829133){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security bypass in GNU Gzip (CVE-2022-1271)](https://www.ibm.com/support/pages/node/6829139){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to elevated privileges in Apple macOS Monterey and macOS Big Sur (CVE-2022-26691)](https://www.ibm.com/support/pages/node/6829141){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to elevated privileges in Linux Kernel (CVE-2022-27666)](https://www.ibm.com/support/pages/node/6829143){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to cross-site scripting in Apache Tomcat (CVE-2022-34305)](https://www.ibm.com/support/pages/node/6829145){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security restrictions bypass in GNU C Library (CVE-2019-19126)](https://www.ibm.com/support/pages/node/6829149){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in GNU C Library ( CVE-2020-10029)](https://www.ibm.com/support/pages/node/6829151){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in GNU glibc (CVE-2020-1751)](https://www.ibm.com/support/pages/node/6829155){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in GNU glibc (CVE-2020-1752)](https://www.ibm.com/support/pages/node/6829157){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to information disclosure or denial of service in GNU glibc (CVE-2021-35942)](https://www.ibm.com/support/pages/node/6829159){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to buffer overflow in OpenSSL (CVE-2021-3711)](https://www.ibm.com/support/pages/node/6829161){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to information disclosure or denial of service in OpenSSL (CVE-2021-3712)](https://www.ibm.com/support/pages/node/6829165){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to weakened security in OpenSSL (CVE-2021-4160)](https://www.ibm.com/support/pages/node/6829167){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in OpenSSL (CVE-2022-0778)](https://www.ibm.com/support/pages/node/6829175){: external}

## 3 August 2022 (Version 4.5.1)
{: #text-to-speech-data-3august2022}

Version 4.5.1 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.5.1 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.5.x and Red Hat OpenShift versions 4.6, 4.8, and 4.10. For more information, see [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=services-watson-speech){: external}.

Support for FIPS-enabled clusters
:   Both {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} and {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} now support running on Federal Information Processing Standard (FIPS)-enabled clusters. For more information, see [Services that support FIPS](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=considerations-services-that-support-fips){: external}.

Defect fix: Fixed ephemeral storage calculations to prevent occasional pod evictions
:   **Defect fix:** A defect was fixed and calculation of ephemeral storage limits is now more precise for the {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} and {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} runtimes. These changes prevent occasional pod evictions when the services' runtimes are under heavy load.

The service does not support multilingual speech synthesis
:   The service does not support multilingual speech synthesis at this time. However, you can use customization to approximate the pronunciation of words from other languages. For more information, see [Multilingual speech synthesis](/docs/text-to-speech?topic=text-to-speech-voices-use#synthesis-multilingual).

Security vulnerabilities addressed
:   The following security vulnerabilities have been fixed:
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in rsyslog (CVE-2022-24903)](https://www.ibm.com/support/pages/node/6610096){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to an HTTP request smuggling issue in Twisted (CVE-2022-24801)](https://www.ibm.com/support/pages/node/6610098){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service, caused by a buffer overflow in Twisted (CVE-2022-21716)](https://www.ibm.com/support/pages/node/6610100){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service, caused by incomplete string comparison in NumPy (CVE-2021-34141)](https://www.ibm.com/support/pages/node/6610102){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service, caused by a buffer overflow in NumPy (CVE-2021-41496)](https://www.ibm.com/support/pages/node/6610104){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to cookie and authorization header exposure in Twisted (CVE-2022-21712)](https://www.ibm.com/support/pages/node/6605065){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in Perl (CVE-2018-18311)](https://www.ibm.com/support/pages/node/6610118){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in Perl (CVE-2018-18312)](https://www.ibm.com/support/pages/node/6610122){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in Perl (CVE-2018-18313)](https://www.ibm.com/support/pages/node/6610124){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in Perl (CVE-2018-18314)](https://www.ibm.com/support/pages/node/6610126){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in Perl (CVE-2018-6913)](https://www.ibm.com/support/pages/node/6610128){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to CRLF injection in Python (CVE-2019-11236)](https://www.ibm.com/support/pages/node/6610234){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in GNU Tar (CVE-2019-9923)](https://www.ibm.com/support/pages/node/6610238){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in Perl (CVE-2020-10543)](https://www.ibm.com/support/pages/node/6610240){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to an integer overflow in Perl (CVE-2020-10878)](https://www.ibm.com/support/pages/node/6610242){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a buffer overflow in Perl (CVE-2020-12723)](https://www.ibm.com/support/pages/node/6610283){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in urllib3 (CVE-2021-33503)](https://www.ibm.com/support/pages/node/6610285){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to injection attacks in Ansible (CVE-2021-3583)](https://www.ibm.com/support/pages/node/6610287){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Golang Go (CVE-2022-23772)](https://www.ibm.com/support/pages/node/6610289){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to incorrect access control in Golang Go (CVE-2022-23773)](https://www.ibm.com/support/pages/node/6610291){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Golang Go (CVE-2022-23806)](https://www.ibm.com/support/pages/node/6610293){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Golang Go (CVE-2022-24675)](https://www.ibm.com/support/pages/node/6610295){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Golang Go (CVE-2022-24921)](https://www.ibm.com/support/pages/node/6610297){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Golang Go (CVE-2022-28327)](https://www.ibm.com/support/pages/node/6610299){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a heap-based buffer overflow in libssh, caused by improper bounds checking (CVE-2021-3634)](https://www.ibm.com/support/pages/node/6610303){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in Python (CVE-2021-3737)](https://www.ibm.com/support/pages/node/6610329){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a possible sensitive information exposure in Python (CVE-2021-4189)](https://www.ibm.com/support/pages/node/6610339){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security restrictions bypass in lxml (CVE-2021-43818)](https://www.ibm.com/support/pages/node/6610341){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in MS Visual Studio (CVE-2021-21300)](https://www.ibm.com/support/pages/node/6610343){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a security restrictions bypass in Git (CVE-2021-40330)](https://www.ibm.com/support/pages/node/6610345){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution in MS Visual Studio (CVE-2022-24765)](https://www.ibm.com/support/pages/node/6610347){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary command execution in Git (CVE-2018-1000021)](https://www.ibm.com/support/pages/node/6610349){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to cross-site scripting in jQuery (CVE-2015-9251)](https://www.ibm.com/support/pages/node/6610351){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to cross-site scripting in jQuery (CVE-2019-11358)](https://www.ibm.com/support/pages/node/6610361){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to cross-site scripting in jQuery (CVE-2020-11022)](https://www.ibm.com/support/pages/node/6610363){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to cross-site scripting in jQuery (CVE-2020-11023)](https://www.ibm.com/support/pages/node/6610365){: external}
    - [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a data binding rules security weakness in Spring Framework (CVE-2022-22968)](https://www.ibm.com/support/pages/node/6610371){: external}

## 29 June 2022 (Version 4.5.0)
{: #text-to-speech-data-29june2022}

Version 4.5.0 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.5.0 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.5.x and Red Hat OpenShift versions 4.6, 4.8, and 4.10. For more information, see [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=services-watson-speech){: external}.

Unified Speech services for {{site.data.keyword.icp4dfull_notm}} documentation
:   The installation and administration documentation for both {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}} is now combined in the {{site.data.keyword.icp4dfull_notm}} documentation. For more information about installing and managing the Speech services, see [{{site.data.keyword.watson}} Speech services on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.5.x?topic=services-watson-speech){: external}.

Changes to Speech services custom resource
:   The custom resource is now created when you initially install the Speech services. The process is described in the {{site.data.keyword.icp4dfull_notm}} installation documentation. The content of the custom resource has changed:
    -   The recommended name of the custom resource has changed from `speech-prod-cr` to `speech-cr`.
    -   All references to storage class have changed from variants of `storageClass` to `blockStorageClass`.
    -   The name of the Portworx block storage class has changed from `portworx-shared-gp3` to `portworx-db-gp3-sc`.
    -   The `createSecret` property has been removed for the MinIO and PostgreSQl datastores. The property is only used internally. The Speech services always use a secrets object if you create one, and they always automatically create the object if none is provided.

User-provided secrets object now supported for RabbitMQ datastore
:   You can now provide security credentials for the RabbitMQ datastore, just as you can for the MinIO and PostgreSQL datastores. The documented process is similar for all three datastores.

Defect fix: Multiple consecutive SSML `<phoneme>` tags are now parsed correctly
:   **Defect fix:** The service now correctly synthesizes text that contains consecutive `<phoneme>` tags. Previously, if the text contained two or more consecutive `<phoneme>` tags, the service synthesized only the first tag, ignoring the others.

Security vulnerabilities addressed
:   No security vulnerabilities were fixed for version 4.5.0.

## 25 May 2022 (Version 4.0.9)
{: #text-to-speech-data-25may2022}

Version 4.0.9 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.0.9 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.x and Red Hat OpenShift versions 4.6 and 4.8. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

New support for `audio/alaw` audio format
:   The list of supported audio formats now includes `audio/alaw;rate={rate}`. Like `audio/basic` and `audio/mulaw`, this format provides single-channel audio that is encoded by using 8-bit u-law (or mu-law) data that is sampled at 8 kHz. For more information, see [Using audio formats](/docs/text-to-speech?topic=text-to-speech-audio-formats).

The Speech services do not support the OADP backup and restore utility
:   Watson Speech services do not support the {{site.data.keyword.icp4dfull_notm}} OpenShift APIs for Data Protection (OADP) backup and restore utility. If the Speech services are installed on a cluster, you might not be able to use the {{site.data.keyword.icp4dfull_notm}} OADP backup and restore utility to back up other services that are installed on that cluster. This limitation applies to version 4.0.0 and later versions of the Speech services.

Security vulnerabilities addressed
:   The following security vulnerabilities have been fixed:
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable a denial of service, caused by a buffer overflow with Twisted (CVE-2022-21716)](https://www.ibm.com/support/pages/node/6593867){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service in NumPy. (CVE-2021-33430)](https://www.ibm.com/support/pages/node/6592841){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a denial of service, caused by improper input validation with Spring Framework (CVE-2022-22950)](https://www.ibm.com/support/pages/node/6593865){: external}

## 1 May 2022 (Version 1.2.x)
{: #text-to-speech-data-1may2022}

Important: End of service for {{site.data.keyword.texttospeechshort}} version 1.2.x on {{site.data.keyword.icp4dfull_notm}} version 3.5
:   **Important:** {{site.data.keyword.texttospeechshort}} version 1.2.x on {{site.data.keyword.icp4dfull_notm}} version 3.5 is out of service as of 1 May 2022. {{site.data.keyword.texttospeechshort}} version 1.2.x is no longer supported, available, or documented. For more information about End of Service for {{site.data.keyword.texttospeechshort}}, which is part of the {{site.data.keyword.watson}} API Kit, see [Software support discontinuance: IBM Watson API Kit for IBM Cloud Pak for Data 1.2.x](https://www.ibm.com/common/ssi/cgi-bin/ssialias?subtype=ca&infotype=an&appname=iSource&supplier=897&letternum=ENUS922-038).

## 27 April 2022 (Version 4.0.8)
{: #text-to-speech-data-27april2022}

Version 4.0.8 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.0.8 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.x and Red Hat OpenShift versions 4.6 and 4.8. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

New environment variables used in {{site.data.keyword.icp4dfull_notm}} documentation
:   Most commands in the {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} documentation have been updated to use a common set of environment variables. The documentation provides a script to automatically export the environment variables before you run installation, upgrade, and administration commands. After you source the script, you can copy most commands from the documentation and run them without making any changes.

    The environment variables that the script defines include the following:
    -   `${PROJECT_CPD_INSTANCE}` identifies the project where you plan to install {{site.data.keyword.icp4dfull_notm}} and the Speech services.
    -   `${PROJECT_CPD_OPS}` identifies the project for the {{site.data.keyword.icp4dfull_notm}} platform operator.
    -   `${PROJECT_CPFS_OPS}` identifies the project for the {{site.data.keyword.icp4dfull_notm}} foundational services.

    For more information about using the environment variables, see [Best practice: Setting up install variables](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=installing-best-practice-setting-up-install-variables){: external}.

The `ttsVoiceMarginalCPU` property is no longer documented
:   The `ttsVoiceMarginalCPU` property has been removed from the documentation for the Speech services custom resource. The property manages the tradeoff between concurrency and speech synthesis speed. The default value of `400` ensures a reasonable balance for most customers and maintains real-time synthesis.

Security vulnerabilities addressed
:   The following security vulnerabilities have been fixed:
    -   [Security Bulletin: A vulnerability with Guava affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2020-8908)](https://www.ibm.com/support/pages/node/6575479){: external}
    -   [Security Bulletin: A Google Guava vulnerability affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2018-10237)](https://www.ibm.com/support/pages/node/6575477){: external}
    -   [Security Bulletin: Vulnerabilities in Apache Tomcat affect IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2022-23181)](https://www.ibm.com/support/pages/node/6575481){: external}
    -   [Security Bulletin: A Cyrus SASL vulnerability affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2022-24407)](https://www.ibm.com/support/pages/node/6575483){: external}
    -   [Security Bulletin: A vulnerability with GNU wget affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2016-4971)](https://www.ibm.com/support/pages/node/6575485){: external}
    -   [Security Bulletin: A vulnerability with GNU Wget affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2018-0494)](https://www.ibm.com/support/pages/node/6575487){: external}
    -   [Security Bulletin: A vulnerability in 'GNU Wget' affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2018-20483)](https://www.ibm.com/support/pages/node/6575489){: external}
    -   [Security Bulletin: A vulnerability in ISC BIND affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2018-5741)](https://www.ibm.com/support/pages/node/6575493){: external}
    -   [Security Bulletin: A vulnerability in Python affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2019-20916)](https://www.ibm.com/support/pages/node/6575495){: external}
    -   [Security Bulletin: A vulnerability with ISC BIND affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2021-25214)](https://www.ibm.com/support/pages/node/6575497){: external}
    -   [Security Bulletin: A vulnerability in ISC BIND affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2021-25215)](https://www.ibm.com/support/pages/node/6575499){: external}
    -   [Security Bulletin: A vulnerability in ISC BIND affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2021-25216)](https://www.ibm.com/support/pages/node/6575503){: external}
    -   [Security Bulletin: A vulnerability in ISC BIND affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2021-25219)](https://www.ibm.com/support/pages/node/6575505){: external}
    -   [Security Bulletin: A vulnerability in PostgreSQL JDBC Driver (PgJDBC) affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2022-21724)](https://www.ibm.com/support/pages/node/6575507){: external}
    -   [Security Bulletin: A vulnerability in GNU Tar affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2019-9923)](https://www.ibm.com/support/pages/node/6575509){: external}
    -   [Security Bulletin: A vulnerability in logback-classic affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2021-42550)](https://www.ibm.com/support/pages/node/6575511){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a stack-based buffer overflow in GNU C Library (CVE-2022-23218)](https://www.ibm.com/support/pages/node/6578617){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to stack-based buffer overflow in GNU C Library (CVE-2022-23219)](https://www.ibm.com/support/pages/node/6578619){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to a buffer overflow and underflow in GNU C Library (CVE-2021-3999)](https://www.ibm.com/support/pages/node/6578621){: external}

## 30 March 2022 (Version 4.0.7)
{: #text-to-speech-data-30march2022}

Version 4.0.7 is now available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 4.0.7 is now available. This version supports {{site.data.keyword.icp4dfull_notm}} version 4.x and Red Hat OpenShift versions 4.6 and 4.8. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

Custom resource property for specifying a default voice
:   The default voice for speech synthesis and pronunciation requests is `en-US_MichaelV3Voice`. If you do not install the `en-US_MichaelV3Voice`, you must either
    -   Use the `voice` parameter to pass the voice that is to be used with each request.
    -   Specify a new default voice for your installation of {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} by using the `defaultTTSVoice` property in the Speech services custom resource. For more information, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external} and [Using the default voice](/docs/text-to-speech?topic=text-to-speech-voices-use#specify-voice-default).

Change to word timing response for WebSocket interface
:   The response object that the service sends when you request word timings with the WebSocket interface has changed. The service now sends word timing results in a single array that includes a string followed by two floats:

    ```json
    {
      "words": [
        ["Hello", 0.0, 0.259],
        ["world", 0.259, 0.532]
      ]
    }
    ```
    {: codeblock}

    The service previously sent timing results as an array that included a string following by an array of two floats:

    ```json
    {
      "words": [
        ["Hello", [0.0629826778195474, 0.2590192737303819]],
        ["world", [0.2598829173456253, 0.5322130804452672]]
      ]
    }
    ```
    {: codeblock}

    Also, the level of precision for word timings and marks is now reduced to three decimal places. For more information about the new responses, see [Generating word timings](/docs/text-to-speech?topic=text-to-speech-timing).

Security vulnerabilities addressed
:   The following security vulnerabilities have been fixed:
    -   [Red Hat CVE-2022-24407](https://access.redhat.com/security/cve/CVE-2022-24407){: external}: A flaw was found in the SQL plugin shipped with Cyrus SASL. The vulnerability occurs due to failure to properly escape SQL input and leads to an improper input validation vulnerability. This flaw allows an attacker to execute arbitrary SQL commands and the ability to change the passwords for other accounts allowing escalation of privileges.
    -   [Security Bulletin: A jwt-go vulnerability affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2020-26160)](https://www.ibm.com/support/pages/node/6574543){: external}
    -   [Security Bulletin: A vulnerability in Golang Go affects IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2021-29923)](https://www.ibm.com/support/pages/node/6574545){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is affected but not classified as vulnerable by a remote code execution in Spring Framework (CVE-2022-22965)](https://www.ibm.com/support/pages/node/6583151){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to arbitrary code execution with IBM WebSphere Application Server (CVE-2021-23450)](https://www.ibm.com/support/pages/node/6583149){: external}

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
    -   [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices)
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

RabbitMQ datastore is now used only by the `sttAysnc` component
:   The RabbitMQ datastore was previously used by components of both Speech services, {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}}. It now handles non-persistent message queuing for the Speech to Text asynchronous HTTP component (`sttAsync`) only. It is used only if the `sttAsync` component is installed and enabled.

New Belgian Dutch and Czech neural voices
:   Two new neural voices are now available:
    -   *Belgian Dutch:* A new male Belgian Dutch (Flemish) voice, `nl-BE_BramVoice`.
    -   *Czech:* A new language, Czech, with a new female voice, `cs-CZ_AlenaVoice`.

    You can install the new voices along with all neural voices by setting the `voiceType` property of the custom resource to `neuralVoices`.
    -   For more information about using the custom resource to install voices, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.
    -   For more information about all available languages and voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

Defect fix: Update SSML documentation
:   **Defect fix:** The SSML documentation was updated to correct the following errors:
    -   The examples of the `<break>` element are now correct. The element is unary, as now shown in the examples. The previous examples included open and close tags with embedded text. The embedded text was not spoken by the service. For more information, see [The `<break>` element](/docs/text-to-speech?topic=text-to-speech-elements#break_element).
    -   The service supports Speech Synthesis Markup Language (SSML) version 1.1. All references and examples now use the correct version. The documentation previously referred to version 1.0.

Security vulnerabilities addressed
:   The following security vulnerabilities associated with Apache Log4j have been fixed:
    -   [Security Bulletin: Vulnerability in Apache Log4j may affect IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data (CVE-2021-4104)](https://www.ibm.com/support/pages/node/6551170){: external}
    -   [Security Bulletin: IBM Watson Speech Services Cartridge for IBM Cloud Pak for Data is vulnerable to denial of service and arbitrary code execution due to Apache Log4j (CVE-2021-45105 and CVE-2021-45046)](https://www.ibm.com/support/pages/node/6551168){: external}

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

Defect fix: Improve upgrade documentation
:   **Defect fix:** Documentation for upgrading the Speech services to new versions of {{site.data.keyword.icp4dfull_notm}} version 4.0.x included incorrect references in some commands. These references are now correct:
    -   The strings `watsonSpeechToTextStatus` and `watsonTextToSpeechStatus` have been changed to `speechStatus` in both cases.
    -   The strings `status.watsonSpeechToTextVersion` and `status.watsonTextToSpeechVersion` have been changed to `.spec.version` in both cases.

    For more information, see [Upgrading {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-upgrading-watson-text){: external}.

Defect fix: Improve SSML and speech synthesis
:   **Defect fix:** The following defects for the Speech Synthesis Markup Language (SSML) and speech synthesis were fixed with this release:

    -   The `pitch` attribute of the `<prosody>` element is now applied to all specified text. Previously, the pitch change was not always applied to the first word of the affected text. Also, the documentation now includes additional guidance about specifying a `pitch` value. For more information, see [The `pitch` attribute](/docs/text-to-speech?topic=text-to-speech-elements#prosody-pitch).
    -   Speech synthesis of Japanese text now speaks the audio more slowly. Previously, the synthesized speech was being spoken too quickly. If you find that synthesis of Japanese text is still spoken too quickly for your application, use the `rate` attribute of the SSML `<prosody>` element to control the rate of speech. For more information, see [The `rate` attribute](/docs/text-to-speech?topic=text-to-speech-elements#prosody-rate).
    -   Neural voices now parse the escaped apostrophe character (`&apos;`) properly. Previously, some neural voices were not interpreting the character properly.

Security vulnerability addressed
:   The following security vulnerability associated with Apache Log4j has been fixed:
    -   [Security Bulletin: Vulnerability in Apache Log4j may affect IBM Watson Speech Services Cartridge for {{site.data.keyword.icp4dfull_notm}} (CVE-2021-4428)](https://www.ibm.com/support/pages/node/6536732){: external}

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

    For more information about all available languages and voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

Installing voices
:   You can install either the enhanced neural voices or the neural voices. You can install only one of the two types of voices. When you install the service, you use the `voiceType` property of the custom resource to indicate the voices that are to be installed:

    -   Specify `enhancedNeuralVoices` to install the enhanced neural voices. You must then specify the individual enhanced neural voices that are to be installed. By default, only `en-US_AllisonV3Voice`, `en-US_LisaV3Voice`, and `en-US_MichaelV3Voice` are installed. You can choose to install these default voices, these and other voices, or just other voices. Only the voices that you install are available.
    -   Specify `neuralVoices` to install the neural voices. All of the neural voices are installed and available. You cannot refine the list of installed voices.

    For more information about using the custom resource to install voices, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

Specifying a voice for speech synthesis
:   Both the HTTP `POST` and `GET /v1/synthesize` methods, as well as the WebSocket `/v1/synthesize` method, accept an optional `voice` query parameter that you use to specify the voice that is to be used for speech synthesis. If you omit the `voice` parameter, the service uses a default voice. The default voice depends on the voices that you installed:

    -   *If you installed the enhanced neural voices,* the service uses the US English `en-US_MichaelV3Voice` by default. If that voice is not installed, you must specify a voice.
    -   *If you installed the neural voices,* the service always uses the Australian English `en-AU_MadisonVoice` by default.

    For more information, see [Using a voice for speech synthesis](/docs/text-to-speech?topic=text-to-speech-voices-use).

Specifying a language for a custom model
:   You use the `POST /v1/customizations` method to create a custom model. The method includes a `language` parameter that you use to identify the language of the new custom model.

    -   *If you installed the enhanced neural voices,* the `language` parameter is optional. By default, the service uses the `en-US` identifier for the language.
    -   *If you installed the neural voices,* the `language` parameter is required. You must specify the language for the custom model in the indicated format (for example, `en-AU` for Australian English).

    For more information about specifying a language when you create a custom model, see [Creating a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsCreate).

Defect fix: Correct intonation for Spanish enhanced neural voices
:   **Defect fix:** For the Castilian Spanish (`es-ES_EnriqueV3Voice` and `es-ES_LauraV3Voice`), Latin American Spanish (`es-LA_SofiaV3Voice`), and North American Spanish (`es-US_SofiaV3Voice`) voices, questions of all types now use the correct intonation. The voices previously did not use the correct intonation for some questions, instead pronouncing them like statements.

Defect fix: Correct multitenancy documentation
:   **Defect fix:** The {{site.data.keyword.icp4dfull_notm}} topic [Multitenancy support](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=planning-multitenancy-support){: external} incorrectly stated that the Speech services do not support multitenancy. The topic has been updated to state that the Speech services support the following operations:

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

    Enhanced neural voices support the use of both IPA and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) with the SSML `<phoneme>` element. Enhanced neural voices also achieve a slightly higher degree of natural-sounding speech. For more information, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

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

    `{Registry}` is the path for the internal Docker registry. It must be `image-registry.openshift-image-registry.svc:5000/{namespace}`, where `{namespace}` is the namespace in which {{site.data.keyword.icp4dfull}} is installed, normally `zen`.

## 9 April 2021 (Version 1.2.1)
{: #text-to-speech-data-9april2021}

Support for modifying installed models and voices
:   The Speech services let you add or remove installed models and voices for version 1.2 or 1.2.1 of the services.

## 26 March 2021 (Version 1.2.1)
{: #text-to-speech-data-26march2021}

Version 1.2.1 is available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.2.1 is now available. Versions 1.2 and 1.2.1 use the same version 1.2 documentation and installation instructions. Version 1.2.1 supports installation on Red Hat OpenShift version 4.6 in addition to versions 4.5 and 3.11.

New installation instructions
:   For both clusters connected to the internet and air-gapped clusters, the installation instructions include the following steps:
    -   Use the `oc label` command to set up required labels for the namespace where {{site.data.keyword.icp4dfull_notm}} is installed.
    -   Use the `oc project` command to ensure that you are pointing at the correct OpenShift project.
    -   Use the `cpd-cli install` command to install an Enterprise DB PostgreSQL server that is used by the Speech services.

    You perform these steps before you install the Speech services.

New uninstallation instructions
:   A step was added to the procedure for uninstalling the Speech services to clean up all of the resources from the installation.

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

    The abbreviated `speech-override.yaml` file has generally been reduced further by fine-tuning its contents to the essential elements.

## 9 December 2020 (Version 1.2)
{: #text-to-speech-data-9december2020}

Version 1.2 is available
:   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.2 is now available. Installation and administration of the service include many changes. This version supports {{site.data.keyword.icp4dfull_notm}} versions 3.5 and 3.0.1, and Red Hat OpenShift versions 4.5 and 3.11.

New voices
:   The service now offers three new voices:
    -   UK English: `en-GB_CharlotteV3Voice` and `en-GB_JamesV3Voice`
    -   French: `fr-FR_NicolasV3Voice`

    The service also offers an improved version of the existing UK voice, `en-KateV3Voice`. For more information about all supported languages and voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

Defect fix: Fix `<prosody>` element for Japanese
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
