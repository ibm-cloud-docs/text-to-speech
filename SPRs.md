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

### Syllable boundaries

You can use a `.` (period) to mark the beginning of each syllable. However, to preserve the valid phonetics of a language, the service can elect not to honor periods in some cases (for example, if a syllable boundary is placed at an illegal or unnatural position for a language). In general, in cases where the user can indicate a valid preference for a syllable boundary or other aspect of a word's pronunciation, the service honors such requests.

### Syllable stress

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

### Speech sound symbols

Each language uses its own inventory of SPR symbols to represent the speech sounds of that language. Tables in the following sections show the valid SPR symbols for the sounds of each language, with examples of words in which each sound occurs. Letters are case-sensitive, so `e` and `E`, for example, represent two different sounds. Two- and three-character symbols must be contained in single quotes (for example, the symbol `aj` in the German word *heim*: `"h'aj'm"`). The service considers invalid any SPR that contains sound symbols that are not allowed in a language.

The sounds of every language have specific distributional patterns within that language. For example, in all dialects of English, the sound `G` in *sing* (`".1sIG"`) does not occur at the beginning of a word. Other US English sounds that have a particularly narrow distribution are the glottal stop (`?`), the flap (`F`), and the syllabic nasal (`N`). If you enter a sound symbol in a context in which it does not normally occur, the resulting speech might sound unnatural.

The {{site.data.keyword.texttospeechshort}} service applies a sophisticated set of linguistic rules to its input to reflect the processes by which sounds change in specific contexts in natural language. For example, in US English, the sound `t` of the word *write* (`".1r1Yt"`) is pronounced as a flap (`F`) in *writer* (`".1rY.0FR"`). SPR input undergoes these modifications just as ordinary input text does. In this example, whether you enter `".1rY.0tR"` or `".1rY.0FR"` does not affect the speech that is generated.

