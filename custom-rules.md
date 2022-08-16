---

copyright:
  years: 2015, 2022
lastupdated: "2022-08-06"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Rules for creating custom entries
{: #rules}

The following rules and guidelines apply to populating a custom model with custom entries (word/translation pairs).

## Maximum custom entries and limits
{: #rulesMaxEntries}

The following limits apply to all custom models and entries:

-   A word in a custom entry can contain a maximum of 49 characters.
-   A translation in a custom entry can contain a maximum of 499 characters.
-   A custom model can include a maximum of 20,000 custom entries.
-   A custom model can include a maximum of 1000 custom prompts.

## Character encoding
{: #rulesCharEncoding}

The service accepts ASCII and UTF-8 character encoding for *word* and *translation* entries. For translations, use ASCII encoding for SPR notations and UTF-8 encoding for IPA notations.

## White space
{: #rulesWhitespace}

A word cannot include white space. The service uses white space to delineate individual words in the input text.

## Case-sensitivity
{: #rulesCase}

A word is case-sensitive. For example, assume that a custom model contains the entry `{word='Sun', translation='Sunday'}`. The service applies its default pronunciation to the word `sun` but the custom translation to the word `Sun`, since only the latter has an initial capital letter.

To apply a custom translation to a word that might appear with or without initial capitalization, create two entries for both possible occurrences. Include both entries only if the translation is to be applied to both forms of the word.

## Context sensitivity
{: #rulesContext}

The pronunciations of some words are context-sensitive. For example, consider the following example input sentence:

```text
St. Anthony lives on Henry St.
```
{: codeblock}

The service's default pronunciation rules correctly synthesize this text as

```text
Saint Anthony lives on Henry Street
```
{: codeblock}

However, if you override the default pronunciation rules for the string `St.` to translate it as `saint`, the service can no longer pronounce the word based on context. Applying a custom model that includes such a translation causes the service to pronounce the previous input sentence as

```text
Saint Anthony lives on Henry saint
```
{: codeblock}

Consider such cases when you develop word/translation pairs.

## Trailing periods
{: #rulesPeriods}

The service applies a word from a custom model only to those strings in the input text that match the word exactly. A trailing `.` (period) in a word entry changes how the word is synthesized:

-   *A word that does not have a trailing period* can contain practically any character. Characters include letters, digits, punctuation (other than a trailing period), non-letter symbols (such as `%`, `&`, and `@`), quotation marks, parentheses, brackets, and so on. Its *translation* can include any legal input to the service, including white space and a phonetic representation in SSML format.
-   *A word that has a trailing period* can contain only letters, periods, and internal apostrophes (not as the first or last character). The word's *translation* can contain only normal words with ordinary spelling that are separated by white space or hyphens. It cannot contain a phonetic representation.

An example of a word with a trailing period is "`div.`". Assume that a custom model includes the entry `{word='div.', translation='division'}`. The service does not apply the translation to the string "`div`" because it does not include a trailing period and therefore does not match the entry.

## Phonetic translation for foreign words
{: #rulesForeignWords}

One use of phonetic translation is to add pronunciations for words that are foreign to the base language of the custom model. For example, you might add a pronunciation for a French word to a custom model that is based on English. In this case, you must use the phonetic symbols for the language of the custom model, English.

The same phonetic symbol can produce different sounds for different languages. Also, not all phonetic symbols are supported for all languages. Make sure to use the phonetic symbols for the base language of the custom model when defining a translation.

## Working with IBM SPR entries
{: #sprNotes}

Symbolic Phonetic Representation (SPR) is a proprietary, language-dependent format developed by {{site.data.keyword.IBM_notm}} for specifying a word's pronunciation. For each supported language, SPR includes a phoneme alphabet, symbols for syllable boundaries, and symbols for levels of lexical stress. The following basic rules apply to creation of SPR entries:

-   The default pronunciation that the customization interface returns for a word begins with a ``` (back quote) and is enclosed in `[]` (square brackets). For example, the interface returns the following pronunciation for the word `tomato`:

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    Omit the back quote and square brackets when you specify a word's translation with methods of the customization interface.
-   You can use a period to indicate the beginning of a syllable in a translation, but periods are optional and do not influence the word's pronunciation. They appear in the pronunciation for a word only if you include them in the word's translation. Do not use spaces to indicate syllable boundaries.
-   {{site.data.keyword.IBM_notm}} recommends that you precede the vowel that has the primary stress for a word with a `1` symbol, though it is not strictly necessary. The service determines where stress occurs if you do not indicate it. You can also use a `2` symbol to indicate each secondary stress position, but the use of `2` symbols is also optional. They appear in the pronunciation for a word only if you include them in the word's translation.

For more information about working with SPR, see [Understanding phonetic symbols](/docs/text-to-speech?topic=text-to-speech-symbols).

## Working with Japanese entries
{: #jaNotes}

Extra rules and a `part_of_speech` field apply to the creation of entries for words in a Japanese custom model:

-   A sounds-like translation can contain only *Katakana* characters. *Kanji* and *Hiragana* characters are not allowed.
-   When you create a translation (sounds-like or phonetic) for a word, you can also specify an optional `part_of_speech` field to identify the word's part of speech. The service uses the part of speech to produce the correct intonation for the word. For a complete list, see [Japanese parts of speech](#partsOfSpeech).
-   You can create only a single entry for any word, and you can specify only a single part of speech for any word. You cannot create multiple entries with different parts of speech (for instance, noun and verb) for the same word. Adding a translation for a word that exists in a model overwrites the word's existing translation, including its part of speech.

    For improved naturalness of synthesized speech, do not create custom entries for long phrases. Create translations for single words or short phrases only. Note that other languages limit translation to single words only.
    {: important}

-   The service applies the longest matching word from the word/translation pairs that are defined for a custom model. For example, consider the following three entries for a custom model.

    ```json
    {
      "words": [
        {
          "word": "ＮＹ",
          "translation": "ニューヨーク",
          "part_of_speech": "Mesi"
        },
        {
          "word": "ＮＹＣ",
          "translation": "ニューヨークシティ",
          "part_of_speech": "Mesi"
        },
        {
          "word": "ＹＣ",
          "translation": "ヨコハマチューカガイ",
          "part_of_speech": "Mesi"
        }
      ]
    }
    ```
    {: codeblock}

    With these entries, assume that the service receives the following input text: `一週間ＮＹＣを訪問した`. In this case, the service matches the word `ＮＹＣ` because `ＮＹＣ` is longer than `ＮＹ` and because `ＮＹＣ` matches before `ＹＣ`.

### Japanese parts of speech
{: #partsOfSpeech}

The following table lists the parts of speech that are supported for Japanese custom entries. For more information about specifying the part of speech for a Japanese custom entry, see [Adding words to a Japanese custom model](/docs/text-to-speech?topic=text-to-speech-customWords#cuJapaneseAdd).

| `part_of_speech` argument | Japanese meaning | English meaning |
|:-----------------------------:|:--------------------:|----------------------|
| `Dosi` | *Doushi* | Verb |
| `Fuku` | *Fukishi* | Adverb |
| `Gobi` | *Gobi* | Inflection |
| `Hoka` | *Hoka* | Other (Words that have a special grammatical meaning of their own that does not fit into any other part of speech. For example, `ありがとう` for "thank you.") |
| `Jodo` | *Jodoushi* | Auxiliary verb |
| `Josi` | *Joshi* | Postpositional particle (For example, `が の を` for "of.") |
| `Kato` | *Kantoushi* | Interjection |
| `Kedo` | *Keiyodoushi* | Adjective verb |
| `Keyo` | *Keiyoshi* | Adjective (For example, `美し` for "beautiful" or `明る` for "bright.") |
| `Kigo` | *Kigou* | Symbol |
| `Koyu` | *Koyuumeishi* | Proper noun |
| `Mesi` | *Meishi* | Noun |
| `Reta` | *Rentaishi* | Determiner |
| `Stbi` | *Setsubiji* | Suffix |
| `Stto` | *Settoji* | Prefix |
| `Stzo` | *Setsuzokushi* | Conjunction |
| `Suji` | *Suuji* | Numeral |
{: caption="Table 1. Japanese parts of speech"}
