---

copyright:
  years: 2021, 2023
lastupdated: "2023-03-21"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# French (Canadian) symbols
{: #caSymbols}

The service supports the following symbols for Canadian French.

## Vowels
{: #caVowels}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| a | a | 0061 | p**a**ttes, l**a**c, c**a**ve, inform**a**tion |
| A | &#593; | 0251 | ch**a**r, m**â**le |
| e | e | 0065 | caf**é**, d**e**former, **é**t**é** |
| E | &#603;  \n   \n &#604; | 025B  \n   \n 025C | **fait**e, dr**e**sser, p**è**re, annu**ai**re, f**ê**te |
| i | i | 0069 | s**i**, t**y**pique |
| I | &#618; | 026A | s**i**te, plast**i**que, r**i**de |
| o | o | 006F | p**au**le, b**eau**, t**ô**t, c**ô**té, v**au**devilliste |
| c | &#596;  \n   \n &#594; | 0254  \n   \n 0252 | p**au**l, n**o**te, échal**o**tte, l**o**ge, enc**o**re |
| u | u | 0075 | r**ou**e, **où**, t**ou**r, f**ou**r, d**ou**ze |
| U | &#650; | 028A | f**ou**le, m**ou**sse |
| y | y | 0079 | **u**tile, p**u**re, Br**u**no, d**u**r, b**u**se |
| Y | &#655; | 028F | autob**u**s, ch**u**te |
| x | &#601; | 0259 | l**e**, qu**e** |
| 'eu' | &#248;  \n   \n &#629; | 00F8  \n   \n 0275 | j**eû**ne, ém**eu**te, m**eu**glement |
| 'oe' | &#339;  \n   \n &#630; | 0153  \n   \n 0276 | p**eu**r, j**eu**ne, déj**eu**ner, c**e**pendant, ch**e**val |
| 'a~' | &#97;&#771;  \n   \n &#593;&#771; | 0061+0303  \n   \n 0251+0303 | b**an**c, **en**, t**em**ps |
| 'E~' | &#101;&#771;  \n   \n &#603;&#771; | 0065+0303  \n   \n 025B+0303 | f**in**, pl**ein**, f**aim** |
| 'o~' | &#111;&#771;  \n   \n &#596;&#771; | 006F+0303  \n   \n 0254+0303 | b**on**, p**on**t, m**on** |
| 'oe~' | &#339;&#771; | 0153+0303 | **un**, auc**un** |
{: caption="Table 1. Vowels (Canadian French)"}

## Consonants
{: #caConsonants}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| b | b | 0062 | **b**é**b**é, **b**alle, ro**b**e |
| d | d | 0064 | **d**ort, **d**olmen |
| D | &#100;&#122;  \n   \n &#675; | 0064+007A  \n   \n 02A3 | **d**uque, **d**ire |
| f | f | 0066 | che**f**, **f**aim, **ph**are |
| g | g  \n   \n &#609; | 0067  \n   \n 0261 | **gu**erre, ba**gu**e, **g**arer |
| H | &#613; | 0265 | s**u**is, l**u**i |
| j | j  \n   \n &#654; | 006A  \n   \n 028E | h**i**érarchie, pa**ill**e, **y**oga |
| k | k | 006B | **k**ilo, **c**aler, **qu**ai |
| l | l | 006C | **l**itre, i**ll**isible, pâ**l**e |
| m | m | 006D | **m**a**m**an, fe**mm**e, **m**iser |
| n | n | 006E | A**nn**e, **n**i, ma**n**iaque |
| 'ng' | &#331; | 014B | parki**ng**, campi**ng** |
| 'nj' | &#626; | 0272 | a**gn**eau, campa**gn**e |
| p | p | 0070 | **p**orte, **p**rêt, guê**p**e |
| r | r  \n   \n &#633;  \n   \n &#640;  \n   \n &#641; | 0072  \n   \n 0279  \n   \n 0280  \n   \n 0281 | pa**r**er, **r**a**r**e, ca**rr**eau |
| s | s | 0073 | **s**ans, ambi**t**ion, fa**ç**on |
| S | &#643; | 0283 | **ch**eval, lâ**ch**e, **sch**éma |
| t | t | 0074 | **t**on, pa**tt**e, théâ**t**re |
| T | &#116;&#115;  \n   \n &#678; | 0074+0073  \n   \n 02A6 | pe**t**it, **t**uque |
| v | v | 0076 | la**v**er, **w**agon, **v**isiter |
| w | w | 0077 | **ou**i, **w**att |
| z | z | 007A | ja**s**er, ré**s**eau, **z**ig**z**aguer |
| Z | &#658; | 0292 | ra**g**e, **g**îte, **j**ouer |
{: caption="Table 2. Consonants (Canadian French)"}

## Liaison
{: #caLiaison}

In Canadian French, the `_` (underscore) can be used immediately following the final consonant of a word (but within the double-quotes that enclose the SPR) to indicate that it is a liaison consonant. A liaison consonant is pronounced only if the word that follows begins with a vowel.

| SPR symbol | IPA symbol | IPA Unicode |
|:----------:|:----------:|:-----------:|
| _ | &#8255; | 203F |
{: caption="Table 3. Liaison (Canadian French)"}

Examples of words with and without the liaison symbol follow:

-   `"p0'oe't1it_"`: The `t` is pronounced only if the following word begins with a vowel.
-   `"nEt"`: The `t` is always pronounced.

A dictionary entry *petit* with the translation value `"p'oe't1it_"` has the final `t` pronounced in the input string *un petit ami* but not in the input string *un petit chien*. An entry with the translation value `"nEt"` has the final `t` pronounced regardless of context.
