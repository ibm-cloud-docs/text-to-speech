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

# Transformação de voz SSML
{: #transformation}

O serviço {{site.data.keyword.texttospeechfull}}, como a maioria dos sistemas de síntese de discurso, pode falar em apenas um número limitado de vozes. Além disso, alguns idiomas oferecem apenas uma ou duas vozes. Para expandir o intervalo de possíveis vozes, o serviço estende SSML com um elemento `<voice-transformation>`. É possível usar esse elemento para adotar diferentes vozes virtuais controlando aspectos de uma voz padrão. As aplicações do recurso incluem
{: shortdesc}

-   *Fornecimento de outra característica para a voz.* Você deseja que uma voz soe um pouco diferente no geral ou para um aplicativo específico.
-   *Marca de voz.* Você deseja usar uma voz exclusiva para diferenciar seus aplicativos.
-   *Aplicativos de diversas funções.* São necessárias diversas vozes para representar diferentes personas.

É possível aplicar o elemento `<voice-transformation>`para o corpo inteiro do texto, uma sentença ou uma palavra ou fragmento. O elemento aceita um atributo necessário, `type`, que descreve o tipo de transformação de voz a ser aplicado ao texto especificado. É possível aplicar uma transformação integrada ou criar uma transformação customizada com base em diferentes aspectos da voz.

## Suporte ao idioma
{: #languages-transformation}

O serviço suporta a transformação de voz somente para as seguintes vozes em inglês americano:

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

A transformação de voz não é suportada com as versões `V2` e baseada em DNN dessas vozes (por exemplo, `en-US_AllisonV2Voice`). O uso do elemento com uma voz não suportada retorna um erro.

## Transformações integradas

As transformações integradas aplicam mudanças pré-configuradas aos atributos de uma voz. Considere-as como vozes virtuais disponibilizadas pelo serviço. O serviço oferece duas transformações integradas. Para usá-las, você especifica o nome da transformação integrada com distinção entre maiúsculas e minúsculas com o atributo `type`:

-   `Young` fornece à voz um som mais jovem.
-   `Soft`faz com que a voz soe mais suave.

É possível aplicar o atributo `força`opcional a uma voz integrada para controlar a extensão na qual o serviço aplica a transformação. Considere o valor como um fator de combinação aplicado pelo serviço à voz original. O atributo aceita um valor no intervalo entre 0 e 100 por cento. Especificar `0%` faz com que a voz não mude e especificar `100%` realiza a transformação integral da voz. Se você omitir o atributo, a intensidade padrão será `100%`.

O serviço ignora os atributos para transformações customizadas quando você usa uma transformação integrada.
{: note}

## Exemplos de transformação integrada

Os exemplos a seguir aplicam as duas transformações integradas à mesma sentença com diferentes intensidades:

```xml
<voice-transformation type="Young" strength="80%">
  Seria possível fornecer novas informações?
< /voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Seria possível fornecer novas informações?
< /voice-transformation>
```
{: codeblock}

## Transformações customizadas

Transformações customizadas fornecem mais controle de baixa granularidade sobre diferentes aspectos da transformação de voz. Para usar uma transformação customizada, você especifica `Custom` para o atributo `type`. Em seguida, será possível usar um ou mais dos atributos opcionais a seguir para controlar a transformação.

<table>
  <caption>Tabela 1. Atributos de Transformação Customizada</caption>
  <tr>
    <th style="width:15%; text-align:left">Atributo</th>
    <th style="width:25%; text-align:center">Intervalo</th>
    <th style="text-align:left">Descrição</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Mudança relativa normalizada do nível médio de perfil de
      tom dentro dos limites seguros. O atributo controla o nível de tom
      médio percebido. Ele é emprestado do atributo <code>pitch</code>
      do elemento <code>&lt;prosody&gt;</code> do SSML. Ele
      contribui para mudar a identidade percebida do falante.
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-narrow</code>, <code>narrow</code>, <code>default</code>,
      <code>wide</code>, <code>x-wide</code>]</td>
    <td>
      Mudança relativa normalizada do intervalo dinâmico do perfil
      de tom dentro dos limites seguros. Aumentar ou diminuir o intervalo de tom
      torna o estilo de fala mais ou menos expressivo. O atributo é
      emprestado do atributo <code>range</code> do elemento <code>&lt;prosody&gt;</code> do SSML.</td>
  </tr>
  <tr>
    <td><code>glottal_tensão</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Mudança relativa normalizada da tensão glotal em segurança
      limites. Aumentar ou diminuir a tensão glótica é percebido
      como uma qualidade de fala mais ou menos tensa. Um valor positivo pode
      produzir sons de zumbido, que podem ser amenizados ao aumentar
      o valor do atributo <code>breathiness</code>. Um valor negativo
      é percebido como mais agradável e mais preenchido de ar.
    </td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Mudança relativa normalizada do nível percebido do ruído de aspiração
      dentro dos limites seguros. Valores extremos podem produzir uma fala
      mais ruidosa (para som positivo de respiração) ou de zumbido (para som negativo de
      respiração). Use esse atributo para compensar o zumbido ou ruído
      adicional produzido como um efeito colateral de outros atributos.
    </td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-slow</code>, <code>slow</code>, <code>default</code>,
      <code>fast</code>, <code>x-fast</code>]</td>
    <td>
      Mudança relativa normalizada da taxa de fala dentro de limites seguros.
      Aumentar ou diminuir a taxa torna a fala mais ou mais lenta.
      Uma taxa positiva (mais rápida) amplia o intervalo de tom percebido
      e uma taxa negativa (mais lenta) limita perceptivamente o intervalo de tom.
      O atributo é emprestado a partir do atributo <code>rate</code>de
      o elemento SSML <code>&lt;prosody&gt;</code>.</td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>,
      <code>Breeze</code>]</td>
    <td>
      O nome com distinção entre maiúsculas e minúsculas de uma das transformações
      de tração vocal integradas: <code>Sunrise</code> ou <code>Breeze</code>.
      Os nomes são simbólicos. Experimente os timbres para aprender
      como impactam a transformação de voz. O atributo contribui
      para mudar a identidade percebida do falante.
    </td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0%, 100%]</td>
    <td>
      A extensão da transformação de tração vocal <code>timbre</code>:
      <code>0%</code> cancela a transformação e <code>100%</code>
      representa a aplicação integral da transformação. O atributo
      quantifica a diferença entre as vozes original e
      transformada. Permite a combinação do timbre selecionado com aquele da
      voz original. Mesmo em valores de extensão moderada de timbre, o atributo
      <code>timbre</code> contribui para mudar a identidade percebida do
      falante.
    </td>
  </tr>
