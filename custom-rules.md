---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Rules for creating custom entries
{: #rules}

The following rules and guidelines apply to populating a custom model with custom entries (word/translation pairs).

## Maximum custom entries

A single custom model can include no more than 20,000 custom entries.

## Character encoding

The service accepts ASCII and UTF-8 character encoding for *word* and *translation* entries. For translations, use ASCII encoding for SPR notations and UTF-8 encoding for IPA notations.

## White space

A *word* cannot include white space. The service uses white space to delineate individual words in the input text.

## Case-sensitivity

A *word* is case-sensitive. For example, assume that a custom model contains the entry `{word='Sun', translation='Sunday'}`. The service applies its default pronunciation to the word `sun` but the custom translation to the word `Sun`, since only the latter has an initial capital letter.


## Context sensitivity

The pronunciations of some words are context-sensitive. For example, consider the following example input sentence:

```
St. Anthony lives on Henry St.
```
{: codeblock}

The service's default pronunciation rules correctly synthesize this text as

```
Saint Anthony lives on Henry Street
```
{: codeblock}

However, if you override the default pronunciation rules for the string `St.` to translate it as `saint`, the service can no longer pronounce the word based on context. Applying a custom voice model that includes such a translation causes the service to pronounce the previous input sentence as

```
Saint Anthony lives on Henry saint
```
{: codeblock}

Consider such cases when you develop word/translation pairs.

## Trailing periods

The service applies a word from a custom model only to those strings in the input text that match the word exactly. A trailing `.` (period) in a word entry changes how the word is synthesized:

-   *A word that does not have a trailing period* can contain practically any character. Characters include letters, digits, punctuation (other than a trailing period), non-letter symbols (such as %, &amp;, and @), quotation marks, parentheses, brackets, and so on. Its *translation* can include any legal input to the service, including white space and a phonetic representation in SSML format.
-   *A word that has a trailing period* can contain only letters, periods, and internal apostrophes (not as the first or last character). The word's *translation* can contain only normal words with ordinary spelling that are separated by white space or hyphens. It cannot contain a phonetic representation.

An example of a word with a trailing period is "`div.`". Assume that a custom model includes the entry `{word='div.', translation='division'}`. The service does not apply the translation to the string "`div`" because it does not include a trailing period and therefore does not match the entry.

## Working with IBM SPR entries
{: #sprNotes}

Symbolic Phonetic Representation (SPR) is a proprietary, language-dependent format developed by {{site.data.keyword.IBM_notm}} for specifying a word's pronunciation. For each supported language, SPR includes a phoneme alphabet, symbols for syllable boundaries, and symbols for levels of lexical stress. The following basic rules apply to creation of SPR entries:

-   The default pronunciation that the customization interface returns for a word begins with a <code>&#96;</code> (back quote) and is enclosed in `[]` (square brackets). For example, the interface returns the following pronunciation for the word `tomato`:

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    Omit the back quote and square brackets when you specify a word's translation with methods of the customization interface.
-   You can use a period to indicate the beginning of a syllable in a translation, but periods are optional and do not influence the word's pronunciation. They appear in the pronunciation for a word only if you include them in the word's translation. Do not use spaces to indicate syllable boundaries.
-   {{site.data.keyword.IBM_notm}} recommends that you precede the vowel that has the primary stress for a word with a `1` symbol, though it is not strictly necessary. The service determines where stress occurs if you do not indicate it. You can also use a `2` symbol to indicate each secondary stress position, but the use of `2` symbols is also optional. They appear in the pronunciation for a word only if you include them in the word's translation.

For more information about working with SPR, see [Using IBM SPR](/docs/services/text-to-speech/SPRs.html).

## Working with Japanese entries
{: #jaNotes}

Extra rules and a `part_of_speech` field apply to the creation of entries for words in a Japanese custom voice model:

-   A sounds-like translation can contain only *Katakana* characters. *Kanji* and *Hiragana* characters are not allowed.
-   When you create a translation (sounds-like or phonetic) for a word, you can also specify an optional `part_of_speech` field to identify the word's part of speech. The service uses the part of speech to produce the correct intonation for the word. For a complete list, see [Japanese parts of speech](#partsOfSpeech).
-   You can create only a single entry for any word, and you can specify only a single part of speech for any word. You cannot create multiple entries with different parts of speech (for instance, noun and verb) for the same word. Adding a translation for a word that exists in a model overwrites the word's existing translation, including its part of speech.
-   The service applies the longest matching word from the word/translation pairs that are defined for a custom voice model. For example, consider the following three entries for a custom model.

    <pre><code>{
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

    With these entries, assume that the service receives the following input text: <code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>. In this case, the service matches the word <code>&#65326;&#65337;&#65315;</code> because <code>&#65326;&#65337;&#65315;</code> is longer than <code>&#65326;&#65337;</code> and because <code>&#65326;&#65337;&#65315;</code> matches before <code>&#65337;&#65315;</code>.

### Japanese parts of speech
{: #partsOfSpeech}

The following table lists the parts of speech that are supported for Japanese custom entries. For more information about specifying the part of speech for a Japanese custom entry, see [Adding words to a Japanese custom model](/docs/services/text-to-speech/custom-entries.html#cuJapaneseAdd).

<table style="width:75%">
  <caption>Table 1. Japanese parts of speech</caption>
  <tr>
    <th style="text-align:center"><code>part_of_speech</code> argument</th>
    <th style="text-align:center; width:35%">Japanese meaning</th>
    <th style="text-align:center; width:35%">English meaning</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>Josi</code></td>
    <td style="text-align:center"><em>Joshi</em></td>
    <td style="text-align:center">Participle</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Mesi</code></td>
    <td style="text-align:center"><em>Meishi</em></td>
    <td style="text-align:center">Noun</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kigo</code></td>
    <td style="text-align:center"><em>Kigou</em></td>
    <td style="text-align:center">Symbol</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Gobi</code></td>
    <td style="text-align:center"><em>Gobi</em></td>
    <td style="text-align:center">Inflection</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Dosi</code></td>
    <td style="text-align:center"><em>Doushi</em></td>
    <td style="text-align:center">Verb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Jodo</code></td>
    <td style="text-align:center"><em>Jodoushi</em></td>
    <td style="text-align:center">Auxiliary verb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Koyu</code></td>
    <td style="text-align:center"><em>Koyuumeishi</em></td>
    <td style="text-align:center">Proper noun</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stbi</code></td>
    <td style="text-align:center"><em>Setsubiji</em></td>
    <td style="text-align:center">Suffix</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Suji</code></td>
    <td style="text-align:center"><em>Suuji</em></td>
    <td style="text-align:center">Numeral</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kedo</code></td>
    <td style="text-align:center"><em>Keiyodoushi</em></td>
    <td style="text-align:center">Adjective verb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Fuku</code></td>
    <td style="text-align:center"><em>Fukishi</em></td>
    <td style="text-align:center">Adverb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Keyo</code></td>
    <td style="text-align:center"><em>Keiyoshi</em></td>
    <td style="text-align:center">Adjective verb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stto</code></td>
    <td style="text-align:center"><em>Settoji</em></td>
    <td style="text-align:center">Prefix</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Reta</code></td>
    <td style="text-align:center"><em>Rentaishi</em></td>
    <td style="text-align:center">Determiner</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stzo</code></td>
    <td style="text-align:center"><em>Setsuzokushi</em></td>
    <td style="text-align:center">Conjunction</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kato</code></td>
    <td style="text-align:center"><em>Kantoushi</em></td>
    <td style="text-align:center">Interjection</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Hoka</code></td>
    <td style="text-align:center"><em>Hoka</em></td>
    <td style="text-align:center">Other</td>
  </tr>
</table>
