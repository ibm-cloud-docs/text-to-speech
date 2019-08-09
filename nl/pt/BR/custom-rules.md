---

copyright:
  years: 2015, 2019
lastupdated: "2018-06-04"

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

# Regras para criar entradas customizadas
{: #rules}

As regras e diretrizes a seguir se aplicam ao preenchimento de um modelo customizado com entradas customizadas (pares de word/tradução).

## Número máximo de entradas customizadas

Um único modelo customizado pode incluir no máximo 20.000 entradas customizadas.

## Codificação de caracteres

O serviço aceita a codificação de caracteres ASCII e UTF-8 para entradas de *palavra* e *tradução*. Para traduções, use a codificação ASCII para notações do SPR e a codificação UTF-8 para notações do IPA.

## Espaço em branco

Uma *palavra*não pode incluir espaço em branco. O serviço usa um espaço em branco para delinear palavras individuais no texto de entrada.

## Distinção entre maiúsculas e minúsculas

Uma *palavra* faz distinção entre maiúsculas e minúsculas. Por exemplo, suponha que um modelo customizado contenha a entrada `{word='Sun', translation='Sunday'}`. O serviço aplica sua pronúncia padrão à palavra `sun`, mas não à tradução customizada para a palavra `Sun`, uma vez que apenas a última tem uma letra maiúscula inicial.


## Sensibilidade de contexto

As pronúncias de algumas palavras são sensíveis ao contexto. Por exemplo, considere a sentença de entrada de exemplo a seguir:

```
St. Anthony lives on Henry St.
```
{: codeblock}

As regras de pronúncia padrão do serviço sintetizam corretamente esse texto como

```
Saint Anthony lives on Henry Street
```
{: codeblock}

No entanto, se você substituir as regras de pronúncia padrão para a sequência `St.` para traduzi-la como `saint`, o serviço não poderá mais pronunciar a palavra com base no contexto. A aplicação de um modelo de voz customizado que inclui tal tradução faz com que o serviço pronuncie a sentença de entrada anterior como

```
Saint Anthony lives on Henry saint
```
{: codeblock}

Considere tais casos ao desenvolver pares de palavra/tradução.

## Pontos finais

O serviço aplica uma palavra de um modelo customizado apenas àquelas sequências no texto de entrada que correspondem exatamente a ela. Um `.` (período) em uma entrada de palavra altera como a palavra é sintetizada:

-   *Uma palavra que não tem um ponto final* pode conter praticamente qualquer caractere. Os caracteres incluem letras, dígitos, pontuação (diferente do ponto final), símbolos diferentes de letras (como %, &amp; e @), aspas, parênteses, colchetes e assim por diante. Sua *tradução* pode incluir qualquer entrada legal para o serviço, incluindo espaço em branco e uma representação fonética no formato do SSML.
-   *Uma palavra que tem um ponto final* pode conter apenas letras, pontos e apóstrofos internos (não como o primeiro ou o último caractere). A *tradução* da palavra pode conter apenas palavras normais com ortografia comum separadas por espaços em branco ou hifens. Ela não pode conter uma representação fonética.

Um exemplo de uma palavra com um ponto final é "`div.`". Suponha que um modelo customizado inclua a entrada `{word='div.', translação = 'division' }`. O serviço não aplica a tradução à sequência "`div`" porque ela não inclui um ponto final e, portanto, não corresponde à entrada.

## Trabalhando com entradas do IBM SPR
{: #sprNotes}

O Symbolic Phonetic Representation (SPR) é um formato proprietário e dependente de idioma desenvolvido pela {{site.data.keyword.IBM_notm}} para especificar a pronúncia de uma palavra. Para cada idioma suportado, o SPR inclui um alfabeto fonético, símbolos para limites silábicos e símbolos para níveis de acento lexical. As regras básicas a seguir se aplicam à criação de entradas do SPR:

-   A pronúncia padrão que a interface de customização retorna para uma palavra começa com um <code>&#96;</code> (acento grave) e é colocada entre `[]` (colchetes). Por exemplo, a interface retorna a seguinte pronúncia para a palavra `tomato`:

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    Omita o acento grave e os colchetes ao especificar a tradução de uma palavra com os métodos da interface de customização.
-   É possível usar um ponto para indicar o início de uma sílaba em uma tradução, mas os pontos são opcionais e não influenciam a pronúncia da palavra. Eles aparecem na pronúncia para uma palavra somente se você os incluir em sua tradução. Não use espaços para indicar limites silábicos.
-   A {{site.data.keyword.IBM_notm}} recomenda que você anteceda a vogal com o acento primário para uma palavra com um símbolo `1`, embora isso não seja estritamente necessário. O serviço determina onde o estresse ocorre se você não indicar isso. Também é possível usar um símbolo `2` para indicar cada posição de acento secundário, mas o uso de símbolos `2` também é opcional. Eles aparecem na pronúncia para uma palavra somente se você os incluir em sua tradução.

Para obter mais informações sobre como trabalhar com o SPR, consulte [Usando o IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs).

## Trabalhando com entradas em japonês
{: #jaNotes}

Regras adicionais e um campo `part_of_speech` se aplicam à criação de entradas para palavras em um modelo de voz customizado em japonês:

-   Uma tradução semelhante pode conter apenas caracteres *Katakana*. Os caracteres *Kanji* e *Hiragana* não são permitidos.
-   Quando você cria uma tradução (semelhante ou fonética) para uma palavra, também é possível especificar um campo `part_of_speech` opcional para identificar sua parte do discurso. O serviço usa a parte do discurso para produzir a entonação correta para a palavra. Para obter uma lista completa, consulte [Partes do discurso em japonês](#partsOfSpeech).
-   É possível criar apenas uma única entrada para qualquer palavra, e é possível especificar apenas uma parte do discurso para qualquer palavra. Não é possível criar diversas entradas com diferentes partes do discurso (por exemplo, substantivo e verbo) para a mesma palavra. A inclusão de uma tradução para uma palavra que existe em um modelo sobrescreve a tradução existente da palavra, incluindo sua parte do discurso.
-   O serviço aplica a palavra de correspondência mais longa dos pares de palavra/tradução definidos para um modelo de voz customizado. Por exemplo, considere as três entradas a seguir para um modelo customizado.

    <pre><code>{
      "words": [
        {
          "word": "&#65326;&#65337;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "& #65326; & #65337; & #65315;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65337;&#65315;",
          "translation": "&#12520;&#12467;&#12495;&#12510;&#12481;&#12517;&#12540;&#12459;&#12460;&#12452;",
          "part_of_speech": "Mesi"
        }
      ]
    }</code></pre>

    Com essas entradas, suponha que o serviço receba o seguinte texto de entrada: <code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>. Nesse caso, o serviço corresponde à palavra <code>&#65326;&#65337;&#65315;</code> porque <code>&#65326;&#65337;&#65315;</code> é mais longa que <code>&#65326;&#65337;</code> e porque <code>&#65326;&#65337;&#65315;</code> corresponde antes de <code>&#65337;&#65315;</code>.

### Partes do discurso em japonês
{: #partsOfSpeech}

A tabela a seguir lista as partes do discurso suportadas para as entradas customizadas em japonês. Para obter mais informações sobre como especificar a parte do discurso para uma entrada customizada em japonês, consulte [Incluindo palavras em um modelo customizado em japonês](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuJapaneseAdd).

<table style="width:75%">
  <caption>Tabela 1. Partes do discurso em japonês</caption>
  <tr>
    <th style="text-align:center">Argumento <code>part_of_speech</code></th>
    <th style="text-align:center; width:35%">Significado em japonês</th>
    <th style="text-align:center; width:35%">Significado em inglês</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>Josi</code></td>
    <td style="text-align:center"><em>Joshi</em></td>
    <td style="text-align:center">Particípio</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Mesi</code></td>
    <td style="text-align:center"><em>Meishi</em></td>
    <td style="text-align:center">Substantivo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kigo</code></td>
    <td style="text-align:center"><em>Kigou</em></td>
    <td style="text-align:center">Símbolo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Gobi</code></td>
    <td style="text-align:center"><em>Gobi</em></td>
    <td style="text-align:center">Flexão</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Dosi</code></td>
    <td style="text-align:center"><em>Doushi</em></td>
    <td style="text-align:center">Verbo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Unir</code></td>
    <td style="text-align:center"><em>Jodoushi</em></td>
    <td style="text-align:center">Verbo auxiliar</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Koyu</code></td>
    <td style="text-align:center"><em>Koyuumeishi</em></td>
    <td style="text-align:center">Substantivo próprio</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stbi</code></td>
    <td style="text-align:center"><em>Setsubiji</em></td>
    <td style="text-align:center">Sufixo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Suji</code></td>
    <td style="text-align:center"><em>Suuji</em></td>
    <td style="text-align:center">Numeral</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kedo</code></td>
    <td style="text-align:center"><em>Keiyodoushi</em></td>
    <td style="text-align:center">Verbo adjetivo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Fuku</code></td>
    <td style="text-align:center"><em>Fukishi</em></td>
    <td style="text-align:center">Advérbio</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Keyo</code></td>
    <td style="text-align:center"><em>Keiyoshi</em></td>
    <td style="text-align:center">Verbo adjetivo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stto</code></td>
    <td style="text-align:center"><em>Settoji</em></td>
    <td style="text-align:center">Prefixo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Reta</code></td>
    <td style="text-align:center"><em>Rentaishi</em></td>
    <td style="text-align:center">Determinante</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stzo</code></td>
    <td style="text-align:center"><em>Setsuzokushi</em></td>
    <td style="text-align:center">Conjunção</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kato</code></td>
    <td style="text-align:center"><em>Kantoushi</em></td>
    <td style="text-align:center">Interjeição</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Hoka</code></td>
    <td style="text-align:center"><em>Hoka</em></td>
    <td style="text-align:center">Outro</td>
  </tr>
</table>
