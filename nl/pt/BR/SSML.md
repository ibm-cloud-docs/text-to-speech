---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-23"

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

# Usando o SSML
{: #ssml}

O Speech Synthesis Markup Language (SSML) é uma linguagem de marcações baseada em XML que fornece anotações de texto para aplicativos de síntese de discurso. É uma recomendação do W3C Voice-Browser Working Group adotada como a linguagem de marcações padrão para a síntese de discurso pela especificação VoiceXML 2.0. O SSML fornece aos desenvolvedores de aplicativos de fala uma maneira padrão de controlar aspectos do processo de síntese, permitindo que especifiquem a pronúncia, o volume, o tom, a velocidade e outros atributos por meio da marcação.
{: shortdesc}

Com o serviço {{site.data.keyword.texttospeechfull}}, é possível usar o SSML para controlar a síntese de seu texto com todos os idiomas suportados. Isso inclui usar o elemento `<phoneme>` do SSML para definir a pronúncia de uma palavra no Alfabeto Fonético Internacional (IPA) ou no {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). O serviço também conta com o elemento `<phoneme>`SSML para definir a tradução fonética para uma palavra com sua interface de customização; para obter mais informações, consulte [Entendendo a Customização](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

## Introdução ao SSML
{: #introduction-SSML}

O SSML opera aumentando o texto sem formatação transmitido a um sintetizador com um conjunto predefinido de elementos ou tags. Um analisador sintático de XML primeiro separa o texto sem formatação de entrada das especificações de marcações. Em seguida, as especificações são processadas e enviadas como um conjunto de instruções de uma maneira que possa ser entendida pelo sintetizador para produzir os efeitos desejados. Para que o analisador sintático de XML execute essa tarefa, a marcação precisa ser bem formada; por exemplo, os elementos devem ser fechados e diversos elementos devem ser aninhados corretamente. Para obter uma introdução sobre os conceitos básicos de XML, consulte [w3schools.com/xml/xml_whatis.asp](http://www.w3schools.com/xml/xml_whatis.asp){: external}.

Um elemento do SSML é qualquer item contido e que inclui uma tag de abertura e sua tag de fechamento correspondente. Conforme mostrado no exemplo a seguir, um elemento pode conter uma combinação de outros elementos (tags podem ser aninhadas) e texto. Além disso, os elementos podem requerer ou, opcionalmente, aceitar atributos configurados para valores específicos.

```xml
<tag1>
  <tag2 attributeName="attributeValue">
    ... algum texto ...
  < /tag2>
< /tag1>
```
{: codeblock}

Um documento SSML legal completo consiste em um prólogo de XML, que contém informações como a codificação e o esquema com relação ao qual validar o documento SSML, seguido pelo elemento-raiz, `<speak>` (para obter mais informações sobre a estrutura do prólogo, consulte
[tizag.com/xmlTutorial/xmlprolog.php](http://www.tizag.com/xmlTutorial/xmlprolog.php){: external}). Dentro do período do elemento `<speak>`, você especifica o texto que deve ser sintetizado, aumentado com elementos adicionais.

```xml
<! -- O Prólogo de XML -- >
< ?xml version="1.0 "encoding="UTF-8" ?>
<!DOCTYPE speak PUBLIC "-//W3C//DTD SYNTHESIS 1.0//EN"
  "http://www.w3.org/TR/speech-synthesis/synthesis.dtd">

<!-- Root Element -->
<speak version="1.0" xmlns="www.w3.org/2001/10/synthesis"
  ... o corpo que contém texto a ser sintetizado mais markup ...
< /speak>
```
{: codeblock}

O serviço suporta fragmentos do SSML, que são elementos do SSML que não incluem o cabeçalho XML completo.

## Suporte do SSML
{: #ssmlSupport}

O serviço {{site.data.keyword.texttospeechshort}} baseia seu suporte no SSML Versão 1.0, que foi recomendado pelo W3C em 7 de setembro de 2004. Para obter mais informações sobre a recomendação W3C SSML, consulte [W3C Speech Synthesis Markup Language (SSML) Versão 1.0](http://www.w3.org/TR/speech-synthesis/){: external}.

Para obter mais informações sobre como usar o SSML com o serviço, consulte o seguinte:

-   Para obter informações completas sobre o nível de suporte do serviço para todos os elementos do SSML, consulte [Elementos do SSML](/docs/services/text-to-speech?topic=text-to-speech-elements). Com algumas exceções, o serviço implementa a maior parte da especificação W3C, bem como fragmentos SSML.
-   O serviço estende SSML com um elemento `<express-as>`que indica como o texto deve ser expresso quando falado (como uma boa notícia, como um pedido de desculpas, ou com a incerteza). O serviço suporta a expressividade somente para a voz de inglês americano Allison. Consulte [Usando o SSML expressivo](/docs/services/text-to-speech?topic=text-to-speech-expressive).
-   O serviço estende SSML com um elemento `<voice-transformation>`que expande o intervalo de possíveis vozes deixando você controlar o breu, intervalo de arremesso, tensão glotal, taxa de ressardo, taxa e timbre do texto falado. O serviço também oferece duas vozes virtuais integradas, *Young* e *Soft*. O serviço suporta a transformação de voz somente para as vozes em inglês americano. Consulte [Usando o SSML de transformação de voz](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   A interface de customização do serviço suporta o uso do elemento `<phoneme>` do SSML para especificar a ortografia fonética usada ao pronunciar uma palavra. A ortografia fonética representa os sons de uma palavra, como eles são divididos em sílabas e quais sílabas recebem acento.
    -   Para obter informações sobre a interface de customização, consulte [Entendendo a customização](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
    -   Para obter informações sobre os símbolos válidos que podem ser usados em uma especificação do {{site.data.keyword.IBM_notm}} SPR ou do IPA para qualquer idioma suportado, consulte [Usando o IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs).

## Validação do SSML
{: #errors}

O serviço valida todos os elementos do SSML enviados em qualquer conteúdo, seja como texto de entrada para a síntese ou como a definição de tradução de uma palavra para a customização. O serviço não pode determinar antecipadamente se o texto enviado para a síntese contém elementos do SSML. Portanto, ele executa a mesma validação para todo o texto de entrada, independentemente de ele conter o SSML.

-   *Todas as entradas do SSML devem estar corretas e bem formadas.* O serviço ignora silenciosamente elementos do SSML não suportados. O serviço sintetiza o texto contido dentro de um elemento não suportado ou de um elemento que usa recursos não suportados, apenas ignorando o elemento.
-   *O serviço relata um código de erro HTTP 400 para elementos inválidos.* A resposta de erro inclui uma mensagem descritiva, e a solicitação falha.

Especificamente, o serviço retorna um erro nos casos a seguir:

-   *Elemento inválido.* Por exemplo, você especifica uma tag incorretamente, omite um atributo necessário ou inclui uma tag de abertura, mas nenhuma tag de fechamento correspondente.
-   *Símbolo inválido.* O atributo `ph`de um elemento `<phoneme>`inclui um símbolo IPA ou SPR não suportado para o idioma especificado.
-   *Sem vogais.* O atributo `ph`de um elemento `<phoneme>`especifica uma palavra pronúncia que inclui nenhuma vogal.
-   *Ligação francesa em local inválido.* No atributo `ph`de um elemento `<phoneme>`, o caractere de ligação não segue uma consoante ou ocorre no meio da palavra pronúncia.
-   O símbolo *japonês `:` não antecede uma vogal.* No atributo `ph`de um elemento `<phoneme>`, um caractere `:`não ocorre antes de uma vogal (possivelmente com outros símbolos, como limite de sílaba, no meio).
-   *Acento silábico inválido.* O atributo `ph`de um elemento `<phoneme>`para um {{site.data.keyword.IBM_notm}}SPR inclui estresse sinalizável inválido. Para o francês, um símbolo de acento silábico não antecede imediatamente uma vogal. Para espanhol ou italiano, um símbolo secundário (`2`) ou nenhum estresse (`0`) é usado. Para o japonês, um símbolo de acento secundário (`2`) é usado.
-   *Uso inválido do elemento SSML `<express-as>`ou `<voice-transformation>`.* É possível usar essas extensões SSML somente com as vozes padrão especificadas em inglês americano.
-   *Uso inválido do elemento SSML `<prosody>`.* Não é possível usar os atributos `contour`, `duration` e `range` do elemento `<prosody>` com qualquer voz. Além disso, não é possível usar o atributo `volume` do elemento `<prosody>` com vozes neurais (por exemplo, `en-US_AllisonV3Voice`).
-   *Caracteres de controle XML não escapados.* O próprio texto de entrada contém um caractere <code>&quot;</code>, <code>&apos;</code>, `&`, `<`ou `>`em vez de sua cadeia de escape equivalente ou codificação de caracteres. Para obter mais informações, consulte [Escapando caracteres de controle XML](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#escape).
