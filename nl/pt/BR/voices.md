---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28"

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

# Idiomas e vozes
{: #voices}

O serviço {{site.data.keyword.texttospeechfull}}suporta uma variedade de idiomas, vozes e dialetos. O serviço oferece ao menos uma voz masculina ou feminina, às vezes ambas, para cada idioma. Cada voz usa a cadência e a entonação apropriadas para seu dialeto.
{: shortdesc}

## Idiomas e vozes suportados
{: #languageVoices}

A Tabela 1 lista as vozes que estão disponíveis para cada idioma e dialeto, incluindo seu sexo. Se você omitir o parâmetro opcional `voice` de uma solicitação, o serviço usará a voz `en-US_MichaelVoice` por padrão. Para entender por que o serviço oferece duas versões de algumas vozes, consulte [Tecnologias de síntese de discurso](#technologiesVoices).

Atualmente, um problema com a implementação das vozes da `V2` causa ruído de segundo plano no discurso sintetizado. Para obter mais informações, consulte [Limitações conhecidas](/docs/services/text-to-speech/release-notes.html#limitations).
{: note}

<table style="width:90%">
  <caption>Tabela 1. Idiomas e vozes suportados</caption>
  <tr>
    <th style="text-align:left">Idioma</th>
    <th style="text-align:center">Voz</th>
    <th style="text-align:center">Gênero</th>
  </tr>
  <tr>
    <td style="text-align:left">Português do Brasil</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Castelhano</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Francês</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Alemão</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code><br/>
     <code>de-DE_BirgitV2Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code><br/>
     <code>de-DE_DieterV2Voice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td style="text-align:left">Italiano</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code><br/>
     <code>it-IT_FrancescaV2Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Japonês</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Espanhol da América Latina</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Espanhol da América do Norte</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglês britânico</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglês americano</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code><br/>
     <code>en-US_AllisonV2Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaVoice</code><br/>
     <code>en-US_LisaV2Voice</code></td>
    <td style="text-align:center">Feminina</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code><br/>
     <code>en-US_MichaelV2Voice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
</table>

As vozes `es-LA_SofiaVoice` e `es-US_SofiaVoice` são essencialmente a mesma. A diferença mais significativa diz respeito a como as duas vozes interpretam um $ (cifrão). A versão da América Latina usa o termo *pesos*, enquanto que a versão da América do Norte usa o termo *d&oacute;lares*. Outras diferenças menores também podem existir entre as duas vozes.
{: note}

### Tecnologias de síntese de discurso
{: #technologiesVoices}

O serviço disponibiliza duas versões de algumas vozes, por exemplo, `en-US_AllisonVoice` e `en-US_AllisonV2Voice`. A diferença primária entre as duas versões reflete a tecnologia que o serviço usa para sintetizar o discurso:

-   A *síntese concatenativa* monta segmentos (ou unidades) de discurso registrado para gerar o áudio solicitado. Ela gera um áudio que pode ser considerado mais nítido, mas os pontos de concatenação dos segmentos registrados, às vezes, resultam em distorções de fala.

    Vozes que não incluem a sequência `V2` em seus nomes (por exemplo, `en-US_AllisonVoice`) são baseadas na síntese concatenativa.
-   A *síntese de deep learning* usa uma Deep Neural Network (DNN) para sintetizar o discurso para o texto especificado. Em vez de incluir os segmentos registrados de áudio em uma sequência, essa abordagem conta com o aprendizado de máquina para treinar uma DNN em dados de discurso registrados. A síntese de deep-learning ou baseada em DNN produz um áudio com uma prosódia mais natural e uma qualidade geral mais consistente.

    As vozes que incluem a sequência `V2` em seus nomes (por exemplo, `en-US_AllisonV2Voice`) são vozes mais novas que usam a síntese baseada em DNN.

É necessário experimentar as novas vozes antes de adotá-las para seu aplicativo. As duas tecnologias produzem áudio com diferentes qualidades de sinal, portanto, as novas vozes podem não ser melhores para todos os aplicativos. Além disso, as vozes baseadas em DNN não suportam os elementos ou atributos do SSML a seguir:

-   O atributo `volume`do elemento `<prosody>`
-   O elemento `<express-as>`
-   O elemento `<voice-transformation>`

Se o seu aplicativo usar esses elementos, continue usando as vozes baseadas na síntese concatenativa.

### Customização de voz
{: #customizeVoice}

Ao sintetizar o texto, o serviço aplica as regras de pronúncia dependentes de idioma para converter a ortografia comum de cada palavra em uma ortografia fonética. As regras de pronúncia do serviço funcionam bem para palavras comuns, mas podem produzir resultados imperfeitos para palavras incomuns, tais como termos com origens estrangeiras, nomes pessoais, abreviações ou acrônimos.

Se o léxico de seu aplicativo incluir essas palavras, será possível usar a interface de customização para especificar como o serviço as pronuncia. Para obter mais informações, consulte [Entendendo a customização](/docs/services/text-to-speech/custom-intro.html).

## Especificando uma voz
{: #specifyVoice}

Os métodos HTTP `GET` e `POST /v1/synthesize`, bem como o método WebSocket `/v1/synthesize`, aceitam um parâmetro de consulta `voice` opcional para especificar a voz para o áudio sintetizado. Para obter mais informações, consulte [A interface HTTP](/docs/services/text-to-speech/http.html) e [A interface WebSocket](/docs/services/text-to-speech/websockets.html).

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
    <td><code>customization_id</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Consulta</td>
    <td style="text-align:center">Sequência</td>
    <td>
      Fornece o identificador exclusivo global (GUID) de um modelo de voz customizado definido para a voz especificada. Ao incluir um ID de customização, deve-se chamar o método com as credenciais de serviço do proprietário do modelo customizado.
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

Os atributos do campo adicional `customization` fornecem informações, como o GUID, o nome, o idioma e a descrição do modelo de voz customizado. Também mostram as credenciais de serviço do proprietário do modelo, a data e o horário nos quais o modelo foi criado e a data e o horário de sua última modificação.
