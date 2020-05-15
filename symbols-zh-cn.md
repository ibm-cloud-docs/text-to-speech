---

copyright:
  years: 2020
lastupdated: "2020-05-15"

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

You can download a PDF file that documents tables 1 through 4: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/Text-to-Speech-Chinese-Pinyin.pdf" download="Text-to-Speech-Chinese-Pinyin.pdf">Text-to-Speech-Chinese-Pinyin.pdf <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. The information in the file matches the tables, but the file might be easier to work with.

## Pinyin characters (part 1)
{: #zhPinyinPart1}

<table>
  <caption>Table 1. Pinyin characters (part 1)</caption>
  <tr>
    <th style="text-align:center;vertical-align:bottom">
      Finals /<br/>Initials
    </th>
    <th style="text-align:center;vertical-align:bottom">
      a
    </th>
    <th style="text-align:center;vertical-align:bottom">
      o
    </th>
    <th style="text-align:center;vertical-align:bottom">
      e
    </th>
    <th style="text-align:center;vertical-align:bottom">
      i
    </th>
    <th style="text-align:center;vertical-align:bottom">
      u
    </th>
    <th style="text-align:center;vertical-align:bottom">
      v
    </th>
    <th style="text-align:center;vertical-align:bottom">
      er
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ai
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ao
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ou
    </th>
    <th style="text-align:center;vertical-align:bottom">
      un
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      **-**
    </td>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      er
    </td>
    <td style="text-align:center">
      ai
    </td>
    <td style="text-align:center">
      ao
    </td>
    <td style="text-align:center">
      ou
    </tph>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **b**
    </td>
    <td style="text-align:center">
      ba
    </td>
    <td style="text-align:center">
      bo
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      bi
    </td>
    <td style="text-align:center">
      bu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      bai
    </td>
    <td style="text-align:center">
      bao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **p**
    </td>
    <td style="text-align:center">
      pa
    </td>
    <td style="text-align:center">
      po
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      pi
    </td>
    <td style="text-align:center">
      pu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      pai
    </td>
    <td style="text-align:center">
      pao
    </td>
    <td style="text-align:center">
      pou
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **m**
    </td>
    <td style="text-align:center">
      ma
    </td>
    <td style="text-align:center">
      mo
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      mi
    </td>
    <td style="text-align:center">
      mu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      mai
    </td>
    <td style="text-align:center">
      mao
    </td>
    <td style="text-align:center">
      mou
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **f**
    </td>
    <td style="text-align:center">
      fa
    </td>
    <td style="text-align:center">
      fo
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      fu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      fou
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **d**
    </td>
    <td style="text-align:center">
      da
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      de
    </td>
    <td style="text-align:center">
      di
    </td>
    <td style="text-align:center">
      du
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      dai
    </td>
    <td style="text-align:center">
      dao
    </td>
    <td style="text-align:center">
      dou
    </td>
    <td style="text-align:center">
      dun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **t**
    </td>
    <td style="text-align:center">
      ta
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      te
    </td>
    <td style="text-align:center">
      ti
    </td>
    <td style="text-align:center">
      tu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      tai
    </td>
    <td style="text-align:center">
      tao
    </td>
    <td style="text-align:center">
      tou
    </td>
    <td style="text-align:center">
      tun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **n**
    </td>
    <td style="text-align:center">
      na
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ne
    </td>
    <td style="text-align:center">
      ni
    </td>
    <td style="text-align:center">
      nu
    </td>
    <td style="text-align:center">
      nv
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      nai
    </td>
    <td style="text-align:center">
      nao
    </td>
    <td style="text-align:center">
      nou
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **l**
    </td>
    <td style="text-align:center">
      la
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      le
    </td>
    <td style="text-align:center">
      li
    </td>
    <td style="text-align:center">
      lu
    </td>
    <td style="text-align:center">
      lv
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      lai
    </td>
    <td style="text-align:center">
      lao
    </td>
    <td style="text-align:center">
      lou
    </td>
    <td style="text-align:center">
      lun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **g**
    </td>
    <td style="text-align:center">
      ga
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ge
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      gu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      gai
    </td>
    <td style="text-align:center">
      gao
    </td>
    <td style="text-align:center">
      gou
    </td>
    <td style="text-align:center">
      gun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **k**
    </td>
    <td style="text-align:center">
      ka
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ke
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ku
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      kai
    </td>
    <td style="text-align:center">
      kao
    </td>
    <td style="text-align:center">
      kou
    </td>
    <td style="text-align:center">
      kun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **h**
    </td>
    <td style="text-align:center">
      ha
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      he
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      hu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      hai
    </td>
    <td style="text-align:center">
      hao
    </td>
    <td style="text-align:center">
      hou
    </td>
    <td style="text-align:center">
      hun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **j**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ji
    </td>
    <td style="text-align:center">
      ju
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      jun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **q**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      qi
    </td>
    <td style="text-align:center">
      qu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      qun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **x**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      xi
    </td>
    <td style="text-align:center">
      xu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      xun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **zh**
    </td>
    <td style="text-align:center">
      zha
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      zhe
    </td>
    <td style="text-align:center">
      zhi
    </td>
    <td style="text-align:center">
      zhu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      zhai
    </td>
    <td style="text-align:center">
      zhao
    </td>
    <td style="text-align:center">
      zhou
    </td>
    <td style="text-align:center">
      zhun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **ch**
    </td>
    <td style="text-align:center">
      cha
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      che
    </td>
    <td style="text-align:center">
      chi
    </td>
    <td style="text-align:center">
      chu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      chai
    </td>
    <td style="text-align:center">
      chao
    </td>
    <td style="text-align:center">
      chou
    </td>
    <td style="text-align:center">
      chun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **sh**
    </td>
    <td style="text-align:center">
      sha
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      she
    </td>
    <td style="text-align:center">
      shi
    </td>
    <td style="text-align:center">
      shu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      shai
    </td>
    <td style="text-align:center">
      shao
    </td>
    <td style="text-align:center">
      shou
    </td>
    <td style="text-align:center">
      shun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **r**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      re
    </td>
    <td style="text-align:center">
      ri
    </td>
    <td style="text-align:center">
      ru
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      rao
    </td>
    <td style="text-align:center">
      rou
    </td>
    <td style="text-align:center">
      run
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **z**
    </td>
    <td style="text-align:center">
      za
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ze
    </td>
    <td style="text-align:center">
      zi
    </td>
    <td style="text-align:center">
      zu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      zai
    </td>
    <td style="text-align:center">
      zao
    </td>
    <td style="text-align:center">
      zou
    </td>
    <td style="text-align:center">
      zun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **c**
    </td>
    <td style="text-align:center">
      ca
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ce
    </td>
    <td style="text-align:center">
      ci
    </td>
    <td style="text-align:center">
      cu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      cai
    </td>
    <td style="text-align:center">
      cao
    </td>
    <td style="text-align:center">
      cou
    </td>
    <td style="text-align:center">
      cun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **s**
    </td>
    <td style="text-align:center">
      sa
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      se
    </td>
    <td style="text-align:center">
      si
    </td>
    <td style="text-align:center">
      su
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      sai
    </td>
    <td style="text-align:center">
      sao
    </td>
    <td style="text-align:center">
      sou
    </td>
    <td style="text-align:center">
      sun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **y**
    </td>
    <td style="text-align:center">
      ya
    </td>
    <td style="text-align:center">
      yo
    </td>
    <td style="text-align:center">
      ye
    </td>
    <td style="text-align:center">
      yi
    </td>
    <td style="text-align:center">
      yu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      yao
    </td>
    <td style="text-align:center">
      you
    </td>
    <td style="text-align:center">
      yun
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **w**
    </td>
    <td style="text-align:center">
      wa
    </td>
    <td style="text-align:center">
      wo
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      wu
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      wai
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
</table>

## Pinyin characters (part 2)
{: #zhPinyinPart2}

<table>
  <caption>Table 2. Pinyin characters (part 2)</caption>
  <tr>
    <th style="text-align:center;vertical-align:bottom">
      Finals /<br/>Initials
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ei
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ia
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ie
    </th>
    <th style="text-align:center;vertical-align:bottom">
      iu
    </th>
    <th style="text-align:center;vertical-align:bottom">
      iao
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ua
    </th>
    <th style="text-align:center;vertical-align:bottom">
      uo
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ui
    </th>
    <th style="text-align:center;vertical-align:bottom">
      uai
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ue
    </th>
    <th style="text-align:center;vertical-align:bottom">
      uan
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      **-**
    </td>
    <td style="text-align:center">
      ei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </tph>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **b**
    </td>
    <td style="text-align:center">
      bei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      bie
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      biao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **p**
    </td>
    <td style="text-align:center">
      pei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      pie
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      piao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **m**
    </td>
    <td style="text-align:center">
      mei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      mie
    </td>
    <td style="text-align:center">
      miu
    </td>
    <td style="text-align:center">
      miao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **f**
    </td>
    <td style="text-align:center">
      fei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **d**
    </td>
    <td style="text-align:center">
      dei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      die
    </td>
    <td style="text-align:center">
      diu
    </td>
    <td style="text-align:center">
      diao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      duo
    </td>
    <td style="text-align:center">
      dui
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      duan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **t**
    </td>
    <td style="text-align:center">
      tei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      tie
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      tiao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      tuo
    </td>
    <td style="text-align:center">
      tui
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      tuan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **n**
    </td>
    <td style="text-align:center">
      nei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      nie
    </td>
    <td style="text-align:center">
      niu
    </td>
    <td style="text-align:center">
      niao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      nuo
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      nue
    </td>
    <td style="text-align:center">
      nuan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **l**
    </td>
    <td style="text-align:center">
      lei
    </td>
    <td style="text-align:center">
      lia
    </td>
    <td style="text-align:center">
      lie
    </td>
    <td style="text-align:center">
      liu
    </td>
    <td style="text-align:center">
      liao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      luo
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      lue
    </td>
    <td style="text-align:center">
      luan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **g**
    </td>
    <td style="text-align:center">
      gei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      gua
    </td>
    <td style="text-align:center">
      guo
    </td>
    <td style="text-align:center">
      gui
    </td>
    <td style="text-align:center">
      guai
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      guan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **k**
    </td>
    <td style="text-align:center">
      kei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      kua
    </td>
    <td style="text-align:center">
      kuo
    </td>
    <td style="text-align:center">
      kui
    </td>
    <td style="text-align:center">
      kuai
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      kuan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **h**
    </td>
    <td style="text-align:center">
      hei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      hua
    </td>
    <td style="text-align:center">
      huo
    </td>
    <td style="text-align:center">
      hui
    </td>
    <td style="text-align:center">
      huai
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      huan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **j**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      jia
    </td>
    <td style="text-align:center">
      jie
    </td>
    <td style="text-align:center">
      jiu
    </td>
    <td style="text-align:center">
      jiao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      jue
    </td>
    <td style="text-align:center">
      juan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **q**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      qia
    </td>
    <td style="text-align:center">
      qie
    </td>
    <td style="text-align:center">
      qiu
    </td>
    <td style="text-align:center">
      qiao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      que
    </td>
    <td style="text-align:center">
      quan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **x**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      xia
    </td>
    <td style="text-align:center">
      xie
    </td>
    <td style="text-align:center">
      xiu
    </td>
    <td style="text-align:center">
      xiao
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      xue
    </td>
    <td style="text-align:center">
      xuan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **zh**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      zhua
    </td>
    <td style="text-align:center">
      zhuo
    </td>
    <td style="text-align:center">
      zhui
    </td>
    <td style="text-align:center">
      zhuai
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      zhuan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **ch**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      chuo
    </td>
    <td style="text-align:center">
      chui
    </td>
    <td style="text-align:center">
      chuai
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      chuan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **sh**
    </td>
    <td style="text-align:center">
      shei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      shua
    </td>
    <td style="text-align:center">
      shuo
    </td>
    <td style="text-align:center">
      shui
    </td>
    <td style="text-align:center">
      shuai
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      shuan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **r**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ruo
    </td>
    <td style="text-align:center">
      rui
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ruan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **z**
    </td>
    <td style="text-align:center">
      zei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      zuo
    </td>
    <td style="text-align:center">
      zui
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      zuan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **c**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      cuo
    </td>
    <td style="text-align:center">
      cui
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      cuan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **s**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      suo
    </td>
    <td style="text-align:center">
      sui
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      suan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **y**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      yue
    </td>
    <td style="text-align:center">
      yuan
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **w**
    </td>
    <td style="text-align:center">
      wei
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
</table>

## Pinyin characters (part 3)
{: #zhPinyinPart3}

<table>
  <caption>Table 3. Pinyin characters (part 3)</caption>
  <tr>
    <th style="text-align:center;vertical-align:bottom">
      Finals /<br/>Initials
    </th>
    <th style="text-align:center;vertical-align:bottom">
      an
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ang
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ong
    </th>
    <th style="text-align:center;vertical-align:bottom">
      en
    </th>
    <th style="text-align:center;vertical-align:bottom">
      eng
    </th>
    <th style="text-align:center;vertical-align:bottom">
      in
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ing
    </th>
    <th style="text-align:center;vertical-align:bottom">
      ian
    </th>
    <th style="text-align:center;vertical-align:bottom">
      iang
    </th>
    <th style="text-align:center;vertical-align:bottom">
      iong
    </th>
    <th style="text-align:center;vertical-align:bottom">
      uang
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      **-**
    </td>
    <td style="text-align:center">
      an
    </td>
    <td style="text-align:center">
      ang
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      en
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </tph>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **b**
    </td>
    <td style="text-align:center">
      ban
    </td>
    <td style="text-align:center">
      bang
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ben
    </td>
    <td style="text-align:center">
      beng
    </td>
    <td style="text-align:center">
      bin
    </td>
    <td style="text-align:center">
      bing
    </td>
    <td style="text-align:center">
      bian
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **p**
    </td>
    <td style="text-align:center">
      pan
    </td>
    <td style="text-align:center">
      pang
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      pen
    </td>
    <td style="text-align:center">
      peng
    </td>
    <td style="text-align:center">
      pin
    </td>
    <td style="text-align:center">
      ping
    </td>
    <td style="text-align:center">
      pian
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **m**
    </td>
    <td style="text-align:center">
      man
    </td>
    <td style="text-align:center">
      mang
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      men
    </td>
    <td style="text-align:center">
      meng
    </td>
    <td style="text-align:center">
      min
    </td>
    <td style="text-align:center">
      ming
    </td>
    <td style="text-align:center">
      mian
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **f**
    </td>
    <td style="text-align:center">
      fan
    </td>
    <td style="text-align:center">
      fang
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      fen
    </td>
    <td style="text-align:center">
      feng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **d**
    </td>
    <td style="text-align:center">
      dan
    </td>
    <td style="text-align:center">
      dang
    </td>
    <td style="text-align:center">
      dong
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      deng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ding
    </td>
    <td style="text-align:center">
      dian
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **t**
    </td>
    <td style="text-align:center">
      tan
    </td>
    <td style="text-align:center">
      tang
    </td>
    <td style="text-align:center">
      tong
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      teng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      ting
    </td>
    <td style="text-align:center">
      tian
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **n**
    </td>
    <td style="text-align:center">
      nan
    </td>
    <td style="text-align:center">
      nang
    </td>
    <td style="text-align:center">
      nong
    </td>
    <td style="text-align:center">
      nen
    </td>
    <td style="text-align:center">
      neng
    </td>
    <td style="text-align:center">
      nin
    </td>
    <td style="text-align:center">
      ning
    </td>
    <td style="text-align:center">
      nian
    </td>
    <td style="text-align:center">
      niang
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **l**
    </td>
    <td style="text-align:center">
      lan
    </td>
    <td style="text-align:center">
      lang
    </td>
    <td style="text-align:center">
      long
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      leng
    </td>
    <td style="text-align:center">
      lin
    </td>
    <td style="text-align:center">
      ling
    </td>
    <td style="text-align:center">
      lian
    </td>
    <td style="text-align:center">
      liang
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **g**
    </td>
    <td style="text-align:center">
      gan
    </td>
    <td style="text-align:center">
      gang
    </td>
    <td style="text-align:center">
      gong
    </td>
    <td style="text-align:center">
      gen
    </td>
    <td style="text-align:center">
      geng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      guang
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **k**
    </td>
    <td style="text-align:center">
      kan
    </td>
    <td style="text-align:center">
      kang
    </td>
    <td style="text-align:center">
      kong
    </td>
    <td style="text-align:center">
      ken
    </td>
    <td style="text-align:center">
      keng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      kuang
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **h**
    </td>
    <td style="text-align:center">
      han
    </td>
    <td style="text-align:center">
      hang
    </td>
    <td style="text-align:center">
      hong
    </td>
    <td style="text-align:center">
      hen
    </td>
    <td style="text-align:center">
      heng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      huang
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **j**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      jin
    </td>
    <td style="text-align:center">
      jing
    </td>
    <td style="text-align:center">
      jian
    </td>
    <td style="text-align:center">
      jiang
    </td>
    <td style="text-align:center">
      jiong
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **q**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      qin
    </td>
    <td style="text-align:center">
      qing
    </td>
    <td style="text-align:center">
      qian
    </td>
    <td style="text-align:center">
      qiang
    </td>
    <td style="text-align:center">
      qiong
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **x**
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      xin
    </td>
    <td style="text-align:center">
      xing
    </td>
    <td style="text-align:center">
      xian
    </td>
    <td style="text-align:center">
      xiang
    </td>
    <td style="text-align:center">
      xiong
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **zh**
    </td>
    <td style="text-align:center">
      zhan
    </td>
    <td style="text-align:center">
      zhang
    </td>
    <td style="text-align:center">
      zhong
    </td>
    <td style="text-align:center">
      zhen
    </td>
    <td style="text-align:center">
      zheng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      zhuang
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **ch**
    </td>
    <td style="text-align:center">
      chan
    </td>
    <td style="text-align:center">
      chang
    </td>
    <td style="text-align:center">
      chong
    </td>
    <td style="text-align:center">
      chen
    </td>
    <td style="text-align:center">
      cheng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      chuang
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **sh**
    </td>
    <td style="text-align:center">
      shan
    </td>
    <td style="text-align:center">
      shang
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      shen
    </td>
    <td style="text-align:center">
      sheng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      shuang
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **r**
    </td>
    <td style="text-align:center">
      ran
    </td>
    <td style="text-align:center">
      rang
    </td>
    <td style="text-align:center">
      rong
    </td>
    <td style="text-align:center">
      ren
    </td>
    <td style="text-align:center">
      reng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **z**
    </td>
    <td style="text-align:center">
      zan
    </td>
    <td style="text-align:center">
      zang
    </td>
    <td style="text-align:center">
      zong
    </td>
    <td style="text-align:center">
      zen
    </td>
    <td style="text-align:center">
      zeng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **c**
    </td>
    <td style="text-align:center">
      can
    </td>
    <td style="text-align:center">
      cang
    </td>
    <td style="text-align:center">
      cong
    </td>
    <td style="text-align:center">
      cen
    </td>
    <td style="text-align:center">
      ceng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **s**
    </td>
    <td style="text-align:center">
      san
    </td>
    <td style="text-align:center">
      sang
    </td>
    <td style="text-align:center">
      song
    </td>
    <td style="text-align:center">
      sen
    </td>
    <td style="text-align:center">
      seng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **y**
    </td>
    <td style="text-align:center">
      yan
    </td>
    <td style="text-align:center">
      yang
    </td>
    <td style="text-align:center">
      yong
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      yin
    </td>
    <td style="text-align:center">
      ying
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      **w**
    </td>
    <td style="text-align:center">
      wan
    </td>
    <td style="text-align:center">
      wang
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      wen
    </td>
    <td style="text-align:center">
      weng
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
    <td style="text-align:center">
      -
    </td>
  </tr>
</table>

## Pinyin tone symbols
{: #zhPinyinTones}

<table style="width:70%">
  <caption>Table 4. Pinyin tone symbols</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:25%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:center; vertical-align:bottom">
      Definition
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      &#741;&#741;
    </td>
    <td style="text-align:center">
      02E5+02E5
    </td>
    <td style="text-align:center">
      Tone 1
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#743;&#741;
    </td>
    <td style="text-align:center">
      02E7+02E5
    </td>
    <td style="text-align:center">
      Tone 2
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#744;&#745;&#742;
    </td>
    <td style="text-align:center">
      02E8+02E9+02E6
    </td>
    <td style="text-align:center">
      Tone 3
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#741;&#745;
    </td>
    <td style="text-align:center">
      02E5+02E9
    </td>
    <td style="text-align:center">
      Tone 4
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#743;&#743;
    </td>
    <td style="text-align:center">
      02E7+02E7
    </td>
    <td style="text-align:center">
      Neutral tone
    </td>
  </tr>
</table>

## Chinese consonants
{: #zhChineseConsonants}

<table style="width:70%">
  <caption>Table 5. Chinese consonants</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:25%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:center; vertical-align:bottom">
      Example
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      0070
    </td>
    <td style="text-align:center">
      **b**o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      p&#688;
    </td>
    <td style="text-align:center">
      0070+02B0
    </td>
    <td style="text-align:center">
      **p**o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      006D
    </td>
    <td style="text-align:center">
      **m**o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      0066
    </td>
    <td style="text-align:center">
      **f**o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      0074
    </td>
    <td style="text-align:center">
      **d**e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t&#688;
    </td>
    <td style="text-align:center">
      0074+02B0
    </td>
    <td style="text-align:center">
      **t**e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      006E
    </td>
    <td style="text-align:center">
      **n**e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      006C
    </td>
    <td style="text-align:center">
      **l**e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t&#642;
    </td>
    <td style="text-align:center">
      0074+0282
    </td>
    <td style="text-align:center">
      **zh**i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      ts
    </td>
    <td style="text-align:center">
      0074+0073
    </td>
    <td style="text-align:center">
      **z**i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t&#642;&#688;
    </td>
    <td style="text-align:center">
      0074+0282+02B0
    </td>
    <td style="text-align:center">
      **ch**i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      ts&#688;
    </td>
    <td style="text-align:center">
      0074+0073+02B0
    </td>
    <td style="text-align:center">
      **c**i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#642;
    </td>
    <td style="text-align:center">
      0282
    </td>
    <td style="text-align:center">
      **sh**i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      0073
    </td>
    <td style="text-align:center">
      **s**i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#656;
    </td>
    <td style="text-align:center">
      0290
    </td>
    <td style="text-align:center">
      **r**i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#680;
    </td>
    <td style="text-align:center">
      02AB
    </td>
    <td style="text-align:center">
      **j**i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#680;&#688;
    </td>
    <td style="text-align:center">
      02AB+02B0
    </td>
    <td style="text-align:center">
      **q**i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#597;
    </td>
    <td style="text-align:center">
      0255
    </td>
    <td style="text-align:center">
      **x**i
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      006B
    </td>
    <td style="text-align:center">
      **g**e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      k&#688;
    </td>
    <td style="text-align:center">
      006B+02B0
    </td>
    <td style="text-align:center">
      **k**e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      x
    </td>
    <td style="text-align:center">
      0078
    </td>
    <td style="text-align:center">
      **h**e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      0077
    </td>
    <td style="text-align:center">
      **w**a
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      006A
    </td>
    <td style="text-align:center">
      **y**a
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#613;
    </td>
    <td style="text-align:center">
      0265
    </td>
    <td style="text-align:center">
      **yu**e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#331;
    </td>
    <td style="text-align:center">
      014B
    </td>
    <td style="text-align:center">
      a**ng**
    </td>
  </tr>
</table>

## Chinese vowels
{: #zhChineseVowels}

<table style="width:70%">
  <caption>Table 6. Chinese vowels</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:25%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:center; vertical-align:bottom">
      Example
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      a
    </td>
    <td style="text-align:center">
      0061
    </td>
    <td style="text-align:center">
      b**a**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      o
    </td>
    <td style="text-align:center">
      006F
    </td>
    <td style="text-align:center">
      p**o**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#601;
    </td>
    <td style="text-align:center">
      0259
    </td>
    <td style="text-align:center">
      d**e**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      a&#618;
    </td>
    <td style="text-align:center">
      0061+026A
    </td>
    <td style="text-align:center">
      k**ai**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      a&#650;
    </td>
    <td style="text-align:center">
      0061+028A
    </td>
    <td style="text-align:center">
      d**ao**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#601;&#650;
    </td>
    <td style="text-align:center">
      0259+028A
    </td>
    <td style="text-align:center">
      t**ou**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e&#618;
    </td>
    <td style="text-align:center">
      0065+026A
    </td>
    <td style="text-align:center">
      f**ei**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      i
    </td>
    <td style="text-align:center">
      0069
    </td>
    <td style="text-align:center">
      x**i**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#616;
    </td>
    <td style="text-align:center">
      0268
    </td>
    <td style="text-align:center">
      zh**i**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      u
    </td>
    <td style="text-align:center">
      0075
    </td>
    <td style="text-align:center">
      zh**u**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      y
    </td>
    <td style="text-align:center">
      0079
    </td>
    <td style="text-align:center">
      **yu**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#603;
    </td>
    <td style="text-align:center">
      025B
    </td>
    <td style="text-align:center">
      ji**e**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#602;
    </td>
    <td style="text-align:center">
      025A
    </td>
    <td style="text-align:center">
      **er**
    </td>
  </tr>
</table>

## English consonants
{: #zhEnglishConsonants}

<table style="width:70%">
  <caption>Table 7. English consonants</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:25%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:center; vertical-align:bottom">
      Example
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      p
    </td>
    <td style="text-align:center">
      0070
    </td>
    <td style="text-align:center">
      **p**en
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      b
    </td>
    <td style="text-align:center">
      0062
    </td>
    <td style="text-align:center">
      **b**ut
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      t
    </td>
    <td style="text-align:center">
      0074
    </td>
    <td style="text-align:center">
      **t**wo
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      d
    </td>
    <td style="text-align:center">
      0064
    </td>
    <td style="text-align:center">
      **d**o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#679;
    </td>
    <td style="text-align:center">
      02A7
    </td>
    <td style="text-align:center">
      **ch**air
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#676;
    </td>
    <td style="text-align:center">
      02A4
    </td>
    <td style="text-align:center">
      **j**oy
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      k
    </td>
    <td style="text-align:center">
      006B
    </td>
    <td style="text-align:center">
      **c**at
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      g
    </td>
    <td style="text-align:center">
      0067
    </td>
    <td style="text-align:center">
      **g**et
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      f
    </td>
    <td style="text-align:center">
      0066
    </td>
    <td style="text-align:center">
      **f**ool
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      v
    </td>
    <td style="text-align:center">
     0076
    </td>
    <td style="text-align:center">
      **v**oice
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#952;
    </td>
    <td style="text-align:center">
      03B8
    </td>
    <td style="text-align:center">
      **th**ink
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#240;
    </td>
    <td style="text-align:center">
      00F0
    </td>
    <td style="text-align:center">
      **th**is
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      s
    </td>
    <td style="text-align:center">
      0073
    </td>
    <td style="text-align:center">
      **s**ee
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      z
    </td>
    <td style="text-align:center">
      007A
    </td>
    <td style="text-align:center">
      **z**oo
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#643;
    </td>
    <td style="text-align:center">
      0283
    </td>
    <td style="text-align:center">
      **sh**e
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#658;
    </td>
    <td style="text-align:center">
      0292
    </td>
    <td style="text-align:center">
      plea**s**ure
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      h
    </td>
    <td style="text-align:center">
      0068
    </td>
    <td style="text-align:center">
      **h**am
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      m
    </td>
    <td style="text-align:center">
      006D
    </td>
    <td style="text-align:center">
      **m**an
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      n
    </td>
    <td style="text-align:center">
      006E
    </td>
    <td style="text-align:center">
      **n**o
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#331;
    </td>
    <td style="text-align:center">
      014B
    </td>
    <td style="text-align:center">
      ri**ng**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      l
    </td>
    <td style="text-align:center">
      006C
    </td>
    <td style="text-align:center">
      **l**eft
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#633;
    </td>
    <td style="text-align:center">
      0279
    </td>
    <td style="text-align:center">
      **wr**ong
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      j
    </td>
    <td style="text-align:center">
      006A
    </td>
    <td style="text-align:center">
      **y**es
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      w
    </td>
    <td style="text-align:center">
      0077
    </td>
    <td style="text-align:center">
      **w**e
    </td>
  </tr>
</table>

## English vowels
{: #zhEnglishVowels}

<table style="width:70%">
  <caption>Table 8. English vowels</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:25%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:center; vertical-align:bottom">
      Example
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      &#593;&#720;
    </td>
    <td style="text-align:center">
      0251+02D0
    </td>
    <td style="text-align:center">
      f**a**ther
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      i&#720;
    </td>
    <td style="text-align:center">
      0069+02D0
    </td>
    <td style="text-align:center">
      s**ee**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#596;&#720;
    </td>
    <td style="text-align:center">
      0254+02D0
    </td>
    <td style="text-align:center">
      l**aw**
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      u&#720;
    </td>
    <td style="text-align:center">
      0075+02D0
    </td>
    <td style="text-align:center">
      s**oo**n
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#604;&#720;
    </td>
    <td style="text-align:center">
      025C+02D0
    </td>
    <td style="text-align:center">
      b**i**rd
    </td>
  </tr>
</table>

## English monophthongs
{: #zhEnglishMonophthongs}

<table style="width:70%">
  <caption>Table 9. English monophthongs</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:25%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:center; vertical-align:bottom">
      Example
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      &#594;
    </td>
    <td style="text-align:center">
      0252
    </td>
    <td style="text-align:center">
      n**o**t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#230;
    </td>
    <td style="text-align:center">
      00E6
    </td>
    <td style="text-align:center">
      c**a**t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e
    </td>
    <td style="text-align:center">
      0065
    </td>
    <td style="text-align:center">
      p**e**t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#618;
    </td>
    <td style="text-align:center">
      026A
    </td>
    <td style="text-align:center">
      c**i**ty
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#650;
    </td>
    <td style="text-align:center">
      028A
    </td>
    <td style="text-align:center">
      p**u**t
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#652;
    </td>
    <td style="text-align:center">
      028C
    </td>
    <td style="text-align:center">
      r**u**n
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#601;
    </td>
    <td style="text-align:center">
      0259
    </td>
    <td style="text-align:center">
      **a**bout
    </td>
  </tr>
</table>

## English diphthongs
{: #zhEnglishDiphthongs}

<table style="width:70%">
  <caption>Table 10. English diphthongs</caption>
  <tr>
    <th style="width:20%; text-align:center; vertical-align:bottom">
      IPA symbol
    </th>
    <th style="width:25%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:center; vertical-align:bottom">
      Example
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      a&#618;
    </td>
    <td style="text-align:center">
      0061+026A
    </td>
    <td style="text-align:center">
      r**i**se
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e&#618;
    </td>
    <td style="text-align:center">
      0065+026A
    </td>
    <td style="text-align:center">
      r**ai**se
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#596;&#618;
    </td>
    <td style="text-align:center">
      0254+026A
    </td>
    <td style="text-align:center">
      n**oi**se
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      a&#650;
    </td>
    <td style="text-align:center">
      0061+028A
    </td>
    <td style="text-align:center">
      r**ou**se
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#601;&#650;
    </td>
    <td style="text-align:center">
      0259+028A
    </td>
    <td style="text-align:center">
      n**o**se
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      e&#601;
    </td>
    <td style="text-align:center">
      0065+0259
    </td>
    <td style="text-align:center">
      st**ai**rs
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#618;&#601;
    </td>
    <td style="text-align:center">
      026A+0259
    </td>
    <td style="text-align:center">
      f**ea**r
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      &#650;&#601;
    </td>
    <td style="text-align:center">
      028A+0259
    </td>
    <td style="text-align:center">
      c**u**re
    </td>
  </tr>
</table>
