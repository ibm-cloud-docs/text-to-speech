---

copyright:
  years: 2015, 2023
lastupdated: "2023-01-14"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Creating and managing custom entries
{: #customWords}

Once a custom model exists, the next step is to add custom entries in the form of word/translation pairs to define how specified words are to be pronounced during synthesis. The definitions override the service's default regular pronunciation rules. You can add and query translations for one or more words at a time, and you can delete individual words that you no longer need. Once you are familiar with the customization interface, manipulating multiple words at once can be more convenient than working on a word-by-word basis. You must use credentials for the instance of the service that owns a custom model to use any method that requires its customization ID.
{: shortdesc}

For more information about the rules and limits that apply to custom entries, see [Rules for creating custom entries](/docs/text-to-speech?topic=text-to-speech-rules).
{: note}

## Adding a single word to a custom model
{: #cuWordAdd}

To add a single word/translation pair to a custom model, use the `PUT /v1/customizations/{customization_id}/words/{word}` method. You specify the word to be added in the URL of the method. You provide the translation for the word as a JSON object with a single `translation` attribute. Adding a new translation for a word that already exists in a model overwrites the word's existing translation.

You can provide a translation by using the sounds-like or the phonetic method (or a combination of the two). For phonetic translations, you can use either the International Phonetic Alphabet (IPA) or the {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) format. The following examples use different approaches to add equivalent translations for the word `IEEE` to a custom model. The required `Content-Type` header identifies the type of the input as `application-json`.

-   **Sounds-like:** For this example, the sounds-like method is the simplest approach:

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X PUT -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"I triple E\"}" \
    "{url}/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X PUT \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"I triple E\"}" \
    "{url}/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **Phonetic IPA:** IPA requires use of the `<phoneme>` element with the `alphabet` attribute set to `ipa` and the `ph` attribute defined in IPA format:

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X PUT -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"<phoneme alphabet=\\\"ipa\\\" ph=\\\"aɪ.tɹˈɨpəl.ˈi\\\"></phoneme>\"}" \
    "{url}/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X PUT \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"<phoneme alphabet=\\\"ipa\\\" ph=\\\"aɪ.tɹˈɨpəl.ˈi\\\"></phoneme>\"}" \
    "{url}/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **Phonetic {{site.data.keyword.IBM_notm}} SPR:** SPR uses the `<phoneme>` element with the `alphabet` attribute set to `ibm` and the `ph` attribute defined in SPR format:

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X PUT -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}" \
    "{url}/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X PUT \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}" \
    "{url}/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

## Adding multiple words to a custom model
{: #cuWordsAdd}

To add one or more words to a custom model at one time, use the `POST /v1/customizations/{customization_id}/words` method. You specify the entries to be added to the custom model as a JSON array of word/translation pairs. The required `Content-Type` header identifies the type of the input as `application-json`.

The following example adds common sounds-like translations for the words `NCAA` and `iPhone` to a custom model:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}" \
"{url}/v1/customizations/{customization_id}/words"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}" \
"{url}/v1/customizations/{customization_id}/words"
```
{: pre}

The JSON content sent in the request body equates to the following:

```javascript
{
  "words": [
    {"word":"NCAA", "translation":"N C double A"},
    {"word":"iPhone", "translation":"I phone"}
  ]
}
```
{: codeblock}

As mentioned in [Updating a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsUpdate), you can also use the `POST /v1/customizations/{customization_id}` method to add words to a custom model. The following example uses this method to add the same two words as the previous example; it makes no changes to the model's metadata. With the exception of the URL, the two methods are identical.

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}" \
"{url}/v1/customizations/{customization_id}"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}" \
"{url}/v1/customizations/{customization_id}"
```
{: pre}

