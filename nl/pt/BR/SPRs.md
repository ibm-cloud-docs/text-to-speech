---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-06"

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

# Usando o IBM SPR
{: #sprs}

O serviço {{site.data.keyword.texttospeechfull}} suporta as notações padrão do Alfabeto Fonético Internacional (IPA) e do {{site.data.keyword.IBM}} Symbolic Phonetic Representation (SPR) para representar os sons de palavras. O SPR é uma codificação fonética que representa a pronúncia de uma palavra, os sons que a compõem, como esses sons são divididos em sílabas e quais sílabas estão acentuadas. O SPR é uma representação alternativa para o IPA.
{: shortdesc}

As seções a seguir introduzem a notação do {{site.data.keyword.IBM_notm}} SPR. Como o IPA é uma notação padrão, a documentação não fornece informações básicas de uso para o IPA. Para obter uma orientação de uso breve, consulte [Trabalhando com o IPA](#ipa).

## Introdução ao IBM SPR
{: #introduction-SPRs}

Uma pronúncia do SPR é definida com [o elemento phoneme](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element) do Speech Synthesis Markup Language (SSML). Ela consiste em uma sequência de símbolos permitidos para um determinado idioma entre aspas duplas. Os símbolos definem como a palavra enfechada no elemento `<phoneme>`deve ser pronunciada. O atributo `alphabet` do elemento tem o valor `ibm` para indicar que a pronúncia está definida no SPR e o atributo `ph` define a pronúncia. A seguir estão exemplos de notação válida do SPR para as palavras *through* e *shocking* em inglês americano:

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

Nas definições, um `.` (ponto) sinaliza o início de uma nova sílaba, os dígitos `1` e `0` indicam o nível de acento das sílabas e as letras representam sons específicos do discurso em inglês americano. Uma entrada do SPR que não está em conformidade com a especificação necessária é inválida.

## Limites silábicos

É possível usar um `.` (ponto) para marcar o início de cada sílaba. No entanto, para preservar a fonética válida de um idioma, o serviço pode optar por não seguir os pontos em alguns casos (por exemplo, se um limite de sílaba for colocado em uma posição ilegal ou não natural para um idioma). Em geral, nos casos nos quais o usuário pode indicar uma preferência válida para um limite de sílabas ou outro aspecto da pronúncia de uma palavra, o serviço cumpre tais solicitações.

## Acento silábico

É possível usar os símbolos na tabela a seguir para marcar o acento silábico para uma pronúncia. A {{site.data.keyword.IBM_notm}} recomenda que você indique o acento primário para pronúncias no SPR ou no IPA. No entanto, a indicação do acento silábico é opcional para ambos os formatos, pois o serviço determinará onde o acento ocorre se você não o indicar.

<table style="width:80%">
  <caption>Tabela 1. Acento silábico</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Símbolo do IBM SPR
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Símbolo do IPA
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Unicode do IPA
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Significado
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      1
    </td>
    <td style="text-align:center">
      <code>& #712;</code>
    </td>
    <td style="text-align:center">
      02C8
    </td>
    <td>
      Acento primário
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
      Acento secundário
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      0
    </td>
    <td style="text-align:center">Sem símbolo</td>
    <td style="text-align:center">Sem valor</td>
    <td>
      Sem acento
    </td>
  </tr>
</table>

**Notas:**

-   No IPA para francês, os símbolos de acento silábico são ignorados. No SPR para francês, o acento silábico não será ignorado e, se for especificado, deverá anteceder imediatamente a vogal da sílaba. No SPR, o acento silábico para o francês é muito mais rígido do que para outros idiomas e um erro ocorrerá se o símbolo de acento silábico estiver em um local inválido.
-   No SPR para espanhol e italiano, é possível especificar apenas `1` (acento primário). Ocorrerá um erro se um acento secundário ou nenhum acento for especificado.
-   Em SPR para japonês, apenas `1`(estresse primário) e `0`(sem estresse) são suportados. Ocorrerá um erro se você especificar o acento secundário.

Deve-se colocar um marcador de acento silábico dentro de um limite silábico, mas sempre à esquerda da vogal da sílaba. É possível colocar um marcador em qualquer lugar à esquerda da vogal acentuada. Por exemplo, cada um dos exemplos a seguir do SPR coloca o acento primário na vogal correta da palavra *construction*:

```xml
< foneme alfabet="ibm " ph="kXn1strHkSXn">construção < /phoneme>
< foneme alfabet="ibm " ph="kXns1trHkSXn">construção < /phoneme>
< foneme alfabet="ibm " ph="kXnst1rHkSXn">construção < /phoneme>
< foneme alfabet="ibm " ph="kXnstr1HkSXn">construção < /phoneme>
```
{: codeblock}

## Símbolos de som de fala

Cada idioma usa seu próprio inventário de símbolos do SPR para representar o som da fala desse idioma. As regras a seguir se aplicam à especificação de um símbolo do SPR:

-   As letras fazem distinção entre maiúsculas e minúsculas, portanto, `e` e `E`, por exemplo, representam dois sons diferentes.
-   Símbolos de dois e de três caracteres devem estar contidos em aspas simples, por exemplo, o símbolo `aj` na palavra alemã *heim*: `"h'aj'm"`.
-   O serviço considera inválida qualquer definição do SPR que contenha símbolos de som que não sejam permitidos em um idioma.

Considere também o seguinte ao definir a pronúncia de uma palavra no formato do SPR:

-   Os sons de cada idioma têm padrões de distribuição específicos. Por exemplo, em todos os dialetos do inglês, o som `G`em *sing*(`".1sIG"`) não ocorre no início de uma palavra. Outros sons em inglês americano que têm uma distribuição particularmente limitada são a parada glótica (`?`), a consoante vibrante simples (`F`) e a consoante nasal silábica (`N`). Se você inserir um símbolo de som em um contexto no qual ele não ocorre normalmente, o discurso resultante poderá soar não natural.
-   O serviço {{site.data.keyword.texttospeechshort}} aplica um conjunto sofisticado de regras linguísticas à sua entrada para refletir os processos pelos quais os sons mudam em contextos específicos em língua natural. Por exemplo, em inglês americano, o som `t` da palavra *write* (`".1r1Yt"`) é pronunciado como uma consoante vibrante simples (`F`) em *writer* (`".1rY.0FR"`). A entrada de SPR passa por essas modificações exatamente como o texto de entrada comum faz. Nesse exemplo, se você inserir `".1rY.0tR"` ou `".1rY.0FR"`, isso não afetará o discurso gerado.

## Trabalhando com o IPA
{: #ipa}

As informações a seguir são aplicadas ao trabalhar com pronúncias na notação do IPA:

-   Use apenas os símbolos do IPA documentados. Quando diversos símbolos (ou combinações de símbolos) do IPA são listados para um símbolo do SPR, todos são equivalentes ao símbolo único do SPR. Nesse caso, o serviço trata todos esses símbolos do IPA da mesma forma e não percebe as diferenças sutis ou regionais que o sistema do IPA está destinado a descrever.
-   Também é possível especificar pronúncias do IPA como valores Unicode do IPA. As tabelas específicas do idioma listadas na seção a seguir documentam os símbolos do IPA e seus valores Unicode do IPA equivalentes. Para obter uma pronúncia de exemplo que usa valores Unicode do IPA, consulte [O elemento phoneme](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element).

Para saber mais, consulte o seguinte:

-   Para obter mais informações sobre o IPA, consulte [Alfabeto fonético internacional](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}.
-   Para obter mais informações sobre símbolos fonéticos para Unicode, consulte [Símbolos
fonéticos em Unicode](https://wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: external}.

## Idiomas suportados
{: #supportedLanguages}

As páginas a seguir documentem os símbolos SPR, símbolos IPA e valores Unicode IPA equivalentes para cada idioma. Eles mostram exemplos de cada símbolo em palavras do idioma. Devido às diferenças dialéticas, os exemplos podem nem sempre corresponder à sua pronúncia.

-   [Símbolos do português do Brasil](/docs/services/text-to-speech?topic=text-to-speech-ptSymbols)
-   [Símbolos do inglês britânico](/docs/services/text-to-speech?topic=text-to-speech-gbSymbols)
-   [Símbolos do francês](/docs/services/text-to-speech?topic=text-to-speech-frSymbols)
-   [Símbolos do alemão](/docs/services/text-to-speech?topic=text-to-speech-deSymbols)
-   [Símbolos do italiano](/docs/services/text-to-speech?topic=text-to-speech-itSymbols)
-   [Símbolos do japonês](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols)
-   [Símbolos do espanhol](/docs/services/text-to-speech?topic=text-to-speech-esSymbols)
-   [Símbolos do inglês americano](/docs/services/text-to-speech?topic=text-to-speech-usSymbols)
