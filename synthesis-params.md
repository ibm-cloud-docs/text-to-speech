---

copyright:
  years: 2022
lastupdated: "2022-07-26"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Modifying speech synthesis characteristics
{: #synthesis-params}

The {{site.data.keyword.texttospeechfull}} service includes a query parameter that you can use to modify the characteristics of speech synthesis for an entire request. The parameter modifies aspects of synthesis globally for all text of a request. It is available for both the HTTP and WebSocket interfaces.
{: shortdesc}

## Specifying how strings are spelled out
{: #params-spell-out-mode}

The service's default pronunciation of alphabetic, numeric, and alphanumeric strings varies by language, with each language having its own rules. For any language, the pronunciation also depends on the length and context of the string, as well its composition in terms of the positions and grouping of its characters

-   Alphabetic strings are pronounced as words if they are pronounceable in the language of the voice. Otherwise, the characters are spelled out individually. Whether a string is pronounced or spelled out can also depend on the case of the letters.
-   Numeric strings can be pronounced as cardinal numbers, ordinal numbers, dates, or in other ways, including as individual digits.
-   Alphanumeric strings that contain both letters and numbers can be pronounced in different ways depending on the characteristics of the string. For example, they might be pronounced as combinations of words, cardinal numbers, or digits. But as mentioned previously, the pronunciation depends largely on the string and its composition.

The best means of controlling how a specific string is pronounced is to use the `<say-as>` element of the Speech Synthesis Markup Language (SSML). The element allows you to specify exactly how a string is synthesized. You use the `interpret-as` attribute of the `<say-as>` element to indicate that a string of characters is to be pronounced as `letters`, `digits`, or in some other way. The available values differ by language.

If you use the `letters` or `digits` attributes, all letters and numbers of the string are pronounced individually. This is especially useful for spelling out the alphanumeric characters of a hexadecimal string or an identification or account number. For more information, see [The `say-as` element](/docs/text-to-speech?topic=text-to-speech-elements#say-as_element).

### Specifying the pace at which strings are spelled out
{: #params-spell-out-mode-rate}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud}} only**

The `spell_out_mode` parameter is beta functionality this is supported only for German voices.
{: beta}

By default, the service reads characters that it spells out at the same rate at which it reads text for the language being synthesized. For German voices, however, you can use the optional `spell_out_mode` query parameter to indicate how the service is to spell out individual characters: one, two, or three at a time. The parameter applies globally to control the pace at which the service reads all strings that it spells out from a request. Use the `spell_out_mode` parameter only for longer strings. The parameter has no effect on a string that contains fewer than three characters.

Table 1 provides examples of how the service pronounces the following text with different values for the `spell_out_mode` parameter:

```xml
Die Nummer ist <say-as interpret-as=‘digits’>AB7234987FFA</say-as>.
```
{: codeblock}

| Specification of the `spell_out_mode` parameter | Resulting audio  |
|-------------------------------------------------|:----------------:|
| `spell_out_mode=default`  \n The service reads the characters in succession, typically with no pause between them, at the rate at which it synthesizes speech for the request. You can also omit the parameter to get the default behavior. | ![spell_out_mode=default](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/spell-out-default.wav){: audio controls} |
| `spell_out_mode=singles`  \n The service reads the characters one at a time, with a brief pause between each character. | ![spell_out_mode=singles](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/spell-out-singles.wav){: audio controls} |
| `spell_out_mode=pairs`  \n The service reads the characters two at a time, with a brief pause between each pair. | ![spell_out_mode=pairs](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/spell-out-pairs.wav){: audio controls} |
| `spell_out_mode=triplets`  \n The service reads the characters three at a time, with a brief pause between each triplet. | ![spell_out_mode=triplets](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/spell-out-triplets.wav){: audio controls} |
{: caption="Table 1. Using the spell_out_mode parameter for German"}

Alphanumeric strings that mix letters and digits can yield different groupings of characters. If you do not use the `<say-as>` element, groups of letters and digits can be pronounced in ways that do not necessarily conform to the requested mode.
{: note}

### Spell-out mode examples
{: #params-spell-out-mode-example}

The following HTTP `POST /v1/synthesize` method uses the `spell_out_mode` query parameter with a value of `singles`. The example uses the German voice `de-DE_ErikaV3Voice`. The alphanumeric text to be synthesized is a hexadecimal string that is wrapped in a `<say-as>` element and interpreted as `digits`.

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output spell-out-mode.wav \
--data "{\"text\":\"Die Nummer ist <say-as interpret-as=‘digits’>AB7234987FFA</say-as>.\"}" \
"{url}/v1/synthesize?voice=de-DE_ErikaV3Voice&spell_out_mode=singles"
```
{: pre}

The following WebSocket example shows inclusion of the parameter with the same value on the request to establish a connection:

```javascript
var access_token = '{access_token}';
var wsURI = '{ws_url}/v1/synthesize'
  + '?access_token=' + access_token
  + '&voice=en-US_AllisonV3Voice'
  + '&spell_out_mode=singles';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
