---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-21"

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

# Entendendo a customização
{: #customIntro}

Ao sintetizar um texto com o {{site.data.keyword.texttospeechfull}}, o serviço aplica as regras de pronúncia dependentes do idioma. O serviço aplica as regras para converter a ortografia comum (ortográfica) de cada palavra em uma ortografia fonética. A ortografia fonética de uma palavra usa símbolos fonéticos para definir como ela será pronunciada. Esses símbolos são as unidades de som distintas que distinguem as palavras em uma língua, os limites entre sílabas, e as marcas de estresse para as sílabas.
{: shortdesc}

As regras de pronúncia regular do serviço funcionam bem para palavras comuns. No entanto, podem produzir resultados imperfeitos para palavras incomuns. Essas palavras incluem termos especiais com origens estrangeiras, nomes pessoais ou geográficos, abreviações ou acrônimos. Se o léxico de seu aplicativo incluir essas palavras, será possível usar a interface de customização para especificar como o serviço as pronunciará.

A interface de customização é a funcionalidade beta disponível para todos os idiomas. Deve-se ter o plano de precificação Padrão para usar a customização
de modelo de voz. Os usuários do plano Lite não podem usar a interface de customização. Para obter mais informações, consulte a [página de precificação](https://www.ibm.com/cloud/watson-text-to-speech/pricing){: external} para o serviço {{site.data.keyword.texttospeechshort}}.
{: note}

## Como Funciona a Customização
{: #ciHow}

A interface de customização do serviço {{site.data.keyword.texttospeechshort}} cria um dicionário de palavras e suas traduções para um idioma específico. Esse dicionário é referido como um *modelo de voz customizado* ou um modelo customizado. Cada entrada customizada em um modelo de voz customizado consiste em um par de *palavra*/*tradução*. A tradução de uma palavra diz ao serviço como pronunciá-la quando ela ocorrer no texto de entrada.

A interface de customização fornece métodos para criar e gerenciar seus modelos de voz customizados, que serão armazenados permanentemente pelo serviço. Depois de criar um modelo customizado, é possível usá-lo durante a síntese com qualquer versão do método `/v1/synthesize`. Quando o serviço sintetiza o texto de entrada, determina a pronúncia de palavras que aparecem no modelo customizado aplicando suas traduções, direta ou indiretamente. Como um modelo de voz customizado é criado para um idioma específico, ele pode ser usado com qualquer voz, padrão ou neural, que esteja disponível nesse idioma.

Você especifica a tradução para uma palavra em um modelo de voz customizado como uma *tradução semelhante* ou uma *tradução fonética*. É possível usar ambos os métodos para entradas no mesmo modelo customizado e combinar os dois dentro da mesma tradução. Diversas regras e diretrizes se aplicam às entradas customizadas. Para obter mais informações, consulte [Regras para criar entradas customizadas](/docs/services/text-to-speech?topic=text-to-speech-rules).

## Tradução semelhante
{: #soundsLike}

A *tradução semelhante* usa as regras de pronúncia regular do serviço para representar a pronúncia de uma palavra de destino indiretamente. Uma tradução de sons semelhantes é formada a partir das pronúncias regulares de uma ou mais outras palavras. Primeiro, o serviço substitui a tradução especificada para qualquer ocorrência da palavra que apareça no texto de entrada. Em seguida, aplica suas regras de pronúncia regular à tradução, convertendo-a para sua representação fonética para obter a pronúncia.

Por exemplo, as regras de pronúncia regular do serviço traduzem corretamente muitas abreviações e acrônimos comuns. O serviço pronuncia a abreviação *cm* como *centímetro*. Ele pronuncia abreviações menos comuns letra por letra. Por exemplo, o serviço pronuncia a sequência *Str* (uma abreviação para *street*) como *S T R*, com cada letra pronunciada individualmente. É possível usar o método de semelhança para especificar a tradução *street* para a sequência *Str*.

Outro exemplo de acrônimo é a palavra *IEEE*, que representa o Institute of Electrical and Electronic Engineers. Por padrão, o serviço pronuncia esse acrônimo como *I E E E*, no entanto, ele é comumente pronunciado como *I triple E* e pode ser definido facilmente usando a tradução simples de semelhança *I triple E*. Se a palavra *IEEE* aparecer em seu modelo customizado com essa tradução, o serviço substituirá cada ocorrência da palavra por ela. Em seguida, ele aplicará suas regras de pronúncia regular para as palavras individuais *I*, *triple* e *E* para produzir a pronúncia comum.

É possível aplicar o método de semelhança a mais do que abreviações e acrônimos. Ele funciona igualmente bem para palavras complexas ou incomuns. Por exemplo, o par de traduções semelhantes a seguir resulta em pronúncias corretas para palavras incomuns manipuladas de forma imperfeita pelas regras de pronúncia regular do serviço. Localizar traduções adequadas para essas palavras pode ser mais desafiador do que para abreviações simples. As traduções a seguir usam as regras de pronúncia regular para mudar a ortografia das palavras.

<table style="width:35%">
  <caption>Tabela 1. Exemplo de traduções semelhantes</caption>
  <tr>
    <th style="text-align:left">Palavra</th>
    <th style="text-align:left">Tradução</th>
  </tr>
  <tr>
    <td>ayurvedic</td>
    <td>aayervedic</td>
  </tr>
  <tr>
    <td>gastroenteritis</td>
    <td>gastro enteritis</td>
  </tr>
</table>

Como estes exemplos mostram, o desenvolvimento de traduções pode ser mais trial e erro do que formulaic. Você cria uma tradução candidata com base em sua intuição e experiência com o serviço. Em seguida, sintetiza a palavra para a tradução candidata como texto de entrada e escuta o áudio resultante. Se estiver satisfeito com a pronúncia, será possível usar a tradução em seu modelo customizado, caso contrário, modifique a tradução e teste-a novamente.

## Tradução fonética
{: #phonetic}

O método de semelhança é uma maneira relativamente simples e útil de obter uma pronúncia. No entanto, nem sempre é possível desenvolver traduções semelhantes. A alternativa direta, o método fonético, pode parecer mais complicada e demorada, mas pode alcançar a pronúncia de qualquer palavra.

A *tradução fonética* especifica uma pronúncia em termos de símbolos de fonema, marcas de acento silábico e limites silábicos opcionais que substituem as regras de pronúncia regular do serviço. Você especifica uma tradução fonética em um dos formatos a seguir:

-   A representação padrão do Alfabeto Fonético Internacional (IPA)
-   O {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) proprietário

Em qualquer caso, você especifica uma tradução usando um formato de fonema específico baseado no Speech Synthesis Markup Language (SSML). O SSML é uma linguagem de marcações baseada em XML que fornece anotações de texto para aplicativos de síntese de discurso. Você especifica a tradução fonética para uma palavra usando o elemento SSML `<phoneme>`:

<pre><code>&lt;phoneme alphabet="{ipa | ibm}" ph="{translation}"&gt;&lt;/phoneme&gt;</code></pre>

O atributo `alfabeto`especifica o tipo de representação phonetic: `ipa`ou `ibm`. O atributo `ph` especifica a sequência de tradução fonética.

Por exemplo, considere a palavra `trinitroglycerin`. As regras de pronúncia regular do serviço produzem uma pronúncia que difere da que é comumente usada por químicos e médicos. A pronúncia correta pode ser alcançada com uma tradução fonética.

<table style="width:35%">
  <caption>Tabela 2. Exemplo de traduções fonéticas</caption>
  <tr>
    <th style="text-align:left">Alfabeto</th>
    <th style="text-align:left">Tradução</th>
  </tr>
  <tr>
    <td>IPA</td>
    <td>t&#633;a&#618;n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n</td>
  </tr>
  <tr>
    <td>SPR</td>
    <td>trYn1YtrxglIsxrXn</td>
  </tr>
</table>

Nesses exemplos, a sequência de tradução fonética é composta de símbolos de fonema e de uma única marca de acento primário. A marca de acento primário é representada por <code>&#712;</code> no IPA e por `1` no SPR. Ela é colocada antes do símbolo para a vogal acentuada em ambos os casos. Embora os exemplos não mostrem isso, também é possível especificar limites silábicos e posições de acento secundário em uma tradução fonética. Esses elementos não são exigidos e normalmente não são necessários para obter uma pronúncia. Como com traduções semelhantes, é possível compor uma tradução fonética de diversas sequências delimitadas por espaços.

Também é possível especificar traduções do IPA como valores Unicode do IPA. Para obter mais informações, consulte [Usando o IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs) e as tabelas específicas do idioma nas páginas referidas em [Idiomas suportados](/docs/services/text-to-speech?topic=text-to-speech-sprs#supportedLanguages). Para obter uma tradução de exemplo que usa valores Unicode do IPA, consulte [O elemento phoneme](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element).
{: note}

### Trabalhando com uma tradução fonética existente
{: #phoneticMethod}

A menos que você seja um especialista em fonologia, compor traduções fonéticas não será uma tarefa fácil. É sempre mais fácil editar uma tradução fonética existente do que compor uma nova. Para ajudá-lo a criar traduções fonéticas, a API do serviço inclui um método `GET /v1/pronunciation`. Ele retorna a representação do IPA ou do SPR gerada pelas regras de pronúncia regular do serviço para uma palavra em um idioma especificado. Também é possível solicitar a pronúncia para uma palavra a partir de um modelo de voz customizado especificado para ver a tradução no idioma desse modelo.

É possível usar o método `/GET v/1/pronunciation` para obter uma tradução fonética inicial para uma palavra. Em seguida, é possível modificar a tradução para obter a pronúncia desejada. Como com o método de semelhança, você segue um processo de tentativa e erro. Você envia sua tradução candidata para o serviço, sintetiza a palavra como texto de entrada, escuta o áudio resultante e edita a tradução candidata. É possível repetir o processo até que você esteja satisfeito com a pronúncia.

Para obter mais informações, consulte [Consultando uma palavra de um idioma](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryLanguage).

### Mais informações sobre a tradução fonética
{: #phoneticInfo}

Os recursos a seguir fornecem informações sobre a tradução fonética:

-   Para obter mais informações sobre como usar SSML e seu elemento `<phoneme>`, consulte [Usando SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml).
-   Para obter mais informações sobre como especificar traduções do SPR e seus símbolos equivalentes do IPA, consulte [Usando o IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs).
-   Para obter mais informações sobre amostras de áudio dos símbolos e como usar símbolos do IPA, consulte as fontes na web. É possível encontrar uma discussão introdutória detalhada em [Alfabeto fonético internacional](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}.

## Tradução combinada dos métodos de semelhança e fonético

É possível combinar os métodos de semelhança e fonético na mesma tradução. Esse recurso pode reduzir o trabalho envolvido na composição de uma tradução.

Por exemplo, suponha que você usou o método de semelhança para obter parte de uma palavra pronunciada satisfatoriamente. Mas agora, você precisa ajustar os elementos restantes da palavra. É possível usar o método fonético para especificar seus aspectos difíceis. O exemplo a seguir aplica a tradução combinada para a palavra `trinitroglycerin`:

<pre><code>try&lt;phoneme alphabet="ipa" ph="n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n"&gt;&lt;/phoneme&gt;</code></pre>
