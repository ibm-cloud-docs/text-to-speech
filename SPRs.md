---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-11"

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

# Using SPRs
{: #sprs}

The {{site.data.keyword.texttospeechshort}} service uses {{site.data.keyword.IBM}} Symbolic Phonetic Representation (SPR) notation to represent the sounds of words. An SPR is a phonetic coding that represents the pronunciation of a word, the sounds that make up the word, how the sounds are divided into syllables, and which syllables are stressed. SPR is an alternative representation to the standard International Phonetic Alphabet (IPA), which the service also supports for use with the SSML `<phoneme>` element.
{: shortdesc}

The following section introduces the basic usage and elements of {{site.data.keyword.IBM_notm}} SPR notation. Because IPA is a standard notation, the documentation does not provide basic usage information for IPA. For more information about IPA, see [en.wikipedia.org/wiki/International_Phonetic_Alphabet ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet){: new_window}. For more information about phonetic symbols for Unicode, see [en.wikipedia.org/wiki/Phonetic_symbols_in_Unicode ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: new_window}.

The remaining sections describe the valid SPR and IPA symbols that you can use for a language with the {{site.data.keyword.texttospeechshort}} service. Tables present the SPR symbols, the IPA symbols, the equivalent IPA Unicode values, and examples that show typical spellings of each sound with the letters representing the given sound underlined. (Because of dialectal differences, the examples might not always match your pronunciation.)

When several IPA symbols (or symbol combinations) are listed for an SPR, all are equivalent to the single SPR symbol shown in the first column of a table. The service treats all of these IPA symbols the same and does not realize the subtle or regional differences that the IPA system is meant to describe. When working with IPA, use only those symbols documented in the following sections.

## Introduction to SPRs
{: #introduction}

An SPR is defined with the `<phoneme>` tag of the Speech Synthesis Markup Language (SSML). It consists of a sequence of allowable symbols for a given language enclosed in double quotes. The symbols define how the word enclosed in the `<phoneme>` tag is to be pronounced. The `alphabet` attribute of the tag has the value `ibm` to indicate that the word is defined as an SPR, and the `ph` attribute defines the pronunciation. The following are examples of valid SPRs for the words *through* and *shocking* in US English:

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

In the definitions, a `.` (period) signals the beginning of a new syllable, the digits `1` and `0` indicate the stress level of the syllables, and the letters represent specific sounds of US English speech, as described in the following sections. An SPR entry that does not conform to the required specification is invalid.

## Syllable boundaries

You can use a `.` (period) to mark the beginning of each syllable. However, to preserve the valid phonetics of a language, the service can elect not to honor periods in some cases (for example, if a syllable boundary is placed at an illegal or unnatural position for a language). In general, in cases where the user can indicate a valid preference for a syllable boundary or other aspect of a word's pronunciation, the service honors such requests.

## Syllable stress

You can use the symbols in the following table to mark syllable stress. However, you do not need to indicate syllable stress in an SPR or IPA; the service determines where stress occurs if you do not indicate it.

<table style="width:80%">
  <caption>Table 1. Syllable stress</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IBM SPR symbol
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Meaning
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      1
    </td>
    <td style="text-align:center">
      <strong>&#712;</strong>
    </td>
    <td style="text-align:center">
      02C8
    </td>
    <td>
      Primary stress
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      2
    </td>
    <td style="text-align:center">
      <strong>&#716;</strong>
    </td>
    <td style="text-align:center">
      02CC
    </td>
    <td>
      Secondary stress
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      0
    </td>
    <td style="text-align:center"></td>
    <td style="text-align:center"></td>
    <td>
      No stress
    </td>
  </tr>
</table>

**Notes:**

-   In IPA for French, syllable stress symbols are ignored. In SPR for French, syllable stress is not ignored; if specified, syllable stress must immediately precede the vowel of the syllable. In SPR, syllable stress for French is much stricter than for other languages; an error occurs if the stress symbol is in an invalid location.
-   In SPR for Spanish (Castilian and North American) and Italian, you can specify only `1` (primary stress). An error occurs if you specify secondary or no stress.
-   In SPR for Japanese, only `1` (primary stress) and `0` (no stress) are supported. An error occurs if you specify secondary stress.

You must place the numeric syllable stress markers within a syllable boundary but always to the left of the vowel of the syllable. You can place the marker anywhere to the left of the stressed vowel. For example, each of the following SPRs places the primary stress on the correct vowel of the word *construction*:

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

## Speech sound symbols

Each language uses its own inventory of SPR symbols to represent the speech sounds of that language. Tables in the following sections show the valid SPR symbols for the sounds of each language, with examples of words in which each sound occurs. Letters are case-sensitive, so `e` and `E`, for example, represent two different sounds. Two- and three-character symbols must be contained in single quotes (for example, the symbol `aj` in the German word *heim*: `"h'aj'm"`). The service considers invalid any SPR that contains sound symbols that are not allowed in a language.

The sounds of every language have specific distributional patterns within that language. For example, in all dialects of English, the sound `G` in *sing* (`".1sIG"`) does not occur at the beginning of a word. Other US English sounds that have a particularly narrow distribution are the glottal stop (`?`), the flap (`F`), and the syllabic nasal (`N`). If you enter a sound symbol in a context in which it does not normally occur, the resulting speech might sound unnatural.

The {{site.data.keyword.texttospeechshort}} service applies a sophisticated set of linguistic rules to its input to reflect the processes by which sounds change in specific contexts in natural language. For example, in US English, the sound `t` of the word *write* (`".1r1Yt"`) is pronounced as a flap (`F`) in *writer* (`".1rY.0FR"`). SPR input undergoes these modifications just as ordinary input text does. In this example, whether you enter `".1rY.0tR"` or `".1rY.0FR"` does not affect the speech that is generated.

## Supported languages
{: #supportedLanguages}

For information about the specific SPR and IPA symbols for each supported language, see the following sections:

-   [Brazilian Portuguese symbols](/docs/services/text-to-speech/pt-BR-SPRs.html)
-   [British Engish symbols](/docs/services/text-to-speech/en-GB-SPRs.html)
-   [French symbols](/docs/services/text-to-speech/fr-FR-SPRs.html)
-   [German symbols](/docs/services/text-to-speech/de-DE-SPRs.html)
-   [Italian symbols](/docs/services/text-to-speech/it-IT-SPRs.html)
-   [Japanese symbols](/docs/services/text-to-speech/ja-JP-SPRs.html)
-   [Spanish symbols](/docs/services/text-to-speech/es-ES-SPRs.html)
-   [US English symbols](/docs/services/text-to-speech/en-US-SPRs.html)
