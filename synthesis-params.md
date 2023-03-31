---

copyright:
  years: 2022, 2023
lastupdated: "2023-03-29"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Modifying speech synthesis characteristics
{: #synthesis-params}

The {{site.data.keyword.texttospeechfull}} service includes query parameters that you can use to globally modify the characteristics of speech synthesis for an entire request: `rate_percentage`, `pitch_percentage`, and `spell_out_mode`. These parameters are available for both the HTTP and WebSocket interfaces.
{: shortdesc}

Each of these parameters interacts with elements of the Speech Synthesis Markup Language (SSML). The descriptions of the parameters include information about how they interact with related SSML elements and attributes.

## Modifying the speaking rate
{: #params-rate-percentage}

The `rate_percentage` parameter is beta functionality.
{: beta}

The speaking rate is the speed at which the service speaks the text that it synthesizes into speech. A higher rate causes the text to be spoken more quickly; a lower rate causes the text to be spoken more slowly.

You can use the optional `rate_percentage` query parameter to modify the rate of the synthesized speech for a voice. Each voice has a default speaking rate that is optimized to represent a normal rate of speech. The parameter accepts an integer that represents the percentage change from the voice's default:

-   Specify a signed negative integer to reduce the speaking rate by that percentage. For example, `-10` reduces the rate by ten percent.
-   Specify an unsigned or signed positive integer to increase the speaking rate by that percentage. For example, `10` and `+10` increase the rate by ten percent.
-   Specify `0` or omit the parameter to get the default speaking rate for the voice.

The best way to determine how the parameter affects the rate of a given voice is to experiment with different values. Increase or decrease the rate incrementally, by five or ten percent, before trying more significant changes. When decreasing the rate, values less than `-50` can begin to yield inadequate pronunciation. When increasing the rate, values greater than `100` might produce results that are not discernibly different from `100`.

Table 1 provides examples of how the service changes the speaking rate with different values for the `rate_percentage` parameter. The examples use the `en-US_AllisonV3Voice`.

| Specification of the `rate_percentage` parameter | Audio sample |
|-------------------------------------------------|:----------------:|
| `rate_percentage=0`  \n The service uses the default speaking rate. You can also omit the parameter to get the default behavior. | ![rate_percentage=0](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-rate-percentage/allison-rate-default.wav){: audio controls} |
| `rate_percentage=-20`  \n The service uses a speaking rate that is 20 percent slower. | ![rate_percentage=-20](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-rate-percentage/allison-rate-slow.wav){: audio controls} |
| `rate_percentage=20`  \n The service uses a speaking rate that is 20 percent faster. | ![rate_percentage=20](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-rate-percentage/allison-rate-fast.wav){: audio controls} |
{: caption="Table 1. Using the rate_percentage parameter"}

### Interaction with SSML `<prosody>` element
{: #params-rate-percentage-ssml}

The `rate_percentage` parameter changes the speaking rate for an entire request. You can also use `rate` attribute of the the SSML `<prosody>` element to modify the rate of specific words of text. Although the `rate_percentage` parameter accepts only a percentage value, the `rate` attribute accepts values of different forms. For more information, see [The `rate` attribute](/docs/text-to-speech?topic=text-to-speech-elements#prosody-rate).

If you use the `rate_percentage` parameter and also use the `rate` attribute of the  `<prosody>` tag to modify the rate for specific text of the same request, the effects are multiplicative. For example, suppose you specify the `rate_percentage` parameter with a value of `-10`, which slows the speaking rate by 10 percent. If you also use the `<prosody>` element to specify an equivalent `rate` of `-10%` for specific text of the request, that text is spoken at a rate that is 81 percent of the default rate for the voice.

### Speaking rate examples
{: #params-rate-percentage-example}

The following HTTP `POST /v1/synthesize` method uses the `rate_percentage` query parameter with a value of `-5`. The resulting audio is spoken at a rate that is five percent slower than it is by default. The example uses the US English voice `en-US_AllisonV3Voice`.

[IBM Cloud]{: tag-ibm-cloud}

```sh
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output rate-percentage.wav \
--data "{\"text\":\"This text is spoken five percent slower than the default.\"}" \
"{url}/v1/synthesize?voice=en-US_AllisonV3Voice&rate_percentage=-5"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```sh
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output rate-percentage.wav \
--data "{\"text\":\"This text is spoken five percent slower than the default.\"}" \
"{url}/v1/synthesize?voice=en-US_AllisonV3Voice&rate_percentage=-5"
```
{: pre}

The following WebSocket example shows inclusion of the parameter with the same value on the request to establish a connection:

```javascript
var access_token = '{access_token}';
var wsURI = '{ws_url}/v1/synthesize'
  + '?access_token=' + access_token
  + '&voice=en-US_AllisonV3Voice'
  + '&rate_percentage=-5';
var websocket = new WebSocket(wsURI);
```
{: codeblock}

## Modifying the speaking pitch
{: #params-pitch-percentage}

The `pitch_percentage` parameter is beta functionality.
{: beta}

The speaking pitch represents the pitch, or tone, of the speech that the service synthesizes, which also affects the intonation. It represents how high or low the tone of the voice is perceived by the listener. A higher pitch results in speech that is spoken at a higher tone and is perceived as a higher voice; a lower pitch results in speech that is spoken in a lower tone and is perceived as a lower, deeper voice.

You can use the optional `pitch_percentage` query parameter to modify the pitch of the synthesized speech for a voice. Each voice has a default, baseline pitch that reflects the intended tone of that voice. The parameter accepts an integer that represents the percentage change from the voice's default:

-   Specify a signed negative integer to reduce the pitch by that percentage. For example, `-10` reduces the pitch by ten percent.
-   Specify an unsigned or signed positive integer to increase the pitch by that percentage. For example, `10` and `+10` increase the pitch by ten percent.
-   Specify `0` or omit the parameter to get the default pitch for the voice.

The best means of determining how the parameter affects the pitch of a given voice is to experiment with different values. Increase or decrease the rate incrementally, by five or ten percent, before trying more drastic changes. When decreasing the pitch, a value of `-50` halves the baseline pitch; lower values might not yield appreciable or positive results. Similarly, when increasing the pitch, a value of `100` doubles the pitch; higher values might produce results that are not discernibly different from `100`.

Table 2 provides examples of how the service changes the speaking pitch with different values for the `pitch_percentage` parameter. The examples use the `en-US_AllisonV3Voice`.

| Specification of the `pitch_percentage` parameter | Audio sample |
|-------------------------------------------------|:----------------:|
| `pitch_percentage=0`  \n The service uses the default speaking pitch. You can also omit the parameter to get the default behavior. | ![pitch_percentage=0](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-pitch-percentage/allison-pitch-default.wav){: audio controls} |
| `pitch_percentage=-20`  \n The service uses a speaking pitch that is 20 percent lower. | ![pitch_percentage=-20](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-pitch-percentage/allison-pitch-low.wav){: audio controls} |
| `pitch-percentage=20`  \n The service uses a speaking pitch that is 20 percent higher. | ![pitch_percentage=20](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-pitch-percentage/allison-pitch-high.wav){: audio controls} |
{: caption="Table 2. Using the pitch_percentage parameter"}

### Interaction with SSML `<prosody>` element
{: #params-pitch-percentage-ssml}

The `pitch_percentage` parameter changes the pitch for an entire request. You can also use `pitch` attribute of the the SSML `<prosody>` element to modify the pitch of specific words of text. Although the `pitch_percentage` parameter accepts only a percentage value, the `pitch` attribute accepts values of different forms. For more information, see [The `pitch` attribute](/docs/text-to-speech?topic=text-to-speech-elements#prosody-pitch).

If you use the `pitch_percentage` parameter and also use the `pitch` attribute of the  `<prosody>` tag to modify the pitch for specific text of the same request, the effects are multiplicative. For example, suppose you specify the `pitch_percentage` parameter with a value of `10`, which increases the pitch by 10 percent. If you also use the `<prosody>` element to specify an equivalent `pitch` of `+10%` for specific text of the request, that text is spoken with a pitch that is 121 percent of the default baseline pitch for the voice.

### Speaking pitch examples
{: #params-pitch-percentage-example}

The following HTTP `POST /v1/synthesize` method uses the `pitch_percentage` query parameter with a value of `5`. The resulting audio is spoken with a pitch that is five percent higher than it is by default. The example uses the US English voice `en-US_AllisonV3Voice`.

[IBM Cloud]{: tag-ibm-cloud}

```sh
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output pitch-percentage.wav \
--data "{\"text\":\"This text is spoken five percent higher than the default.\"}" \
"{url}/v1/synthesize?voice=en-US_AllisonV3Voice&pitch_percentage=5"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```sh
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output pitch-percentage.wav \
--data "{\"text\":\"This text is spoken five percent higher than the default.\"}" \
"{url}/v1/synthesize?voice=en-US_AllisonV3Voice&pitch_percentage=5"
```
{: pre}

The following WebSocket example shows inclusion of the parameter with the same value on the request to establish a connection:

```javascript
var access_token = '{access_token}';
var wsURI = '{ws_url}/v1/synthesize'
  + '?access_token=' + access_token
  + '&voice=en-US_AllisonV3Voice'
  + '&pitch_percentage=5';
var websocket = new WebSocket(wsURI);
```
{: codeblock}

## Specifying how strings are spelled out
{: #params-spell-out-mode}

The service's default pronunciation of alphabetic, numeric, and alphanumeric strings varies by language, with each language having its own rules. For any language, the pronunciation also depends on the length and context of the string, as well its composition in terms of the positions and grouping of its characters

-   Alphabetic strings are pronounced as words if they are pronounceable in the language of the voice. Otherwise, the characters are spelled out individually. Whether a string is pronounced or spelled out can also depend on the case of the letters.
-   Numeric strings can be pronounced as cardinal numbers, ordinal numbers, dates, or in other ways, including as individual digits.
-   Alphanumeric strings that contain both letters and numbers can be pronounced in different ways depending on the characteristics of the string. For example, they might be pronounced as combinations of words, cardinal numbers, or digits. But as mentioned previously, the pronunciation depends largely on the string and its composition.

The best means of controlling how a specific string is pronounced is to use the `<say-as>` element of the SSML. The element allows you to specify exactly how a string is synthesized. You use the `interpret-as` attribute of the `<say-as>` element to indicate that a string of characters is to be pronounced as `letters`, `digits`, or in some other way. The available values differ by language.

If you use the `letters` or `digits` attributes, all letters and numbers of the string are pronounced individually. This is especially useful for spelling out the alphanumeric characters of a hexadecimal string or an identification or account number. For more information, including language-specific differences, see [The `say-as` element](/docs/text-to-speech?topic=text-to-speech-elements#say-as_element).

### Specifying the pace at which strings are spelled out
{: #params-spell-out-mode-rate}

The `spell_out_mode` parameter is beta functionality that is supported only for German voices.
{: beta}

By default, the service reads characters that it spells out at the same rate at which it reads text for the language being synthesized. For German voices, however, you can use the optional `spell_out_mode` query parameter to indicate how the service is to spell out individual characters: one, two, or three at a time. The parameter applies globally to control the pace at which the service reads all strings that it spells out from a request. Use the `spell_out_mode` parameter only for longer strings. The parameter has no effect on a string that contains fewer than three characters.

Table 3 provides examples of how the service pronounces the following text with different values for the `spell_out_mode` parameter:

```xml
Die Nummer ist <say-as interpret-as=‘digits’>AB7234987FFA</say-as>.
```
{: codeblock}

| Specification of the `spell_out_mode` parameter | Audio sample |
|-------------------------------------------------|:----------------:|
| `spell_out_mode=default`  \n The service reads the characters in succession, typically with no pause between them, at the rate at which it synthesizes speech for the request. You can also omit the parameter to get the default behavior. | ![spell_out_mode=default](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-spell-out/spell-out-default.wav){: audio controls} |
| `spell_out_mode=singles`  \n The service reads the characters one at a time, with a brief pause between each character. | ![spell_out_mode=singles](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-spell-out/spell-out-singles.wav){: audio controls} |
| `spell_out_mode=pairs`  \n The service reads the characters two at a time, with a brief pause between each pair. | ![spell_out_mode=pairs](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-spell-out/spell-out-pairs.wav){: audio controls} |
| `spell_out_mode=triplets`  \n The service reads the characters three at a time, with a brief pause between each triplet. | ![spell_out_mode=triplets](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-spell-out/spell-out-triplets.wav){: audio controls} |
{: caption="Table 3. Using the spell_out_mode parameter for German"}

Alphanumeric strings that mix letters and digits can yield different groupings of characters. If you do not use the `<say-as>` element, groups of letters and digits can be pronounced in ways that do not necessarily conform to the requested mode.
{: note}

### Spell-out mode examples
{: #params-spell-out-mode-example}

The following HTTP `POST /v1/synthesize` method uses the `spell_out_mode` query parameter with a value of `singles`. The example uses the German voice `de-DE_ErikaV3Voice`. The alphanumeric text to be synthesized is a hexadecimal string that is wrapped in a `<say-as>` element and interpreted as `digits`.

[IBM Cloud]{: tag-ibm-cloud}

```sh
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output spell-out-mode.wav \
--data "{\"text\":\"Die Nummer ist <say-as interpret-as=‘digits’>AB7234987FFA</say-as>.\"}" \
"{url}/v1/synthesize?voice=de-DE_ErikaV3Voice&spell_out_mode=singles"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```sh
curl -X POST \
--header "Authorization: Bearer {token}" \
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
  + '&voice=de-DE_ErikaV3Voice'
  + '&spell_out_mode=singles';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
