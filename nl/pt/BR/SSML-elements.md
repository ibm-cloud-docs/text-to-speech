---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-09"

subcollection: text-to-speech

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Elementos do SSML
{: #elements}

Com o serviço {{site.data.keyword.texttospeechfull}}, é possível usar a maioria dos elementos do Speech Synthesis Markup Language (SSML) para controlar a síntese de seu texto. Os elementos estão disponíveis para todos os idiomas suportados. A tabela a seguir resume o suporte do serviço para atributos e elementos do SSML.

-   *Integral* significa que o serviço suporta totalmente o elemento ou atributo com suas interfaces HTTP e WebSocket.
-   *Parcial*significa que o serviço não suporta todos os aspectos do elemento ou atributo. Isso também pode significar que o serviço suporta o elemento ou atributo com apenas uma de suas interfaces ou que o elemento ou atributo não é suportado com todas as vozes.
-   *Nenhum* significa que o serviço não suporta o elemento ou atributo.

Para obter mais informações sobre um elemento ou atributo, consulte sua descrição. Onde indicado, o suporte para alguns atributos e valores difere ligeiramente da especificação do SSML. Para obter mais informações, consulte [W3C Speech Synthesis Markup Language (SSML) Versão 1.0 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.w3.org/TR/speech-synthesis/){: new_window}.

<table>
  <caption>Tabela 1. Elementos do SSML</caption>
  <tr>
    <th style="text-align:left; width:30%">Elemento ou atributo</th>
    <th style="text-align:center; width:12%">Suporte</th>
    <th style="text-align:left; width:46%; padding-left:75px">Elemento ou atributo</th>
    <th style="text-align:center; width:12%">Suporte</th>
  </tr>
  <tr>
    <td>[Áudio](#audio_element)</td>
    <td style="text-align:center">Nenhum</td>
    <td style="padding-left:75px">[Say-as](#say-as_element)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Quebra](#break_element)</td>
    <td style="text-align:center">Integral</td>
    <td style="padding-left:100px">[cardinal](#sayAsCardinal)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Desc](#desc_element)</td>
    <td style="text-align:center">Nenhum</td>
    <td style="padding-left:100px">[data](#sayAsDate)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Ênfase](#emphasis_element)</td>
    <td style="text-align:center">Nenhum</td>
    <td style="padding-left:100px">[dígitos](#sayAsDigits)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Léxico](#lexicon_element)</td>
    <td style="text-align:center">Nenhum</td>
    <td style="padding-left:100px">[letras](#sayAsLetters)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Marca](#mark_element)</td>
    <td style="text-align:center">Parcial</td>
    <td style="padding-left:100px">[número](#sayAsNumber)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Meta](#mm_element)</td>
    <td style="text-align:center">Nenhum</td>
    <td style="padding-left:125px">cardinal</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Metadados](#mm_element)</td>
    <td style="text-align:center">Nenhum</td>
    <td style="padding-left:125px">ordinal</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Parágrafo](#ps_element)</td>
    <td style="text-align:center">Integral</td>
    <td style="padding-left:125px">telefone</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Phoneme](#phoneme_element)</td>
    <td style="text-align:center">Integral</td>
    <td style="padding-left:150px">pontuação</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">Integral</td>
    <td style="padding-left:100px">[ordinal](#sayAsOrdinal)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">Integral</td>
    <td style="padding-left:100px">[vxml: booleano](#vxml-boolean)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Prosódia](#prosody_element)</td>
    <td style="text-align:center">Parcial</td>
    <td style="padding-left:100px">[vxml:currency](#vxml-currency)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">perfil</td>
    <td style="text-align:center">Nenhum</td>
    <td style="padding-left:100px">[vxml:date](#vxml-date)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">duração</td>
    <td style="text-align:center">Nenhum</td>
    <td style="padding-left:100px">[vxml:digits](#vxml-digits)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[tom](#prosody-pitch)</td>
    <td style="text-align:center">Integral</td>
    <td style="padding-left:100px">[vxml:phone](#vxml-phone)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">intervalo</td>
    <td style="text-align:center">Nenhum</td>
    <td style="padding-left:75px">[Sentença](#ps_element)</td>
    <td style="text-align:center">Integral</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[taxa](#prosody-rate)</td>
    <td style="text-align:center">Integral</td>
    <td style="padding-left:75px">[Fala](#speak_element)</td>
    <td style="text-align:center">Integral</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[volume](#prosody-volume)</td>
    <td style="text-align:center">Parcial</td>
    <td style="padding-left:75px">[Sub](#sub_element)</td>
    <td style="text-align:center">Integral</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td style="padding-left:75px">[Voz](#voice_element)</td>
    <td style="text-align:center">Nenhum</td>
  </tr>
</table>

## O elemento de áudio
{: #audio_element}

Esse elemento `<audio>` insere elementos registrados no áudio gerado pelo serviço. Ele não é suportado.

## O elemento de quebra
{: #break_element}

O elemento `<break>`insere uma pausa no texto falado. Ele tem os atributos opcionais a seguir:

-   `strength` especifica o comprimento da pausa em termos de valores de intensidade variados:
    -   `none` suprime uma quebra que poderia ser produzida durante o processamento.
    -   `x-weak`, `weak`, `medium`, `strong` ou `x-strong` inserem quebras cada vez mais intensas.
-   `time`especifica o comprimento da pausa em termos de segundos ou milissegundos. Os formatos de valor válidos são `{integer}s` para segundos ou `{integer}ms` para milissegundos.

```xml
< fala version="1.0 ">
  Diferente tamanho < break consol="none">sem pausa < /break>
  Diferente tamanho < break fortal="x-weak">x-fraca pausa < /break>
  Diferente tamanho de < break fortal="weak">pausa fraca < /break>
  Diferente tamanho de < break fortal="médio">médio pause < /break>
  Diferente tamanho < break fortal="strong">strong pause < /break>
  Diferente tamanho < break fortal="x-strong">x-forte pausa < /break>
  Diferente tamanho < break time="1s">pausa de um-segundo < /break>
  Diferente tamanho < break time="1500ms">1500-milissegundo pausa < /break>
< /speak>
```
{: codeblock}

## O elemento desc
{: #desc_element}

O elemento `<desc>` pode ocorrer em apenas um elemento `<audio>`. Porque o `<audio>`não é suportado, nem o elemento `<desc>`.

## O elemento de ênfase
{: #emphasis_element}

O elemento `<emphasis>`solicita que o texto anexado seja falado com ênfase. Ele não é suportado.

## O elemento de léxico
{: #lexicon_element}

Este elemento `<lexicon>`introduz dicionários de pronúncia para o documento SSML fornecido. Ele não é suportado.

É possível usar a interface de customização do serviço para definir um dicionário de entradas customizadas (pares de palavra/tradução) para uso durante a síntese de discurso. Para obter mais informações, consulte [Entendendo a customização](/docs/services/text-to-speech/custom-intro.html).

## O elemento de marca
{: #mark_element}

O elemento `<mark>` é suportado somente pela interface WebSocket do serviço e não por sua interface HTTP, que o ignora. Para obter mais informações, consulte [Especificando uma marca do SSML](/docs/services/text-to-speech/word-timing.html#mark).
{: note}

O elemento `<mark>` é um elemento vazio que coloca um marcador no texto a ser sintetizado. O cliente é notificado quando todo o texto que antecede o elemento `<mark>` foi sintetizado. O elemento aceita um único atributo `name`que especifica uma sequência que identifica exclusivamente a marca; o nome deve começar com um caractere alfanumérico. O nome é retornado com o horário no qual a marca ocorre no áudio sintetizado.

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
< /speak>
```
{: codeblock}

## Os elementos meta e metadados
{: #mm_element}

O valor `<meta>`e os elementos `<metadata>`são contêineres nos quais é possível colocar informações sobre o documento. Eles não são suportados.

## Os elementos do parágrafo e da sentença
{: #ps_element}

O `<paragraph>`(ou `<p>`) e `<sentence>`(ou `<s>`) elementos são elementos opcionais que podem ser usados para fornecer sugestões sobre a estrutura textual. Se o texto que está incluído em um elemento `<paragraph>`ou `<sentence>`não terminar com um caractere de pontuação de fim de frase (como um ponto), o serviço incluirá uma pausa mais longa do que o normal no áudio sintetizado.

O único atributo válido para qualquer elemento é `xml:lang`, que permite a alternância de idioma. O atributo não é suportado.

```xml
<speak version="1.0">
  <paragraph>
    <sentence>Texto em um elemento de sentença.</sentence>
    <s>Mais texto em outra sentença.</s>
  < /paragraph>
< /speak>
```
{: codeblock}

## O elemento phoneme
{: #phoneme_element}

O elemento `<phoneme>`fornece uma pronunciação fonética para o texto anexado. A ortografia fonética representa os sons de uma palavra, como eles são divididos em sílabas e quais sílabas recebem o acento. O elemento tem dois atributos:

-   `alphabet` é um atributo opcional que especifica a fonologia a ser usada. Os alfabetos suportados são
    -   O Alfabeto Fonético Internacional (IPA): `alphabet="ipa "`
    -   O {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR): `alphabet="ibm"`

    Se nenhum alfabeto for especificado, o serviço usará o IBM SPR por padrão.
-   `ph` é um atributo necessário que fornece a pronúncia no alfabeto indicado. Os exemplos a seguir mostram a pronúncia para a palavra *tomato*em ambos os formatos:

    -   Formato do IPA:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomateiro&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   Formato do IPA com símbolos Unicode:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomateiro&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   Formato do IBM SPR:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomateiro&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

Para obter mais informações sobre o uso de notações SPR e IPA com o elemento `<phoneme>`, consulte [Usando o IBM SPR](/docs/services/text-to-speech/SPRs.html).

## O elemento prosody
{: #prosody_element}

O elemento `<prosody>`controla o breu, a taxa de fala e o volume do texto. Todos os atributos são opcionais, mas ocorrerá um erro se nenhum atributo for especificado. A especificação do SSML permite três atributos que o serviço não suporta: `contour`, `range` e `duration`. O serviço suporta os atributos `pitch`, `rate`, e `volume`.

### O atributo de tom
{: #prosody-pitch}

O atributo `pitch` modifica o tom de referência para o texto dentro do elemento. Os valores aceitos são

-   Um número seguido pela designação `Hz` (Hertz): o tom de referência é transposto (para cima ou para baixo) para o valor especificado.
-   Um valor de mudança relativo (em semitons): um número que causa uma mudança absoluta da referência atual. O número é precedido por `+`(um aumento) ou `-`(uma diminuição) e seguido por `st`(semitones), por exemplo, `+ 5st`.
-   Uma mudança relativa em percentual: um número que causa uma mudança relativa na referência atual. O número é precedido por `+`(um aumento) ou `-`(uma diminuição) e seguido por `%`(sinal de porcentagem), por exemplo, `-10%`.
-   Uma das seis palavras-chave a seguir, que modifica o tom para os valores predefinidos correspondentes:
    -   `default` usa o tom de referência padrão do serviço.
    -   `x-low` muda a referência do tom para baixo por 12 semitons.
    -   `low` muda a referência do tom para baixo por seis semitons.
    -   `medium` produz o mesmo comportamento que `default`.
    -   `high` muda a referência do tom para cima por seis semitons.
    -   `x-high` muda a referência do tom para cima por até 12 semitons.

    ```xml
    <speak version="1.0">
      <prosody pitch="150Hz">Transpor o tom para 150 Hz</prosody>
      <prosody pitch="-20Hz">Diminuir o tom em 20 Hz da referência</prosody>
      <prosody pitch="+20Hz">Aumentar o tom em 20 Hz da referência</prosody>
      <prosody pitch="-12st">Diminuir o tom em 12 semitons da referência</prosody>
      <prosody pitch="+12st">Aumentar o tom em 12 semitons da referência</prosody>
      <prosody pitch="x-low">Diminuir o tom em 12 semitons da referência</prosody>
    </speak>
    ```
    {: codeblock}

### O atributo de taxa
{: #prosody-rate}

O atributo `rate` indica uma mudança na taxa de fala para o texto dentro do elemento. A taxa é especificada em termos de palavras por minuto e, se a taxa de fala for de 50 palavras por minuto, `rate` será igual a `50`. Quando `rate` é configurado para um número positivo, a implementação não fica em conformidade com a especificação de atributo de taxa de prosódia do W3C atual. Além disso, o serviço suporta mudanças de porcentagem relativa (por exemplo, `+15%`), mas não mudanças de valor relativo (por exemplo, `+15`). Os valores aceitos são

-   Uma porcentagem relativa de aumento ou redução: `+ 10%`.
-   Um número de palavras por minuto como um número positivo: `75`.
-   `default` usa a taxa padrão do serviço.
-   `x-slow` diminui a taxa em 50 por cento.
-   `slow` diminui a taxa em 25 por cento.
-   `medium` produz o mesmo comportamento que `default`.
-   `fast` aumenta a taxa em 25 por cento.
-   `x-fast` aumenta a taxa em 50 por cento.

```xml
< fala version="1.0 ">
  < prosody rate="ler">Diminuir taxa de falantes por 25% < /prosody>
  < prosody rate="50">Configurar taxa de fala em 50 palavras por minuto < /prosody>
  < prosody rate=" + 5% ">Aumentar a taxa de fala em 5 por cento < /prosody>
< /speak>
```
{: codeblock}

### O atributo de volume
{: #prosody-volume}

O serviço não suporta o atributo `volume`do elemento `<prosody>`com suas vozes baseadas em DNN (por exemplo, `en-US_AllisonV2Voice`). Para obter mais informações sobre essas vozes, consulte [Tecnologias de síntese de discurso](/docs/services/text-to-speech/voices.html#technologiesVoices).
{: note}

O atributo `volume` modifica o volume para o texto dentro do elemento. É possível especificar um número inteiro ou um valor decimal no intervalo de 1,0 a 100,0 (volume máximo). Também é possível usar um dos valores de sequência a seguir, que correspondem a configurações predefinidas no intervalo de 0 a 100. (O valor `silent`não é suportado.)

-   `x-soft` tem o valor 30.
-   `soft` tem o valor 50.
-   `medium` tem o valor 80.
-   `loud` tem o valor 90.
-   `default` tem o valor 92.
-   `x-loud` tem o valor 100.

```xml
< fala version="1.0 ">
  < prosody volume="75">Volume modificado é 75 < /prosody>
  < prosody volume=" 88.9">Volume modificado é 88.9 < /prosody>
  < prosody volume="loud">Volume Modificado é 90 < /prosody>
< /speak>
```
{: codeblock}

## O elemento say-as
{: #say-as_element}

O elemento `<say-as>`é apenas parcialmente suportado para a maioria dos idiomas. Para idiomas diferentes do inglês americano, o serviço geralmente suporta somente os atributos `digits` e `letters` do elemento.
{: note}

O elemento `<say-as>`fornece informações sobre o tipo de texto que está contido no elemento e especifica o nível de detalhes para renderização do texto. O elemento tem um atributo necessário, `interpret-as`, que indica como o texto entre aspas deve ser interpretado. Ele tem dois atributos opcionais, `format` e `detail`, que são usados somente com valores específicos no atributo `interpret-as`, conforme ilustrado nos exemplos a seguir.

A seguir, valores aceitos para o atributo `interpret-as` e exemplos de cada um deles.

### cardinal
{: #sayAsCardinal}

O valor `cardinal` indica o número cardinal para o numeral dentro do elemento. Os exemplos a seguir dizem *Super Bowl de quarenta e nove*. O primeiro é supérfluo, uma vez que não muda o comportamento padrão do serviço.

```xml
< fala version="1.0 ">
  Super Bowl < say-como interpretar-as="cardinal">49 < /say-as>
  Super Bowl < say-as interpretar-as="cardinal">XLIX < /say-as>
< /speak>
```
{: codeblock}

### data
{: #sayAsDate}

O valor `date` indica a data dentro do elemento, de acordo com o formato especificado no atributo `format` associado. O atributo `format` é necessário para o valor `date`. Se nenhum `format` estiver presente, o serviço ainda tentará pronunciar a data. Os exemplos a seguir indicam as datas determinadas nos formatos especificados, em que `d`, `m` e `y` representam dia, mês e ano.

```xml
< fala version="1.0 ">
  < say-as interpretar-as = "date " format="mdy">12/17/2005 < /say-as>
  < say-as interpretar-as = "date " format="ymd">2005/12/17 < /say-as>
  < say-as interpretar-as = "date " format="dmy">17/12/2005 < /say-as>
  < say-as interpreta-as = "date " format="ydm">2005/17/12 < /say-as>
  < say-as interpretar-as = "date " format="my">12/2005 < /say-as>
  < say-as interpretar-as = "date " format="md">12/17 < /say-as>
  < say-as interpretar-as = "date " format="ym">2005/12 < /say-as>
< /speak>
```
{: codeblock}

### dígitos
{: #sayAsDigits}

O valor `digits` indica os dígitos no número dentro do elemento. O exemplo a seguir indica os dígitos individuais *123456*.

```xml
< fala version="1.0 ">
  < say-as interpretar-as="digits">123456 < /say-as>
< /speak>
```
{: codeblock}

### letras
{: #sayAsLetters}

O valor `letters` soletra os caracteres na palavra dentro do elemento. O exemplo a seguir soletra as letras da palavra *hello*.

```xml
< fala version="1.0 ">
  < say-as interpretar-as="letters">Olá < /say-as>
< /speak>
```
{: codeblock}

### número
{: #sayAsNumber}

O valor `number` oferece uma alternativa aos valores `cardinal` e `ordinal`. É possível usar o atributo `format` opcional para indicar como uma série de números deve ser interpretada. O primeiro exemplo omite o atributo `format` para pronunciar o número como um valor cardinal. O segundo exemplo especifica explicitamente que o número deve ser pronunciado como um valor `cardinal`. O terceiro exemplo especifica que o número deve ser pronunciado como um valor `ordinal`.

```xml
< fala version="1.0 ">
  < say-as interpretar-as="number">123456 < /say-as>
  < say-as interpretar-as = "number " format="cardinal">123456 < /say-as>
  < say-as interpretar-as = "number " format="ordinal">123456 < /say-as>
< /speak>
```
{: codeblock}

Também é possível especificar o valor `telephone` para o atributo `format`. Os exemplos mostram duas maneiras diferentes de pronunciar uma série de números como um número de telefone. Para pronunciar os números com a pontuação incluída, especifique o valor `pontuation` para o atributo `detail` opcional.

```xml
< fala version="1.0 ">
  < say-as interpretar-as = "number " format="telephone">555-555-5555 < /say-as>
  < say-as interpretar-as = "number "format="telefone" detail="punctuation">555-555-5555 < /say-as>
< /speak>
```
{: codeblock}

### ordinal
{: #sayAsOrdinal}

O valor `ordinal` indica o valor ordinal para o dígito dentro do elemento. O exemplo a seguir diz *second first*.

```xml
< fala version="1.0 ">
  < say-as interpretar-as="ordinal">2 < /say-as>
  < say-as interpretar-as="ordinal">1 < /say-as>
< /speak>
```
{: codeblock}

### vxml: booleano
{: #vxml-boolean}

O valor `vxml:boolean` indica *sim* ou *não*, dependendo do valor `true` ou `false` dentro do elemento.

```xml
< fala version="1.0 ">
  < say-as interpretar-as="vxml:boolean">true < /say-as>
  < say-as interpretar-as="vxml:boolean">falso < /say-as>
< /speak>
```
{: codeblock}

### vxml:currency
{: #vxml-currency}

O valor `vxml: currency`é usado para controlar a síntese de valores monetários. A sequência deve ser gravada no formato `UUUmm.nn`, em que `UUU` é o indicador de moeda de três caracteres especificado pelo padrão ISO 4217 e `mm.nn` é a quantidade. O exemplo a seguir diz *forty-five dollars and thirty cents*.

```xml
< fala version="1.0 ">
  < say-as interpretar-as="vxml:currency">USD45.30 < /say-as>
< /speak>
```
{: codeblock}

Se o número especificado incluir mais de duas casas decimais, a quantia será sintetizada como um número decimal seguido pelo indicador de moeda. Se o indicador de moeda de três caracteres não estiver presente, a quantia será sintetizada somente como um número decimal e o tipo de moeda não será pronunciado. O exemplo a seguir diz *forty-five point three two nine US dollars*.

```xml
< fala version="1.0 ">
  < say-as interpretar-as="vxml:currency">USD45.329 < /say-as>
< /speak>
```
{: codeblock}

### vxml:date
{: #vxml-date}

O valor `vxml:date` funciona como o valor `date`, mas o formato é predefinido como `YYYYMMDD`. Se um valor de dia, mês ou ano não for conhecido ou se você não desejar que ele seja falado, substitua o valor por um `?` (ponto de interrogação). O segundo e terceiro exemplos incluem pontos de interrogação.

```xml
< fala version="1.0 ">
  < say-as interpretar-as="vxml:date">20050720 < /say-as>
  < say-as interpretar-as="vxml:date">? ???0720 < /say-as>
  < say-as interpretar-as="vxml:date">200507?? < /say-as>
< /speak>
```
{: codeblock}

### vxml:digits
{: #vxml-digits}

O valor `vxml:digits` fornece a mesma função que o valor `digits`.

### vxml:phone
{: #vxml-phone}

O valor `vxml:phone` indica um número de telefone com ambos os dígitos e a pontuação. É equivalente a usar o valor `number` especificando `telephone` para o atributo `format` e `punctuation` para o atributo `detail`.

```xml
< fala version="1.0 ">
  < say-as interpret-as="vxml:phone">555-555-5555 < /say-as>
< /speak>
```
{: codeblock}

## O elemento de fala
{: #speak_element}

O elemento `<speak>`é o elemento-raiz para documentos SSML. Os atributos válidos são

-   `version` é um atributo necessário que determina a especificação do SSML. O valor aceito é `1,0`.
-   `xml:lang` não é necessário para o serviço. Omita o atributo quando usar esse elemento.
-   `xml:base` não tem efeito.

```xml
<speak version="1.0">
  O texto a ser falado.
< /speak>
```
{: codeblock}

## O elemento sub
{: #sub_element}

O elemento `<sub>`indica que o texto que é especificado pelo atributo `alias`é substituir o texto que é colocado dentro do elemento quando o discurso é sintetizado. O atributo `alias` é o único do elemento e é necessário.

```xml
< fala version="1.0 ">
 <sub alias="International Business Machines">IBM</sub>
< /speak>
```
{: codeblock}

## O elemento de voz
{: #voice_element}

Este elemento `<voice>`solicita uma mudança de voz. Ele não é suportado.
