---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-25"

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

# Idiomas e vozes
{: #voices}

O serviço {{site.data.keyword.texttospeechfull}}suporta uma variedade de idiomas, vozes e dialetos. O serviço oferece pelo menos uma voz feminina para cada idioma. Para alguns idiomas, o serviço oferece diversas vozes, incluindo vozes masculinas e femininas. Cada voz usa a cadência e a entonação apropriadas para seu dialeto.
{: shortdesc}

As vozes da `V2`, que estavam disponíveis anteriormente com o serviço, foram descontinuadas. Se você usar uma voz da `V2` em seu aplicativo, o serviço usará automaticamente a voz equivalente da `V3` como alternativa.
{: note}

## Idiomas e vozes suportados
{: #languageVoices}

A tabela 1 lista as vozes disponíveis para cada idioma e dialeto, incluindo seu tipo e gênero. Todas as vozes estão disponíveis como [Vozes padrão](#standardVoices) e [Vozes neurais](#neuralVoices). Se o parâmetro opcional `voice` for omitido de uma solicitação, o serviço usará a voz padrão `en-US_MichaelVoice`.

<table style="width:100%">
  <caption>Tabela 1. Idiomas e vozes suportados</caption>
  <tr>
    <th style="text-align:left">Idioma</th>
    <th style="text-align:center">Tipo</th>
    <th style="text-align:center">Voz</th>
    <th style="text-align:center">Gênero</th>
  </tr>
  <tr>
    <td style="text-align:left">Português do Brasil</td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Castelhano</td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Francês</td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Alemão</td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td style="text-align:left">Italiano</td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Japonês</td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>ja-JP_EmiV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Espanhol da América Latina</td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Espanhol da América do Norte</td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglês britânico</td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglês americano</td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>en-US_LisaVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Padrão</td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neural</td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
</table>

As vozes `es-LA_SofiaVoice` e `es-US_SofiaVoice` são essencialmente a mesma. A diferença mais significativa diz respeito a como as duas vozes interpretam um $ (cifrão). A versão da América Latina usa o termo *pesos*, enquanto que a versão da América do Norte usa o termo *d&oacute;lares*. Outras diferenças menores também podem existir entre as duas vozes.
{: note}

### Vozes padrão
{: #standardVoices}

As vozes padrão não incluem uma sequência de versões (`V3`) em seu nome (por exemplo, `pt-BR_IsabelaVoice` e `en-US_AllisonVoice`). As vozes padrão usam a síntese concatenativa para montar segmentos (ou unidades) de discursos gravados para gerar o áudio solicitado. Os pontos de concatenação dos segmentos registrados, às vezes, resultam em descontinuidades de fala que podem comprometer a qualidade e a naturalidade do discurso resultante.

### Vozes neurais
{: #neuralVoices}

As vozes neurais incluem uma sequência de versões (`V3`) em seu nome (por exemplo, `pt-BR_IsabelaV3Voice` e `en-US_AllisonV3Voice`). Em vez de depender da seleção e da concatenação de segmentos, a tecnologia de voz neural usa diversas Redes Neurais Profundas (DNNs) para prever os recursos acústicos (espectrais) do discurso. As DNNs são treinadas em discursos humanos naturais e geram o áudio resultante por meio dos recursos acústicos preditos.

Durante a síntese, as DNNs preveem a duração do tom e do fonema (prosódia), a estrutura espectral e a forma de onda do discurso. As
vozes neurais produzem um discurso nítido e limpo, com uma qualidade de áudio muito natural e suave. Assim, elas têm maior consistência na qualidade geral do que as vozes padrão.

Para obter mais informações sobre a tecnologia de voz neural do serviço, consulte

-   A postagem do blog [IBM
Watson Text to Speech: vozes neurais com disponibilidade geral](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   O documento de pesquisa [Text to Speech de alta qualidade, leve e adaptável usando o LPCNet](https://arxiv.org/abs/1905.00590){: external}

As vozes neurais não suportam os elementos ou atributos SSML a seguir:

-   O atributo `volume`do elemento `<prosody>`
-   O elemento `<express-as>`
-   O elemento `<voice-transformation>`

No entanto, é possível que você descubra que esses recursos SSML não são mais necessários ao usar as vozes neurais. Além disso, é possível fazer modificações de tom e taxa em vozes neurais usando o elemento `<prosody>` em vez do elemento `<voice-transformation>`. Para obter mais informações, consulte [O elemento prosody](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element).

### Customização de voz
{: #customizeVoice}

Ao sintetizar o texto, o serviço aplica as regras de pronúncia dependentes de idioma para converter a ortografia comum de cada palavra em uma ortografia fonética. As regras de pronúncia do serviço funcionam bem para palavras comuns, mas podem produzir resultados imperfeitos para palavras incomuns, tais como termos com origens estrangeiras, nomes pessoais, abreviações ou acrônimos.

Se o léxico de seu aplicativo incluir essas palavras, será possível usar a interface de customização para especificar como o serviço as pronuncia. Para obter mais informações, consulte [Entendendo a customização](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

É possível criar um modelo de voz customizado para um idioma específico, não para uma voz específica. Portanto, um modelo customizado pode ser usado com qualquer voz, padrão ou neural, para o idioma especificado.

## Especificando uma voz
{: #specifyVoice}

Os métodos HTTP `GET` e `POST /v1/synthesize`, bem como o método WebSocket `/v1/synthesize`, aceitam um parâmetro de consulta `voice` opcional para especificar a voz para o áudio sintetizado. Para obter mais informações, consulte [A interface HTTP](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) e [A interface WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).

O serviço baseia seu entendimento do idioma para o texto de entrada na voz especificada. Certifique-se de especificar uma voz que corresponda ao idioma do texto de entrada. Por exemplo, ao especificar a voz francesa (`fr-FR_ReneeVoice`), o serviço assumirá que o texto de entrada está escrito em francês. Ao transmitir um texto que não está escrito no idioma da voz (por exemplo, texto em inglês para a voz francesa), o serviço poderá não produzir resultados significativos.

## Listando todas as vozes disponíveis
{: #listVoices}

O método `GET /v1/voices` lista informações sobre todas as vozes disponíveis. Não é necessário nenhum argumento, e ele retorna uma matriz JSON denominada `voices`. A matriz inclui um objeto separado para cada voz.

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaVoice",
      "language": "en-US",
      "gender": "female",
      "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
      "description": "Lisa: American English female voice.", "customizável": true,
      "supported_features": {
        "voice_transformation": true,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

Os campos dos objetos de voz fornecem as informações a seguir:

-   `name` é um identificador para a voz (por exemplo, `en-US_LisaVoice`). Especifique esse valor para o parâmetro `voice` do método `/v1/synthesize`.
-   `language`especifica o idioma e a região da voz (por exemplo, `en-US`).
-   `gender` identifica a voz como `male` ou `female`.
-   `url` identifica a URL para a voz.
-   `description` fornece uma breve descrição da voz.
-   `customizable` é um valor booleano que indica se a voz pode ser customizada com a interface de customização do serviço (esse campo, que fornece as mesmas informações que o campo `custom_pronunciation`, é mantido para a compatibilidade com versões anteriores).
-   `supported_features` descreve os recursos de serviço adicionais suportados pela voz:
    -   `voice_transformation`é um valor booleano que indica se a voz pode ser transformada usando o elemento SSML `<voice-transformation>`.
    -   `custom_pronunciation` é um valor booleano que indica se a voz pode ser customizada com a interface de customização do serviço.

## Listando uma Voz Específica
{: #listVoice}

O método `GET /v1/voices/{voice}` lista informações sobre uma voz específica. Ele aceita dois parâmetros.

<table>
  <caption>Tabela 2. Parâmetros do método <code>voices</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parâmetro</th>
    <th style="text-align:center; width:12%">Tipo</th>
    <th style="text-align:center; width:12%">Tipo de dados</th>
    <th style="text-align:left">Descrição</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Necessário</em></td>
    <td style="text-align:center">Caminho</td>
    <td style="text-align:center">Sequência</td>
    <td>
      Identifica a voz para a qual as informações devem ser retornadas. Você especifica uma voz por seu nome (por exemplo, <code>en-US_LisaVoice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Consulta</td>
    <td style="text-align:center">Sequência</td>
    <td>
      Fornece o Identificador Exclusivo Global (GUID) de um modelo de voz customizado que foi definido para o idioma da voz especificada. Se você incluir um ID de customização, a solicitação deverá ser realizada com credenciais para a instância do serviço que possui o modelo customizado.
    </td>
  </tr>
</table>

Se você omitir o parâmetro `customization_id`, o método retornará a saída JSON para a voz especificada que é idêntica às informações retornadas para uma voz pelo método `GET /v1/voices`. Se você especificar um `customization_id`, a saída incluirá um campo `customization` que fornecerá informações sobre o modelo de voz customizado especificado.

```javascript
{
  "name": "en-US_LisaVoice",
  "language": "en-US",
  "gender": "female",
  "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
  "description": "Lisa: American English female voice.", "customizável": true,
      "supported_features": {
    "voice_transformation": true,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

Os atributos do campo adicional `customization` fornecem informações, como o GUID, o nome, o idioma e a descrição do modelo de voz customizado. Eles também mostram as credenciais do proprietário do modelo, a data e a hora nas quais o modelo foi criado e a data e a hora da última
modificação.
