---

copyright:
  years: 2015, 2020
lastupdated: "2020-09-20"

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

# French symbols
{: #frSymbols}

The following sections describe the valid symbols for French.

## Vowels
{: #frVowels}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| a | a<br/><br/>&#593;<br/><br/>&#592; | 0061<br/><br/>0251<br/><br/>0250 | p**a**ttes, l**a**c, c**a**ve |
| e | e | 0065 | caf**&egrave;**, d**&egrave;**form**e**r, **&egrave;**t**&egrave;** |
| E | &#603;<br/><br/>&#604; | 025B<br/><br/>025C | f**ai**te, m**ai**, h**e**rb |
| i | i<br/><br/>&#618; | 0069<br/><br/>026A | f**i**lm, t**y**p**i**que |
| o | o | 006F | **eau**, **au**x, g**au**che |
| c | &#596;<br/><br/>&#594; | 0254<br/><br/>0252 | P**au**l, n**o**te, &egrave;chal**o**tte |
| u | u<br/><br/>&#650; | 0075<br/><br/>028A | r**ou**e, **o&ugrave;**, t**ou**r |
| y | &#121;<br/><br/>&#655; | 0079<br/><br/>028F | **u**tile, p**u**re, Br**u**no |
| x [**1**] | &#601; | 0259 | litr**e**s, marbr**e** |
| 'eu' | &#248;<br/><br/>&#629; | 00F8<br/><br/>0275 | m**eu**gle, p**eu**, joy**eu**x |
| 'oe' | &#339;<br/><br/>&#630; | 0153<br/><br/>0276 | p**eu**r, c**oeu**r, j**eu**ne |
| 'a~' | &#97;&#771;<br/><br/>&#593;&#771; | 0061+0303<br/><br/>0251+0303 | b**an**c, **en**, t**em**ps |
| 'E~' | &#101;&#771;<br/><br/>&#603;&#771;<br/><br/>&#230;&#771; | 0065+0303<br/><br/>025B+0303<br/><br/>00E6+0303 | f**i**n, pl**e**in, f**ai**m |
| 'o~' | &#111;&#771;<br/><br/>&#596;&#771; | 006F+0303<br/><br/>0254+0303 | b**on**, p**on**t, m**on** |
| 'oe~' | &#339;&#771; | 0153+0303 | **un**, auc**un**, br**un** |
{: caption="Table 1. Vowels (French)"}

**Note:**

1.  The `x` is elided in certain contexts.

## Consonants
{: #frConsonants}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| b | b | 0062 | **b**&egrave;**b**&egrave;, **b**alle, ro**b**e |
| p | p | 0070 | **p**orte, **p**r&ecirc;t, gu&ecirc;**p**e |
| d | d | 0064 | **d**ort, **d**olmen |
| t | t | 0074 | **t**on, pa**tt**e, th&egrave;&acirc;**t**re |
| g | g<br/><br/>&#609; | 0067<br/><br/>0261 | **gu**erre, ba**gu**e, **g**arer |
| k | k | 006B | **k**ilo, **c**aler, **qu**ai |
| v | v | 0076 | la**v**er, **w**agon, **v**isiter |
| f | f | 0066 | che**f**, **f**aim, **ph**are |
| z | z | 007A | ja**s**er, r&egrave;**s**eau, **z**ig**z**aguer |
| s | s | 0073 | **s**ans, ambi**t**ion, fa**&ccedil;**on |
| Z | &#658; | 0292 | ra**g**e, **g**&icirc;te, **j**ouer |
| S | &#643; | 0283 | **ch**eval, l&acirc;**ch**e, **sch**&egrave;ma |
| m | m | 006D | **m**a**m**an, fe**mm**e, **m**iser |
| n | n | 006E | A**nn**e, **n**i, ma**n**iaque |
| 'nj' | &#626; | 0272 | a**gn**eau, campa**gn**e |
| 'ng' | &#331; | 014B | parki**ng**, campi**ng** |
| r | r<br/><br/>&#633;<br/><br/>&#640;<br/><br/>&#641;<br/><br/>x<br/><br/>&#967; | 0072<br/><br/>0279<br/><br/>0280<br/><br/>0281<br/><br/>0078<br/><br/>03C7 | pa**r**er, **r**a**r**e, ca**rr**eau |
| l | l | 006C | **l**itre, i**ll**isible, p&acirc;**l**e |
| j | j<br/><br/>&#654; | 006A<br/><br/>028E | h**i**&egrave;rarchie, pa**ill**e, **y**oga |
| w | w | 0077 | **ou**i, b**ou**&egrave;e, **w**att |
| H | &#613; | 0265 | s**u**is, l**u**i, n**u**&egrave;e |
{: caption="Table 2. Consonants (French)"}

## Liaison
{: #frLiaison}

In French, the `_` (underscore) can be used following a word-final consonant (but within the double-quotes that enclose the SPR) to indicate that it is a liaison consonant. A liaison consonant is pronounced only if the following word begins with a vowel.

<table style="width:55%">
  <caption>Table 3. Liaison (French)</caption>
  <tr>
    <th style="width:33%; text-align:center; vertical-align:bottom">
      SPR symbol
    </th>
    <th style="width:33%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="text-align:center; vertical-align:bottom">
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
