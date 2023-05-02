---

copyright:
  years: 2015, 2023
lastupdated: "2023-04-29"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Understanding phonetic symbols
{: #symbols}

All languages and voices of the {{site.data.keyword.texttospeechfull}} service support both the standard International Phonetic Alphabet (IPA) and {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) notations to represent the sounds of words. Both notations provide phonetic encoding that represents the pronunciation of a word, the sounds that make up the word, how the sounds are divided into syllables, and which syllables are stressed. [Phonetic symbols for supported languages](#supportedLanguages) provides links to topics that document the phonetic symbols for each language.
{: shortdesc}

## Defining a word pronunciation
{: #define-pronunciation}

To define the phonetic pronunciation for a word, either within input text or for a custom model, you use the `<phoneme>` element of the Speech Synthesis Markup Language (SSML) or equivalent method parameters. The `<phoneme>` element has two attributes:

-   The `alphabet` attribute specifies the notation of the pronunciation. Use the value `ibm` to indicate that the pronunciation is defined in SPR. Use the value `ipa` to indicate that the pronunciation is defined in IPA.
-   The `ph` attribute defines the pronunciation. It consists of a sequence of allowable symbols for a given language. The symbols define how the word that is enclosed in the `<phoneme>` element is to be pronounced.

Follow these rules when you define a pronunciation:

-   Use only the documented SPR or IPA symbols. The service considers invalid any definition that contains phonetic symbols that are not allowed in a language. An SPR or IPA entry that does not conform to the required specification is invalid.
-   When multiple IPA symbols (or symbol combinations) are documented for an SPR symbol, all of the IPA symbols are equivalent to the single SPR symbol. The service treats all of these IPA symbols the same and does not realize the subtle or regional differences that IPA is meant to describe.

For more information, see

-   [The phoneme element](/docs/text-to-speech?topic=text-to-speech-elements#phoneme_element)
-   [Rules for creating custom entries](/docs/text-to-speech?topic=text-to-speech-rules)
-   [Creating and managing custom entries](/docs/text-to-speech?topic=text-to-speech-customWords)

## Working with IBM SPR
{: #intro-SPRs}

IBM SPR is an alternative representation to standard IPA. The following examples of valid SPR notations define the words *through* and *shocking* in US English:

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

In the definitions, the letters represent specific sounds of US English speech. A `.` signals the beginning of a new syllable, and the digits `1` and `0` indicate syllable stress. For more information, see [Specifying syllables](#syllables).

### Speech sound symbols
{: #intro-SPRs-symbols}

Each language uses its own inventory of SPR symbols to represent the speech sounds of that language. The following rules apply to specifying an SPR symbol:

-   Letters are case-sensitive, so `e` and `E`, for example, represent two different sounds.
-   Two- and three-character symbols must be enclosed in single quotes when indicated in the symbol tables. The single quotes indicate that the multiple characters are actually a single symbol. For example, the symbol `'aj'` in the German word *heim* is specified as `"h'aj'm"`.
-   Some three-character symbols include single quotes around only two of the characters. The single quotes indicate that the two characters are a single symbol. So the SPR consists of two symbols. For example, the symbol `'a:'n` in the Netherlands Dutch word **dependances** contains two symbols, `'a:'` and `n`, and is specified as `d'e:'.pEn.1d'a:'n.s@s`.

Also consider the following when defining a word's pronunciation in SPR format:

-   The sounds of every language have specific distributional patterns within that language. For example, in all dialects of English, the sound `G` in *sing* (`".1sIG"`) does not occur at the beginning of a word. Other US English sounds that have a particularly narrow distribution are the glottal stop (`?`), the flap (`F`), and the syllabic nasal (`N`). If you enter a sound symbol in a context in which it does not normally occur, the resulting speech might sound unnatural.
-   The service applies a sophisticated set of linguistic rules to its input to reflect the processes by which sounds change in specific contexts in natural language. For example, in US English, the sound `t` of the word *write* (`".1r1Yt"`) is pronounced as a flap (`F`) in *writer* (`".1rY.0FR"`). SPR input undergoes these modifications just as ordinary input text does. In this example, whether you enter `".1rY.0tR"` or `".1rY.0FR"` does not affect the speech that is generated.

## Working with IPA
{: #intro-ipa}

You can define IPA pronunciations by using phonetic symbols or Unicode values. The following are examples of valid IPA notations for the word *tomato* in phonetic symbols and Unicode:

```xml
<phoneme alphabet="ipa" ph="təˈmeɪ.ɾoʊ">tomato</phoneme>
<phoneme alphabet="ipa" ph="t&#x0259;&#x02C8;me&#x026A;.&#x027E;o&#x028A;">tomato</phoneme>
```
{: codeblock}

IPA is an industry standard notation. For more information, see the following pages:

-   For more information about IPA, see [International Phonetic Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}.
-   For more information about phonetic symbols for Unicode, see [Phonetic symbols in Unicode](https://wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: external}.

## Specifying syllables
{: #syllables}

You can specify syllable boundaries and stress in both SPR and IPA.

### Syllable boundaries
{: #syllables-boundaries}

You can use a `.` (period, IPA Unicode `002E`) to mark the beginning of each syllable in SPR or IPA. However, to preserve the valid phonetics of a language, the service can elect not to honor periods in some cases (for example, if a syllable boundary is placed at an illegal or unnatural position for a language). In general, in cases where you can indicate a valid preference for a syllable boundary or other aspect of a word's pronunciation, the service honors such requests.

### Syllable stress
{: #syllables-stress}

Table 1 identifies the symbols that you can use to indicate syllable stress for a pronunciation. {{site.data.keyword.IBM_notm}} recommends that you indicate primary stress for pronunciations in either SPR or IPA. However, indicating syllable stress is optional for both formats; the service determines where stress occurs if you do not indicate it.

| Stress | SPR symbol | IPA symbol | IPA Unicode |
|---------|:----------:|:----------:|:-----------:|
| Primary stress | `1` | `ˈ` | `02C8` |
| Secondary stress | `2` | `ˌ` | `02CC` |
| No stress | `0` | No symbol | No value |
{: caption="Table 1. Syllable stress"}

You must place a syllable stress marker within a syllable boundary but always to the left of the syllable's vowel. You can place a marker anywhere to the left of the stressed vowel. For example, each of the following SPR examples places the primary stress (`1`) on the correct vowel of the word *construction*:

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

### Language-specific rules for using syllable stress
{: #syllables-languages}

Table 2 lists language-specific considerations that apply to specifying syllable stress. Unless the table qualifies the rules for a language, you can use the syllable stress symbols described in the previous section.

| Language | Notation | Language-specific rules |
|:--------:|:--------:|-------------------------|
| French and  \n Canadian French | SPR | All syllable stress symbols are honored. But syllable stress must immediately precede the vowel of the syllable. Syllable stress for French is much stricter than for other languages. An error occurs if you place the stress symbol in an invalid location. |
| French and  \n Canadian French  | IPA | All syllable stress symbols are ignored. |
| Italian | SPR and IPA | You can specify only `1` (primary stress). An error occurs if you specify secondary or no stress. |
| Japanese | SPR and IPA | You can specify only `1` (primary stress) and `0` (no stress). An error occurs if you specify secondary stress. |
| Spanish | SPR and IPA | You can specify only `1` (primary stress). An error occurs if you specify secondary or no stress. |
{: caption="Table 2. Language-specific rules for using syllable stress"}

## Phonetic symbols for supported languages
{: #supportedLanguages}
{: help}
{: support}

Table 3 lists the languages that the service supports and provides links to topics that describe their SPR symbols, IPA symbols, and IPA Unicode values. The topics provide examples of each symbol in words from the language. Because of dialectal differences, the examples might not always match your pronunciation.

The *Availability* column indicates whether each voice is available for [IBM Cloud]{: tag-ibm-cloud}, [IBM Cloud Pak for Data]{: tag-cp4d}, or both (*All versions*). For more information about the supported voices, see [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices).

| Language | Availability |
|----------|:------------:|
| [Dutch (Netherlands) symbols](/docs/text-to-speech?topic=text-to-speech-nlSymbols-new) | All versions |
| [English (Australian) symbols](/docs/text-to-speech?topic=text-to-speech-auSymbols-new) | All versions |
| [English (United Kingdom) symbols](/docs/text-to-speech?topic=text-to-speech-gbSymbols) | All versions |
| [English (United States) symbols](/docs/text-to-speech?topic=text-to-speech-usSymbols) | All versions |
| [French (Canadian) symbols](/docs/text-to-speech?topic=text-to-speech-caSymbols) | All versions |
| [French (France) symbols](/docs/text-to-speech?topic=text-to-speech-frSymbols) | All versions |
| [German symbols](/docs/text-to-speech?topic=text-to-speech-deSymbols) | All versions |
| [Italian symbols](/docs/text-to-speech?topic=text-to-speech-itSymbols) | All versions |
| [Japanese symbols](/docs/text-to-speech?topic=text-to-speech-jaSymbols) | All versions |
| [Korean symbols](/docs/text-to-speech?topic=text-to-speech-koSymbols-new) | All versions |
| [Portuguese (Brazilian) symbols](/docs/text-to-speech?topic=text-to-speech-ptSymbols) | All versions |
| [Spanish symbols](/docs/text-to-speech?topic=text-to-speech-esSymbols) | All versions |
{: caption="Table 3. Phonetic symbols for supported languages"}
