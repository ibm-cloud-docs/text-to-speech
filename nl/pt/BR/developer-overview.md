---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-06"

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

# Visão geral para desenvolvedores
{: #overview}

É possível acessar os recursos de síntese de discurso do serviço {{site.data.keyword.texttospeechfull}} por meio de uma API de Representational State Transfer (REST) HTTP ou de uma interface WebSocket. Diversos Kits de Desenvolvimento de Software (SDKs) também estão disponíveis para simplificar o desenvolvimento de aplicativos em diversas linguagens de programação. As seções a seguir fornecem uma visão geral do desenvolvimento de aplicativos com o serviço.
{: shortdesc}

## Interface HTTP
{: #overview-http}

Para sintetizar textos com a API HTTP, você chama a versão `GET` ou `POST` do método `/v1/synthesize` do serviço. Geralmente, as duas versões do método oferecem uma funcionalidade equivalente:

-   *Texto de entrada:* você transmite o texto de entrada que deve ser sintetizado de duas maneiras diferentes:
    -   O método `GET /v1/synthesthesize` aceita o texto de entrada como um parâmetro de consulta. O tamanho máximo da solicitação é de 8 KB, que inclui o texto de entrada e a URL e os cabeçalhos.
    -   O método `POST /v1/synthesize` aceita o texto de entrada no corpo da solicitação. O tamanho máximo da solicitação é de 8 KB para a URL e os cabeçalhos e 5 KB para o texto de entrada enviado no corpo da solicitação.

    É possível transmitir o texto sem formatação ou anotado com o Speech Synthesis Markup Language (SSML). O SSML é uma linguagem de marcações baseada em XML que fornece anotações de texto para aplicativos de síntese de discurso, como o serviço {{site.data.keyword.texttospeechshort}}. O serviço aumenta o SSML com elementos expressivos e de transformação de voz específicos do serviço, que estão disponíveis para algumas vozes padrão em inglês americano.

    Para obter mais informações, consulte [Especificando o texto de entrada](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#input).
-   *Vozes:* o serviço aceita o texto e produz o áudio em diversos idiomas, vozes e dialetos. O serviço oferece pelo menos uma voz feminina para cada idioma. Para alguns idiomas, o serviço oferece diversas vozes, incluindo vozes masculinas e femininas. O serviço também oferece dialetos diferentes, como o inglês americano e o inglês britânico. Ele oferece a versão padrão (concatenativa) e a versão neural aprimorada da maioria das vozes.

    É possível usar os métodos `GET /v1/voices` ou `GET /v1/voices/{voice}` do serviço para saber mais sobre as vozes suportadas. O serviço sintetiza o texto no idioma da voz especificada. Certifique-se de corresponder a voz e o texto de entrada.

    Para obter mais informações, consulte [Idiomas e vozes](/docs/services/text-to-speech?topic=text-to-speech-voices).
-   *Formatos de áudio:* o serviço pode produzir áudio nos formatos a seguir: formato Ogg ou Web Media (WebM) com o codec Opus (padrão) ou Vorbis, formato MP3 (Motion Picture Experts Group ou MPEG), Waveform Audio File Format (WAV), Free Lossless Audio Codec (FLAC), Linear 16-bit Pulse-Code Modulation (PCM), mu-law (u-law) de 8 bits ou áudio de base.

    Para obter mais informações, consulte [Formatos de áudio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).

## Interface WebSocket
{: #overview-websocket}

O serviço oferece uma interface WebSocket que pode ser usada para sintetizar o texto. A interface fornece uma única versão do método `/v1/synthesize`, que aceita um máximo de 5 KB de texto de entrada. Você especifica o texto a ser sintetizado, a voz a ser usada e o formato para o áudio. É possível fornecer um texto sem formatação ou anotado com o SSML. Para obter mais informações, consulte [A interface WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).

A interface WebSocket suporta o uso do elemento SSML `<mark>`para identificar locais específicos no áudio. Também é possível solicitar informações de sincronização de palavra para todas as palavras do texto de entrada. Para obter mais informações, consulte [Obtendo sincronizações de palavra](/docs/services/text-to-speech?topic=text-to-speech-timing).

## Interface de customização
{: #overview-customization}

O serviço inclui uma interface de customização que pode ser usada para criar modelos de voz customizados para uso durante a síntese do discurso. Um modelo de voz customizado é um dicionário de palavras e suas traduções para um idioma específico. Cada par de palavra/tradução em um modelo informa ao serviço como pronunciar a palavra quando ela ocorre no texto de entrada.

É possível usar modelos de voz customizados para criar traduções específicas do aplicativo para palavras incomuns para as quais as regras de pronúncia regular do serviço podem produzir pronúncias imperfeitas. É possível definir a entrada customizada para um par de palavra/tradução na representação padrão do Alfabeto Fonético Internacional (IPA) ou no {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) proprietário.

Por exemplo, seu aplicativo pode rotineiramente encontrar termos especiais com origens estrangeiras, nomes pessoais ou geográficos, abreviações e acrônimos. Usando a customização, é possível definir traduções que dizem ao serviço como você deseja que tais termos sejam pronunciados. Para obter mais informações, consulte [Entendendo a customização](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

A interface de customização é uma liberação beta. Além disso, deve-se ter o plano de precificação Padrão para usar a customização de modelo de voz. Os usuários do plano Lite não podem usar a interface de customização. Para obter mais informações, consulte a [página de precificação](https://www.ibm.com/cloud/watson-text-to-speech/pricing){: external} para o serviço {{site.data.keyword.texttospeechshort}}.
{: note}

## Suporte ao CORS
{: #cors}

O serviço suporta o Cross-Origin Resource Sharing (CORS). Usando o CORS, as páginas da Web podem solicitar recursos diretamente de um domínio externo. O CORS contorna a política de segurança de mesma origem que, caso contrário, evitaria essas solicitações. Como o serviço suporta o CORS, uma página da web pode se comunicar diretamente com ele sem transmitir a solicitação por meio do servidor da web que a hospeda.

Por exemplo, uma página da web carregada por meio de um servidor no {{site.data.keyword.cloud}} pode chamar a API de customização diretamente, efetuando bypass do servidor do {{site.data.keyword.cloud_notm}}. Para obter mais informações, consulte [enable-cors.org](https://enable-cors.org/){: external}.

## Usando Kits de Desenvolvimento de Software
{: #sdks}

Os SDKs estão disponíveis para o serviço {{site.data.keyword.texttospeechshort}} com o objetivo de simplificar o desenvolvimento de aplicativos de fala. Os SDKs do {{site.data.keyword.ibmwatson}} estão disponíveis para muitas linguagens de programação e plataformas populares.

-   Para obter uma lista completa de SDKs e links para os SDKs no GitHub, consulte [Usando SDKs](/docs/services/watson?topic=watson-using-sdks).
-   Para obter informações detalhadas sobre todos os métodos dos SDKs de Node, Java&trade;, Python, Ruby, Swift e Go para o serviço {{site.data.keyword.texttospeechshort}}, consulte a [Referência de API](https://{DomainName}/apidocs/text-to-speech){: external}.

## Aprendendo mais sobre o desenvolvimento de aplicativos
{: #learn}

Para obter mais informações sobre como trabalhar com os serviços {{site.data.keyword.watson}} e com o {{site.data.keyword.cloud_notm}}, consulte

-   Para obter uma introdução ao trabalho com os serviços {{site.data.keyword.watson}} e com o {{site.data.keyword.cloud_notm}}, consulte [Introdução ao {{site.data.keyword.watson}} e ao {{site.data.keyword.cloud_notm}}](/docs/services/watson?topic=watson-about).
-   Todas as novas instâncias de serviço usam o {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) para a autenticação. As instâncias de serviço mais antigas podem continuar usando o `{username}` e o `{password}` de suas credenciais de serviço existentes do Cloud Foundry para a autenticação. Para obter mais informações sobre a autenticação no serviço, consulte a [Atualização de serviço de 30 de outubro de 2018](/docs/services/text-to-speech?topic=text-to-speech-release-notes#October2018) nas notas sobre a liberação.
-   Para obter informações sobre como controlar a criação de log de solicitação padrão executada para todos os serviços {{site.data.keyword.watson}}, consulte [Controlando a criação de log de solicitação para serviços {{site.data.keyword.watson}}](/docs/services/watson?topic=watson-gs-logging-overview).
