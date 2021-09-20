---

copyright:
  years: 2015, 2020
lastupdated: "2020-09-10"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Italian symbols
{: #itSymbols}

The following sections describe the valid symbols for Italian.

## Regular vowels
{: #itRegularVowels}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| a | a | 0061 | l**a**s**a**gn**a**, **a**llegro |
| e | e | 0065 | n**e**ro, du**e**tto |
| E | &#603; | 025B | **e**cco, lic**e**o |
| i | i | 0069 | **i**sola, form**i**ca |
| o | o | 006F | padr**o**ne, att**o**re |
| c | &#596; | 0254 | c**o**sta, m**o**sse |
| u | u | 0075 | l**u**na, **u**fficio |
{: caption="Table 1. Regular vowels (Italian)"}

## Consonants
{: #itConsonants}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| b | b | 0062 | **b**occa, **b**ere |
| p | p | 0070 | **p**artire, **p**oco |
| d | d | 0064 | **d**are, **d**ata |
| t | t | 0074 | **t**occare, len**t**o |
| g | g | 0067<br/>0261 | **g**rande, re**g**alo |
| k | k | 006B | **c**asa, ve**cch**io |
| v | v | 0076 | **v**ano, **v**i**v**ere |
| f | f | 0066 | **f**are, **f**orte |
| z | z | 007A | pae**s**e, **s**baglio |
| s | s | 0073 | pe**s**to, **s**tare |
| S | &#643; | 0283 | **sc**egliere, la**sc**iare |
| J | d&#658;<br/><br/>&#676; | 0064+0292<br/><br/>02A4 | **Gi**ovanni, con**g**elare |
| C | t&#643;<br/><br/>&#679; | 0074+0283<br/><br/>02A7 | **c**e**c**e, **c**iao |
| D | dz<br/><br/>&#675; | 0064+007A<br/><br/>02A3 | **z**abaione, **z**ero, **z**ona |
| T | ts<br/><br/>&#678; | 0074+0073<br/><br/>02A6 | **z**ampa, **z**uppa |
| m | m | 006D | **m**a**mm**a, **m**ano |
| n | n | 006E | **n**ie**n**te, **n**otte |
| N | &#626; | 0272 | **gn**occhi, lasa**gn**a |
| r | r<br/><br/>&#638; | 0072<br/><br/>027E | ca**r**o, se**r**eno |
| R | rr<br/><br/>r&#720; | 0072+0072<br/><br/>0072+02D0 | te**rr**a, to**rr**e |
| l | l | 006C | **l**ento, pa**l**ma |
| L | &#654; | 028E | **gl**ielo, **gl**i |
| y | j | 006A | **i**eri, raso**i**o |
| w | w | 0077 | n**u**ovo, q**u**ando |
{: caption="Table 2. Consonants (Italian)"}

## Geminates
{: #itGeminates}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| DD | d&#675;<br/><br/>ddz | 0064+02A3<br/><br/>0064+0064+007A | a**zz**urro, me**zz**o |
| JJ | dd&#658;<br/><br/>d&#676; | 0064+0064+0292<br/><br/>0064+02A4 | Chio**gg**ia, ma**gg**io |
| TT | tts<br/><br/>t&#678; | 0074+0074+0073<br/><br/>0074+02A6 | ta**zz**a, chia**zz**a |
| CC | t&#679;<br/><br/>tt&#643; | 0074+02A7<br/><br/>0074+0074+0283 | ghia**cc**io, fe**cc**ia |
{: caption="Table 3. Geminates (Italian)"}

## Allophones
{: #itAllophones}

If an allophone is not used in SPR, the {{site.data.keyword.texttospeechshort}} service automatically generates the appropriate variant for the given context.

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| 'ng' [**1**] | &#331;g | 014B+0067<br/>014B+0261 | a**ng**olo, lu**ng**o |
| 'nk' [**1**] | &#331;k | 014B+006B | a**nc**ora, bia**nc**o |
{: caption="Table 4. Allophones (Italian)"}

**Note:**

1.  The `ng` and `nk` allophones are supported in the IPA specification but cannot be used in SPR.
