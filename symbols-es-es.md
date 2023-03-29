---

copyright:
  years: 2015, 2023
lastupdated: "2023-03-23"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Spanish symbols
{: #esSymbols}

The service supports the following symbols for Spanish. The information applies to the Castilian, Latin American, and North American dialects. Except where noted, the dialects are identical.

## Regular vowels
{: #esReducedVowels}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| a | a | 0061 | **a**gua, c**a**s**a** |
| e | e | 0065 | **e**st**e**, b**e**so |
| i | i | 0069 | **i**gual, h**i**jo |
| o | o | 006F | **o**s**o**, cant**o** |
| u | u | 0075 | **u**va, l**u**gar |
{: caption="Table 1. Regular vowels (Spanish)"}

## Consonants
{: #esConsonants}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| b | b | 0062 | **b**asta, **b**eber, **v**aca |
| C | &#679;  \n   \n t&#643; | 02A7  \n   \n 0074+0283 | **ch**alupa, mu**ch**o |
| d | d | 0064 | **d**ar, **d**edo |
| f | f | 0066 | **f**laco, a**f**uera |
| g | g | 0067  \n 0261 | **g**oma, **g**orra |
| j | h ^**1**^  \n   \n x ^**2**^ | 0068  \n   \n 0078 | **j**unco, re**j**a, **g**ente |
| k | k | 006B | **c**uen**c**o, **c**anto |
| l | l | 006C | **l**oco, a**l**go |
| L ^**3**^ | &#654;  \n   \n &#669; ^**4**^ | 028E  \n   \n 029D | **ll**over, po**ll**o  \n   \n **y**egua, pla**y**a |
| m | m | 006D | **m**ano, a**m**or |
| n | n | 006E | **n**ada, ma**n**o |
| N | &#626; | 0272 | pi**ñ**a, ni**ñ**o |
| p | p | 0070 | **p**arte, a**p**agar |
| r | &#638; | 027E | pa**r**a, pe**r**o |
| R | r | 0072 | **r**opa, pe**rr**o |
| s | s | 0073 | **s**illa, ca**s**a |
| t | t | 0074 | **t**oma, a**t**ar |
| T ^**5**^ | &#952; | 03B8 | **z**apato, so**c**io |
| w | w | 0077 | f**u**era, de**u**da |
| y | j | 006A | med**i**o, o**i**go |
| Y | &#669; ^**6**^ | 029D | **y**egua, pla**y**a |
{: caption="Table 2. Consonants (Spanish)"}

**Notes:**

1.  The IPA symbol `h` applies to North American and Latin American Spanish only.
1.  The IPA symbol `x` applies to Castilian Spanish only.
1.  The SPR symbol `L` maps to two different IPA symbols with different pronunciations for both North American and Latin American Spanish: `ʎ` and `ʝ`. Specifying this SPR symbol with these dialects might yield either of the two variants. The difference between the pronunciations is often indistinguishable to native speakers.
1.  The IPA symbol `ʝ` maps to the SPR symbol `L` in North American and Latin American Spanish.
1.  The SPR symbol `T` is realized only in Castilian Spanish. It is replaced internally with the phonetic symbol `s` in North American and Latin American Spanish, even when present in the SPR input.
1.  The IPA symbol `ʝ` maps to the SPR symbol `Y` in Castilian Spanish.

## Allophones
{: #esAllophones}

Each allophone is a variation of the phoneme indicated in parentheses. If an allophone is not used in SPR, the {{site.data.keyword.texttospeechshort}} service automatically generates the appropriate variant for the given context.

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| B (b) | &#946; | 03B2 | bo**b**o, nue**v**e |
| D (d) | &#240; | 00F0 | ha**d**a, de**d**o |
| G (g) | &#611; | 0263 | se**g**ar, lu**g**ar |
| z (s) | z | 007A | mi**s**mo, de**s**de |
| 'ng' ^**1**^ | &#331;g | 014B+0067 | ta**n**go, e**n**gaño |
| 'nk' ^**1**^ | &#331;k | 014B+006B | a**n**cla, ci**n**co |
{: caption="Table 3. Allophones (Spanish)"}

**Note:**

1.  The `ng` and `nk` allophones are supported in the IPA specification but cannot be used in SPR.
