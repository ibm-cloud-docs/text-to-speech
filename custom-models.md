---

copyright:
  years: 2015, 2020
lastupdated: "2020-07-20"

subcollection: text-to-speech

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Creating and managing custom voice models
{: #customModels}

The first step in working with any custom model is to create it. Once it exists, you can manage the model by querying or updating its metadata and entries, and by deleting it if it is no longer needed. Before getting started, review the following general usage information about custom models.
{: shortdesc}

## Usage notes
{: #customGuidelines}

Consider the following guidelines when working with the customization interface.

### Ownership of custom voice models
{: #customOwner}

A custom voice model is owned by the instance of the {{site.data.keyword.texttospeechshort}} service whose credentials are used to create it. You must use credentials for that service instance with methods of the customization interface to work with the custom model in any way.

All credentials obtained for the same instance of the {{site.data.keyword.texttospeechshort}} service share access to all custom models created for that service instance. To restrict access to a custom model, create a separate instance of the service and use only the credentials for that service instance to create and work with the model. Credentials for other service instances cannot affect the custom model.

An advantage of sharing ownership across credentials is that you can cancel a set of credentials, for example, if they become compromised. You can then create new credentials for the same service instance and still maintain ownership of and access to custom models created with the original credentials.

### Request logging and data privacy
{: #customLogging}

How the service handles request logging for calls to the customization interface depends on the request:

-   The service *does not* log data (words and translations) that are used to build custom voice models. You do not need to set the `X-Watson-Learning-Opt-Out` request header when using the customization interface to manage the words and translations in a custom model. Your training data is never used to improve the service's base models.
-   The service *does* log data when a custom model is used with a synthesize request. You must set the `X-Watson-Learning-Opt-Out` request header to `true` to prevent logging for synthesize requests.

For more information, see [Controlling request logging for {{site.data.keyword.watson}} services](/docs/watson?topic=watson-gs-logging-overview).

### Information security
{: #customSecurity}

The service allows you to associate a customer ID with data that is added or updated for custom voice models. You can associate a customer ID with custom words by passing the `X-Watson-Metadata` header with the following methods. If necessary, you can then delete the data associated with the customer ID by using the `DELETE /v1/user_data` method.

-   `POST /v1/customizations/{customization_id}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word}`

In addition, if you delete an instance of the {{site.data.keyword.texttospeechshort}} service from the {{site.data.keyword.cloud_notm}} console, all data associated with that service instance is automatically deleted. This includes all custom voice models and word/translation pairs. This data is purged automatically and regardless of whether a customer ID is associated with the data.

For more information, see [Information security](/docs/text-to-speech?topic=text-to-speech-information-security).

## Creating a custom model
{: #cuModelsCreate}

To create a new custom model, use the `POST /v1/customizations` method. A new model is always empty when you first create it. You must use other methods to populate it with word/translation pairs. The new custom model is owned by the service instance whose credentials are used to create it. For more information, see [Ownership of custom voice models](#customOwner).

You pass the following attributes as a JSON object with the body of the request.

<table>
  <caption>Table 1. Parameters of the <code>POST /v1/customizations</code>
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
      to label the model for easy identification. The name must be unique
      among all custom models that you own.
    </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>Optional</em></td>
    <td style="text-align:center">String</td>
    <td>
      An identifier for the language of the custom model. The default
      is <code>en-US</code> for US English. The custom model can be used
      with any voice, standard or neural, that is available in the specified
      language. For example, a custom model that is created for the `en-US`
      language can be used with any US English voice. It cannot, however,
      be used with an `en-GB` voice.
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

The following example `curl` command creates a new custom model named `curl Test`. The `Content-Type` header identifies the type of the input as `application/json`.

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--data "{\"name\":\"curl Test\", \"language\":\"en-US\", \"description\":\"Customization test via curl\"}" \
"{url}/v1/customizations"
```
{: pre}

The method returns a JSON object that contains a globally unique identifier (GUID) for the new model. The GUID is used as the `customization_id` parameter in calls to access the model, such as those for querying, modifying, and using the model and its words.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

## Querying a custom model
{: #cuModelsQuery}

To query information about an existing custom model, use the `GET /v1/customizations/{customization_id}` method. This is the most direct means of seeing all of the information about a model, both its metadata and the word/translation pairs that it contains.

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/customizations/{customization_id}"
```
{: pre}

The method returns its results as a JSON object of the following form:

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T18:12:31.743Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T18:12:31.743Z",
  "words": []
}
```
{: codeblock}

In addition to the information entered when the model was created, the output includes the credentials of the model's owner, the model's language, and the times at which the model was created and last modified. Because the model has not been modified since its creation, the two times in the example are the same.

The output also includes a `words` array that lists the model's custom entries. Because the model has yet to be updated, the array in the example is empty.

## Querying all custom models
{: #cuModelsQueryAll}

To see information about all of the custom models that you own, use the `GET /v1/customizations` method:

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/customizations"
```
{: pre}

The method returns a JSON array that includes an object for each custom model owned by the requester. The owner's credentials are shown in the `owner` field.

```javascript
{
  "customizations": [
    {
      "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T19:15:17.926Z",
      "name": "curl Test",
      "language": "en-US",
      "description": "Customization test via curl",
      "last_modified": "2016-07-15T19:15:17.926Z"
    },
    {
      "customization_id": "63f5807f-a4f2-5766-914e-7abb1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T18:12:31.743Z",
      "name": "curl Test Two",
      "language": "en-US",
      "description": "Second customization test via curl",
      "last_modified": "2016-07-15T18:23:50.912Z"
    }
  ]
}
```
{: codeblock}

The `created` and `last_modified` times for the first model are the same because it has yet to be updated. The times for the second model are different, indicating that it has been changed since its initial creation. The information does not include the custom entries defined for the models.

## Updating a custom model
{: #cuModelsUpdate}

To update information about a custom model, use the `POST /v1/customizations/{customization_id}` method. You specify the updates as a JSON object. In addition to modifying its name and description, you can also use this method to add or update word/translation pairs in the model. You cannot change a model's language once it is created.

The following example updates the name and description of a custom model. An empty JSON array is sent with the `words` parameter to indicate that the model's entries are to remain unchanged.

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--data "{\"name\":\"curl Test Update\", \"description\":\"Customization test update via curl\", \"words\":[]}" \
"{url}/v1/customizations/{customization_id}"
```
{: pre}

For information about updating the words in a model, see [Adding multiple words to a custom model](/docs/text-to-speech?topic=text-to-speech-customWords#cuWordsAdd).

## Deleting a custom model
{: #cuModelsDelete}

To discard a custom model that you no longer need, use the `DELETE /v1/customizations/{customization_id}` method. Use this method only if you are sure that you no longer need the model, since deletion is permanent.

```bash
curl -X DELETE -u "apikey:{apikey}" \
"{url}/v1/customizations/{customization_id}"
```
{: pre}
