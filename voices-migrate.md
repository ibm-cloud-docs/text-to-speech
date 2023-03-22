---

copyright:
  years: 2023
lastupdated: "2023-03-15"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Migrating from neural voices
{: #voices-migrate}

[IBM Cloud]{: tag-ibm-cloud}

The {{site.data.keyword.texttospeechfull}} service offers neural, enhanced neural, and expressive neural voices. All *neural voices* were deprecated on 31 March 2022. All neural voices reach their end of service date on **31 March 2023**, when they will be removed from the service and the documentation. No enhanced neural voices or expressive neural voices are effected by the deprecation.
{: shortdesc}

New enhanced neural and expressive neural voices are available for deprecated Australian English, Dutch Netherlands, and Korean voices. You must migrate your use of any deprecated voices to the new voices by the 31 March 2023 end of service date. This topic describes the steps that you need to take to migrate from deprecated neural voices to enhanced or expressive neural voices.

## Step 1: Identify the new voices to which you can migrate
{: #voices-migrate-identify}

Identify the new voices that you can use in place of the deprecated neural voices. Table 1 lists the new voices to which you can migrate from deprecated voices.

| Language | Deprecated neural voices | New enhanced and expressive neural voices |
|----------|:------------------------:|:-----------------------------------------:|
| Australian English   | `en-AU_CraigVoice`  \n `en-AU_MadisonVoice`  \n `en-AU_SteveVoice` | `en-AU_HeidiExpressive` (expressive neural)  \n `en-AU_JackExpressive` (expressive neural) |
| Dutch Netherlands    | `nl-NL_EmmaVoice`  \n `nl-NL_LiamVoice` | `nl-NL_MerelV3Voice` (enhanced neural) |
| Korean             | `ko-KR_HyunjunVoice`  \n `ko-KR_SiWooVoice`  \n `ko-KR_YoungmiVoice`  \n `ko-KR_YunaVoice` | `ko-KR_JinV3Voice` (enhanced neural) |
{: caption="Table 1. Voices to which you can migrate from neural voices"}

## Step 2: Use the new voices in speech synthesis
{: #voices-migrate-use}

Use the new voices in speech synthesis requests to determine their effectiveness for your application. For example, the following example uses the deprecated Australian English voice `en-AU_CraigVoice`:

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--data "{\"text\":\"hello world\"}" \
--output hello_world.wav \
"{url}/v1/synthesize?voice=en-AU_CraigVoice"
```
{: pre}

The following example replaces the deprecated voice with the new Australian English voice `en-AU_JackExpressive`:

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--data "{\"text\":\"hello world\"}" \
--output hello_world.wav \
"{url}/v1/synthesize?voice=en-AU_JackExpressive"
```
{: pre}

Repeat this substitution for each use of a deprecated voice in your application.

## Step 3: Update any custom models that are based on the neural voices
{: #voices-migrate-models}

If you used custom models to create a dictionary of custom words for your application, you need to verify that the custom words work properly with the new voices. At a minimum, you need to compare the phonetic symbols that you used with custom words for neural voices with the symbols that are available for the new enhanced and expressive neural voices. Table 2 provides links to the topics that provide the phonetic symbols for the deprecated and new voices.

| Language | Phonetic symbols for deprecated voices | Phonetic symbols for new voices |
|----------|:--------------------------------------:|:-------------------------------:|
| Australian English | [English (Australian) symbols (deprecated)](/docs/text-to-speech?topic=text-to-speech-auSymbols) | [English (Australian) symbols](/docs/text-to-speech?topic=text-to-speech-auSymbols-new) |
| Dutch Netherlands  | [Dutch (Netherlands) symbols (deprecated)](/docs/text-to-speech?topic=text-to-speech-nlSymbols) | [Dutch (Netherlands) symbols](/docs/text-to-speech?topic=text-to-speech-nlSymbols-new) |
| Korean             | [Korean symbols (deprecated)](/docs/text-to-speech?topic=text-to-speech-koSymbols) | [Korean symbols](/docs/text-to-speech?topic=text-to-speech-koSymbols-new) |
{: caption="Table 2. Phonetic symbols for deprecated and new voices"}

You need to be aware of the following information when validating your custom words:

-   Enhanced and expressive neural voices support both standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) phonetic symbols. Deprecated neural voices support only IPA symbols.
-   Enhanced and expressive neural voices use IPA symbols that are different from those that are available with deprecated neural voices. Some overlap exists, but you need to verify and test the translations of all words to ensure that they are defined to your satisfaction.
-   If you update custom words in a custom model, adding a new translation for a word that already exists overwrites the word's existing translation.

Because custom models are based on languages, not on specific voices, you do not need to create new custom models. But you might find it easier to work with a new models to avoid confusion between existing and new custom words that the models contain.

For more information about about working with custom models and entries for custom words, see the following topics:

-   [Creating and managing custom models](/docs/text-to-speech?topic=text-to-speech-customModels)
-   [Creating and managing custom entries](/docs/text-to-speech?topic=text-to-speech-customWords)
-   [Using a custom model for speech synthesis](/docs/text-to-speech?topic=text-to-speech-custom-using)