## Adding words to a Japanese custom model
{: #cuJapaneseAdd}

Additional considerations and an additional `part_of_speech` field apply when creating entries for words in a Japanese custom model; for more information, see [Working with Japanese entries](/docs/text-to-speech?topic=text-to-speech-rules#jaNotes). Specify a part of speech for a Japanese custom entry as follows:

-   For the `PUT /v1/customizations/{customization_id}/words/{word}` method, pass a JSON object of the following form:

    ```javascript
    {
      "translation": "value",
      "part_of_speech": "value"
    }
    ```
    {: codeblock}

-   For the `POST /v1/customizations/{customization_id}/words` and `POST customizations/{customization_id}` methods, pass a JSON object like the following:

    ```javascript
    {
      "words": [
        {
          "word": "value",
          "translation": "value",
          "part_of_speech": "value"
        }
        . . .
      ]
    }
    ```
    {: codeblock}

The following examples of the `PUT /v1/customizations/{customization_id}/words/{word}` method translate the URL-encoded, double-byte string for `NY` to the noun (`Mesi`) `ニューヨーク` (`New York` in English). If this custom translation is not defined, the string is read as `enu wai`.

-   **Sounds-like:**

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X PUT -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"ニューヨーク\", \"part_of_speech\":\"Mesi\"}" \
    "{url}/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X PUT \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"ニューヨーク\", \"part_of_speech\":\"Mesi\"}" \
    "{url}/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"
    ```
    {: pre}

-   **Phonetic IPA:**

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X PUT -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"<phoneme alphabet=\\\"ipa\\\" ph=\\\"ɲɯːjoːkɯ\\\"></phoneme>\", \"part_of_speech\":\"Mesi\"}" \
    "{url}/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X PUT \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"<phoneme alphabet=\\\"ipa\\\" ph=\\\"ɲɯːjoːkɯ\\\"></phoneme>\", \"part_of_speech\":\"Mesi\"}" \
    "{url}/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"
    ```
    {: pre}

-   **Phonetic {{site.data.keyword.IBM_notm}} SPR:**

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X PUT -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"></phoneme>\", \"part_of_speech\":\"Mesi\"}" \
    "{url}/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X PUT \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"></phoneme>\", \"part_of_speech\":\"Mesi\"}" \
    "{url}/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"
    ```
    {: pre}

## Querying a single word from a custom model
{: #cuWordQueryModel}

To query the translation of a single word from a custom model, use the `GET /v1/customizations/{customization_id}/words/{word}` method. You specify the word in the URL of the method. The translation is returned as it is defined in the custom model (sounds-like or phonetic).

The following example queries a custom model for the translation of the word `IEEE`:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

If the word has the sounds-like translation in the model, the example returns the following JSON output:

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

## Querying all words from a custom model
{: #cuWordsQueryModel}

To see the translations for all of the words defined in a custom model, use the `GET /v1/customizations/{customization_id}/words` method. The following example uses the method to list the entries from a custom model that contains sounds-like translations for three words:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/customizations/{customization_id}/words"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/customizations/{customization_id}/words"
```
{: pre}

The method returns a JSON array with the following data. For Japanese custom models, the output includes the part of speech for individual words.

```javascript
{
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

As described in [Querying a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery), you can also use the `GET /v1/customizations/{customization_id}` method to see both the metadata and the words for a custom model:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/customizations/{customization_id}"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/customizations/{customization_id}"
```
{: pre}

The method returns JSON output of the following form. Because this and the previous example specify the same custom model, the array of words in their output is identical.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T19:15:17.926Z",
  "name": "Test",
  "language": "en-US",
  "description": "Customization test",
  "last_modified": "2016-07-15T19:46:01.387Z",
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

## Querying a word from a language
{: #cuWordsQueryLanguage}

To query the pronunciation of a word, use the `GET /v1/pronunciation` method. Specify a voice to get the pronunciation in the language of that voice. By default, the method returns the pronunciation based on the service's regular pronunciation rules, but you can also request the pronunciation for a specified custom model. The method includes four query parameters that let you specify the information that is to be returned:

-   The required `text` parameter specifies the word whose pronunciation is to be returned.
-   The optional `voice` parameter lets you specify the language of the pronunciation. You specify one of the voices (for example, `en-US_LisaV3Voice`) to indicate the desired language; all voices for the same language (for example, `en-US`) return the same pronunciation. By default, the pronunciation is returned for the language of the default voice. For more information, see [Using the default voice](/docs/text-to-speech?topic=text-to-speech-voices-use#specify-voice-default).
-   The optional `format` parameter lets you specify the phonetic format of the pronunciation, either `ipa` or `ibm`. By default, the pronunciation is returned in IPA format.
-   The optional `customization_id` parameter lets you specify a custom model for which the pronunciation is to be returned. If the word is not defined in the specified custom model, the service returns the default pronunciation for the model's language. Omit the parameter to see the translation for the specified voice with no customization. Do not specify both a voice and a custom model.

This method is useful because it allows you to query a word from any language and, because it does not require a customization ID, places no restrictions on the words that you can see. It can prove especially helpful when composing a phonetic translation for a new word; you can use it to obtain the pronunciation for an existing word and then use that as the basis of your new translation, which is far more convenient than creating a translation from scratch.

The following example obtains the pronunciation for the word `IEEE` in the default IPA format:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/pronunciation?text=IEEE"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/pronunciation?text=IEEE"
```
{: pre}

The response shows the IPA symbols for the pronunciation:

```javascript
{
  "pronunciation": ".ˈaɪ .ˈi .ˈi .ˈi"
}
```
{: codeblock}

The following example enters a sounds-like translation for the word `IEEE` and obtains the phonetic equivalent in {{site.data.keyword.IBM_notm}} SPR format. Obtaining the phonetic pronunciation for a sounds-like translation is an especially interesting approach to composing a phonetic translation. The spaces of the word are URL-encoded in the example.

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/pronunciation?text=i%20triple%20e&format=ibm"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/pronunciation?text=i%20triple%20e&format=ibm"
```
{: pre}

The response shows the SPR symbols for the pronunciation:

```javascript
{
  "pronunciation": "1Y.tr1Ipxl.1i"
}
```
{: codeblock}

## Deleting a word from a custom model
{: #cuWordDelete}

To delete a word from a custom model, use the `DELETE /v1/customizations/{customization_id}/words/{word}` method. You specify the word to be deleted in the URL of the method. You can delete individual words only; you cannot delete multiple words with a single method.

The following example deletes the word `IEEE` from the specified custom model:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X DELETE -u "apikey:{apikey}" \
"{url}/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X DELETE \
--header "Authorization: Bearer {token}" \
"{url}/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}
