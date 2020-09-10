---

copyright:
  years: 2020
lastupdated: "2020-09-10"

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

# Mandarin Chinese symbols
{: #zhSymbols}

The following sections describe the valid symbols for Mandarin (Simplified) Chinese. Chinese symbols are described by using [Pinyin](https://en.wikipedia.org/wiki/Pinyin){: external}, which is a system that uses Latin characters to express how Chinese characters sound.

-   *Tables 1 through 3* show the initial (consonant) and final (vowel) characters that are used to express Chinese characters in pinyin.
-   *Table 4* shows the tone symbols that can be used with the initial and final symbols to specify the intonation of a Chinese character.
-   *Tables 5 and 6* provide groups of phonetic representations and examples of Mandarin Chinese synthesis.
-   *Tables 7 through 10* provide English symbols for consonants and different forms of vowels that you can use to construct pinyin representations.

## Using pinyin
{: #zhPinyinUsing}

In summary, a pinyin translation is expressed as: *Initial* + *Final* + *Tone*. This information identifies how to convert Chinese pinyin characters to actual Chinese IPA symbols. In tables 1 through 3:

-   The first column shows *initial* characters, which are the same in all three tables. A dash (`-`) in the first column indicates the absence of an initial.
-   The top row shows the *final* characters, which change from table to table.
-   The intersecting cells of the table show how the initial and final characters can be combined to produce a Chinese character. A dash (`-`) in a cell indicates that the combination of initial and final characters is not supported.

You can download a PDF file that documents tables 1 through 4: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/Text-to-Speech-Chinese-Pinyin.pdf" download="Text-to-Speech-Chinese-Pinyin.pdf">Text-to-Speech-Chinese-Pinyin.pdf <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. The information in the file matches the tables, but the file might be easier to work with.

## Pinyin characters (part 1)
{: #zhPinyinPart1}

| Finals /<br/>Initials | a | o | e | i | u | v | er | ai | ao | ou | un |
|:---------------------:|:-:|:-:|:-:|:-:|:-:|:-:|:--:|:--:|:--:|:--:|:--:|
| **-** | a | o | e | - | - | - | er | ai | ao | ou</tph>| - |
| **b** | ba | bo | - | bi | bu | - | - | bai | bao | - | - |
| **p** | pa | po | - | pi | pu | - | - | pai | pao | pou | - |
| **m** | ma | mo | - | mi | mu | - | - | mai | mao | mou | - |
| **f** | fa | fo | - | - | fu | - | - | - | - | fou | - |
| **d** | da | - | de | di | du | - | - | dai | dao | dou | dun |
| **t** | ta | - | te | ti | tu | - | - | tai | tao | tou | tun |
| **n** | na | - | ne | ni | nu | nv | - | nai | nao | nou | - |
| **l** | la | - | le | li | lu | lv | - | lai | lao | lou | lun |
| **g** | ga | - | ge | - | gu | - | - | gai | gao | gou | gun |
| **k** | ka | - | ke | - | ku | - | - | kai | kao | kou | kun |
| **h** | ha | - | he | - | hu | - | - | hai | hao | hou | hun |
| **j** | - | - | - | ji | ju | - | - | - | - | - | jun |
| **q** | - | - | - | qi | qu | - | - | - | - | - | qun |
| **x** | - | - | - | xi | xu | - | - | - | - | - | xun |
| **zh** | zha | - | zhe | zhi | zhu | - | - | zhai | zhao | zhou | zhun |
| **ch** | cha | - | che | chi | chu | - | - | chai | chao | chou | chun |
| **sh** | sha | - | she | shi | shu | - | - | shai | shao | shou | shun |
| **r** | - | - | re | ri | ru | - | - | - | rao | rou | run |
| **z** | za | - | ze | zi | zu | - | - | zai | zao | zou | zun |
| **c** | ca | - | ce | ci | cu | - | - | cai | cao | cou | cun |
| **s** | sa | - | se | si | su | - | - | sai | sao | sou | sun |
| **y** | ya | yo | ye | yi | yu | - | - | - | yao | you | yun |
| **w** | wa | wo | - | - | wu | - | - | wai | - | - | - |
{: caption="Table 1. Pinyin characters (part 1)"}

## Pinyin characters (part 2)
{: #zhPinyinPart2}

| Finals /<br/>Initials | ei | ia | ie | iu | iao | ua | uo | ui | uai | ue | uan |
|:---------------------:|:--:|:--:|:--:|:--:|:---:|:--:|:--:|:--:|:---:|:--:|:---:|
| **-** | ei | - | - | - | - | - | - | - | - | -</tph>| - |
| **b** | bei | - | bie | - | biao | - | - | - | - | - | - |
| **p** | pei | - | pie | - | piao | - | - | - | - | - | - |
| **m** | mei | - | mie | miu | miao | - | - | - | - | - | - |
| **f** | fei | - | - | - | - | - | - | - | - | - | - |
| **d** | dei | - | die | diu | diao | - | duo | dui | - | - | duan |
| **t** | tei | - | tie | - | tiao | - | tuo | tui | - | - | tuan |
| **n** | nei | - | nie | niu | niao | - | nuo | - | - | nue | nuan |
| **l** | lei | lia | lie | liu | liao | - | luo | - | - | lue | luan |
| **g** | gei | - | - | - | - | gua | guo | gui | guai | - | guan |
| **k** | kei | - | - | - | - | kua | kuo | kui | kuai | - | kuan |
| **h** | hei | - | - | - | - | hua | huo | hui | huai | - | huan |
| **j** | - | jia | jie | jiu | jiao | - | - | - | - | jue | juan |
| **q** | - | qia | qie | qiu | qiao | - | - | - | - | que | quan |
| **x** | - | xia | xie | xiu | xiao | - | - | - | - | xue | xuan |
| **zh** | - | - | - | - | - | zhua | zhuo | zhui | zhuai | - | zhuan |
| **ch** | - | - | - | - | - | - | chuo | chui | chuai | - | chuan |
| **sh** | shei | - | - | - | - | shua | shuo | shui | shuai | - | shuan |
| **r** | - | - | - | - | - | - | ruo | rui | - | - | ruan |
| **z** | zei | - | - | - | - | - | zuo | zui | - | - | zuan |
| **c** | - | - | - | - | - | - | cuo | cui | - | - | cuan |
| **s** | - | - | - | - | - | - | suo | sui | - | - | suan |
| **y** | - | - | - | - | - | - | - | - | - | yue | yuan |
| **w** | wei | - | - | - | - | - | - | - | - | - | - |
{: caption="Table 2. Pinyin characters (part 2)"}

## Pinyin characters (part 3)
{: #zhPinyinPart3}

| Finals /<br/>Initials | an | ang | ong | en | eng | in | ing | ian | iang | iong | uang |
|:---------------------:|:--:|:---:|:---:|:--:|:---:|:--:|:---:|:---:|:----:|:----:|:----:|
| **-** | an | ang | - | en | - | - | - | - | - | -</tph>| - |
| **b** | ban | bang | - | ben | beng | bin | bing | bian | - | - | - |
| **p** | pan | pang | - | pen | peng | pin | ping | pian | - | - | - |
| **m** | man | mang | - | men | meng | min | ming | mian | - | - | - |
| **f** | fan | fang | - | fen | feng | - | - | - | - | - | - |
| **d** | dan | dang | dong | - | deng | - | ding | dian | - | - | - |
| **t** | tan | tang | tong | - | teng | - | ting | tian | - | - | - |
| **n** | nan | nang | nong | nen | neng | nin | ning | nian | niang | - | - |
| **l** | lan | lang | long | - | leng | lin | ling | lian | liang | - | - |
| **g** | gan | gang | gong | gen | geng | - | - | - | - | - | guang |
| **k** | kan | kang | kong | ken | keng | - | - | - | - | - | kuang |
| **h** | han | hang | hong | hen | heng | - | - | - | - | - | huang |
| **j** | - | - | - | - | - | jin | jing | jian | jiang | jiong | - |
| **q** | - | - | - | - | - | qin | qing | qian | qiang | qiong | - |
| **x** | - | - | - | - | - | xin | xing | xian | xiang | xiong | - |
| **zh** | zhan | zhang | zhong | zhen | zheng | - | - | - | - | - | zhuang |
| **ch** | chan | chang | chong | chen | cheng | - | - | - | - | - | chuang |
| **sh** | shan | shang | - | shen | sheng | - | - | - | - | - | shuang |
| **r** | ran | rang | rong | ren | reng | - | - | - | - | - | - |
| **z** | zan | zang | zong | zen | zeng | - | - | - | - | - | - |
| **c** | can | cang | cong | cen | ceng | - | - | - | - | - | - |
| **s** | san | sang | song | sen | seng | - | - | - | - | - | - |
| **y** | yan | yang | yong | - | - | yin | ying | - | - | - | - |
| **w** | wan | wang | - | wen | weng | - | - | - | - | - | - |
{: caption="Table 3. Pinyin characters (part 3)"}

## Pinyin tone symbols
{: #zhPinyinTones}

| IPA symbol | IPA Unicode | Definition |
|:----------:|:-----------:|:----------:|
| &#741;&#741; | 02E5+02E5 | Tone 1 |
| &#743;&#741; | 02E7+02E5 | Tone 2 |
| &#744;&#745;&#742; | 02E8+02E9+02E6 | Tone 3 |
| &#741;&#745; | 02E5+02E9 | Tone 4 |
| &#743;&#743; | 02E7+02E7 | Neutral tone |
{: caption="Table 4. Pinyin tone symbols"}

## Chinese consonants
{: #zhChineseConsonants}

| IPA symbol | IPA Unicode | Example |
|:----------:|:-----------:|:-------:|
| p | 0070 | **b**o |
| p&#688; | 0070+02B0 | **p**o |
| m | 006D | **m**o |
| f | 0066 | **f**o |
| t | 0074 | **d**e |
| t&#688; | 0074+02B0 | **t**e |
| n | 006E | **n**e |
| l | 006C | **l**e |
| t&#642; | 0074+0282 | **zh**i |
| ts | 0074+0073 | **z**i |
| t&#642;&#688; | 0074+0282+02B0 | **ch**i |
| ts&#688; | 0074+0073+02B0 | **c**i |
| &#642; | 0282 | **sh**i |
| s | 0073 | **s**i |
| &#656; | 0290 | **r**i |
| &#680; | 02AB | **j**i |
| &#680;&#688; | 02AB+02B0 | **q**i |
| &#597; | 0255 | **x**i |
| k | 006B | **g**e |
| k&#688; | 006B+02B0 | **k**e |
| x | 0078 | **h**e |
| w | 0077 | **w**a |
| j | 006A | **y**a |
| &#613; | 0265 | **yu**e |
| &#331; | 014B | a**ng** |
{: caption="Table 5. Chinese consonants"}

## Chinese vowels
{: #zhChineseVowels}

| IPA symbol | IPA Unicode | Example |
|:----------:|:-----------:|:-------:|
| a | 0061 | b**a** |
| o | 006F | p**o** |
| &#601; | 0259 | d**e** |
| a&#618; | 0061+026A | k**ai** |
| a&#650; | 0061+028A | d**ao** |
| &#601;&#650; | 0259+028A | t**ou** |
| e&#618; | 0065+026A | f**ei** |
| i | 0069 | x**i** |
| &#616; | 0268 | zh**i** |
| u | 0075 | zh**u** |
| y | 0079 | **yu** |
| &#603; | 025B | ji**e** |
| &#602; | 025A | **er** |
{: caption="Table 6. Chinese vowels"}

## English consonants
{: #zhEnglishConsonants}

| IPA symbol | IPA Unicode | Example |
|:----------:|:-----------:|:-------:|
| p | 0070 | **p**en |
| b | 0062 | **b**ut |
| t | 0074 | **t**wo |
| d | 0064 | **d**o |
| &#679; | 02A7 | **ch**air |
| &#676; | 02A4 | **j**oy |
| k | 006B | **c**at |
| g | 0067 | **g**et |
| f | 0066 | **f**ool |
| v | 0076 | **v**oice |
| &#952; | 03B8 | **th**ink |
| &#240; | 00F0 | **th**is |
| s | 0073 | **s**ee |
| z | 007A | **z**oo |
| &#643; | 0283 | **sh**e |
| &#658; | 0292 | plea**s**ure |
| h | 0068 | **h**am |
| m | 006D | **m**an |
| n | 006E | **n**o |
| &#331; | 014B | ri**ng** |
| l | 006C | **l**eft |
| &#633; | 0279 | **wr**ong |
| j | 006A | **y**es |
| w | 0077 | **w**e |
{: caption="Table 7. English consonants"}

## English vowels
{: #zhEnglishVowels}

| IPA symbol | IPA Unicode | Example |
|:----------:|:-----------:|:-------:|
| &#593;&#720; | 0251+02D0 | f**a**ther |
| i&#720; | 0069+02D0 | s**ee** |
| &#596;&#720; | 0254+02D0 | l**aw** |
| u&#720; | 0075+02D0 | s**oo**n |
| &#604;&#720; | 025C+02D0 | b**i**rd |
{: caption="Table 8. English vowels"}

## English monophthongs
{: #zhEnglishMonophthongs}

| IPA symbol | IPA Unicode | Example |
|:----------:|:-----------:|:-------:|
| &#594; | 0252 | n**o**t |
| &#230; | 00E6 | c**a**t |
| e | 0065 | p**e**t |
| &#618; | 026A | c**i**ty |
| &#650; | 028A | p**u**t |
| &#652; | 028C | r**u**n |
| &#601; | 0259 | **a**bout |
{: caption="Table 9. English monophthongs"}

## English diphthongs
{: #zhEnglishDiphthongs}

| IPA symbol | IPA Unicode | Example |
|:----------:|:-----------:|:-------:|
| a&#618; | 0061+026A | r**i**se |
| e&#618; | 0065+026A | r**ai**se |
| &#596;&#618; | 0254+026A | n**oi**se |
| a&#650; | 0061+028A | r**ou**se |
| &#601;&#650; | 0259+028A | n**o**se |
| e&#601; | 0065+0259 | st**ai**rs |
| &#618;&#601; | 026A+0259 | f**ea**r |
| &#650;&#601; | 028A+0259 | c**u**re |
{: caption="Table 10. English diphthongs"}
