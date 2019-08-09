---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-30"

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

# Nota sobre a Liberação
{: #release-notes}

As seções a seguir documentam os novos recursos e mudanças que foram incluídos para cada liberação e atualização do serviço {{site.data.keyword.texttospeechfull}}. As informações incluem quaisquer limitações conhecidas. A menos que seja indicado de outra forma, todas as mudanças são compatíveis com as liberações anteriores e são disponibilizadas de forma automática e transparente para todos os aplicativos novos e existentes.
{: shortdesc}

## Limitações conhecidas
{: #limitations}

Nenhuma limitação conhecida neste momento.

## 30 de julho de 2019
{: #July2019}

Agora, o serviço oferece uma voz neural em japonês: `ja-JP_EmiV3Voice`. Além disso, agora, ambas as versões padrão e neural de todas as vozes disponíveis em todos os idiomas suportados estão disponíveis. Para obter mais informações, consulte [Idiomas e vozes](/docs/services/text-to-speech?topic=text-to-speech-voices).

## 24 de junho de 2019
{: #June2019}

-   Agora, o serviço oferece duas versões da maioria de suas vozes disponíveis:
    -   [Vozes padrão](/docs/services/text-to-speech?topic=text-to-speech-voices#standardVoices), que usam a síntese concatenativa para montar segmentos de discurso gravado para gerar áudio. As vozes padrão não incluem uma sequência de versões em seu nome (por exemplo, `en-US_AllisonVoice`).
    -   [Vozes neurais](/docs/services/text-to-speech?topic=text-to-speech-voices#neuralVoices), que usam as Redes Neurais Profundas (DNNs) para prever os recursos acústicos (espectrais) do discurso. As vozes neurais incluem uma sequência de versões (`V3`) em seu nome (por exemplo,
`en-US_AllisonV3Voice`).

    Versões neurais aprimoradas estão disponíveis para todas as vozes padrão, exceto para a voz `ja-JP_EmiVoice`, que está pendente e estará disponível em breve. Não é possível usar os elementos SSML `<express-as>` e `<voice-transformation>` com as vozes neurais e não é possível usar o atributo `volume` do elemento `<prosody>` com as vozes neurais.

    Para obter mais informações sobre todas as vozes disponíveis, consulte [Idiomas e vozes](/docs/services/text-to-speech?topic=text-to-speech-voices).
-   O serviço não inclui mais as vozes DNN da `V2`, que estavam disponíveis anteriormente. Se você usar uma voz da `V2` em seu aplicativo, o serviço usará automaticamente a voz equivalente da `V3` como alternativa.

## 24 de março de 2019
{: #March2019c}

-   Agora, o serviço oferece as versões de Rede Neural Profunda (DNN) da `V2` de suas vozes em alemão:
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

    Para obter mais informações sobre as vozes baseadas em DNN, consulte [Idiomas e vozes](/docs/services/text-to-speech?topic=text-to-speech-voices).
-   Agora, todas as vozes baseadas em DNN do serviço suportam os atributos `pitch` e `rate` do elemento `<prosody>` do SSML. As vozes baseadas em DNN não suportam o atributo `volume`do elemento `<prosody>`. Para obter mais informações, consulte [O elemento prosody](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element).

## Liberações mais antigas
{: #older}

-   [21 de Março de 2019](#March2019b)
-   [4 de março de 2019](#March2019a)
-   [28 de janeiro de 2019](#January2019)
-   [13 de dezembro de 2018](#December2018)
-   [7 de novembro de 2018](#November2018)
-   [30 de outubro de 2018](#October2018)
-   [12 de junho de 2018](#June2018)
-   [15 de maio de 2018](#May2018)
-   [2 de outubro de 2017](#October2017)
-   [14 de julho de 2017](#July2017)
-   [10 de abril de 2017](#April2017)
-   [1º de dezembro de 2016](#December2016)
-   [22 de setembro de 2016](#September2016)
-   [23 de junho de 2016](#June2016)
-   [10 de março de 2016](#March2016)
-   [22 de fevereiro de 2016](#February2016)
-   [17 de dezembro de 2015](#December2015)
-   [21 de setembro de 2015](#September2015)
-   [1º de julho de 2015](#July2015)

### 21 de Março de 2019
{: #March2019b}

Agora, os usuários podem ver somente informações de credenciais de serviço associadas à função designada à sua conta do {{site.data.keyword.cloud_notm}}. Por exemplo, se uma função `reader` estiver designada a você, qualquer nível `writer` ou superior de credenciais de serviço não estará mais visível.

Essa mudança não afeta o acesso à API para usuários ou aplicativos com credenciais de serviço existentes. A mudança afeta somente a visualização de credenciais no {{site.data.keyword.cloud_notm}}.

Para obter mais informações sobre chaves de serviço e funções de usuário, consulte [Chaves de API do serviço IAM](/docs/services/watson?topic=watson-api-key-bp#api-key-bp).

### 4 de março de 2019
{: #March2019a}

Agora, o serviço oferece quatro novas vozes da `V2`, que usam sínteses de deep learning para gerar áudio:

-   `it-IT_FrancescaV2Voice`
-   `en-US_AllisonV2Voice`
-   `en-US_LisaV2Voice`
-   `en-US_MichaelV2Voice`

Essas novas vozes usam o aprendizado de máquina e uma DNN para sintetizar o texto para fala. Baseada em deep learning ou em Rede Neural Profunda (DNN), a síntese produz áudio com uma prosódia mais natural e uma qualidade geral mais consistente.

Mas as novas vozes também produzem áudio com diferentes qualidades de sinal das vozes existentes, portanto, elas podem não ser apropriadas para todos os aplicativos. Além disso, as novas vozes não suportam os elementos SSML `<prosody>`, `<express-as>`, e `<voice-transformation>`.

Para obter mais informações sobre essas vozes baseadas em DNN e como elas diferem das vozes existentes, consulte
[Idiomas e vozes](/docs/services/text-to-speech?topic=text-to-speech-voices).

### 28 de janeiro de 2019
{: #January2019}

Agora, a interface WebSocket suporta a autenticação do Identity and Access Management (IAM) baseada em token por meio do código JavaScript baseado em navegador. A limitação para o contrário foi removida. Para estabelecer uma conexão autenticada com o método WebSocket `/v1/synthesize`:

-   Se usar a autenticação do IAM, inclua o parâmetro de consulta `access_token`.
-   Se você usar as credenciais de serviço do Cloud Foundry, inclua o parâmetro de consulta `watson-token`.

Para obter mais informações, consulte [Estabelecer uma conexão](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket#WSopen).

### 13 de dezembro de 2018
{: #December2018}

Agora, o serviço {{site.data.keyword.texttospeechshort}} está disponível no {{site.data.keyword.cloud}} em Londres (**eu-gb**). Como todos os locais, Londres usa a autenticação do Identity and Access Management (IAM) baseada em token. Todas as novas instâncias de serviço que você cria nessa localização usam a autenticação do IAM.

### 7 de novembro de 2018
{: #November2018}

Agora, o serviço {{site.data.keyword.texttospeechshort}} está disponível no {{site.data.keyword.cloud}} em Tóquio (**jp-tok**). Como todos os locais, Tóquio usa a autenticação do Identity and Access Management (IAM) baseada em token. Todas as novas instâncias de serviço que você cria nessa localização usam a autenticação do IAM.

### 30 de outubro de 2018
{: #October2018}

O serviço {{site.data.keyword.texttospeechshort}}migrou para a autenticação de Identity and Access Management (IAM) baseado em token para todos os locais. Agora, todos os serviços {{site.data.keyword.cloud_notm}} usam a autenticação do IAM. O serviço {{site.data.keyword.texttospeechshort}} migrou em cada local nas datas a seguir:

-   Dallas (**us-south**): 30 de outubro de 2018
-   Frankfurt (**eu-de**): 30 de outubro de 2018
-   Washington, DC (**us-este**): 12 de junho de 2018
-   Sydney (**au-syd**): 15 de maio de 2018

A migração para a autenticação do IAM afeta as instâncias de serviço novas e existentes de forma diferente:

-   *Agora, todas as novas instâncias de serviço criadas em qualquer local* usam a autenticação do IAM para acessar o serviço. É possível transmitir um token de acesso ou uma chave de API: os tokens suportam solicitações autenticadas sem integrarem credenciais de serviço em cada chamada e as chaves de API usam a autenticação básica HTTP. Quando você usa qualquer um dos SDKs do {{site.data.keyword.ibmwatson}}, é possível passar a chave de API e deixar que o SDK gerencie o ciclo de vida dos tokens.
-   *As instâncias de serviço existentes criadas em um local antes da data de migração indicada* continuam usando o `{username}` e a `{password}` de suas credenciais de serviço anteriores do Cloud Foundry para a autenticação, até que sejam migradas por você para usar a autenticação do IAM. Para obter mais informações sobre a migração para a autenticação do IAM, consulte [Migrando instâncias de serviço do Cloud Foundry para um grupo de recursos](https://{DomainName}/docs/resources?topic=resources-migrate).

Para obter mais informações, consulte a documentação a seguir:

-   Para saber qual mecanismo de autenticação sua instância de serviço usa, visualize suas credenciais de serviço clicando, na instância, no [Painel do {{site.data.keyword.cloud_notm}}](https://{DomainName}/dashboard/apps){: external}.
-   Para obter mais informações sobre como usar tokens do IAM com os serviços {{site.data.keyword.watson}}, consulte [Autenticando-se com tokens do IAM](/docs/services/watson?topic=watson-iam).
-   Para obter mais informações sobre como usar chaves de API do IAM com os serviços {{site.data.keyword.watson}}, consulte [Chaves de API do serviço IAM](/docs/services/watson?topic=watson-api-key-bp).
-   Para obter exemplos que usam a autenticação do IAM, consulte a [Referência de API](https://{DomainName}/apidocs/text-to-speech){: external}.

### 12 de junho de 2018
{: #June2018}

Os recursos a seguir estão ativados para aplicativos hospedados em Washington, DC (**us-east**):

-   Agora, o serviço suporta um novo processo de autenticação de API. Para obter mais informações, consulte a [Atualização de serviço de 30 de outubro de 2018](#October2018).
-   Agora, o serviço suporta o cabeçalho `X-Watson-Metadata` e o método `DELETE /v1/user_data`. Para obter mais informações, consulte [Segurança de informações](/docs/services/text-to-speech?topic=text-to-speech-information-security).

### 15 de maio de 2018
{: #May2018}

Os recursos a seguir estão ativados para aplicativos em Sydney (**au-syd**):

-   Agora, o serviço suporta um novo processo de autenticação de API. Para obter mais informações, consulte a [Atualização de serviço de 30 de outubro de 2018](#October2018).
-   Agora, o serviço suporta o cabeçalho `X-Watson-Metadata` e o método `DELETE /v1/user_data`. Para obter mais informações, consulte [Segurança de informações](/docs/services/text-to-speech?topic=text-to-speech-information-security).

### 2 de outubro de 2017
{: #October2017}

Para o formato `audio/l16`, agora é possível especificar opcionalmente a ordenação do áudio retornado (deve-se especificar nesse momento a taxa de amostragem). Os exemplos são `audio/l16;rate=22050;endianness=big-endian` e `audio/l16;rate=22050;endianness=little-endian`, sendo o padrão o big endian. Para obter mais informações, consulte [Formatos de áudio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).

### 14 de julho de 2017
{: #July2017}

O serviço agora suporta o formato de áudio MP3 ou Motion Picture Experts Group (MPEG). Para obter mais informações sobre formatos de áudio suportados, consulte [Formatos de áudio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).

### 10 de abril de 2017
{: #April2017}

-   O serviço agora suporta o formato de áudio Web Media (WebM) com o codec Opus ou Vorbis. Agora, o serviço também suporta o formato de áudio Ogg com o codec Vorbis, além do codec Opus. Para obter mais informações sobre formatos de áudio suportados, consulte [Formatos de áudio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   Agora, o serviço suporta o Cross-Origin Resource Sharing (CORS) para permitir que os clientes baseados em navegador chamem o serviço diretamente. Para obter mais informações, consulte [Suporte ao CORS](/docs/services/text-to-speech?topic=text-to-speech-overview#cors).
-   Os códigos de resposta HTTP para a conclusão bem-sucedida de alguns métodos da interface de customização foram mudados:
    -   O método `POST /v1/customizations` agora retorna 201 (em vez de 200).
    -   O método `POST /v1/customizations/{customization_id}` agora retorna 200 (em vez de 201).
    -   O método `POST /v1/customizations/{customization_id}/words` agora retorna 200 (em vez de 201).
    -   O método `PUT /v1/customizations/{customization_id}/words/{word}` agora retorna 200 (em vez de 201).
-   Os métodos `POST /v1/customizations/{custom_id}/words` e `PUT /v1/customizations/{customization_id}/words/{word}` agora retornam o código de resposta HTTP 400 com a mensagem de erro `Parte do discurso é suportada somente para o idioma ja-JP` se você tentar especificar um `part_of_speech` para um idioma diferente do japonês.
-   O método `POST /v1/customizations/{custom_id}/words` agora retorna um corpo de resposta vazio (`{}`).

### 1º de dezembro de 2016
{: #December2016}

-   O serviço inclui uma nova voz, `es-LA_SofiaVoice`, que é o equivalente na América Latina da voz `es-US_SofiaVoice`. A diferença mais significativa entre as duas vozes se refere a como elas interpretam um `$` (cifrão): a versão da América Latina usa o termo *pesos*, enquanto a versão da América do Norte usa o termo *dólares*. Outras diferenças menores também podem existir entre as duas vozes.
-   Além da `en-US_AllisonVoice`, mais duas vozes são agora transformáveis com a transformação de voz do SSML: `en-US_LisaVoice` e `en-US_MichaelVoice`. Para obter mais informações sobre a transformação de voz, consulte [Transformação de voz SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   Quando você usa a interface de customização com o japonês, o serviço agora corresponde à palavra mais longa dos pares de palavra/tradução que são definidos para um modelo de voz customizado. Por exemplo, considere as duas entradas a seguir para uma voz customizada:

    <pre><code data-copy="false" class="language-javascript">  {
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    Se o serviço localizar a sequência <code>&#65326;&#65337;&#65315;</code> no texto de entrada, corresponderá a essa palavra porque ela é uma correspondência mais longa do que <code>&#65326;&#65337;</code>. Anteriormente, o serviço teria correspondido à sequência <code>&#65326;&#65337;</code>. Para obter mais informações sobre como trabalhar com entradas em japonês para um modelo de voz customizado, consulte [Trabalhando com entradas em japonês](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes).

### 22 de setembro de 2016
{: #September2016}

-   A interface de customização, que inclui os métodos de customização e `GET /v1/pronation`, está agora disponível para todos os idiomas que são suportados pelo serviço. A interface permanece uma liberação beta. Para obter mais informações, consulte [Entendendo a customização](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
-   Agora, o serviço suporta o Speech Synthesis Markup Language (SSML) para o japonês. Para obter informações gerais sobre o suporte do SSML, consulte [Usando o SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml). Para obter informações sobre os símbolos do SPR e do IPA do japonês, consulte [Símbolos do japonês](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols). Considerações adicionais e um campo `part_of_speech` se aplicam ao criar entradas para palavras em um modelo de voz customizado em japonês. Para obter mais informações, consulte [Trabalhando com entradas em japonês](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes).
-   O serviço agora oferece a transformação de voz SSML por meio do novo elemento `<voice-transformation>`. É possível expandir o intervalo de possíveis vozes criando transformações de voz customizadas que modificam o tom, o intervalo de tom, a tensão glótica, a respiração, a taxa e o timbre de uma voz. O serviço também oferece duas vozes virtuais integradas, *Young* e *Soft*. O serviço atualmente suporta a transformação de voz somente para a voz em inglês americano Allison. Para obter mais informações, consulte [SSML de transformação de voz](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   Agora, o serviço pode retornar informações de sincronização de palavra para todas as sequências do texto de entrada que você transmite à interface WebSocket. Para receber o horário de início e de término de cada sequência na entrada, especifique uma matriz que inclua a sequência `words` para o parâmetro opcional `timings` do objeto JSON transmitido ao serviço. Atualmente, o recurso não está disponível para o texto de entrada em japonês. Para obter mais informações, consulte [Obtendo sincronizações de palavra](/docs/services/text-to-speech?topic=text-to-speech-timing).
-   Agora, o serviço valida todos os elementos do SSML enviados em qualquer contexto. Se ele localizar uma tag inválida, relatará um código de resposta HTTP 400 com uma mensagem descritiva e o método falhará. Em liberações anteriores, o serviço manipulou erros de forma inconsistente. A especificação de uma pronúncia de palavra inválida, por exemplo, poderia causar um comportamento imprevisível ou inconsistente. Para obter mais informações, consulte [Validação do SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml#errors).
-   O uso de `spr`foi descontinuado como um argumento para a opção `format`do método `GET /v1/pronation`e para uso com o atributo `alfabeto`de um elemento SSML `<phoneme>`. Para usar a notação do {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR), use o argumento `ibm` em vez de `spr` em todos os casos.
-   Agora, a lista de formatos de áudio suportados inclui `audio/mulaw;rate=8000`. Como `audio/basic`, esse formato fornece um áudio de canal único que é codificado usando dados u-law (ou mulei) de 8 bits amostrados em 8 kHz. Para obter mais informações, consulte [Formatos de áudio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   Os métodos `GET /v1/voice`e `GET /v1/voices/ { voice }`agora retornam um objeto `supported_features`como parte de sua saída para cada voz. O objeto descreve se a voz suporta a customização e o elemento `<voice_transformation>`SSML. Para obter mais informações, consulte [Idiomas e vozes](/docs/services/text-to-speech?topic=text-to-speech-voices).

### 23 de junho de 2016
{: #June2016}

-   Agora, o serviço oferece uma interface WebSocket para sintetizar o texto para fala. A interface oferece os mesmos recursos que o método `/v1/synthesize` da interface HTTP. Ele aceita texto simples ou texto que é marcado com SSML. Além disso, também suporta o uso do elemento `<mark>` do SSML para identificar o horário no áudio no qual ele conclui a síntese de todo o texto que antecede a marca. Para obter mais informações, consulte [A interface WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).
-   Agora, o serviço oferece suporte para o texto anotado com o SSML para os idiomas castelhano e espanhol da América do Norte, italiano e português do Brasil. O serviço já suportava o uso do SSML para inglês americano e britânico, francês e alemão. A partir dessa atualização, o serviço suporta o SSML para todos os idiomas, exceto japonês. Além disso, é possível usar as notações {{site.data.keyword.IBM_notm}}SPR e IPA para definir pronúncias de palavras com o elemento SSML `<phoneme>`. Para obter mais informações, consulte [Usando o SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml) e [Usando o IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs).

    Para inglês dos EUA, também é possível usar o elemento `<phoneme>`SSML para criar entradas de palavras em um modelo de voz customizado; a customização é suportada apenas para inglês dos EUA. Para obter mais informações, consulte [Entendendo a customização](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
-   O serviço apresenta uma maior expressividade e naturalidade para as vozes mais frequentemente usadas. As melhorias são baseadas na predição de prosódia baseada em Recursive Neural Network (RNN) do texto de entrada. Elas são disponibilizadas como um novo mecanismo de serviço e atualizações de modelo de voz para os idiomas a seguir:

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   O método `GET /v1/pronunciation` agora aceita um parâmetro de consulta `customization_id` opcional. O parâmetro obterá uma tradução de palavra de um modelo de voz customizado especificado. Se o modelo de voz não contiver a palavra, o método retornará a pronúncia padrão da palavra. Para obter mais informações, consulte a [Referência de API](https://{DomainName}/apidocs/text-to-speech){: external}.

    Ao usar o método `GET /v1/pronunciation` sem um ID de customização e para um idioma diferente do inglês americano, é possível solicitar a pronúncia de uma palavra somente na notação do {{site.data.keyword.IBM_notm}} SPR. Para um idioma diferente do inglês americano, deve-se especificar `spr` com a opção `format` do método.
    {: note}
-   A lista de formatos de áudio suportados agora inclui o `áudio / básico`, que fornece áudio de canal único que é codificado usando dados de 8 bits u-law (ou mulei) que são amostrados em 8 kHz. Para obter mais informações, consulte [Formatos de áudio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   Os métodos de HTTP e WebSocket `/v1/synthesize` podem retornar uma resposta `warnings` que inclui mensagens sobre parâmetros de consulta inválidos ou campos JSON incluídos com uma solicitação. O formato dos avisos mudou. O exemplo a seguir mostra o formato anterior:

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    Agora, o mesmo aviso tem o formato a seguir:

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

### 10 de março de 2016
{: #March2016}

-   Os métodos `GET` e `POST /v1/synthesize` podem agora retornar um cabeçalho de resposta `Warnings` que inclui uma lista de mensagens de aviso sobre parâmetros de consulta inválidos ou campos JSON incluídos com a solicitação. Cada elemento da lista inclui uma sequência que descreve a natureza do aviso, seguida por uma matriz de sequências de argumentos inválidos, por exemplo, `Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}'].` Para obter mais informações, consulte a [Referência de API](https://{DomainName}/apidocs/text-to-speech){: external}.
-   O Speech Software Development Kit (SDK) do *{{site.data.keyword.watson}} beta para o sistema operacional Apple&reg; iOS* foi descontinuado e substituído pelo *{{site.data.keyword.watson}} Swift SDK*. O novo SDK está disponível no [repositório swift-sdk](https://github.com/watson-developer-cloud/swift-sdk){: external} do namespace `watson-developer-cloud` no GitHub.

### 22 de fevereiro de 2016
{: #February2016}

O serviço foi atualizado com um novo recurso do SSML expressivo. O serviço estende o SSML (Speech Synthesis Markup Language) com um elemento `<express-as>`que pode ser usado para indicar a expressão em um dos três estilos de fala: `GoodNews`, `Apology`ou `Incerteza`. É possível aplicar o elemento ao corpo inteiro do texto, a uma frase ou a uma palavra. Atualmente, o serviço suporta a expressividade apenas para a voz do inglês americano Allison (`en-US_AllisonVoice`). Para obter mais informações, consulte [SSML expressivo](/docs/services/text-to-speech?topic=text-to-speech-expressive).

### 17 de dezembro de 2015
{: #December2015}

-   O serviço oferece uma nova interface de customização que pode ser usada para especificar como ele pronuncia palavras incomuns que ocorrem em sua entrada. A interface inclui diversos novos métodos que podem ser usados para criar e gerenciar modelos de voz customizados e os pares de palavra/tradução que eles contêm. Em seguida, é possível usar seus modelos customizados ao sintetizar o texto para áudio.

    O serviço suporta traduções semelhantes e fonéticas. As traduções pônéticas podem utilizar a representação padrão da Alphabet Internacional Phonetica (IPA) ou a {{site.data.keyword.IBM_notm}}Representação Phonética Simbólica (SPR). Você usa o Speech Synthesis Markup Language (SSML) para especificar traduções fonéticas.

    A interface de customização inclui uma coleção de novos métodos de HTTP que possuem os nomes `POST /v1/customizations`, `POST /v1/customizations/{customization_id}`, `POST /v1/customizations/{customization_id}/words` e `PUT /v1/customizations/{customization_id}/words/{word}`. O serviço também fornece um novo método `GET /v1/pronunciation` que retorna a pronúncia para qualquer palavra e um novo método `GET /v1/voices/{voice}` que retorna informações detalhadas sobre uma voz específica. Além disso, os métodos existentes da interface do serviço agora aceitam parâmetros customizados de modelo de voz, conforme necessário.

    Para obter mais informações sobre a customização e sua interface, consulte [Entendendo a customização](/docs/services/text-to-speech?topic=text-to-speech-customIntro) e [Referência de API](https://{DomainName}/apidocs/text-to-speech){: external}.

    A interface de customização é uma liberação beta que atualmente suporta apenas o inglês americano. Todos os métodos de customização e o método `GET /v1/pronunciation` podem ser usados atualmente para criar e manipular modelos de voz customizados e traduções de palavra somente em inglês americano.
    {: note}
-   O serviço suporta uma nova voz feminina, `pt-BR_IsabelaVoice`, para sintetizar áudio em português do Brasil. Para obter mais informações, consulte [Idiomas e vozes](/docs/services/text-to-speech?topic=text-to-speech-voices).

### 21 de setembro de 2015
{: #September2015}

-   Dois novos Kits de Desenvolvimento de Software (SDKs) beta móveis estão disponíveis para os serviços de fala. Os SDKs permitem que os aplicativos móveis interajam com os serviços {{site.data.keyword.texttospeechshort}} e {{site.data.keyword.speechtotextshort}}. É possível usar os SDKs para enviar um texto para o serviço {{site.data.keyword.texttospeechshort}} e receber uma resposta de áudio.
    -   O *SDK do {{site.data.keyword.watson}} Swift* está disponível no [repositório swift-sdk ](https://github.com/watson-developer-cloud/swift-sdk){: external} do namespace `watson-developer-cloud` no GitHub.
    -   O *SDK do {{site.data.keyword.watson}} Speech Android* está disponível no [repositório speech-android-sdk](https://github.com/watson-developer-cloud/speech-android-sdk){: external} do namespace `watson-developer-cloud` no GitHub.

    Os SDKs suportam a autenticação com os serviços de fala usando suas credenciais do serviço {{site.data.keyword.cloud_notm}} ou um token de autenticação.

    Como os SDKs são funcionalidades beta, estão sujeitos a mudanças no futuro.
    {: note}
-   O serviço suporta um novo idioma, o japonês. A voz `ja-JP_EmiVoice` é uma voz feminina em japonês.

### 1º de julho de 2015
{: #July2015}

O serviço mudou de beta para a disponibilidade geral (GA) em 1º de julho de 2015. As diferenças a seguir existiam entre as versões beta e de disponibilidade geral da API do {{site.data.keyword.texttospeechshort}}. A liberação de disponibilidade geral requer que os usuários façam upgrade para a nova versão do serviço.

-   Um novo modelo de programação suporta a interação direta entre um cliente e o serviço. Ao usar esse modelo, um cliente pode obter um token de autenticação para a comunicação diretamente com o serviço. Usando o token, o cliente pode efetuar bypass na necessidade de um aplicativo de proxy do lado do servidor no {{site.data.keyword.cloud_notm}} para chamar o serviço em seu nome. Os tokens são os meios preferenciais para os clientes interagirem com o serviço.

    O serviço continua a suportar o modelo de programação antigo que dependia de um proxy do lado do servidor para retransmitir comunicações e dados entre o cliente e o serviço. Mas o novo modelo é mais eficiente e fornece um rendimento mais alto.
-   Agora, é possível transmitir o Speech Synthesis Markup Language (SSML) para as versões de HTTP `GET` e `POST` do método `/v1/synthesize`. O SSML é uma linguagem de marcações baseada em XML que foi projetada para fornecer anotações de texto para aplicativos de síntese de fala, como o serviço {{site.data.keyword.texttospeechshort}}. Para obter mais informações sobre como transmitir a entrada do SSML ao serviço, consulte [Especificando o texto de entrada](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#input).

    O serviço inicialmente suporta o uso de SSML apenas para os idiomas inglês e americano inglês, francês e alemão. O serviço não suporta SSML para uso com italiano e espanhol. Ao usar o SSML, certifique-se de não selecionar uma voz para o áudio em um dos idiomas não suportados. Os resultados, neste caso, não são significativos.
-   As vozes suportadas para o discurso sintetizado mudaram e foram expandidas. Agora, o serviço suporta diversas vozes, idiomas e dialetos adicionais com os métodos `/v1/synthesize`. Para obter mais informações sobre as vozes suportadas, consulte [Idiomas e vozes](/docs/services/text-to-speech?topic=text-to-speech-voices).

    As três vozes que estavam disponíveis no beta foram renomeadas para a disponibilidade geral:
    -   `VoiceEnUsMichael`agora é `en-US_MichaelVoice`
    -   `VoiceEnUsLisa` agora é `en-US_LisaVoice`
    -   `VoiceEsEsEnrique` agora é `es-ES_EnriqueVoice`

    Os nomes anteriores das vozes continuam a funcionar com a versão beta do serviço (por meio de terminais de API `-beta`) e essa versão permanece disponível. No entanto, deve-se usar os novos nomes com a versão de disponibilidade geral do serviço.
-   Agora, é possível solicitar que o serviço retorne o áudio no formato Free Lossless Audio Codec (FLAC). O serviço ainda pode retornar o áudio no formato Ogg com o codec Opus (o padrão) e no formato Waveform Audio File Format (WAV). Para obter mais informações sobre como usar formatos de áudio com os métodos `/v1/synthesize`, consulte [Formatos de áudio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   O texto enviado para o método `/v1/synthesize` na URL de uma solicitação de HTTP `GET` ou no corpo de uma solicitação de HTTP `POST` está agora limitado a um máximo de 5 KB. O texto tinha um tamanho máximo de 4 MB para a versão beta.
-   Os métodos `/v1/synthesize` agora incluem o cabeçalho `X-WDC-PL-OPT-OUT` para controlar se o serviço usa ou não o texto e os resultados de áudio de uma operação para melhorar os resultados futuros. Especifique um valor de `1` para o cabeçalho para evitar que o serviço use o texto e os resultados de áudio. O parâmetro é aplicado somente à solicitação atual. O novo cabeçalho substitui o cabeçalho `X-logging` dos métodos beta. Para obter mais informações, consulte [Controlando a criação de logs de solicitação para serviços {{site.data.keyword.watson}}](/docs/services/watson?topic=watson-gs-logging-overview).
-   Para os métodos `/v1/synthesize`, os códigos de erro a seguir foram alterados:
    -   O código de erro 406 ("Não aceitável. Tipo MIME não suportado".) foi removido.
    -   O código de erro 415 ("Tipo de mídia não suportado") foi incluído.
    -   O código de erro 503 ("Serviço indisponível") foi incluído.
-   Para o método `GET /v1/vozes`, os códigos de erro a seguir mudaram:
    -   O código de erro 406 ("Não aceitável. Tipo MIME não suportado".) foi removido.
    -   O código de erro 415 ("Tipo de mídia não suportado") foi incluído.