</table>

### Usando intervalos
{: #ranges}

Os intervalos numéricos dos diferentes atributos indicam a extensão do impacto do atributo na voz. Por exemplo, o atributo `rate`possui um intervalo de -100% a 100%:

-   Um valor de `100%` não significa que a voz se torna 100% mais rápida. Significa que o serviço aumenta a taxa da voz para o máximo permitido para essa voz.
-   Um valor de `-100%` significa que o serviço usa a taxa mínima que permite para a voz.
-   Um valor de `0%`representa o nível inerente do atributo para a voz; a voz permanece inalterada.

### Usando valores literais
{: #literals}

Por conveniência, muitos dos atributos também definem valores literais que podem ser usados em vez de porcentagens. Os significados desses valores são diferentes dos valores que são usados com o elemento SSML `<prosody>`. O elemento `<voice-transformation>`usa uma escala que é consistente em seus atributos.

-   `x-low`, `x-slow`e `x-estreita`é igual a um valor de `-100%`.
-   `baixa`, `lenta`, e `estreita`igual a um valor de `-50%`.
-   `default` equivale a um valor de `0%`, o valor padrão para esse atributo e voz.
-   `alta`, `rápida`e `ampla`igual a um valor de `+ 50%`.
-   `x-high`, `x-fast`e `x-wide`igual a um valor de `+ 100%`.

### Diretrizes de uso
{: #guidelines}

Use as diretrizes e informações de advertência a seguir:

-   Para aplicativos de marca de voz ou de diversas funções, use os atributos `timbre`, `pitch` e `glottal_tension` para mudar a identidade percebida do falante. É possível usar combinações desses três atributos para criar vozes virtuais. Considere uma voz virtual como um ponto no espaço multidimensional que é posto em prática pelo timbre, pelo tom e pela tensão glótica especificados. Diferentes combinações dos atributos produzem vozes virtuais diferentes.
-   É possível usar os atributos `pitch_range`, `breathiness` e `rate` para incluir características em uma voz virtual. Outros usuários podem escolher os mesmos valores de atributos ou valores semelhantes, portanto, o serviço não pode garantir a exclusividade de sua voz virtual.
-   Esteja ciente dos possíveis efeitos colaterais da aplicação dos atributos:
    -   A alta tensão glótica, o tom elevado e a baixa taxa podem causar sons de zumbido. Aumente a respiração para atenuar o efeito.
    -   A tensão glotal muito baixa pode produzir um discurso ruidoso. Diminua a respiração para reduzir o ruído.
    -   Aumentar ou reduzir o intervalo de tom e a taxa para níveis extremos simultaneamente pode fazer com que a fala não soe natural.
-   Conforme observado, alguns dos atributos são emprestados a partir do elemento SSML `<prosody>`. Para obter mais informações, consulte [O elemento prosody](/docs/services/text-to-speech/SSML-elements.html#prosody_element). Para ativar o controle preciso de prosódia de uma voz virtual, é possível
    -   Neste elementos `<prosody>`dentro dos elementos `<voice-transformation>`.
    -   Neste elementos `<voice-transformation>`dentro dos elementos `<prosody>`.

    Você *não pode*aninhar elementos `<voice-transformation>`.

## Exemplos de transformação customizada

Os exemplos a seguir aplicam atributos diferentes para demonstrar possíveis aplicações da transformação customizada. O primeiro exemplo diminui a tensão glótica para tornar a voz mais suave. Também aumenta o intervalo de tom e a taxa moderadamente para introduzir um estilo de fala mais dinâmico.

```xml
<voice-transformation type="Custom" glottal_tension="-50%"
  pitch_range="30%" rate="10%">
  Você tem mais informações?
< /voice-transformation>
```
{: codeblock}

O segundo exemplo usa tensão glótica e tom máximos e taxa mínima. Essas combinações geralmente não são favoráveis e podem produzir um som de zumbido. O exemplo atenua esse efeito aumentando a respiração.

```xml
< voice-transformation type="Custom "glottal_tension="100%" pitch="100% "
  rate="-100% " respirthiness="60% ">
  Você tem mais informações?
< /voice-transformation>
```
{: codeblock}

Os próximos dois exemplos mudam a identidade percebida do falante ao aplicar o timbre. A voz é alterada controlando a extensão da combinação e mudando o nível do tom. O primeiro exemplo usa a extensão de timbre padrão, 100%.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="40%">
  Você tem mais informações?
< /voice-transformation>

<voice-transformation type="Custom" timbre="Breeze" timbre_extent="30%"
  pitch="-30%">
  Você tem mais informações?
< /voice-transformation>
```
{: codeblock}

O exemplo final usa diversos atributos para transformar a voz. Ele usa a extensão de timbre padrão e omite a respiração.

```xml
< voice-transformation type="Custom "timbre="Sunrise" pitch="-30% "
  pitch_range=" 80% "rate="60%" glottal_tension="-80% ">
  Você tem mais informações?
< /voice-transformation>
```
{: codeblock}
