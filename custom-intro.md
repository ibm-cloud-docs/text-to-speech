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

# Understanding customization
{: #customIntro}

When you synthesize text with the {{site.data.keyword.texttospeechshort}} service, the service applies language-dependent pronunciation rules to convert the ordinary (orthographic) spelling of each word to a phonetic spelling. A word's phonetic spelling defines how it is pronounced. It consists of phoneme symbols, which are the distinct units of sound that distinguish words in a language, the boundaries between syllables, and the stress marks for the syllables.
{: shortdesc}

The service's regular pronunciation rules work well for common words. However, they might yield imperfect results for unusual words such as special terms with foreign origins, personal or geographic names, and abbreviations and acronyms. When your application's lexicon includes such words, the service can produce imperfect pronunciations.

To address this issue, the service provides a customization interface that you can use to specify how it pronounces unusual words that occur in your input. This section introduces customization and its main concepts. For detailed information about using the customization interface, see [Using customization](/docs/services/text-to-speech/custom-using.html).

> **Note:** The customization interface is currently a beta release.

## How customization works
{: #ciHow}

The customization interface of the {{site.data.keyword.texttospeechshort}} service lets you create a dictionary of words and their translations for a specific language. This dictionary of words and their translations is referred to as a *custom voice model*, or just a custom model. Each entry in a custom voice model consists of a *word*/*translation* pair. A word's translation tells the service how to pronounce the word when it occurs in input text.

The customization interface provides methods to create and manage your custom models, which the service stores permanently. The interface includes methods to add, modify, delete, and query the words and translations in a custom model.

Each custom model has a globally unique identifier (GUID). Once you create a custom model, you can use it during synthesis by specifying its GUID with the `synthesize` method. When the service synthesizes input text, it determines the pronunciation of words that appear in the custom model by applying their translations either directly or indirectly, as explained below.

## Specifying word translations
{: #ciTranslation}

You specify the translation for a word in a custom voice model via one of two methods: *sounds-like* or *phonetic*. You can use both methods for entries in the same custom model, but a single custom model can include no more than 20,000 entries.

### Sounds-like translation

Sounds-like translation leverages the service's regular pronunciation rules to represent the desired pronunciation of a target word indirectly. A translation is formed from the regular pronunciations of one or more other words. The service first substitutes the specified translation for any occurrence of the word that appears in the input text. It then applies its regular pronunciation rules to the translation, converting the translation to its phonetic representation to obtain the desired pronunciation.

The service's regular pronunciation rules properly translate some common abbreviations and acronyms. For example, the service pronounces the abbreviation *cm* as *centimeter*. It pronounces less common abbreviations letter by letter. For instance, the service pronounces the word *Str* as *S T R*, with each letter pronounced individually. You can use the sounds-like method to specify the translation *street* for the word *Str*.

An example of a common acronym is the word *IEEE*, which stands for Institute of Electrical and Electronic Engineers. By default, the service pronounces this acronym as *I E E E*. But the acronym is commonly pronounced *I triple E*, which you can easily define by using the sounds-like method. If the word *IEEE* appears in your custom model with the associated sounds-like translation *I triple E*, the service substitutes each occurrence of the word with the translation and applies its regular pronunciation rules to the individual words *I*, *triple*, and *E* to yield the desired pronunciation.

The sounds-like method is applicable to more than just abbreviations and acronyms. It works equally well for complex or unusual words. For example, the following pair of sounds-like translations yield correct pronunciations for unusual words that are handled improperly by the regular pronunciation rules. Finding proper translations for such words can be more challenging than for simple abbreviations; the translations shown alter the correct spelling to leverage the service's regular pronunciation rules.

<table style="width:35%">
  <caption>Table 1. Example sounds-like translations</caption>
  <tr>
    <th style="text-align:left">Word</th>
    <th style="text-align:left">Translation</th>
  </tr>
  <tr>
    <td>Ayurvedic</td>
    <td>aayervedic</td>
  </tr>
  <tr>
    <td>gastroenteritis</td>
    <td>gastro enteritis</td>
  </tr>
</table>

As these examples indicate, developing sounds-like translations can be more trial-and-error than formulaic. You create a candidate translation based on your intuition and experience with the service. You then synthesize the word for the candidate translation as input text and listen to the resulting audio. If you are satisfied with the pronunciation, you can use the translation in your custom model; otherwise, you modify the translation and test it again.

### Phonetic translation

In many cases, the sounds-like method is a relatively simple and useful way of achieving a desired pronunciation. But it is not always possible to develop sounds-like translations. The direct alternative, the phonetic method, might appear to be more complicated and time-consuming, but it can achieve the desired pronunciation for any word.

Phonetic translation specifies a pronunciation in terms of phoneme symbols, syllable stress marks, and, optionally, syllable boundaries that override the service's regular pronunciation rules. You specify a phonetic translation in one of two formats:

-   The standard International Phonetic Alphabet (IPA) representation
-   The proprietary {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR)

In either case, you specify a translation by using a specific phoneme format that is based on the Speech Synthesis Markup Language (SSML), an XML-based markup language that provides annotations of text for speech-synthesis applications. You specify the phonetic translation for a word by using the SSML `<phoneme>` element:

```xml
<phoneme alphabet="<ipa | ibm>" ph="<translation>"></phoneme>
```
{: codeblock}

The `alphabet` attribute specifies the phonetic representation type, `ipa` or `ibm`. The `ph` attribute specifies the phonetic translation string.

For example, consider the word `trinitroglycerin`. The service's regular pronunciation rules produce a pronunciation that differs from the one commonly used by chemists and physicians. The correct pronunciation can be achieved with a phonetic translation:

<table style="width:35%">
  <caption>Table 2. Example phonetic translations</caption>
  <tr>
    <th style="text-align:left">Alphabet</th>
    <th style="text-align:left">Translation</th>
  </tr>
  <tr>
    <td>IPA</td>
    <td>t&#633;a&#618;n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n</td>
  </tr>
  <tr>
    <td>SPR</td>
    <td>trYn1YtrxglIsxrXn</td>
  </tr>
</table>

In these examples, the phonetic translation string is composed of phoneme symbols and a single primary stress mark per word. The primary stress mark is represented by <code>&#712;</code> in IPA and by `1` in SPR; it is placed just before the phoneme that corresponds to the stressed vowel in both cases. Although the examples do not show this, it is also possible to specify syllable boundaries and secondary stress positions in a phonetic translation, but these elements are not required and normally are not needed for achieving a desired pronunciation. As with sounds-like translations, you can compose a phonetic translation from multiple words delimited by spaces.

Unless you are an expert in phonology, composing phonetic translations is not an easy task. It is always easier to edit an existing phonetic translation than to compose one from scratch. To help you create phonetic translations, the service's API includes a `pronunciation` method that returns the IPA or SPR representation generated by the service's regular pronunciation rules for a word in a specified language. You can also request the pronunciation for a specified custom voice model to see the translation in the language of that model.

You can use the `pronunciation` method to obtain an initial translation for a word and then modify the translation to achieve the desired pronunciation. As with the sounds-like method, you follow a trial-and-error process of submitting your candidate translation to the service, synthesizing the word as input text and listening to the resulting audio, and editing the candidate translation and repeating the process until you are satisfied with the pronunciation.

The following resources provide more information about phonetic representation:

-   For information about using SSML and its `<phoneme>` element, see [Using SSML](/docs/services/text-to-speech/SSML.html).
-   For information about specifying SPR translations and their equivalent IPA symbols, see [Using SPRs](/docs/services/text-to-speech/SPRs.html).
-   For more information about using IPA symbols, including audio samples, consult sources on the Web, including a detailed introductory discussion at [en.wikipedia.org/wiki/International_Phonetic_Alphabet ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet){: new_window}.

### Mixed sounds-like and phonetic translation

You can mix the sounds-like and phonetic methods in the same translation. This feature can reduce the work involved in composing a translation.

For instance, assume that you got part of a word pronounced satisfactorily by using the sounds-like method but need to fine-tune the remaining elements of the word. You can use the phonetic method to specify the problematic aspects of the word. The following example applies mixed translation to the word `trinitroglycerin`:

<pre><code data-copy="false" class="language-xml">try&lt;phoneme alphabet="ipa" ph="n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n"&gt;&lt;/phoneme&gt;</code></pre>

## Rules for creating custom model entries
{: #ciRules}

You need to be aware of a few rules and considerations when populating a custom model with `{word, translation}` pairs.

### Character encoding

The service accepts ASCII and UTF-8 character encoding for *word* and *translation* entries. For translations, use ASCII encoding for SPR notations and UTF-8 for IPA notations.

### Whitespace

In general, a *word* cannot include whitespace. Whitespace is used to delineate individual words in the input text.

### Context sensitivity

The pronunciation of some words is context-sensitive. For example, consider the following example input sentence:

```
St. Anthony lives on Henry St.
```
{: screen}

The service's default pronunciation rules correctly synthesize this text as

```
Saint Anthony lives on Henry street
```
{: screen}

However, if you override the default pronunciation rules for the word *St.* to translate it as *saint*, the service loses the ability to pronounce the word based on context. Applying a custom voice model that includes such a translation causes the service to pronounce the previous input sentence as

```
Saint Anthony lives on Henry saint
```
{: screen}

Exercise caution and consider such corner cases when developing word/translation pairs.

### Words without a trailing period

A *word* that does not have a trailing `.` (period) can contain practically any character, including letters, digits, punctuation (other than a trailing period), non-letter symbols (such as %, &amp;, and @), quotation marks, parentheses, brackets, and so on.

Its *translation* can include any legal input to the service, including whitespace and a phonetic representation in SSML format.

### Words with a trailing period

A *word* that has a trailing period can contain only letters, periods, and internal apostrophes (though not as the first and last characters). An example of a word with a trailing period is `div.`.

Its *translation* can contain only normal words in ordinary spelling separated by whitespace or hyphens. It cannot include a phonetic representation.

Be aware that during synthesis, the custom model is applied only to those strings in the input text that match a word exactly. For example, assume a custom model contains the entry `{word='Sun', translation='Sunday'}`. In this case, the service applies the default pronunciation to the word '`sun`' but the custom translation to the word '`Sun`', since only the latter has an initial capital letter.

Similarly, assume a custom model includes the entry `{word='div.', translation='division'}`. The service does not apply the translation to the string '`div` ' because it does not include a trailing period and therefore does not match the entry.

### Japanese entries

When working with Japanese entries in a custom voice model, additional considerations and an additional `part_of_speech` field apply. For more information, see [Working with Japanese entries](/docs/services/text-to-speech/custom-using.html#jaNotes).

## Working with IBM SPR entries
{: #sprNotes}

As mentioned earlier, SPR is a proprietary, language-dependent format developed by {{site.data.keyword.IBM_notm}} for specifying a word's pronunciation. For each supported language, SPR includes a phoneme alphabet, symbols for syllable boundaries, and symbols for levels of lexical stress. The following basic rules apply to creation of SPR entries:

-   The default pronunciation that the customization interface returns for a word begins with a <code>&#96;</code> (backquote) and is enclosed in `[]` (square brackets). For example, the interface returns the following pronunciation for the word `tomato`:

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    However, you must omit the backquote and square brackets when you specify a word's translation with methods of the customization interface.
-   You can use a period to indicate the beginning of a syllable in a translation, but periods are optional and do not influence the word's pronunciation. They appear in the pronunciation for a word only if you include them in the word's translation. (Do not use spaces to indicate syllable boundaries.)
-   You must precede the vowel that has the primary stress for a word with a `1` symbol. You can also use `2` symbol to indicate each secondary stress position, but the use of `2` symbols is optional; they appear in the pronunciation for a word only if you include them in the word's translation.

For more information about working with SPRs, see [Using SPRs](/docs/services/text-to-speech/SPRs.html).
