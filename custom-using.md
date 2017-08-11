---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-09"

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

# Using customization
{: #customUsing}

The {{site.data.keyword.texttospeechshort}} service provides a robust interface for managing and using custom voice models and their entries. The following sections logically group the methods of the interface:
{: shortdesc}

-   [Managing custom voice models](#cuModels) explains how to create, update, and delete a custom voice model and how to list one or all of your custom models.
-   [Managing words and translations](#cuWords) describes how to add, delete, and query words and their translations in a custom model.
-   [Using a custom model](#cuSynthesize) shows you how to use a custom model to synthesize text with the service.

For detailed information about the methods of the {{site.data.keyword.texttospeechshort}} service, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/){: new_window}.

> **Note:** The customization interface is currently a beta release.

## Usage notes
{: #customGuidelines}

Keep the following in mind when working with the customization interface.

### Ownership of custom voice models
{: #customOwner}

A custom voice model is owned by the instance of the {{site.data.keyword.texttospeechshort}} service whose credentials are used to create it. You must use service credentials created for that service instance with methods of the customization interface to work with the custom model in any way.

All service credentials obtained for the same instance of the {{site.data.keyword.texttospeechshort}} service share access to all custom models created for that service instance. If you want to restrict access to a custom model, create a separate instance of the service and use only the credentials for that service instance to create and work with the model. Credentials for other service instances cannot affect the custom model.

An advantage of sharing ownership across service credentials is that you can cancel a set of credentials, for example, if they become compromised. You can then create new credentials for the same service instance and still maintain ownership of and access to custom models created with the original credentials.

### Request logging and data privacy
{: #customLogging}

How the service handles request logging for calls to the customization interface depends on the request:

-   The service *does not* log data (words and translations) that are used to build custom voice models. You do not need to set the `X-Watson-Learning-Opt-Out` request header when using the customization interface to manage the words and translations in a custom model. Your training data is never used to improve the service's base models.
-   The service *does* log data when a custom model is used with a synthesize request. You must set the `X-Watson-Learning-Opt-Out` request header to prevent logging for synthesize requests.

For more information about request logging, see [Controlling request logging for {{site.data.keyword.watson}} services ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/doc/common/getting-started-logging.html){: new_window}.

### Using the examples
{: #customCurl}

The examples that follow use cURL to demonstrate the methods of the customization interface. To run the examples, create an instance of the {{site.data.keyword.texttospeechshort}} service in {{site.data.keyword.Bluemix_notm}}. Then replace `{username}:{password}` in each example with the values of your *username* and *password* from your HTTP basic authentication credentials for the service instance. Concatenate the two values with an embedded colon to create a single string of the form *username*:*password*.

Note that you must use your service credentials, *not* your {{site.data.keyword.Bluemix_notm}} ID and password. For more information, see [Service credentials for {{site.data.keyword.watson}} services ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/doc/common/getting-started-credentials.html){: new_window}.

## Managing custom voice models
{: #cuModels}

The first step in working with any custom model is to create it. Once it exists, you can manage the model by querying or updating its metadata and entries, and by deleting it if it is no longer needed.

-   [Creating a custom model](#cuModelsCreate) with the `POST customizations` method
-   [Querying a single custom model](#cuModelsQuery) with the `GET customizations/{customization_id}` method
-   [Querying all custom models](#cuModelsQueryAll) with the `GET customizations` method
-   [Updating a custom model](#cuModelsUpdate) with the `POST customizations/{customization_id}` method
-   [Deleting a custom model](#cuModelsDelete) with the `DELETE customizations/{customization_id}` method

### Creating a custom model
{: #cuModelsCreate}

To create a new custom model, you use the `POST customizations` method. A new model is always empty when you first create it; you must use other methods to populate it with word/translation pairs.

The following example cURL command creates a new custom model named `cURL Test`:

```bash
curl -X POST -u {username}:{password}
--header "Content-Type:application/json"
--data "{\"name\":\"cURL Test\", \"language\":\"en-US\", \"description\":\"Customization test via cURL\"}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

The arguments to the example command specify the following values:

-   `-u` provides your service credentials for the {{site.data.keyword.texttospeechshort}} service.
-   `-X POST` specifies that the command is to use the HTTP `POST` request method.
-   `--header` specifies an HTTP header parameter for the call to the service. For this request, the `Content-Type` header identifies the type of the input from the request body as JSON.
-   `--data` contains information needed for creating the custom model. This information is passed in JSON format as the body of the request. It consists of key/attribute pairs of values that define the new custom model.
-   The final argument tells the command the URL to contact, in this case the `customizations` method of the {{site.data.keyword.texttospeechshort}} service.

You can pass the following attributes in the JSON sent via the body of the request.

<table>
  <caption>Table 1. Parameters of the <code>customizations</code>
    method</caption>
  <tr>
    <th style="text-align:left; width:18%">Parameter</th>
    <th style="text-align:center; width:12%">Data type</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>Required</em></td>
    <td style="text-align:center">String</td>
    <td>
      A user-defined name for the new custom model. The name is used
      to label the model for easy identification.
    </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>Optional</em></td>
    <td style="text-align:center">String</td>
    <td>
      The language of the custom model. The default is <code>en-US</code>
      for US English, but you can specify any of the supported languages.
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>Optional</em></td>
    <td style="text-align:center">String</td>
    <td>
      A description of the new model. Although it is optional, a
      description is highly recommended.
    </td>
  </tr>
</table>

The method returns a JSON object that contains just a globally unique identifier (GUID) for the new model. The GUID is used as the `customization_id` parameter in calls to access the model, such as those for querying, modifying, and using the model and its words. In the example, the GUID is overwritten with an alphabetic character string.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

The new custom model is owned by the user whose service credentials are used to create it. For more information, see [Ownership of custom voice models](#customOwner).

### Querying a custom model
{: #cuModelsQuery}

To query information about an existing custom model, you use the `GET customizations/{customization_id}` method. This is the most direct means of seeing all of the information about a model, both its metadata and the word/translation pairs that it contains.

```bash
curl -X GET -u {username}:{password}
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

The method returns its results as a JSON object of the following form. In the example that follows, GUIDs are overwritten with alphabetic character strings; this is done for all of the examples in this section.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T18:12:31.743Z",
  "name": "cURL Test",
  "language": "en-US",
  "description": "Customization test via cURL",
  "last_modified": "2016-07-15T18:12:31.743Z",
  "words": []
}
```
{: codeblock}

In addition to the information entered when the model was created, the output includes the service credentials for the model's owner (the person who created the model), the model's language, and the times at which the model was created and last modified. Because the model has not been modified since its creation, the two times in the example are the same.

The output also includes an array of the words in the model and their translations. Again, because the model has yet to be updated, the array in the example is empty.

### Querying all custom models
{: #cuModelsQueryAll}

To see information about all of the custom models that you own, you use the `GET customizations` method:

```bash
curl -X GET -u {username}:{password}
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

The method returns a JSON array that includes an object for each custom model owned by the requester. The owner's service credentials are shown in the `owner` field. The example shows output for a user who owns two custom models.

```javascript
{
  "customizations": [
    {
      "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T19:15:17.926Z",
      "name": "cURL Test",
      "language": "en-US",
      "description": "Customization test via cURL",
      "last_modified": "2016-07-15T19:15:17.926Z"
    },
    {
      "customization_id": "63f5807f-a4f2-5766-914e-7abb1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T18:12:31.743Z",
      "name": "cURL Test Two",
      "language": "en-US",
      "description": "Second customization test via cURL",
      "last_modified": "2016-07-15T18:23:50.912Z"
    }
  ]
}
```
{: codeblock}

The `created` and `last_modified` times for the first model are the same because it has yet to be updated. The times for the second model are different, indicating that it has been changed since its initial creation.

### Updating a custom model
{: #cuModelsUpdate}

To update information about a custom model, you use the `POST customizations/{customization_id}` method. You specify the updates as a JSON object. In addition to modifying its name and description, you can also use this method to add or update word/translation pairs in the model. You cannot change a model's language once it is created.

The following example updates the name and description of a custom model. An empty JSON array is sent with the `words` parameter to indicate that the model's entries are to remain unchanged.

```bash
curl -X POST -u {username}:{password}
--header "Content-Type:application/json"
--data "{\"name\":\"cURL Test Update\", \"description\":\"Customization test update via cURL\", \"words\":[]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

For information about updating the words in a model, see [Adding words to a custom model](#cuWordsAdd).

### Deleting a custom model
{: #cuModelsDelete}

To discard a custom model that you no longer need, you use the `DELETE customizations/{customization_id}` method. Use this method only if you are sure that you no longer need the model, since deletion is permanent.

```bash
curl -X DELETE -u {username}:{password}
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

## Managing words and translations
{: #cuWords}

Once a custom model exists, the next step is to add contents in the form of word/translation pairs to define how specified words are to be pronounced during synthesis. The definitions override the service's default regular pronunciation rules. You can add and query translations for one or more words at a time, and you can delete individual words that you no longer need. Once you are familiar with the customization interface, manipulating multiple words at once can be more convenient than working on a word-by-word basis.

-   [Adding words to a custom model](#cuWordsAdd) with the `PUT customizations/{customization_id}/words/{word}`, `POST customizations/{customization_id}/words`, and `POST customizations/{customization_id}` methods
-   [Querying words from a custom model](#cuWordsQueryModel) with the `GET customizations/{customization_id}/words/{word}`, `GET customizations/{customization_id}/words`, and `GET customizations/{customization_id}` methods
-   [Querying words from a language](#cuWordsQueryLanguage) with the `GET pronunciation` method
-   [Deleting words from a custom model](#cuWordsDelete) with the `DELETE customizations/{customization_id}/words/{word}` method

### Adding words to a custom model
{: #cuWordsAdd}

To add a single word/translation pair to a custom model, you use the `PUT customizations/{customization_id}/words/{word}` method. You specify the word to be added in the URL of the method. You provide the translation for the word as a JSON object with a single `translation` attribute. Adding a new translation for a word that already exists in a model overwrites the word's existing translation.

As described in [Specifying word translations](/docs/services/text-to-speech/custom-intro.html#ciTranslation), you can provide a translation by using either the sounds-like or the phonetic method (or even a combination of the two). And for phonetic translations, you can use either the International Phonetic Alphabet (IPA) or the {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) format.

The following examples add the word `IEEE` to a custom model with each of the three possible formats. The translations specify a common way of referring to the organization.

-   **Sounds-like:** For this simple example, the sounds-like method is the simplest approach:

    ```bash
    curl -X PUT -u {username}:{password}
    --header "Content-Type:application/json"
    --data "{\"translation\":\"I triple E\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **Phonetic IPA:** IPA requires use of the `<phoneme>` tag with the `alphabet` attribute set to `ipa` and the `ph` attribute defined in IPA format:

    <pre><code class="language-bash">  curl -X PUT -u {username}:{password}
    --header "Content-Type:application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#712;a&#618;.t&#633;&#712;&#616;p&#601;l.&#712;i\\\"&gt;&lt;/phoneme&gt;\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"</code></pre>

-   **Phonetic {{site.data.keyword.IBM_notm}} SPR:** SPR uses the `<phoneme>` tag with the `alphabet` attribute set to `ibm` and the `ph` attribute defined in SPR format:

    ```bash
    curl -X PUT -u {username}:{password}
    --header "Content-Type:application/json"
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

You can also add one or more words to a custom model at one time by using the `POST customizations/{customization_id}/words` method. You specify the entries to be added to the custom model as a JSON array of word/translation pairs. The following example adds common sounds-like translations for the words `NCAA` and `iPhone` to a custom model:

```bash
curl -X POST -u {username}:{password}
--header "Content-Type:application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
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

As mentioned in [Updating a custom model](#cuModelsUpdate), you can also use the `POST customizations/{customization_id}` method to add words to a custom model. The following example uses that method to add the same two words as the previous example; it makes no changes to the model's metadata. With the exception of the URL, the two methods are identical.

```bash
curl -X POST -u {username}:{password}
--header "Content-Type:application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

> **Note:** Additional considerations and an additional `part_of_speech` field apply when creating entries for words in Japanese; see [Working with Japanese entries](#jaNotes).

### Querying words from a custom model
{: #cuWordsQueryModel}

To query the translation of a single word from a custom model, you use the `GET customizations/{customization_id}/words/{word}` method. You specify the word to be shown in the URL of the method. The translation is returned as it is defined in the custom model (sounds-like or phonetic). Because the URL for the method includes the `customization_id`, you must be the owner of the model to use the method.

The following example queries a custom model for the translation of the word `IEEE`:

```bash
curl -X GET -u {username}:{password}
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

Assuming the word has the sounds-like translation in the model, the example returns the following JSON output:

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

To see all of the words defined in a custom model, you use the `GET customizations/{customization_id}/words` method. The following example uses the method to see the entries from a custom model that contains sounds-like translations for three words:

```bash
curl -X GET -u {username}:{password}
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
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

As described in [Querying a custom model](#cuModelsQuery), you can also use the `GET customizations/{customization_id}` method to see both the metadata and the words for a custom model:

```bash
curl -X GET -u {username}:{password}
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

The method returns JSON output of the following form. Because this and the previous example are run against the same custom model, the array of words in their output is identical.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T19:15:17.926Z",
  "name": "cURL Test",
  "language": "en-US",
  "description": "Customization test via cURL",
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

### Querying words from a language
{: #cuWordsQueryLanguage}

To query the pronunciation of a word, use the `GET pronunciation` method. Specify a voice to get the pronunciation in the language of that voice. By default, the method returns the pronunciation based on the service's regular pronunciation rules, but you can also request the pronunciation for a specified custom voice model. The method includes four query parameters that let you specify the information that is to be returned:

-   The required `text` parameter specifies the word whose pronunciation is to be returned.
-   The optional `voice` parameter lets you specify the language of the pronunciation. You specify one of the voice models (for example, `en-US_LisaVoice`) to indicate the desired language; all voices for the same language (for example, `en-US`) return the same pronunciation. By default, the pronunciation is returned for US English.
-   The optional `format` parameter lets you specify the phonetic format of the pronunciation, either `ipa` or `ibm`. By default, the pronunciation is returned in IPA format.
-   The optional `customization_id` parameter lets you specify a custom voice model for which the pronunciation is to be returned. If the word is not defined in the specified voice model, the service returns the default pronunciation for the model's language. Omit the parameter to see the translation for the specified voice with no customization. Do not specify both a voice and a custom voice model.

This method is useful because it allows you to query a word from any language and, because it does not require a customization ID, places no restrictions on the words that you can see. It can prove especially helpful when composing a phonetic translation for a new word; you can use it to obtain the pronunciation for an existing word and then use that as the basis of your new translation, which is far more convenient than creating a translation from scratch.

The following example obtains the pronunciation for the word `IEEE` in the default IPA format.

```bash
curl -X GET -u {username}:{password}
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=IEEE"
```
{: pre}

<pre><code data-copy="false" class="language-javascript">{
  "pronunciation": ".&#712;a&#618; .&#712;i .&#712;i .&#712;i"
}</code></pre>

The following example enters a sounds-like translation for the word `IEEE` and obtains the phonetic equivalent in {{site.data.keyword.IBM_notm}} SPR format. Obtaining the phonetic pronunciation for a sounds-like translation is an especially interesting approach to composing a phonetic translation. The spaces of the word are URL-encoded in the example command.

```bash
curl -X GET -u {username}:{password}
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=i%20triple%20e&format=ibm"
```
{: pre}

```javascript
{
  "pronunciation": "1Y.tr1Ipxl.1i"
}
```
{: codeblock}

### Deleting words from a custom model
{: #cuWordsDelete}

To delete a word from a custom model, you use the `DELETE customizations/{customization_id}/words/{word}` method. You specify the word to be deleted in the URL of the method. You can delete individual words only; you cannot delete multiple words with a single method.

The following example deletes the word `IEEE` from the specified custom model:

```bash
curl -X DELETE -u {username}:{password}
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

## Using a custom model
{: #cuSynthesize}

Once you create a custom model and populate it with word/translation pairs, you use it by passing its GUID with the `customization_id` query parameter of the HTTP `GET` or `POST synthesize` method or the WebSocket `synthesize` method. As with all methods that accept a customization ID, the service credentials of a model's owner must be used to call a `synthesize` method that uses a custom model.

The following example uses the HTTP `GET` version of the `synthesize` method to generate a Waveform Audio File Format (WAV) file named `ieee-orig.wav` with the default pronunciation for `IEEE` that is based on the service's regular pronunciation rules:

```bash
curl -X GET -u {username}:{password}
--header "Accept: audio/wav"
--output ieee-orig.wav
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE"
```
{: pre}

The following example uses the same method but instead uses a custom model to generate a WAV audio file named `ieee-new.wav` with a pronunciation for `IEEE` that is based on the indicated custom model:

```bash
curl -X GET -u {username}:{password}
--header "Accept: audio/wav"
--output ieee-new.wav
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE&customization_id={customization_id}"
```
{: pre}

## Working with Japanese entries
{: #jaNotes}

For Japanese, the following additional rules apply to the creation of entries for words in a custom voice model:

-   A sounds-like translation can contain only Katakana characters. Kanji and Hiragana characters are not allowed.
-   When you create a translation (sounds-like or phonetic) for a word, you can also specify an optional `part_of_speech` field to identify the word's part of speech. The service uses the value to produce the correct intonation for the word. You can create only a single entry, with or without a single part of speech, for any word; you cannot create multiple entries with different parts of speech (for instance, noun and verb) for the same word. Adding a new translation for a word that already exists in a model overwrites the word's existing translation, including its part of speech.

    <table style="width:65%">
      <caption>Table 2. Japanese parts of speech</caption>
      <tr>
        <th style="text-align:center"><code>part_of_speech</code><br/>
          argument</th>
        <th style="text-align:center">Japanese<br/>meaning</th>
        <th style="text-align:center">English<br/>meaning</th>
      </tr>
      <tr>
        <td style="text-align:center"><code>Josi</code></td>
        <td style="text-align:center"><em>Joshi</em></td>
        <td style="text-align:center">participle</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Mesi</code></td>
        <td style="text-align:center"><em>Meishi</em></td>
        <td style="text-align:center">noun</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Kigo</code></td>
        <td style="text-align:center"><em>Kigou</em></td>
        <td style="text-align:center">symbol</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Gobi</code></td>
        <td style="text-align:center"><em>Gobi</em></td>
        <td style="text-align:center">inflection</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Dosi</code></td>
        <td style="text-align:center"><em>Doushi</em></td>
        <td style="text-align:center">verb</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Jodo</code></td>
        <td style="text-align:center"><em>Jodoushi</em></td>
        <td style="text-align:center">auxiliary verb</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Koyu</code></td>
        <td style="text-align:center"><em>Koyuumeishi</em></td>
        <td style="text-align:center">proper noun</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Stbi</code></td>
        <td style="text-align:center"><em>Setsubiji</em></td>
        <td style="text-align:center">suffix</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Suji</code></td>
        <td style="text-align:center"><em>Suuji</em></td>
        <td style="text-align:center">numeral</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Kedo</code></td>
        <td style="text-align:center"><em>Keiyodoushi</em></td>
        <td style="text-align:center">adjective verb</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Fuku</code></td>
        <td style="text-align:center"><em>Fukishi</em></td>
        <td style="text-align:center">adverb</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Keyo</code></td>
        <td style="text-align:center"><em>Keiyoshi</em></td>
        <td style="text-align:center">adjective verb</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Stto</code></td>
        <td style="text-align:center"><em>Settoji</em></td>
        <td style="text-align:center">prefix</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Reta</code></td>
        <td style="text-align:center"><em>Rentaishi</em></td>
        <td style="text-align:center">determiner</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Stzo</code></td>
        <td style="text-align:center"><em>Setsuzokushi</em></td>
        <td style="text-align:center">conjunction</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Kato</code></td>
        <td style="text-align:center"><em>Kantoushi</em></td>
        <td style="text-align:center">interjection</td>
      </tr>
      <tr>
        <td style="text-align:center"><code>Hoka</code></td>
        <td style="text-align:center"><em>Hoka</em></td>
        <td style="text-align:center">other</td>
      </tr>
    </table>

-   The service applies the longest matching word from the word/translation pairs that are defined for a custom voice model. For example, consider the following three entries for a custom model:

    <pre><code data-copy="false" class="language-javascript">{
      "words": [
        {
          "word": "&#65326;&#65337;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65326;&#65337;&#65315;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65337;&#65315;",
          "translation": "&#12520;&#12467;&#12495;&#12510;&#12481;&#12517;&#12540;&#12459;&#12460;&#12452;",
          "part_of_speech": "Mesi"
        }
      ]
    }</code></pre>

    With these entries, assume the service receives the following input text: <code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>. In this case, the service matches the word <code>&#65326;&#65337;&#65315;</code> because <code>&#65326;&#65337;&#65315;</code> is longer than <code>&#65326;&#65337;</code> and because <code>&#65326;&#65337;&#65315;</code> matches before <code>&#65337;&#65315;</code>.

<!--
Words are NY, NYC, and YC, in that order.
-->

<!--
Preserve for when English adopts the Japanese longest-match feature.

```javascript
{
  "words": [
    {
      "word": "NY",
      "translation": "New York",
      "part_of_speech": "Mesi"
    },
    {
      "word": "NYC",
      "translation": "New York City",
      "part_of_speech": "Mesi"
    }
  ]
}
```
{: codeblock}

-->

For the `PUT customizations/{customization_id}/words/{word}` method, you pass a JSON object of the following form:

```javascript
{
  "translation": "value",
  "part_of_speech": "value"
}
```
{: codeblock}

For the `POST customizations/{customization_id}/words` and `POST customizations/{customization_id}` methods, you pass a JSON object like the following:

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

The following examples of the `PUT customizations/{customization_id}/words/{word}` method translate the URL-encoded, double-byte string for `NY` to the noun <code>&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;</code> (`New York` in English). If this custom translation is not defined, the string is read as `enu wai`.

-   **Sounds-like:**

    <pre><code class="language-bash">curl -X PUT -u {username}:{password}
    --header "Content-Type:application/json"
    --data "{\"translation\":\"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **Phonetic IPA:**

    <pre><code class="language-bash">curl -X PUT -u {username}:{password}
    --header "Content-Type:application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#626;&#623;&#720;&#106;&#111;&#720;&#107;&#623;\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **Phonetic {{site.data.keyword.IBM_notm}} SPR:**

    ```bash
    curl -X PUT -u {username}:{password}
    --header "Content-Type:application/json"
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"></phoneme>\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"
    ```
    {: pre}
