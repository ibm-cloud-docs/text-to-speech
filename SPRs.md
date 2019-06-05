---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-04"

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

# Using IBM SPR
{: #sprs}

The {{site.data.keyword.texttospeechfull}} service supports both the standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM}} Symbolic Phonetic Representation (SPR) notation to represent the sounds of words. SPR is a phonetic coding that represents the pronunciation of a word, the sounds that make up the word, how the sounds are divided into syllables, and which syllables are stressed. SPR is an alternative representation to IPA.
{: shortdesc}

The following sections introduce {{site.data.keyword.IBM_notm}} SPR notation. Because IPA is a standard notation, the documentation does not provide basic usage information for IPA. For brief usage guidance, see [Working with IPA](#ipa).

## Introduction to IBM SPR
{: #introduction-SPRs}

An SPR pronunciation is defined with [the phoneme element](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element) of the Speech Synthesis Markup Language (SSML). It consists of a sequence of allowable symbols for a given language enclosed in double quotes. The symbols define how the word enclosed in the `<phoneme>` element is to be pronounced. The `alphabet` attribute of the element has the value `ibm` to indicate that the pronunciation is defined in SPR, and the `ph` attribute defines the pronunciation. The following are examples of valid SPR notation for the words *through* and *shocking* in US English:

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

In the definitions, a `.` (period) signals the beginning of a new syllable, the digits `1` and `0` indicate the stress level of the syllables, and the letters represent specific sounds of US English speech. An SPR entry that does not conform to the required specification is invalid.

## Syllable boundaries

You can use a `.` (period) to mark the beginning of each syllable. However, to preserve the valid phonetics of a language, the service can elect not to honor periods in some cases (for example, if a syllable boundary is placed at an illegal or unnatural position for a language). In general, in cases where the user can indicate a valid preference for a syllable boundary or other aspect of a word's pronunciation, the service honors such requests.

## Syllable stress

You can use the symbols in the following table to mark syllable stress for a pronunciation. {{site.data.keyword.IBM_notm}} recommends that you indicate primary stress for pronunciations in either SPR or IPA. However, indicating syllable stress is optional for both formats; the service determines where stress occurs if you do not indicate it.

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
      <code>&#712;</code>
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
      <code>&#716;</code>
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
    <td style="text-align:center">No symbol</td>
    <td style="text-align:center">No value</td>
    <td>
      No stress
    </td>
  </tr>
</table>

**Notes:**

-   In IPA for French, syllable stress symbols are ignored. In SPR for French, syllable stress is not ignored; if specified, syllable stress must immediately precede the vowel of the syllable. In SPR, syllable stress for French is much stricter than for other languages; an error occurs if the stress symbol is in an invalid location.
-   In SPR for Spanish and Italian, you can specify only `1` (primary stress). An error occurs if you specify secondary or no stress.
-   In SPR for Japanese, only `1` (primary stress) and `0` (no stress) are supported. An error occurs if you specify secondary stress.

You must place a syllable stress marker within a syllable boundary but always to the left of the syllable's vowel. You can place a marker anywhere to the left of the stressed vowel. For example, each of the following SPR examples places the primary stress on the correct vowel of the word *construction*:

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

## Speech sound symbols

Each language uses its own inventory of SPR symbols to represent the speech sounds of that language. The following rules apply to specifying an SPR symbol:

-   Letters are case-sensitive, so `e` and `E`, for example, represent two different sounds.
-   Two- and three-character symbols must be contained in single quotes; for example, the symbol `aj` in the German word *heim*: `"h'aj'm"`.
-   The service considers invalid any SPR definition that contains sound symbols that are not allowed in a language.

Also consider the following when defining a word's pronunciation in SPR format:

-   The sounds of every language have specific distributional patterns within that language. For example, in all dialects of English, the sound `G` in *sing* (`".1sIG"`) does not occur at the beginning of a word. Other US English sounds that have a particularly narrow distribution are the glottal stop (`?`), the flap (`F`), and the syllabic nasal (`N`). If you enter a sound symbol in a context in which it does not normally occur, the resulting speech might sound unnatural.
-   The {{site.data.keyword.texttospeechshort}} service applies a sophisticated set of linguistic rules to its input to reflect the processes by which sounds change in specific contexts in natural language. For example, in US English, the sound `t` of the word *write* (`".1r1Yt"`) is pronounced as a flap (`F`) in *writer* (`".1rY.0FR"`). SPR input undergoes these modifications just as ordinary input text does. In this example, whether you enter `".1rY.0tR"` or `".1rY.0FR"` does not affect the speech that is generated.

## Working with IPA
{: #ipa}

The following information applies to working with pronunciations in IPA notation:

-   Use only the documented IPA symbols. When several IPA symbols (or symbol combinations) are listed for an SPR symbol, all are equivalent to the single SPR symbol. In this case, the service treats all of these IPA symbols the same and does not realize the subtle or regional differences that the IPA system is meant to describe.
-   You can also specify IPA pronunciations as IPA Unicode values. The language-specific tables listed in the following section document both the IPA symbols and their equivalent IPA Unicode values. For an example pronunciation that uses IPA Unicode values, see [The phoneme element](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element).

To learn more, see the following:

-   For more information about IPA, see [wikipedia.org/wiki/International_Phonetic_Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}.
-   For more information about phonetic symbols for Unicode, see [wikipedia.org/wiki/Phonetic_symbols_in_Unicode](https://wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: external}.

## Supported languages
{: #supportedLanguages}

The following pages document the SPR symbols, IPA symbols, and equivalent IPA Unicode values for each language. They show examples of each symbol in words from the language. Because of dialectal differences, the examples might not always match your pronunciation.

-   [Brazilian Portuguese symbols](/docs/services/text-to-speech?topic=text-to-speech-ptSymbols)
-   [British English symbols](/docs/services/text-to-speech?topic=text-to-speech-gbSymbols)
-   [French symbols](/docs/services/text-to-speech?topic=text-to-speech-frSymbols)
-   [German symbols](/docs/services/text-to-speech?topic=text-to-speech-deSymbols)
-   [Italian symbols](/docs/services/text-to-speech?topic=text-to-speech-itSymbols)
-   [Japanese symbols](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols)
-   [Spanish symbols](/docs/services/text-to-speech?topic=text-to-speech-esSymbols)
-   [US English symbols](/docs/services/text-to-speech?topic=text-to-speech-usSymbols)
