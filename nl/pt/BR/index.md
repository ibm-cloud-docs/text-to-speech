---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-08"

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

# Sobre
{: #about}

> ** Atualização de serviço:***o serviço {{site.data.keyword.texttospeechshort}} foi atualizado em 24 de março de 2019. O serviço agora oferece versões da Deep Neural Network (DNN) de suas vozes alemãs, e todas as vozes baseadas em DNN agora suportam os atributos `pitch`e `rate`do elemento SSML `<prosody>`. Para obter mais informações, consulte a [Atualização de serviço de 24 de março de 2019](/docs/services/text-to-speech/release-notes.html#March2019c) nas notas sobre a liberação*.

O serviço {{site.data.keyword.texttospeechfull}} fornece uma interface de programação de aplicativos (API) que usa os recursos de síntese de discurso do {{site.data.keyword.IBM_notm}} para converter o texto escrito em discurso semelhante ao natural. O serviço flui os resultados de volta para o cliente com um atraso mínimo. O serviço oferece as interfaces [HTTP](/docs/services/text-to-speech/http.html) e [WebSocket](/docs/services/text-to-speech/websockets.html).

## Recursos

O serviço {{site.data.keyword.texttospeechshort}} oferece os recursos a seguir:

-   **Formatos de áudio** - Produz áudio em Ogg ou WebM com o codec Opus ou Vorbis, WAV, WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw ou formato básico. Para obter mais informações, consulte [Formatos de áudio](/docs/services/text-to-speech/audio-formats.html).
-   **Vozes** - Sincroniza o texto para áudio em diversos idiomas, vozes e dialetos. O serviço oferece versões baseadas em DNN de algumas vozes. Para obter mais informações, consulte [Idiomas e vozes](/docs/services/text-to-speech/voices.html).
-   **SSML** - Aceita texto sem formatação ou texto marcado com o Speech Synthesis Markup Language (SSML) baseado em XML. Para obter mais informações, consulte [Usando o SSML](/docs/services/text-to-speech/SSML.html).
-   **Expressividade** - Estende o SSML com um elemento expressivo que pode ser usado para indicar um estilo de fala de *GoodNews*, *Apology* ou *Uncertainty*. Disponível somente para a voz em inglês americano Allison, que não é baseada em DNN. Para obter mais informações, consulte [SSML expressivo](/docs/services/text-to-speech/SSML-expressive.html).
-   **Transformação de voz** - Estende o SSML incluindo um elemento de transformação de voz. É possível usar o elemento para expandir o intervalo de possíveis vozes, controlando aspectos como tom, taxa e timbre. Também oferece duas vozes virtuais integradas, *Young* e *Soft*. Disponível apenas para vozes em inglês dos EUA que não são baseadas em DNNs. Para obter mais informações, consulte [SSML de transformação de voz](/docs/services/text-to-speech/SSML-transformation.html).
-   **Sincronizações de palavra** - Com a interface WebSocket, suporta o elemento `<mark>` do SSML e as informações opcionais de sincronização de palavra para todas as sequências do texto de entrada. As informações de sincronização sincronizam o texto de entrada e o áudio resultante. Para obter mais informações, consulte [Obtendo sincronizações de palavra](/docs/services/text-to-speech/word-timing.html).
-   **Customização**-Fornece uma interface de customização que pode ser usada para especificar como o serviço pronuncia palavras incomuns que ocorrem em sua entrada. É possível definir pronúncias com o Alfabeto Fonético Internacional (IPA) ou com o {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). Para obter mais informações, consulte [Entendendo a customização](/docs/services/text-to-speech/custom-intro.html).

Para obter mais informações sobre os planos de precificação para o serviço, consulte o serviço {{site.data.keyword.texttospeechshort}} no [Catálogo do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/text-to-speech){: new_window}.

## Suporte ao idioma
{: #languages-index}

O serviço suporta vozes nos seguintes idiomas: português do Brasil, inglês (dialetos britânico e americano), francês, alemão, italiano, japonês e espanhol (dialetos castelhano, da América Latina e da América do Norte). O serviço oferece ao menos uma voz masculina ou feminina, às vezes ambas, para cada idioma. Cada voz usa a cadência e a entonação apropriadas para seu dialeto. Para obter mais informações sobre as vozes disponíveis para cada idioma, consulte [Idiomas e vozes](/docs/services/text-to-speech/voices.html).

## Casos de uso
{: #usecases}

O serviço é apropriado para aplicativos orientados por voz e sem tela, nos quais o áudio é o método preferencial de saída:

-   Interfaces para pessoas com deficiência, como ferramentas de assistência para deficientes visuais
-   Leitura em voz alta de mensagens de texto e e-mails para motoristas
-   Narração de roteiros de vídeo e dublagem de vídeo
-   Ferramentas educacionais baseadas em leitura
-   Soluções de automação residencial

## Experimente o serviço

Para obter exemplos do serviço em ação, consulte

-   Uma [demo rápida ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://text-to-speech-demo.ng.bluemix.net/){: new_window} do serviço {{site.data.keyword.texttospeechshort}} que aceita texto e gera fala com vozes diferentes. Ela oferece a expressividade e a transformação, quando suportadas.
-   Aplicativos nos {{site.data.keyword.ibmwatson}} Kits do Iniciador [ ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/starter-kits.html){: new_window}, que demonstram o serviço {{site.data.keyword.texttospeechshort}}.