## US English symbols
{: #usSymbols}

The following sections describe the inventory of valid symbols for US English.

### Regular vowels (US English)

<table style="width:90%">
  <caption>Table 2. Regular vowels (US English)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      US English<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      a<br/><br/>
      &#97;&#720;<br/><br/>
      &#593;<br/><br/>
      &#593;&#720;<br/><br/>
      &#592;
    </td>
    <td style="text-align:center">
      0061<br/><br/>
      0061+02D0<br/><br/>
      0251<br/><br/>
      0251+02D0<br/><br/>
      0250
    </td>
    <td>
      f<u>a</u>ther, l<u>o</u>t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      A
    </td>
    <td style="text-align:center">
      &#230;
    </td>
    <td style="text-align:center">
      00E6
    </td>
    <td>b<u>a</u>ck, h<u>a</u>d
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      e<br/><br/>
      &#101;&#618;
    </td>
    <td style="text-align:center">
      0065<br/><br/>
      0065+026A
    </td>
    <td>
      c<u>a</u>ke, p<u>ai</u>n
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      E
    </td>
    <td style="text-align:center">
      &#603;
    </td>
    <td style="text-align:center">
      025B
    </td>
    <td>
      h<u>e</u>dge, l<u>e</u>t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      i<br/><br/>
      &#105;&#720;
    </td>
    <td style="text-align:center">
      0069<br/><br/>
      0069+02D0
    </td>
    <td>
      s<u>ee</u>, sp<u>ea</u>k, bel<u>ie</u>ve
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      I
    </td>
    <td style="text-align:center">
      &#618;
    </td>
    <td style="text-align:center">
      026A
    </td>
    <td>
      p<u>i</u>ck, <u>i</u>ll
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      o<br/><br/>
      &#111;&#650;
    </td>
    <td style="text-align:center">
      006F<br/><br/>
      006F+028A
    </td>
    <td>
      b<u>o</u>th, <u>o</u>ak
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      c
    </td>
    <td style="text-align:center">
      &#596;<br/><br/>
      &#596;&#720;<br/><br/>
      &#594;
    </td>
    <td style="text-align:center">
      0254<br/><br/>
      0254+02D0<br/><br/>
      0252
    </td>
    <td>
      l<u>a</u>w, c<u>ou</u>gh
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      u<br/><br/>
      &#117;&#720;
    </td>
    <td style="text-align:center">
      0075<br/><br/>
      0075+02D0
    </td>
    <td>
      z<u>oo</u>, tr<u>u</u>th
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      U
    </td>
    <td style="text-align:center">
      &#650;<br/><br/>
      &#623;
    </td>
    <td style="text-align:center">
      028A<br/><br/>
      026F
    </td>
    <td>
      t<u>oo</u>k, p<u>u</u>t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      H
    </td>
    <td style="text-align:center">
      &#652;
    </td>
    <td style="text-align:center">
      028C
    </td>
    <td>
      b<u>u</u>t, m<u>u</u>g, s<u>o</u>n
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      R
    </td>
    <td style="text-align:center">
      &#601;&#734;<br/><br/>
      &#602;<br/><br/>
      &#604;&#720;<br/><br/>
      &#605;
    </td>
    <td style="text-align:center">
      0259+02DE<br/><br/>
      025A<br/><br/>
      025C+02D0<br/><br/>
      025D
    </td>
    <td>
      butt<u>er</u>, h<u>ur</u>t
    </td>
  </tr>
</table>

### Diphthongs (US English)

<table style="width:90%">
  <caption>Table 3. Diphthongs (US English)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      US English<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      O
    </td>
    <td style="text-align:center">
      &#596;&#618;
    </td>
    <td style="text-align:center">
      0254+026A
    </td>
    <td>
      t<u>oi</u>l, b<u>oy</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      W
    </td>
    <td style="text-align:center">
      &#97;&#650;
    </td>
    <td style="text-align:center">
      0061+028A
    </td>
    <td>
      <u>ou</u>t, c<u>ow</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Y
    </td>
    <td style="text-align:center">
      &#97;&#618;
    </td>
    <td style="text-align:center">
      0061+026A
    </td>
    <td>
      l<u>i</u>fe, f<u>i</u>ne
    </td>
  </tr>
</table>

### Reduced vowels (US English)

<table style="width:90%">
  <caption>Table 4. Reduced vowels (US English)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      US English<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      x
    </td>
    <td style="text-align:center">
      &#601;
    </td>
    <td style="text-align:center">
      0259
    </td>
    <td>
      sof<u>a</u>, <u>a</u>lone, s<u>u</u>ppose, tedi<u>ou</u>s,
      <u>A</u>meric<u>a</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      X
    </td>
    <td style="text-align:center">
      &#616;<br/><br/>
      &#305;
    </td>
    <td style="text-align:center">
      0268<br/><br/>
      0131
    </td>
    <td>
      ros<u>e</u>s, c<u>o</u>nnect, mel<u>o</u>dy, symph<u>o</u>ny,
      hint<u>e</u>d
    </td>
  </tr>
</table>

### Consonants (US English)

<table style="width:90%">
  <caption>Table 5. Consonants (US English)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      US English<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
        0062
    </td>
    <td>
      <u>b</u>ad, so<u>b</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      0070
    </td>
    <td>
      <u>p</u>it, ri<u>p</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      0064
    </td>
    <td>
      <u>d</u>ip, ha<u>d</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      0074
    </td>
    <td>
      <u>t</u>ip, pe<u>t</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      g<br/><br/>
      &#609;
    </td>
    <td style="text-align:center">
      0067<br/><br/>
      0261
    </td>
    <td>
      <u>g</u>ood, bu<u>g</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      006B
    </td>
    <td>
      <u>k</u>ill, <u>c</u>at, ma<u>k</u>e, ba<u>ck</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      D
    </td>
    <td style="text-align:center">
      &#240;
    </td>
    <td style="text-align:center">
      00F0
    </td>
    <td>
      <u>th</u>is, brea<u>th</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      T
    </td>
    <td style="text-align:center">
      &#952;
    </td>
    <td style="text-align:center">
      03B8
    </td>
    <td>
      <u>th</u>ing, Be<u>th</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      0076
    </td>
    <td>
      <u>v</u>ase, sa<u>v</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      0066
    </td>
    <td>
      <u>f</u>ield, i<u>f</u>, gra<u>ph</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      007A
    </td>
    <td>
      <u>z</u>ip, pha<u>s</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      0073
    </td>
    <td>
      <u>s</u>eal, mi<u>ss</u>, <u>c</u>eiling
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Z
    </td>
    <td style="text-align:center">
      &#658;
    </td>
    <td style="text-align:center">
      0292
    </td>
    <td>
      trea<u>s</u>ure, gara<u>g</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      S
    </td>
    <td style="text-align:center">
      &#643;
    </td>
    <td style="text-align:center">
      0283
    </td>
    <td>
      <u>sh</u>ip, wi<u>sh</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      J
    </td>
    <td style="text-align:center">
      &#100;&#658;<br/><br/>
      &#676;
    </td>
    <td style="text-align:center">
      0064+0292<br/><br/>
      02A4
    </td>
    <td>
      <u>J</u>ane, hu<u>g</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      C
    </td>
    <td style="text-align:center">
      &#116;&#643;<br/><br/>
      &#679;
    </td>
    <td style="text-align:center">
      0074+0283<br/><br/>
      02A7
    </td>
    <td>
      <u>ch</u>ip, wit<u>ch</u>, na<u>t</u>ure
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      h
    </td>
    <td style="text-align:center">
      h<br/><br/>
      &#614;<br/><br/>
      x<br/><br/>
      &#967;
    </td>
    <td style="text-align:center">
      0068<br/><br/>
      0266<br/><br/>
      0078<br/><br/>
      03C7
    </td>
    <td>
      <u>h</u>ot, <u>h</u>ero, <u>ch</u>allah
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      006D
    </td>
    <td>
      <u>m</u>an, hu<u>m</u>, su<u>mm</u>er
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      006E
    </td>
    <td>
      <u>n</u>ever, su<u>n</u>, wi<u>nn</u>er
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      G
    </td>
    <td style="text-align:center">
      &#331;
    </td>
    <td style="text-align:center">
      014B
    </td>
    <td>
      si<u>ng</u>, fi<u>ng</u>er
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      r
    </td>
    <td style="text-align:center">
      r<br/><br/>
      &#633;
    </td>
    <td style="text-align:center">
      0072<br/><br/>
      0279
    </td>
    <td>
      bo<u>rr</u>ow, <u>r</u>ake
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      006C
    </td>
    <td>
      <u>l</u>ow, ha<u>ll</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      w<br/><br/>
      &#653;
    </td>
    <td style="text-align:center">
      0077<br/><br/>
      028D
    </td>
    <td>
      <u>w</u>ear, q<u>ui</u>ck
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      y
    </td>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      006A
    </td>
    <td>
      <u>y</u>es, Virgin<u>i</u>a
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      M
    </td>
    <td style="text-align:center">
      &#109;&#809;
    </td>
    <td style="text-align:center">
      006D+0329
    </td>
    <td>
      h<u>mmm</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      ? (glottal stop)
    </td>
    <td style="text-align:center">
      &#660;
    </td>
    <td style="text-align:center">
      0294
    </td>
    <td>
      ki<u>tt</u>en, La<u>t</u>in
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      F (flap)
    </td>
    <td style="text-align:center">
      &#638;
    </td>
    <td style="text-align:center">
      027E
    </td>
    <td>
      wri<u>t</u>er, fi<u>dd</u>le
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      N (syllabic nasal)
    </td>
    <td style="text-align:center">
      &#110;&#809;
    </td>
    <td style="text-align:center">
      006E+0329
    </td>
    <td>
      butt<u>on</u>, sat<u>in</u>, eat<u>en</u>, burd<u>en</u>
    </td>
  </tr>
</table>

## British English symbols
{: #gbSymbols}

The following sections describe the inventory of valid symbols for British English.

### Regular vowels (British English)

<table style="width:90%">
  <caption>Table 6. Regular vowels (British English)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      British English<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      a<br/><br/>
      &#97;&#720;<br/><br/>
      &#593;<br/><br/>
      &#593;&#720;<br/><br/>
      &#592;
    </td>
    <td style="text-align:center">
      0061<br/><br/>
      0061+02D0<br/><br/>
      0251<br/><br/>
      0251+02D0<br/><br/>
      0250
    </td>
    <td>
      p<u>a</u>th, f<u>a</u>ther, ch<u>a</u>nt
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      A
    </td>
    <td style="text-align:center">
      &#230;
    </td>
    <td style="text-align:center">
      00E6
    </td>
    <td>
      b<u>a</u>ck, h<u>a</u>d
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      e<br/><br/>
      &#101;&#618;
    </td>
    <td style="text-align:center">
      0065<br/><br/>
      0065+026A
    </td>
    <td>
      c<u>a</u>ke, p<u>ai</u>n
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      E
    </td>
    <td style="text-align:center">
      &#603;
    </td>
    <td style="text-align:center">
      025B
    </td>
    <td>
      h<u>e</u>dge, l<u>e</u>t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      &#105;&#720;
    </td>
    <td style="text-align:center">
      0069+02D0
    </td>
    <td>
      s<u>ee</u>, sp<u>ea</u>k, bel<u>ie</u>ve
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      I
    </td>
    <td style="text-align:center">
      &#618;
    </td>
    <td style="text-align:center">
      026A
    </td>
    <td>
      p<u>i</u>ck, <u>i</u>ll
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      o<br/><br/>
      &#111;&#650;<br/><br/>
      &#601;&#650;
    </td>
    <td style="text-align:center">
      006F<br/><br/>
      006F+028A<br/><br/>
      0259+028A
    </td>
    <td>
      b<u>o</u>th, <u>oa</u>k
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      c
    </td>
    <td style="text-align:center">
      &#596;<br/><br/>
      &#596;&#720;
    </td>
    <td style="text-align:center">
      0254<br/><br/>
      0254+02D0
    </td>
    <td>
      l<u>a</u>w, c<u>ou</u>rt, h<u>a</u>ll, w<u>a</u>ter
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      @
    </td>
    <td style="text-align:center">
      &#594;
    </td>
    <td style="text-align:center">
      0252
    </td>
    <td>r<u>o</u>d, c<u>ou</u>gh
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      u<br/><br/>
      &#117;&#720;
    </td>
    <td style="text-align:center">
      0075<br/><br/>
      0075+02D0
    </td>
    <td>
      z<u>oo</u>, tr<u>u</u>th
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      U
    </td>
    <td style="text-align:center">
      &#650;
    </td>
    <td style="text-align:center">
      028A
    </td>
    <td>
      t<u>oo</u>k, p<u>u</u>t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      H
    </td>
    <td style="text-align:center">
      &#652;
    </td>
    <td style="text-align:center">
      028C
    </td>
    <td>
      b<u>u</u>t, m<u>u</u>g, s<u>o</u>n
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      R
    </td>
    <td style="text-align:center">
      &#604;<br/><br/>
      &#604;&#720;<br/><br/>
      &#602;<br/><br/>
      &#605;
    </td>
    <td style="text-align:center">
      025C<br/><br/>
      025C+02D0<br/><br/>
      025A<br/><br/>
      025D
    </td>
    <td>
      butt<u>er</u>, h<u>u</u>rt
    </td>
  </tr>
</table>

### Diphthongs (British English

<table style="width:90%">
  <caption>Table 7. Diphthongs (British English)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      British English<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      O
    </td>
    <td style="text-align:center">
      &#596;&#618;
    </td>
    <td style="text-align:center">
      0254+026A
    </td>
    <td>
      t<u>oi</u>l, b<u>oy</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      W
    </td>
    <td style="text-align:center">
      &#97;&#650;
    </td>
    <td style="text-align:center">
      0061+028A
    </td>
    <td>
      <u>ou</u>t, c<u>ow</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Y
    </td>
    <td style="text-align:center">
      &#97;&#618;
    </td>
    <td style="text-align:center">
      0061+026A
    </td>
    <td>
      l<u>i</u>fe, f<u>i</u>ne
    </td>
  </tr>
</table>

### Reduced vowels (Britsh English)

<table style="width:90%">
  <caption>Table 8. Reduced vowels (British English)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      British English<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      x
    </td>
    <td style="text-align:center">
      &#601;
    </td>
    <td style="text-align:center">
      0259
    </td>
    <td>
      sof<u>a</u>, <u>a</u>lone, s<u>u</u>ppose, <u>A</u>meric<u>a</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      X
    </td>
    <td style="text-align:center">
      i<br/><br/>
      &#616;
    </td>
    <td style="text-align:center">
      0069<br/><br/>
      0268
    </td>
    <td>
      ros<u>e</u>s, hint<u>e</u>d
    </td>
  </tr>
</table>

### Consonants (British English)

<table style="width:90%">
  <caption>Table 9. Consonants (British English)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      British English<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      0062
    </td>
    <td>
      <u>b</u>ad, so<u>b</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      0070
    </td>
    <td>
      <u>p</u>it, ri<u>p</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      0064
    </td>
    <td>
      <u>d</u>ip, ha<u>d</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      0074
    </td>
    <td>
      <u>t</u>ip, pe<u>t</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      g<br/><br/>
      &#609;
    </td>
    <td style="text-align:center">
      0067<br/><br/>
      0261
    </td>
    <td>
      <u>g</u>ood, bu<u>g</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      006B
    </td>
    <td>
      <u>k</u>ill, ma<u>k</u>e, ba<u>ck</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      D
    </td>
    <td style="text-align:center">
      &#240;
    </td>
    <td style="text-align:center">
      00F0
    </td>
    <td>
      <u>th</u>is, brea<u>th</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      T
    </td>
    <td style="text-align:center">
      &#952;
    </td>
    <td style="text-align:center">
      03B8
    </td>
    <td>
      <u>th</u>ing, Be<u>th</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      0076
    </td>
    <td>
      <u>v</u>ase, sa<u>v</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      0066
    </td>
    <td>
      <u>f</u>ield, i<u>f</u>, gra<u>ph</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      007A
    </td>
    <td>
      <u>z</u>ip, pha<u>s</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      0073
    </td>
    <td>
      <u>s</u>eal, mi<u>ss</u>, <u>c</u>eiling
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Z
    </td>
    <td style="text-align:center">
      &#658;
    </td>
    <td style="text-align:center">
      0292
    </td>
    <td>
      trea<u>s</u>ure, gara<u>g</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      S
    </td>
    <td style="text-align:center">
      &#643;
    </td>
    <td style="text-align:center">
      0283
    </td>
    <td>
      <u>sh</u>ip, wi<u>sh</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      J
    </td>
    <td style="text-align:center">
      &#100;&#658;<br/><br/>
      &#676;
    </td>
    <td style="text-align:center">
      0064+0292<br/><br/>
      02A4
    </td>
    <td>
      <u>J</u>ane, hu<u>g</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      C
    </td>
    <td style="text-align:center">
      &#116;&#643;<br/><br/>
      &#679;
    </td>
    <td style="text-align:center">
      0074+0283<br/><br/>
      02A7
    </td>
    <td>
      <u>ch</u>ip, wit<u>ch</u>, na<u>t</u>ure
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      h
    </td>
    <td style="text-align:center">
      h<br/><br/>
      x<br/><br/>
      &#967;<br/><br/>
      &#614;
    </td>
    <td style="text-align:center">
      0068<br/><br/>
      0078<br/><br/>
      03C7<br/><br/>
      0266
    </td>
    <td>
      <u>h</u>ot, <u>h</u>ero
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      006D
    </td>
    <td>
      <u>m</u>an, hu<u>m</u>, su<u>mm</u>er
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      006E
    </td>
    <td>
      <u>n</u>ever, su<u>n</u>, wi<u>nn</u>er
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      G
    </td>
    <td style="text-align:center">
      &#331;
    </td>
    <td style="text-align:center">
      014B
    </td>
    <td>
      si<u>ng</u>, fi<u>ng</u>er
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      r
    </td>
    <td style="text-align:center">
      r<br/><br/>
      &#633;<br/><br/>
      &#638;
    </td>
    <td style="text-align:center">
      0072<br/><br/>
      0279<br/><br/>
      027E
    </td>
    <td>
      bo<u>rr</u>ow, <u>r</u>ake
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      006C
    </td>
    <td>
      <u>l</u>ow, ha<u>ll</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      L
    </td>
    <td style="text-align:center">
      &#108;&#809;
    </td>
    <td style="text-align:center">
      006C+0329
    </td>
    <td>
      cand<u>l</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      0077
    </td>
    <td>
      <u>w</u>ear, q<u>u</u>ick
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      y
    </td>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      006A
    </td>
    <td>
      <u>y</u>es, Virgin<u>i</u>a
    </td>
  </tr>
</table>

## French symbols
{: #frSymbols}

The following sections describe the inventory of valid symbols for French.

### Vowels (French)

<table style="width:90%">
  <caption>Table 10. Vowels (French)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      French<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      a<br/><br/>
      &#593;<br/><br/>
      &#592;
    </td>
    <td style="text-align:center">
      0061<br/><br/>
      0251<br/><br/>
      0250
    </td>
    <td>
      p<u>a</u>ttes, l<u>a</u>c, c<u>a</u>ve
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      0065
    </td>
    <td>
      caf<u>&egrave;</u>, d<u>&egrave;</u>form<u>e</u>r,
      <u>&egrave;</u>t<u>&egrave;</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      E
    </td>
    <td style="text-align:center">
      &#603;<br/><br/>
      &#604;
    </td>
    <td style="text-align:center">
      025B<br/><br/>
      025C
    </td>
    <td>
      f<u>ai</u>te, m<u>ai</u>, h<u>e</u>rb
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      i<br/><br/>
      &#618;
    </td>
    <td style="text-align:center">
      0069<br/><br/>
      026A
    </td>
    <td>
      f<u>i</u>lm, t<u>y</u>p<u>i</u>que
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      006F
    </td>
    <td>
      <u>eau</u>, <u>au</u>x, g<u>au</u>che
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      c
    </td>
    <td style="text-align:center">
      &#596;<br/><br/>
      &#594;
    </td>
    <td style="text-align:center">
      0254<br/><br/>
      0252
    </td>
    <td>
      P<u>au</u>l, n<u>o</u>te, &egrave;chal<u>o</u>tte
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      u<br/><br/>
      &#650;
    </td>
    <td style="text-align:center">
      0075<br/><br/>
      028A
    </td>
    <td>
      r<u>ou</u>e, <u>o&ugrave;</u>, t<u>ou</u>r
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      y
    </td>
    <td style="text-align:center">
      &#121;<br/><br/>
      &#655;
    </td>
    <td style="text-align:center">
      0079<br/><br/>
      028F
    </td>
    <td>
      <u>u</u>tile, p<u>u</u>re, Br<u>u</u>no
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      x [<strong>1</strong>]
    </td>
    <td style="text-align:center">
      &#601;
    </td>
    <td style="text-align:center">
      0259
    </td>
    <td>
      litr<u>e</u>s, marbr<u>e</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'eu'
    </td>
    <td style="text-align:center">
      &#248;<br/><br/>
      &#629;
    </td>
    <td style="text-align:center">
      00F8<br/><br/>
      0275
    </td>
    <td>
      m<u>eu</u>gle, p<u>eu</u>, joy<u>eu</u>x
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'oe'
    </td>
    <td style="text-align:center">
      &#339;<br/><br/>
      &#630;
    </td>
    <td style="text-align:center">
      0153<br/><br/>
      0276
    </td>
    <td>
      p<u>eu</u>r, c<u>oeu</u>r, j<u>eu</u>ne
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'a~'
    </td>
    <td style="text-align:center">
      &#97;&#771;<br/><br/>
      &#593;&#771;
    </td>
    <td style="text-align:center">
      0061+0303<br/><br/>
      0251+0303
    </td>
    <td>
      b<u>an</u>c, <u>en</u>, t<u>em</u>ps
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'E~'
    </td>
    <td style="text-align:center">
      &#101;&#771;<br/><br/>
      &#603;&#771;<br/><br/>
      &#230;&#771;
    </td>
    <td style="text-align:center">
      0065+0303<br/><br/>
      025B+0303<br/><br/>
      00E6+0303
    </td>
    <td>
      f<u>i</u>n, pl<u>e</u>in, f<u>ai</u>m
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'o~'
    </td>
    <td style="text-align:center">
      &#111;&#771;<br/><br/>
      &#596;&#771;
    </td>
    <td style="text-align:center">
      006F+0303<br/><br/>
      0254+0303
    </td>
    <td>
      b<u>on</u>, p<u>on</u>t, m<u>on</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'oe~'
    </td>
    <td style="text-align:center">
      &#339;&#771;
    </td>
    <td style="text-align:center">
      0153+0303
    </td>
    <td>
      <u>un</u>, auc<u>un</u>, br<u>un</u>
    </td>
  </tr>
</table>

**Note:**

1.  The `x` is elided in certain contexts.

### Consonants (French)

<table style="width:90%">
  <caption>Table 11. Consonants (French)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      French<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      0062
    </td>
    <td>
      <u>b</u>&egrave;<u>b</u>&egrave;, <u>b</u>alle, ro<u>b</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      0070
    </td>
    <td>
      <u>p</u>orte, <u>p</u>r&ecirc;t, gu&ecirc;<u>p</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      0064
    </td>
    <td>
      <u>d</u>ort, <u>d</u>olmen
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      0074
    </td>
    <td>
      <u>t</u>on, pa<u>tt</u>e, th&egrave;&acirc;<u>t</u>re
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      g<br/><br/>
      &#609;
    </td>
    <td style="text-align:center">
      0067<br/><br/>
      0261
    </td>
    <td>
      <u>gu</u>erre, ba<u>gu</u>e, <u>g</u>arer
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      006B
    </td>
    <td>
      <u>k</u>ilo, <u>c</u>aler, <u>qu</u>ai
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      0076
    </td>
    <td>
      la<u>v</u>er, <u>w</u>agon, <u>v</u>isiter
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      0066
    </td>
    <td>
      che<u>f</u>, <u>f</u>aim, <u>ph</u>are
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      007A
    </td>
    <td>
      ja<u>s</u>er, r&egrave;<u>s</u>eau, <u>z</u>ig<u>z</u>aguer
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      0073
    </td>
    <td>
      <u>s</u>ans, ambi<u>t</u>ion, fa<u>&ccedil;</u>on
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Z
    </td>
    <td style="text-align:center">
      &#658;
    </td>
    <td style="text-align:center">
      0292
    </td>
    <td>
      ra<u>g</u>e, <u>g</u>&icirc;te, <u>j</u>ouer
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      S
    </td>
    <td style="text-align:center">
      &#643;
    </td>
    <td style="text-align:center">
      0283
    </td>
    <td>
      <u>ch</u>eval, l&acirc;<u>ch</u>e, <u>sch</u>&egrave;ma
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      006D
    </td>
    <td>
      <u>m</u>a<u>m</u>an, fe<u>mm</u>e, <u>m</u>iser
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      006E
    </td>
    <td>
      A<u>nn</u>e, <u>n</u>i, ma<u>n</u>iaque
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'nj'
    </td>
    <td style="text-align:center">
      &#626;
    </td>
    <td style="text-align:center">
      0272
    </td>
    <td>
      a<u>gn</u>eau, campa<u>gn</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'ng'
    </td>
    <td style="text-align:center">
      &#331;
    </td>
    <td style="text-align:center">
      014B
    </td>
    <td>
      parki<u>ng</u>, campi<u>ng</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      r
    </td>
    <td style="text-align:center">
      r<br/><br/>
      &#633;<br/><br/>
      &#640;<br/><br/>
      &#641;<br/><br/>
      x<br/><br/>
      &#967;
    </td>
    <td style="text-align:center">
      0072<br/><br/>
      0279<br/><br/>
      0280<br/><br/>
      0281<br/><br/>
      0078<br/><br/>
      03C7
    </td>
    <td>
      pa<u>r</u>er, <u>r</u>a<u>r</u>e, ca<u>rr</u>eau
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      006C
    </td>
    <td>
      <u>l</u>itre, i<u>ll</u>isible, p&acirc;<u>l</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      j<br/><br/>
      &#654;
    </td>
    <td style="text-align:center">
      006A<br/><br/>
      028E
    </td>
    <td>
      h<u>i</u>&egrave;rarchie, pa<u>ill</u>e, <u>y</u>oga
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      0077
    </td>
    <td>
      <u>ou</u>i, b<u>ou</u>&egrave;e, <u>w</u>att
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      H
    </td>
    <td style="text-align:center">
      &#613;
    </td>
    <td style="text-align:center">
      0265
    </td>
    <td>
      s<u>u</u>is, l<u>u</u>i, n<u>u</u>&egrave;e
    </td>
  </tr>
</table>

### Liaison (French)

In French, the `_` (underscore) can be used following a word-final consonant (but within the double-quotes that enclose the SPR) to indicate that it is a liaison consonant. A liaison consonant is pronounced only if the following word begins with a vowel.

<table style="width:54%">
  <caption>Table 12. Liaison (French)</caption>
  <tr>
    <th style="width:33%; text-align:center; vertical-align:bottom">
      French<br/>SPR symbol
    </th>
    <th style="width:33%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:34%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      _
    </td>
    <td style="text-align:center">
      &#8255;
    </td>
    <td style="text-align:center">
      0203F
    </td>
  </tr>
</table>

Examples of words with and without the liaison symbol follow:

-   `"p0'oe't1it_"`: The `t` is pronounced only if the following word begins with a vowel.
-   `"nEt"`: The `t` is always pronounced.

A dictionary entry *petit* with the translation value `"p'oe't1it_"` has the final `t` pronounced in the input string *un petit ami* but not in the input string *un petit chien*. An entry with the translation value `"nEt"` has the final `t` pronounced regardless of context.

## German symbols
{: #deSymbols}

The following sections describe the inventory of valid symbols for German.

### Regular vowels (German)

<table style="width:90%">
  <caption>Table 13. Regular vowels (German)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      German<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      i<br/><br/>
      &#105;&#720;
    </td>
    <td style="text-align:center">
      0069<br/><br/>
      0069+02D0
    </td>
    <td>
      l<u>ie</u>ben, T<u>i</u>tel, t<u>ie</u>f
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      I
    </td>
    <td style="text-align:center">
      &#618;
    </td>
    <td style="text-align:center">
      026A
    </td>
    <td>
      b<u>i</u>tte, T<u>i</u>sch, L<u>i</u>cht
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      e<br/><br/>
      &#101;&#720;
    </td>
    <td style="text-align:center">
      0065<br/><br/>
      0065+02D0
    </td>
    <td>
      g<u>e</u>ben, <u>Eh</u>re, S<u>ee</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      E
    </td>
    <td style="text-align:center">
      &#603;
    </td>
    <td style="text-align:center">
      025B
    </td>
    <td>
      tr<u>e</u>ffen, G<u>e</u>ld, k<u>&auml;</u>mmen
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'E:'
    </td>
    <td style="text-align:center">
      &#603;&#720;
    </td>
    <td style="text-align:center">
      025B+02D0
    </td>
    <td>
      K<u>&auml;</u>se, M<u>&auml;</u>dchen, w<u>&auml;</u>gen
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      &#97;&#720;<br/><br/>
      &#593;
    </td>
    <td style="text-align:center">
      0061+02D0<br/><br/>
      0251
    </td>
    <td>
      H<u>aa</u>r, h<u>a</u>ben, f<u>a</u>hren
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      A
    </td>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      0061
    </td>
    <td>
      l<u>a</u>ssen, m<u>a</u>tt, <u>A</u>pfel
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      u<br/><br/>
      &#117;&#720;
    </td>
    <td style="text-align:center">
      0075<br/><br/>
      0075+02D0
    </td>
    <td>
      g<u>u</u>t, <u>Uh</u>r, <u>U</u>we
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      U
    </td>
    <td style="text-align:center">
      &#650;
    </td>
    <td style="text-align:center">
      028A
    </td>
    <td>
      H<u>u</u>nd, Fl<u>u</u>ss, M<u>u</u>tter
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      o<br/><br/>
      &#111;&#720;
    </td>
    <td style="text-align:center">
      006F<br/><br/>
      006F+02D0
    </td>
    <td>
      <u>O</u>ber, <u>oh</u>ne, B<u>oo</u>t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      O
    </td>
    <td style="text-align:center">
      &#596;
    </td>
    <td style="text-align:center">
      0254
    </td>
    <td>
      K<u>o</u>pf, St<u>o</u>pp
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      y
    </td>
    <td style="text-align:center">
      y<br/><br/>
      &#121;&#720;
    </td>
    <td style="text-align:center">
      0079<br/><br/>
      0079+02D0
    </td>
    <td>
      B<u>&uuml;</u>cher, f<u>&uuml;h</u>len, T<u>&uuml;</u>r,
      k<u>&uuml;</u>hn
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Y
    </td>
    <td style="text-align:center">
      &#655;
    </td>
    <td style="text-align:center">
      028F
    </td>
    <td>
      f<u>&uuml;</u>nf, f<u>&uuml;</u>llen, K<u>&uuml;</u>nstler
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'oe'
    </td>
    <td style="text-align:center">
      &#248;<br/><br/>
      &#248;&#720;
    </td>
    <td style="text-align:center">
      00F8<br/><br/>
      00F8+02D0
    </td>
    <td>
      L<u>&ouml;</u>we, h<u>&ouml;</u>ren, S<u>&ouml;h</u>ne
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'OE'
    </td>
    <td style="text-align:center">
      &#339;<br/><br/>
      &#630;
    </td>
    <td style="text-align:center">
      0153<br/><br/>
      0276
    </td>
    <td>
      k<u>&ouml;</u>nnen, h<u>&ouml;</u>lzern, <u>&ouml;</u>stlich
    </td>
  </tr>
</table>

### Reduced vowels (German)

<table style="width:90%">
  <caption>Table 14. Reduced vowels (German)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      German<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      @
    </td>
    <td style="text-align:center">
      &#601;<br/><br/>
      &#629;<br/><br/>
      &#600;
    </td>
    <td style="text-align:center">
      0259<br/><br/>
      0275<br/><br/>
      0258
    </td>
    <td>
      bitt<u>e</u>, Kam<u>e</u>ra, Bod<u>e</u>n
    </td>
  </tr>
</table>

### Diphthongs (German)

<table style="width:90%">
  <caption>Table 15. Diphthongs (German)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      German<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      'aj'
    </td>
    <td style="text-align:center">
      &#97;&#105;<br/><br/>
      &#97;&#618;
    </td>
    <td style="text-align:center">
      0061+0069<br/><br/>
      0061+026A
    </td>
    <td>
      h<u>ei</u>m, W<u>ai</u>se, M<u>ai</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'aw'
    </td>
    <td style="text-align:center">
      &#97;&#117;<br/><br/>
      &#97;&#650;
    </td>
    <td style="text-align:center">
      0061+0075<br/><br/>
      0061+028A
    </td>
    <td>
      H<u>au</u>s, M<u>au</u>l, Fr<u>au</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'oj'
    </td>
    <td style="text-align:center">
      &#596;&#105;<br/><br/>
      &#596;&#121;<br/><br/>
      &#596;&#618;<br/><br/>
      &#596;&#655;
    </td>
    <td style="text-align:center">
      0254+0069<br/><br/>
      0254+0079<br/><br/>
      0254+026A<br/><br/>
      0254+028F
    </td>
    <td>
      h<u>eu</u>te, Geb<u>&auml;u</u>de, H<u>&auml;u</u>ser
    </td>
  </tr>
</table>

### Nasalized vowels (German)

Nasalized vowels in French occur mostly in foreign loan words.

<table style="width:90%">
  <caption>Table 16. Nasalized vowels (German)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      German<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      'a~'
    </td>
    <td style="text-align:center">
      &#97;&#771;<br/><br/>
      &#592;&#771;
    </td>
    <td style="text-align:center">
      0061+0303<br/><br/>
      0250+0303
    </td>
    <td>
      Ch<u>an</u>ce
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'E~'
    </td>
    <td style="text-align:center">
      &#101;&#771;<br/><br/>
      &#603;&#771;
    </td>
    <td style="text-align:center">
      0065+0303<br/><br/>
      025B+0303
    </td>
    <td>
      T<u>ein</u>t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'o~'
    </td>
    <td style="text-align:center">
      &#111;&#771;<br/><br/>
      &#596;&#771;
    </td>
    <td style="text-align:center">
      006F+0303<br/><br/>
      0254+0303
    </td>
    <td>
      Pard<u>on</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'oe~'
    </td>
    <td style="text-align:center">
      &#248;&#771;<br/><br/>
      &#339;&#771;
    </td>
    <td style="text-align:center">
      00F8+0303<br/><br/>
      0153+0303
    </td>
    <td>
      Parf<u>um</u>
    </td>
  </tr>
</table>

### Consonants (German)

<table style="width:90%">
  <caption>Table 17. Consonants (German)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      German<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
        0062
    </td>
    <td>
      <u>B</u>oden, <u>B</u>ett, o<u>b</u>en
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      0070
    </td>
    <td>
      <u>P</u>apier, Li<u>pp</u>e, Gra<u>b</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      d<br/><br/>
      &#240; [<strong>1</strong>]
    </td>
    <td style="text-align:center">
      0064<br/><br/>
      00F0
    </td>
    <td>
      <u>d</u>unkel, kin<u>d</u>isch, Hel<u>d</u>en
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      0074
    </td>
    <td>
      <u>T</u>ag, bi<u>tt</u>e, Ra<u>d</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      g<br/><br/>
      &#609;<br/><br/>
      &#611;
    </td>
    <td style="text-align:center">
      0067<br/><br/>
      0261<br/><br/>
      0263
    </td>
    <td>
      <u>g</u>eben, <u>g</u>rau, Ta<u>g</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      006B
    </td>
    <td>
      <u>K</u>atze, E<u>ck</u>e, S<u>k</u>ulptur, la<u>g</u>,
      <u>q</u>uitt
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      0076
    </td>
    <td>
      <u>W</u>agen, <u>v</u>isk&ouml;s, <u>V</u>olum, o<u>v</u>al
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      0066
    </td>
    <td>
      <u>f</u>ast, ho<u>ff</u>en, <u>V</u>ater
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      007A
    </td>
    <td>
      <u>S</u>ee, <u>S</u>atz, le<u>s</u>en
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      0073
    </td>
    <td>
      Ma<u>&szlig;</u>, la<u>ss</u>en, La<u>s</u>t, H<u>au</u>s
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Z
    </td>
    <td style="text-align:center">
      &#658;
    </td>
    <td style="text-align:center">
      0292
    </td>
    <td>
      Gara<u>g</u>e, <u>G</u>enie
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      S
    </td>
    <td style="text-align:center">
      &#643;
    </td>
    <td style="text-align:center">
      0283
    </td>
    <td>
      <u>sch</u>on, <u>s</u>pielen, <u>S</u>til, w&auml;<u>sch</u>t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      X
    </td>
    <td style="text-align:center">
      &#231;
    </td>
    <td style="text-align:center">
      00E7
    </td>
    <td>
      i<u>ch</u>, <u>Ch</u>emie, Kel<u>ch</u>, man<u>ch</u>er
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      x
    </td>
    <td style="text-align:center">
      x<br/><br/>
      &#967;
    </td>
    <td style="text-align:center">
      0078<br/><br/>
      03C7
    </td>
    <td>
      Bu<u>ch</u>, Ba<u>ch</u>, Wo<u>ch</u>en
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      P
    </td>
    <td style="text-align:center">
      &#112;&#102;
    </td>
    <td style="text-align:center">
      0070+0066
    </td>
    <td>
      <u>Pf</u>lanze, Stum<u>pf</u>en
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      R
    </td>
    <td style="text-align:center">
      &#592;<br/><br/>
      &#652;<br/><br/>
      &#602;<br/><br/>
      &#605;
    </td>
    <td style="text-align:center">
      0250<br/><br/>
      028C<br/><br/>
      025A<br/><br/>
      025D
    </td>
    <td>
      Wied<u>er</u>, &uuml;b<u>er</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      T
    </td>
    <td style="text-align:center">
      &#116;&#115;<br/><br/>
      &#678;<br/><br/>
      &#952; [<strong>2</strong>]
    </td>
    <td style="text-align:center">
      0074+0073<br/><br/>
      02A6<br/><br/>
      03B8
    </td>
    <td>
      <u>Z</u>auber, Poli<u>z</u>ei, Glan<u>z</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      J
    </td>
    <td style="text-align:center">
      &#100;&#658;<br/><br/>
      &#676;
    </td>
    <td style="text-align:center">
      0064+0292<br/><br/>
      02A4
    </td>
    <td>
      <u>J</u>ob, <u>Dsch</u>ungel
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      C
    </td>
    <td style="text-align:center">
      &#116;&#643;<br/><br/>
      &#116;&#643;
    </td>
    <td style="text-align:center">
      0074+0283<br/><br/>
      02A7
    </td>
    <td>
      deuts<u>ch</u>, <u>Ch</u>ile, <u>C</u>ello
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      006D
    </td>
    <td>
      <u>M</u>ann, ko<u>mm</u>en, Ate<u>m</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      006E
    </td>
    <td>
      <u>N</u>acht, k&ouml;<u>nn</u>en, Ki<u>n</u>d
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      G
    </td>
    <td style="text-align:center">
      &#331;
    </td>
    <td style="text-align:center">
      014B
    </td>
    <td>
      Fi<u>ng</u>er, l&auml;<u>ng</u>s, Anfa<u>ng</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      006C
    </td>
    <td>
      <u>l</u>esen, fa<u>ll</u>en, Pu<u>l</u>t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      r
    </td>
    <td style="text-align:center">
      r<br/><br/>
      &#633;<br/><br/>
      &#640;<br/><br/>
      &#641;<br/><br/>
      &#638;
    </td>
    <td style="text-align:center">
      0072<br/><br/>
      0279<br/><br/>
      0280<br/><br/>
      0281<br/><br/>
      027E
    </td>
    <td>
      <u>R</u>ad, f&uuml;h<u>r</u>en
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      j<br/><br/>
      &#669;
    </td>
    <td style="text-align:center">
      006A<br/><br/>
      029D
    </td>
    <td>
      <u>J</u>unge, <u>j</u>a, <u>J</u>ahr, Minister<u>i</u>um
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      w<br/><br/>
      &#651;
    </td>
    <td style="text-align:center">
      0077<br/><br/>
      028B
    </td>
    <td>
      Ed<u>u</u>ard, akt<u>u</u>ell, Jan<u>u</u>ar
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      h
    </td>
    <td style="text-align:center">
      h<br/><br/>
      &#614;
    </td>
    <td style="text-align:center">
      0068<br/><br/>
      0266
    </td>
    <td>
      <u>h</u>och, <u>H</u>and, A<u>h</u>orn
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      ? (glottal stop)
    </td>
    <td style="text-align:center">
      &#660;
    </td>
    <td style="text-align:center">
      0294
    </td>
    <td>
      _er_obern (IPA <code>&#660;&#603;&#592;&#712;&#660;&#111;&#720;&#98;&#592;&#110;</code>)<br/>_erinnern (IPA <code>&#660;&#603;&#592;&#712;&#641;&#618;&#110;&#592;&#110;</code>)
<!--
      <u>e</u>r<u>o</u>bern (IPA &#660;&#603;&#592;&#712;&#660;&#111;&#720;&#98;&#592;&#110;)<br/><u>e</u>rinnern (IPA &#660;&#603;&#592;&#712;&#641;&#618;&#110;&#592;&#110;)
-->
    </td>
  </tr>
</table>

**Notes:**

1.  The IPA symbol <code>&#240;</code> (IPA Unicode `00F0`) occurs only in loanwords from foreign languages, mostly English (for example, *The New York Times*). However, the service realizes that sound as IPA symbol `d` (IPA Unicode `0064`).
1.  The IPA symbol <code>&#952;</code> (IPA Unicode `03B8`) occurs only in loanwords from foreign languages, mostly English (for example, *thriller*). However, the service realizes that sound as IPA symbol <code>&#678;</code> (IPA Unicode `02A6`).

## Spanish symbols
{: #esSymbols}

The following sections describe the inventory of valid symbols for Castilian and North American Spanish. Except where noted, the two dialects are identical.

### Regular vowels (Spanish)

<table style="width:90%">
  <caption>Table 18. Regular vowels (Spanish)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Spanish<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      0061
    </td>
    <td>
      <u>a</u>gua, c<u>a</u>s<u>a</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      0065
    </td>
    <td>
      <u>e</u>st<u>e</u>, b<u>e</u>so
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      0069
    </td>
    <td>
      <u>i</u>gual, h<u>i</u>jo
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      006F
    </td>
    <td>
      <u>o</u>s<u>o</u>, cant<u>o</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      0075
    </td>
    <td>
      <u>u</u>va, l<u>u</u>gar
    </td>
  </tr>
</table>

### Consonants (Spanish)

<table style="width:90%">
  <caption>Table 19. Consonants (Spanish)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Spanish<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      0062
    </td>
    <td>
      <u>b</u>asta, <u>b</u>eber, <u>v</u>aca
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      0070
    </td>
    <td>
      <u>p</u>arte, a<u>p</u>agar
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      0064
    </td>
    <td>
      <u>d</u>ar, <u>d</u>edo
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      0074
    </td>
    <td>
      <u>t</u>oma, a<u>t</u>ar
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      0067<br/>
      0261
    </td>
    <td>
      <u>g</u>oma, <u>g</u>orra
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      006B
    </td>
    <td>
      <u>c</u>uen<u>c</u>o, <u>c</u>anto
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      0066
    </td>
    <td>
      <u>f</u>laco, a<u>f</u>uera
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      0073
    </td>
    <td>
      <u>s</u>illa, ca<u>s</u>a
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      R
    </td>
    <td style="text-align:center">
      r
    </td>
    <td style="text-align:center">
      0072
    </td>
    <td>
      <u>r</u>opa, pe<u>rr</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      T [<strong>1</strong>]
    </td>
    <td style="text-align:center">
      &#952;
    </td>
    <td style="text-align:center">
      03B8
    </td>
    <td>
      <u>z</u>apato, so<u>c</u>io
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      C
    </td>
    <td style="text-align:center">
      &#679;<br/></br>
      t&#643;
    </td>
    <td style="text-align:center">
      02A7<br/></br>
      0074+0283
    </td>
    <td>
      <u>ch</u>alupa, mu<u>ch</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      h [<strong>2</strong>]<br/><br/>
      x [<strong>3</strong>]
    </td>
    <td style="text-align:center">
      0068<br/><br/>
      0078
    </td>
    <td>
      <u>j</u>unco, re<u>j</u>a, <u>g</u>ente
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      006D
    </td>
    <td>
      <u>m</u>ano, a<u>m</u>or
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      006E
    </td>
    <td>
      <u>n</u>ada, ma<u>n</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      N
    </td>
    <td style="text-align:center">
      &#626;
    </td>
    <td style="text-align:center">
      0272
    </td>
    <td>
      pi<u>&ntilde;</u>a, ni<u>&ntilde;</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      r
    </td>
    <td style="text-align:center">
      &#638;
    </td>
    <td style="text-align:center">
      027E
    </td>
    <td>
      pa<u>r</u>a, pe<u>r</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      006C
    </td>
    <td>
      <u>l</u>oco, a<u>l</u>go
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      L [<strong>4</strong>]
    </td>
    <td style="text-align:center">
      &#654;<br/><br/>
      &#669; [<strong>5</strong>]
    </td>
    <td style="text-align:center">
      028E<br/><br/>
      029D
    </td>
    <td>
      <u>ll</u>over, po<u>ll</u>o<br/><br/>
      <u>y</u>egua, pla<u>y</u>a
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Y
    </td>
    <td style="text-align:center">
      &#669; [<strong>6</strong>]
    </td>
    <td style="text-align:center">
      029D
    </td>
    <td>
      <u>y</u>egua, pla<u>y</u>a
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      y
    </td>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      006A
    </td>
    <td>
      med<u>i</u>o, o<u>i</u>go
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      0077
    </td>
    <td>
      f<u>u</u>era, de<u>u</u>da
    </td>
  </tr>
</table>

**Notes:**

1.  The SPR symbol `T` is realized only in Castilian Spanish. It is replaced internally with the phonetic symbol `s` in North American Spanish, even when present in the SPR input.
1.  The IPA symbol `h` applies to North American Spanish only.
1.  The IPA symbol `x` applies to Castilian Spanish only.
1.  The SPR symbol `L` maps to two different IPA symbols with different pronunciations in North American Spanish: <code>&#654;</code> and <code>&#669;</code>. Specifying this SPR symbol might yield either of the two variants, but the difference between the pronunciations is often indistinguishable to native speakers.
1.  The IPA symbol <code>&#669;</code> maps to the SPR symbol `L` in North American Spanish.
1.  The IPA symbol <code>&#669;</code> maps to the SPR symbol `Y` in Castilian Spanish.

### Allophones (Spanish)

Each allophone is a variation of the phoneme indicated in parentheses. If an allophone is not used in an SPR, the {{site.data.keyword.texttospeechshort}} service automatically generates the appropriate variant for the given context.

<table style="width:90%">
  <caption>Table 20. Allophones (Spanish)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Spanish allophone<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      B (b)
    </td>
    <td style="text-align:center">
      &#946;
    </td>
    <td style="text-align:center">
      03B2
    </td>
    <td>
      bo<u>b</u>o, nue<u>v</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      D (d)
    </td>
    <td style="text-align:center">
      &#240;
    </td>
    <td style="text-align:center">
      00F0
    </td>
    <td>
      ha<u>d</u>a, de<u>d</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      G (g)
    </td>
    <td style="text-align:center">
      &#611;
    </td>
    <td style="text-align:center">
      0263
    </td>
    <td>
      se<u>g</u>ar, lu<u>g</u>ar
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      z (s)
    </td>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      007A
    </td>
    <td>
      mi<u>s</u>mo, de<u>s</u>de
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'ng' [<strong>1</strong>]
    </td>
    <td style="text-align:center">
      &#331;g
    </td>
    <td style="text-align:center">
      014B+0067
    </td>
    <td>
      ta<u>n</u>go, e<u>n</u>ga&ntilde;o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'nk' [<strong>1</strong>]
    </td>
    <td style="text-align:center">
      &#331;k
    </td>
    <td style="text-align:center">
      014B+006B
    </td>
    <td>
      a<u>n</u>cla, ci<u>n</u>co
    </td>
  </tr>
</table>

**Note:**

1.  The `ng` and `nk` allophones are supported in the IPA specification but cannot be used in an SPR.

## Italian symbols
{: #itSymbols}

The following sections describe the inventory of valid symbols for Italian.

### Regular vowels (Italian)

<table style="width:90%">
  <caption>Table 21. Regular vowels (Italian)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Italian<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      0061
    </td>
    <td>
      l<u>a</u>s<u>a</u>gn<u>a</u>, <u>a</u>llegro
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      0065
    </td>
    <td>
      n<u>e</u>ro, du<u>e</u>tto
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      E
    </td>
    <td style="text-align:center">
      &#603;
    </td>
    <td style="text-align:center">
      025B
    </td>
    <td>
      <u>e</u>cco, lic<u>e</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      0069
    </td>
    <td>
      <u>i</u>sola, form<u>i</u>ca
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      006F
    </td>
    <td>
      padr<u>o</u>ne, att<u>o</u>re
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      c
    </td>
    <td style="text-align:center">
      &#596;
    </td>
    <td style="text-align:center">
      0254
    </td>
    <td>
      c<u>o</u>sta, m<u>o</u>sse
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      0075
    </td>
    <td>
      l<u>u</u>na, <u>u</u>fficio
    </td>
  </tr>
</table>

### Consonants (Italian)

<table style="width:90%">
  <caption>Table 22. Consonants (Italian)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Italian<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      0062
    </td>
    <td>
      <u>b</u>occa, <u>b</u>ere
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      0070
    </td>
    <td>
      <u>p</u>artire, <u>p</u>oco
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      0064
    </td>
    <td>
      <u>d</u>are, <u>d</u>ata
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      0074
    </td>
    <td>
      <u>t</u>occare, len<u>t</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      0067<br/>
      0261
    </td>
    <td>
      <u>g</u>rande, re<u>g</u>alo
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      006B
    </td>
    <td>
      <u>c</u>asa, ve<u>cch</u>io
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      0076
    </td>
    <td>
      <u>v</u>ano, <u>v</u>i<u>v</u>ere
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      0066
    </td>
    <td>
      <u>f</u>are, <u>f</u>orte
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      007A
    </td>
    <td>
      pae<u>s</u>e, <u>s</u>baglio
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      0073
    </td>
    <td>
      pe<u>s</u>to, <u>s</u>tare
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      S
    </td>
    <td style="text-align:center">
      &#643;
    </td>
    <td style="text-align:center">
      0283
    </td>
    <td>
      <u>sc</u>egliere, la<u>sc</u>iare
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      J
    </td>
    <td style="text-align:center">
      d&#658;<br/><br/>
      &#676;
    </td>
    <td style="text-align:center">
      0064+0292<br/><br/>
      02A4
    </td>
    <td>
      <u>Gi</u>ovanni, con<u>g</u>elare
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      C
    </td>
    <td style="text-align:center">
      t&#643;<br/><br/>
      &#679;
    </td>
    <td style="text-align:center">
      0074+0283<br/><br/>
      02A7
    </td>
    <td>
      <u>c</u>e<u>c</u>e, <u>c</u>iao
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      D
    </td>
    <td style="text-align:center">
      dz<br/><br/>
      &#675;
    </td>
    <td style="text-align:center">
      0064+007A<br/><br/>
      02A3
    </td>
    <td>
      <u>z</u>abaione, <u>z</u>ero, <u>z</u>ona
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      T
    </td>
    <td style="text-align:center">
      ts<br/><br/>
      &#678;
    </td>
    <td style="text-align:center">
      0074+0073<br/><br/>
      02A6
    </td>
    <td>
      <u>z</u>ampa, <u>z</u>uppa
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      006D
    </td>
    <td>
      <u>m</u>a<u>mm</u>a, <u>m</u>ano
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      006E
    </td>
    <td>
      <u>n</u>ie<u>n</u>te, <u>n</u>otte
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      N
    </td>
    <td style="text-align:center">
      &#626;
    </td>
    <td style="text-align:center">
      0272
    </td>
    <td>
      <u>gn</u>occhi, lasa<u>gn</u>a
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      r
    </td>
    <td style="text-align:center">
      r<br/><br/>
      &#638;
    </td>
    <td style="text-align:center">
      0072<br/><br/>
      027E
    </td>
    <td>
      ca<u>r</u>o, se<u>r</u>eno
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      R
    </td>
    <td style="text-align:center">
      rr<br/><br/>
      r&#720;
    </td>
    <td style="text-align:center">
      0072+0072<br/><br/>
      0072+02D0
    </td>
    <td>
      te<u>rr</u>a, to<u>rr</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      006C
    </td>
    <td>
      <u>l</u>ento, pa<u>l</u>ma
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      L
    </td>
    <td style="text-align:center">
      &#654;
    </td>
    <td style="text-align:center">
      028E
    </td>
    <td>
      <u>gl</u>ielo, <u>gl</u>i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      y
    </td>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      006A
    </td>
    <td>
      <u>i</u>eri, raso<u>i</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      0077
    </td>
    <td>
      n<u>u</u>ovo, q<u>u</u>ando
    </td>
  </tr>
</table>

### Geminates (Italian)

<table style="width:90%">
  <caption>Table 23. Geminates (Italian)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Italian<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      DD
    </td>
    <td style="text-align:center">
      d&#675;<br/><br/>
      ddz
    </td>
    <td style="text-align:center">
      0064+02A3<br/><br/>
      0064+0064+007A
    </td>
    <td>
      a<u>zz</u>urro, me<u>zz</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      JJ
    </td>
    <td style="text-align:center">
      dd&#658;<br/><br/>
      d&#676;
    </td>
    <td style="text-align:center">
      0064+0064+0292<br/><br/>
      0064+02A4
    </td>
    <td>
      Chio<u>gg</u>ia, ma<u>gg</u>io
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      TT
    </td>
    <td style="text-align:center">
      tts<br/><br/>
      t&#678;
    </td>
    <td style="text-align:center">
      0074+0074+0073<br/><br/>
      0074+02A6
    </td>
    <td>
      ta<u>zz</u>a, chia<u>zz</u>a
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      CC
    </td>
    <td style="text-align:center">
      t&#679;<br/><br/>
      tt&#643;
    </td>
    <td style="text-align:center">
      0074+02A7<br/><br/>
      0074+0074+0283
    </td>
    <td>
      ghia<u>cc</u>io, fe<u>cc</u>ia
    </td>
  </tr>
</table>

### Allophones (Italian)

If an allophone is not used in an SPR, the {{site.data.keyword.texttospeechshort}} service automatically generates the appropriate variant for the given context.

<table style="width:90%">
  <caption>Table 24. Allophones (Italian)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Italian allophone<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      'ng' [<strong>1</strong>]
    </td>
    <td style="text-align:center">
      &#331;g
    </td>
    <td style="text-align:center">
      014B+0067<br/>
      014B+0261
    </td>
    <td>
      a<u>ng</u>olo, lu<u>ng</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'nk' [<strong>1</strong>]
    </td>
    <td style="text-align:center">
      &#331;k
    </td>
    <td style="text-align:center">
      014B+006B
    </td>
    <td>
      a<u>nc</u>ora, bia<u>nc</u>o
    </td>
  </tr>
</table>

**Note:**

1.  The `ng` and `nk` allophones are supported in the IPA specification but cannot be used in an SPR.

## Brazilian Portuguese symbols
{: #ptSymbols}

The following sections describe the inventory of valid symbols for Brazilian Portuguese.

### Regular vowels (Brazilian Portuguese)

<table style="width:90%">
  <caption>Table 25. Regular vowels (Brazilian Portuguese)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Brazilian Portuguese<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      a [<strong>1</strong>]
    </td>
    <td style="text-align:center">
      a<br/><br/>
      &#592;
    </td>
    <td style="text-align:center">
      0061<br/><br/>
      0250
    </td>
    <td>
      vir<u>ar</u>, m<u>a</u>r<br/><br/>
      Terr<u>a</u>, muit<u>a</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      0065
    </td>
    <td>
      d<u>e</u>do, portugu<u>&ecirc;</u>s
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      E
    </td>
    <td style="text-align:center">
      &#603;
    </td>
    <td style="text-align:center">
      025B
    </td>
    <td>
      <u>&eacute;</u>s, b<u>e</u>lo, <u>e</u>co
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      0069
    </td>
    <td>
      l<u>i</u>gar, bod<u>e</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      006F
    </td>
    <td>
      c<u>o</u>r, b<u>o</u>lha
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      c
    </td>
    <td style="text-align:center">
      &#596;
    </td>
    <td style="text-align:center">
      0254
    </td>
    <td>
      pr<u>&oacute;</u>ximo, p<u>o</u>rta
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      0075
    </td>
    <td>
      l<u>u</u>gar, per<u>u</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'a~'
    </td>
    <td style="text-align:center">
      &#592;&#771;
    </td>
    <td style="text-align:center">
      0250+0303
    </td>
    <td>
      b<u>a</u>nco, l<u>&atilde;</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'e~'
    </td>
    <td style="text-align:center">
      &#101;&#771;
    </td>
    <td style="text-align:center">
      0065+0303<br/>
      1EBD
    </td>
    <td>
      inc<u>en</u>so, ag<u>en</u>te
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'i~'
    </td>
    <td style="text-align:center">
      &#105;&#771;
    </td>
    <td style="text-align:center">
      0069+0303<br>
      0129
    </td>
    <td>
      ass<u>im</u>, <u>in</u>censo
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'o~'
    </td>
    <td style="text-align:center">
      &#111;&#771;
    </td>
    <td style="text-align:center">
      006F+0303<br/>
      00F5
    </td>
    <td>
      c<u>&ocirc;n</u>sul, t<u>om</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'u~'
    </td>
    <td style="text-align:center">
      &#117;&#771;
    </td>
    <td style="text-align:center">
      0075+0303<br/>
      0169
    </td>
    <td>
      alg<u>un</u>s, <u>um</u>
    </td>
  </tr>
</table>

**Note:**

1.  The SPR symbol `a` maps to two different IPA symbols with different pronunciations: `a` and <code>&#592;</code>. In general, the SPR symbol maps to `a` for synthesis of stressed syllables and to <code>&#592;</code> for synthesis of unstressed syllables.

### Semi-vowels (Brazilian Portuguese)

<table style="width:90%">
  <caption>Table 26. Semi-vowels (Brazilian Portuguese)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Brazilian Portuguese<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      y
    </td>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      006A
    </td>
    <td>
      do<u>i</u>s, no<u>i</u>va
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Y
    </td>
    <td style="text-align:center">
      j&#771;
    </td>
    <td style="text-align:center">
      006A+0303
    </td>
    <td>
      m&atilde;<u>e</u>, mu<u>i</u>to
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      0077
    </td>
    <td>
      me<u>u</u>, q<u>u</u>arto
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      W
    </td>
    <td style="text-align:center">
      w&#771;
    </td>
    <td style="text-align:center">
      0077+0303
    </td>
    <td>
      capit&atilde;<u>o</u>, S&atilde;<u>o</u>
    </td>
  </tr>
</table>

### Consonants (Brazilian Portuguese)

<table style="width:90%">
  <caption>Table 27. Consonants (Brazilian Portuguese)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Brazilian Portuguese<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      0062
    </td>
    <td>
      a<u>b</u>ra&ccedil;o, <u>B</u>rasil
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      0070
    </td>
    <td>
      <u>p</u>luma, <u>p</u>rimo
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      0064
    </td>
    <td>
      <u>d</u>ar, <u>d</u>ente
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      0074
    </td>
    <td>
      <u>t</u>rono, por<u>t</u>a
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      0067<br/>
      0261
    </td>
    <td>
      <u>g</u>ato, <u>g</u>uarda
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      006B
    </td>
    <td>
      <u>c</u>ama, <u>qu</u>eda
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
      0076
    </td>
    <td>
      <u>v</u>ila, bre<u>v</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      0066
    </td>
    <td>
      <u>f</u>lauta, <u>f</u>aixa
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      007A
    </td>
    <td>
      <u>z</u>ero, ca<u>s</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      0073
    </td>
    <td>
      <u>c</u>erto, avan<u>&ccedil</u>ar, <u>s</u>ete
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      Z
    </td>
    <td style="text-align:center">
      &#658;
    </td>
    <td style="text-align:center">
      0292
    </td>
    <td>
      <u>g</u>eral, <u>j</u>ogo
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      S
    </td>
    <td style="text-align:center">
      &#643;
    </td>
    <td style="text-align:center">
      0283
    </td>
    <td>
      <u>ch</u>ave, bai<u>x</u>a
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      J
    </td>
    <td style="text-align:center">
      &#100;&#658;<br/><br/>
      &#676;
    </td>
    <td style="text-align:center">
      0064+0292<br/><br/>
      02A4
    </td>
    <td>
      bo<u>d</u>e, <u>d</u>iz
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      C
    </td>
    <td style="text-align:center">
      &#116;&#643;<br/><br/>
      &#679;
    </td>
    <td style="text-align:center">
      0074+0283<br/><br/>
      02A7
    </td>
    <td>
      se<u>t</u>e, bo<u>t</u>e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      006D
    </td>
    <td>
      for<u>m</u>a, <u>m</u>acaco
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      006E
    </td>
    <td>
      do<u>n</u>o, <u>n</u>ovo
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      N
    </td>
    <td style="text-align:center">
      &#626;
    </td>
    <td style="text-align:center">
      0272
    </td>
    <td>
      cu<u>nh</u>a, ni<u>nh</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      r
    </td>
    <td style="text-align:center">
      &#638;
    </td>
    <td style="text-align:center">
      027E
    </td>
    <td>
      ca<u>r</u>o, t<u>r</u>em
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      R
    </td>
    <td style="text-align:center">
      &#641;
    </td>
    <td style="text-align:center">
      0281
    </td>
    <td>
      ca<u>rr</u>o, <u>r</u>io
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      006C
    </td>
    <td>
      <u>l</u>eite, cava<u>l</u>o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'ly'
    </td>
    <td style="text-align:center">
      &#654;
    </td>
    <td style="text-align:center">
      028E
    </td>
    <td>
      <u>lh</u>e, bagu<u>lh</u>o
    </td>
  </tr>
</table>

## Japanese symbols
{: #jaSymbols}

The following sections describe the inventory of valid symbols for Japanese.

### Vowels and marks (Japanese)

<table style="width:90%">
  <caption>Table 28. Vowels and marks (Japanese)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Japanese<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      a<br/><br/>
      &#592;<br/><br/>
      &#593;
    </td>
    <td style="text-align:center">
      0061<br/><br/>
      0250<br/><br/>
      0251
    </td>
    <td>
      &#30456;&#25163;(<u>&#12450;</u>&#12452;&#12486;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      i<br/><br/>
      &#618;
    </td>
    <td style="text-align:center">
      0069<br/><br/>
      026A
    </td>
    <td>
      &#12356;&#12383;&#12378;&#12425;(<u>&#12452;</u>&#12479;&#12474;&#12521;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      &#623;<br/><br/>
      u
    </td>
    <td style="text-align:center">
      026F<br/><br/>
      0075
    </td>
    <td>
      &#23431;&#23449;(<u>&#12454;</u>&#12481;&#12517;&#12454;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      e<br/><br/>
      &#603;
    </td>
    <td style="text-align:center">
      0065<br/><br/>
      025B
    </td>
    <td>
      &#32117;&#26412;(<u>&#12456;</u>&#12507;&#12531;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      o<br/><br/>
      &#594;<br/><br/>
      &#596;
    </td>
    <td style="text-align:center">
      006F<br/><br/>
      0252<br/><br/>
      0254
    </td>
    <td>
      &#12362;&#33747;&#23376;(<u>&#12458;</u>&#12459;&#12471;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      : [<strong>1</strong>]
    </td>
    <td style="text-align:center">
      &#720;
    </td>
    <td style="text-align:center">
      02D0
    </td>
    <td>
      &#12524;<u>&#12540;</u>&#12473;
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      ^
    </td>
    <td style="text-align:center">
      &#42780;<br/><br/>
      ^
    </td>
    <td style="text-align:center">
      A71C<br/><br/>
      005E
    </td>
    <td>
      &#12467;&#12464;<u>&#42780;</u>&#12491;&#12486;&#12451;&#12502;
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      '_n'
    </td>
    <td style="text-align:center">
      &#628;<br/><br/>
      &#331;
    </td>
    <td style="text-align:center">
      0274<br/><br/>
      014B
    </td>
    <td>
      &#28288;&#26376;(&#12510;<u>&#12531;</u>&#12466;&#12484;)
    </td>
  </tr>
</table>

**Note:**

1.  The `:` symbol must be followed by a vowel, possibly with other symbols, such as syllable boundary, in between.

### Consonants (Japanese)

<table style="width:90%">
  <caption>Table 29. Consonants (Japanese)</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      Japanese<br/>SPR symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Example words
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      006B
    </td>
    <td>
      &#20844;&#22290;(<u>&#12467;</u>&#12454;&#12456;&#12531;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      0073
    </td>
    <td>
      &#23551;&#21496;(<u>&#12473;</u>&#12471;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'sh'
    </td>
    <td style="text-align:center">
      &#597;<br/><br/>
      &#643;
    </td>
    <td style="text-align:center">
      0255<br/><br/>
      0283
    </td>
    <td>
      &#22235;&#23395;(<u>&#12471;</u>&#12461;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      0074
    </td>
    <td>
      &#22823;&#27827;(<u>&#12479;</u>&#12452;&#12460;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'ch'
    </td>
    <td style="text-align:center">
      &#679;<br/><br/>
      &#680;
    </td>
    <td style="text-align:center">
      02A7<br/><br/>
      02A8
    </td>
    <td>
      &#22320;&#22259;(<u>&#12481;</u>&#12474;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'ts'
    </td>
    <td style="text-align:center">
      &#678;
    </td>
    <td style="text-align:center">
      02A6
    </td>
    <td>
      &#37347;&#12426;(<u>&#12484;</u>&#12522;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      006E
    </td>
    <td>
      &#20108;&#36650;&#36554;(<u>&#12491;</u>&#12522;&#12531;&#12471;&#12515;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      h
    </td>
    <td style="text-align:center">
      h
    </td>
    <td style="text-align:center">
      0068
    </td>
    <td>
      &#33457;&#26564;(<u>&#12495;</u>&#12490;&#12460;&#12521;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      &#632;<br/><br/>
      f
    </td>
    <td style="text-align:center">
      0278<br/><br/>
      066
    </td>
    <td>
      &#19981;&#22812;&#22478;(<u>&#12501;</u>&#12516;&#12472;&#12519;&#12454;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      006D
    </td>
    <td>
      &#39764;&#27861;(<u>&#12510;</u>&#12507;&#12454;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      y
    </td>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      006A
    </td>
    <td>
      &#38525;&#27671;(<u>&#12520;</u>&#12454;&#12461;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      r
    </td>
    <td style="text-align:center">
      &#638;<br/><br/>
      r<br/><br/>
      &#633;<br/><br/>
      l<br/><br/>
      &#637;
    </td>
    <td style="text-align:center">
      027E<br/><br/>
      0072<br/><br/>
      0279<br/><br/>
      006C<br/><br/>
      027D
    </td>
    <td>
      &#12521;&#12452;&#40614;(<u>&#12521;</u>&#12452;&#12512;&#12462;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      w<br/><br/>
      &#624;
    </td>
    <td style="text-align:center">
      0077<br/><br/>
      0270
    </td>
    <td>
      &#24746;&#12384;&#12367;&#12415;(<u>&#12527;</u>&#12523;&#12480;&#12463;&#12511;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      &#609;<br/><br/>
      &#611;
    </td>
    <td style="text-align:center">
      0067<br/><br/>
      0263
    </td>
    <td>
      &#32676;&#38738;(<u>&#12464;</u>&#12531;&#12472;&#12519;&#12454;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      &#675;<br/><br/>
      z
    </td>
    <td style="text-align:center">
      02A3<br/><br/>
      007A
    </td>
    <td>
      &#20840;&#37096;(<u>&#12476;</u>&#12531;&#12502;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      &#676;<br/><br/>
      &#677;
    </td>
    <td style="text-align:center">
      02A4<br/><br/>
      02A5
    </td>
    <td>
      &#12472;&#12517;&#12468;&#12531;(<u>&#12472;&#12517;</u>&#12468;&#12531;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      0064
    </td>
    <td>
      &#22243;&#23376;(<u>&#12480;</u>&#12531;&#12468;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      b<br/><br/>
      v
    </td>
    <td style="text-align:center">
      0062<br/><br/>
      0076
    </td>
    <td>
      <u>&#12496;</u>&#12490;&#12490;
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      0070
    </td>
    <td>
      <u>&#12497;</u>&#12531;&#12480;
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'ky'
    </td>
    <td style="text-align:center">
      kj
    </td>
    <td style="text-align:center">
      02B7+006A
    </td>
    <td>
      &#20241;&#26085;(<u>&#12461;&#12517;</u>&#12454;&#12472;&#12484;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'dy'
    </td>
    <td style="text-align:center">
      dj
    </td>
    <td style="text-align:center">
      0064+006A
    </td>
    <td>
      <u>&#12487;&#12517;</u>&#12456;&#12483;&#12488;
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'ny'
    </td>
    <td style="text-align:center">
      &#626;
    </td>
    <td style="text-align:center">
      0272
    </td>
    <td>
      &#29275;&#20083;(<u>&#12462;&#12517;</u>&#12454;&#12491;&#12517;&#12454;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'hy'
    </td>
    <td style="text-align:center">
      &#231;
    </td>
    <td style="text-align:center">
      00E7
    </td>
    <td>
      &#30334;&#24180;(<u>&#12498;&#12515;</u>&#12463;&#12493;&#12531;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'my'
    </td>
    <td style="text-align:center">
      mj
    </td>
    <td style="text-align:center">
      006D+006A
    </td>
    <td>
      &#38512;&#38525;&#24107;(&#12458;&#12531;<u>&#12511;&#12519;</u>&#12454;&#12472;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'ry'
    </td>
    <td style="text-align:center">
      &#638;j
    </td>
    <td style="text-align:center">
      027E+006A
    </td>
    <td>
      &#27969;&#26143;&#32676;(<u>&#12522;&#12517;</u>&#12454;&#12475;&#12452;&#12464;&#12531;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'gy'
    </td>
    <td style="text-align:center">
      &#609;j
    </td>
    <td style="text-align:center">
      0067+006A
    </td>
    <td>
      &#29275;&#20028;(<u>&#12462;&#12517;</u>&#12454;&#12489;&#12531;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'by'
    </td>
    <td style="text-align:center">
      bj
    </td>
    <td style="text-align:center">
      0062+006A
    </td>
    <td>
      &#30333;&#22812;(<u>&#12499;&#12515;</u>&#12463;&#12516;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'py'
    </td>
    <td style="text-align:center">
      pj
    </td>
    <td style="text-align:center">
      0070+006A
    </td>
    <td>
      &#12404;&#12423;&#12371;&#12435;(<u>&#12500;&#12519;</u>&#12467;&#12531;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qk'
    </td>
    <td style="text-align:center">
      kk
    </td>
    <td style="text-align:center">
      02B7+02B7
    </td>
    <td>
      &#26376;&#20809;(&#12466;<u>&#12483;&#12467;</u>&#12454;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qs'
    </td>
    <td style="text-align:center">
      ss
    </td>
    <td style="text-align:center">
      0073+0073
    </td>
    <td>
      &#30142;&#36208;(&#12471;<u>&#12483;&#12477;</u>&#12454;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qsh'
    </td>
    <td style="text-align:center">
      &#597;&#597;
    </td>
    <td style="text-align:center">
      0255+0255
    </td>
    <td>
      &#20843;&#23610;(&#12495;<u>&#12483;&#12471;&#12515;</u>&#12463;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qt'
    </td>
    <td style="text-align:center">
      tt
    </td>
    <td style="text-align:center">
      0074+0074
    </td>
    <td>
      &#38634;&#39364;(&#12475;<u>&#12483;&#12479;</u>)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qch'
    </td>
    <td style="text-align:center">
      &#679;&#679;
    </td>
    <td style="text-align:center">
      02A7+02A7
    </td>
    <td>
      &#12362;&#12387;&#12385;&#12419;&#12435;(&#12458;<u>&#12483;&#12481;&#12515;</u>&#12531;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qts'
    </td>
    <td style="text-align:center">
      &#678;&#678;
    </td>
    <td style="text-align:center">
      02A6+02A6
    </td>
    <td>
      &#37444;&#27084;(&#12486;<u>&#12483;&#12484;</u>&#12452;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qh'
    </td>
    <td style="text-align:center">
      hh
    </td>
    <td style="text-align:center">
      0068+0068
    </td>
    <td>
      &#12467;&#12483;&#12504;&#12523;(&#12467;<u>&#12483;&#12504;</u>&#12523;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qf'
    </td>
    <td style="text-align:center">
      &#632;&#632;
    </td>
    <td style="text-align:center">
      0278+0278
    </td>
    <td>
      &#12501;<u>&#12483;&#12501;</u>&#12540;&#12523;
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qg'
    </td>
    <td style="text-align:center">
      &#609;&#609;
    </td>
    <td style="text-align:center">
      0067+0067
    </td>
    <td>
      &#12479;<u>&#12483;&#12464;</u>&#12510;&#12483;&#12481;
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qz'
    </td>
    <td style="text-align:center">
      &#675;&#675;
    </td>
    <td style="text-align:center">
      02A3+02A3
    </td>
    <td>
      &#12461;<u>&#12483;&#12474;</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qj'
    </td>
    <td style="text-align:center">
      &#676;&#676;
    </td>
    <td style="text-align:center">
      02A4+02A4
    </td>
    <td>
      &#12376;&#12419;&#12387;&#12376;&#12419;&#12417;(&#12472;&#12515;<u>&#12483;&#12472;&#12515;</u>&#12513;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qd'
    </td>
    <td style="text-align:center">
      dd
    </td>
    <td style="text-align:center">
      0064+0064
    </td>
    <td>
      &#12505;<u>&#12483;&#12489;</u>
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qb'
    </td>
    <td style="text-align:center">
      bb
    </td>
    <td style="text-align:center">
      0062+0062
    </td>
    <td>
      &#12400;&#12387;&#12400;&#12540;&#12435;(&#12496;<u>&#12483;&#12496;</u>&#12540;&#12531;)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qp'
    </td>
    <td style="text-align:center">
      pp
    </td>
    <td style="text-align:center">
      0070+0070
    </td>
    <td>
      &#12495;<u>&#12483;&#12500;</u>&#12540;
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qky'
    </td>
    <td style="text-align:center">
      kkj
    </td>
    <td style="text-align:center">
      02B7+02B7+006A
    </td>
    <td>
      &#29305;&#35377;(&#12488;<u>&#12483;&#12461;&#12519;</u>)
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      'Qpy'
    </td>
    <td style="text-align:center">
      ppj
    </td>
    <td style="text-align:center">
      0070+0070+006A
    </td>
    <td>
      &#31361;&#25293;&#23376;(&#12488;<u>&#12483;&#12500;&#12519;</u>&#12454;&#12471;)
    </td>
  </tr>
</table>
