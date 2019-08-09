---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-24"

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

# A interface WebSocket
{: #usingWebSocket}

Para sintetizar o texto para fala com a interface WebSocket do serviço {{site.data.keyword.texttospeechfull}}, primeiro estabeleça uma conexão com o serviço chamando seu método `/v1/synthesize`. Em seguida, envie o texto que deve ser sintetizado ao serviço como uma mensagem de texto JSON pela conexão. O serviço encerra automaticamente a conexão do WebSocket quando conclui o processamento da solicitação.
{: shortdesc}

O ciclo de solicitação e resposta sintetizado inclui as etapas a seguir:

1.  [Estabelecer uma conexão](#WSopen).
1.  [Enviar o texto de entrada](#WSsend).
1.  [Receber uma resposta](#WSreceive).

A interface WebSocket aceita entradas idênticas e produz resultados idênticos, como os métodos `GET` e `POST /v1/synthesize` da interface HTTP. No entanto, a interface WebSocket suporta o uso do elemento `<mark>` do SSML para identificar o local de marcadores especificados pelo usuário no áudio. Ele também pode retornar informações de sincronização para todas as cadeias do texto de entrada. Para obter mais informações, consulte [Obtendo sincronizações de palavra](/docs/services/text-to-speech?topic=text-to-speech-timing).

Os fragmentos de código de exemplo a seguir são gravados em JavaScript e são baseados na API do WebSocket HTML5. Para obter mais informações sobre o protocolo WebSocket, consulte o Internet Engineering Task Force (IETF) [Solicitação de comentários (RFC) 6455](http://tools.ietf.org/html/rfc6455){: external}.
{: note}

## Estabelecer uma conexão
{: #WSopen}

Você chama o método `/v1/synthesize` por meio do protocolo WebSocket Secure (WSS) para estabelecer uma conexão com o serviço. O método está disponível no terminal a seguir:

```
wss://{host_name}/text-to-speech/api/v1/synthesize
```
{: codeblock}

em que `{host_name}` é o local no qual seu aplicativo está hospedado:

-   `stream.watsonplatform.net` para Dallas (os exemplos a seguir usam esse nome de host)
-   `stream-fra.watsonplatform.net` para Frankfurt
-   `gateway-syd.watsonplatform.net`para Sydney
-   `gateway-wdc.watsonplatform.net` para Washington, DC
-   `gateway-tok.watsonplatform.net` para Tóquio
-   `gateway-lon.watsonplatform.net` para Londres

Um cliente WebSocket chama esse método com os parâmetros de consulta a seguir para estabelecer uma conexão autenticada com o serviço. Se você usar a autenticação do Identity and Access Management (IAM), use o parâmetro de consulta `access_token`. Se você usar as credenciais de serviço do Cloud Foundry, use o parâmetro de consulta `watson-token`.

<table>
  <caption>Tabela 1. Parâmetros do método <code>/v1/synthesize</code></caption>
  <tr>
    <th style="text-align:left; width:23%">Parâmetro</th>
    <th style="text-align:center; width:12%">Tipo de dados</th>
    <th style="text-align:left">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>access_token</code>
      <br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Sequência</td>
    <td style="text-align:left">
      <em>Se você usar a autenticação do IAM,</em> transmita um token de acesso IAM válido para autenticar-se com o serviço. Você transmite um token de acesso do IAM em vez de uma chave de API com a chamada. Deve-se usar o token de acesso antes de sua expiração. Para obter informações sobre como obter um token de acesso, consulte [Autenticando-se com tokens do IAM](/docs/services/watson?topic=watson-iam).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>watson-token</code>
      <br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Sequência</td>
    <td style="text-align:left">
      <em>Se você usar as credenciais de serviço do Cloud Foundry,</em> transmita um token de autenticação do {{site.data.keyword.watson}} válido para autenticar-se com o serviço. Você transmite um token do {{site.data.keyword.watson}} em vez de credenciais de serviço com a chamada.
      Os tokens do {{site.data.keyword.watson}} são baseados em credenciais de serviço do Cloud Foundry, que usam um `username` e uma `password` para a autenticação básica HTTP. Para obter informações sobre como obter um token do {{site.data.keyword.watson}}, consulte
[Tokens do {{site.data.keyword.watson}}](/docs/services/watson?topic=watson-gs-tokens-watson-tokens).
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Especifica a voz na qual o texto deve ser falado no áudio.
      Omita o parâmetro para usar a voz padrão, `en-US_MichaelVoice`.
      Para obter mais informações, consulte [Idiomas e vozes](/docs/services/text-to-speech?topic=text-to-speech-voices).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Especifica o Identificador Exclusivo Global (GUID) para uma voz customizada
      modelo que deve ser usado para a síntese. É garantido que um modelo de voz customizado funcione apenas se ele corresponder ao idioma da voz usada para a síntese. Se você incluir um ID de customização, a solicitação deverá ser realizada com credenciais para a instância do serviço que possui o modelo customizado. Omita o parâmetro para usar a voz especificada sem a customização. Para obter mais informações, consulte [Entendendo a customização](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
    </td>
  </tr>
  <tr>
    <td><code>x-watson-learning-opt-out</code><br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Booleano</td>
    <td>
      Indica se o serviço registra solicitações e resultados enviados por meio da conexão. Para evitar que a IBM acesse seus dados para melhorias gerais de serviço, especifique <code>true</code> para o parâmetro. Para obter mais informações, consulte [Controlando a criação de log de solicitação para serviços do Watson](/docs/services/watson?topic=watson-gs-logging-overview).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>x-watson-metadata</code>
      <br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Sequência</td>
    <td style="text-align:left">
      Associa um ID do cliente aos dados transmitidos pela conexão. O parâmetro aceita o argumento <code>customer_id={id}</code>, em que <code>id</code> é uma sequência genérica ou aleatória que deve ser associada aos dados. Deve-se codificar com URL o argumento para o parâmetro, por exemplo, `customer_id%3dmy_ID`. Por padrão, nenhum ID do cliente está associado aos dados. Para obter mais informações, consulte [Segurança de informações](/docs/services/text-to-speech?topic=text-to-speech-information-security).
    </td>
  </tr>
</table>

O fragmento de código JavaScript a seguir estabelece uma conexão com o serviço. A chamada para o método `/v1/synthesize` transmite os parâmetros de consulta `voice` e `access_token`, o primeiro deles para direcionar o serviço para o uso da voz Allison em inglês americano. Depois que a conexão estiver estabelecida, os listeners de eventos (`onOpen`, `onClose` e assim por diante) serão definidos para responder a eventos do serviço.

```javascript
var IAM_access_token = '{ access_token }';
var wsURI = 'wss: //stream.watsonplatform.net/text-to-speech/api/v1/synthesize '
  + '?access_token=' + IAM_access_token
  + '&voice=en-US_AllisonVoice';
var websocket = new WebSocket(wsURI);

websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

## Enviar o texto de entrada
{: #WSsend}

Para sintetizar o texto, o cliente transmite uma mensagem de texto JSON simples para o serviço com os parâmetros a seguir.

<table>
  <caption>Tabela 2. Parâmetros da mensagem de texto JSON</caption>
  <tr>
    <th style="text-align:left; width:23%">Parâmetro</th>
    <th style="text-align:center; width:12%">Tipo de dados</th>
    <th style="text-align:left">Descrição</th>
  </tr>
  <tr>
    <td><code>text</code><br/><em>Necessário</em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Fornece o texto que deve ser sintetizado. O cliente pode transmitir um texto sem formatação ou anotado com o Speech Synthesis
      Markup Language (SSML). O cliente pode transmitir um máximo de 5 KB de texto de entrada com a solicitação. O limite inclui qualquer SSML especificado. Para obter informações adicionais, consulte
     [Especificando Texto de Entrada](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#input)
      e as seções que o seguem.<br/><br/>
      A entrada do SSML também pode incluir o elemento <code>&lt;mark&gt;</code>.
      Para obter mais informações, consulte [Especificando uma marca do SSML](/docs/services/text-to-speech?topic=text-to-speech-timing#mark).
    </td>
  </tr>
  <tr>
    <td><code>aceitar</code><br/><em>Necessário</em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Especifica o formato solicitado (tipo MIME) do áudio. Use
      `*/*` para solicitar o formato de áudio padrão, <code>audio/ogg;codecs=opus</code>. Para obter mais informações, consulte [Formatos de áudio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>      Opcional
    </em></td>
    <td style="text-align:center">String[ ]</td>
    <td>
      Especifica que o serviço deve retornar informações de sincronização de palavra para todas as sequências do texto de entrada. O serviço retorna o horário de início e de término de cada token da entrada. Especifique <code>words</code> como o elemento lone da matriz para solicitar sincronizações de palavra. Especifique uma matriz vazia ou omita o parâmetro para não receber sincronizações de palavra.
      Para obter mais informações, consulte [Obtendo sincronizações de palavra](/docs/services/text-to-speech?topic=text-to-speech-timing#timing). <em>Não suportado para o texto de entrada em japonês.</em>
    </td>
  </tr>
</table>

O fragmento a seguir do código JavaScript transmite uma mensagem "Hello world" simples como o texto de entrada e solicita o formato padrão para o áudio. As chamadas são incluídas na função `onOpen` definida para o cliente com o objetivo de garantir que sejam enviadas somente após a conexão ser estabelecida.

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

O serviço responde essa mensagem enviando uma mensagem de texto que confirma o formato da resposta de áudio. A resposta a seguir confirma o formato de áudio padrão.

```javascript
{
  'binary_streams': [
    {
      content_type: 'audio/ogg;codecs=opus'
    }
  ]
}
```
{: codeblock}

## Receber uma resposta
{: #WSreceive}

Depois de confirmar o formato de áudio, o serviço envia o áudio sintetizado como um fluxo binário de dados no formato indicado. O serviço envia informações de sincronização como uma ou mais mensagens de texto se

-   O texto de entrada incluir um ou mais elementos `<mark>` do SSML.
-   Você especificar o parâmetro `timings` com a solicitação.

O serviço também pode enviar mensagens de texto com avisos ou erros. Quando conclui a síntese do texto de entrada, o serviço encerra automaticamente a conexão do WebSocket.

O cliente precisa anexar respostas binárias do serviço aos resultados de áudio recebidos por meio da conexão. Ele pode manipular mensagens de texto as respondendo, exibindo ou capturando para uso pelo aplicativo (por exemplo, se contiverem locais de marca). O exemplo simples a seguir de uma função `onMessage` anexa mensagens de texto e binárias recebidas do serviço para a variável apropriada com base em seu tipo. Quando a função `onClose()` é executada, o fluxo de áudio inteiro foi recebido.

```javascript
var messages;
var audioStream;

function onMessage(evt) {
  if (typeof evt.data === string) {
    mensagens + = evt.data;
  } else {
    console.log('Received ' + evt.data.size() + ' binary bytes');
    audioStream += evt.data;
  }
}

function onClose(evt) {
  // The audio stream is complete.
}
```
{: codeblock}

## Códigos de retorno do WebSocket
{: #returnCodes}

O serviço pode enviar os códigos de retorno a seguir para o cliente por meio da conexão do WebSocket:

-   `1000` indica encerramento normal da conexão, o que significa que a finalidade para a qual a conexão foi estabelecida foi atendida.
-   `1002` indica que o serviço está encerrando a conexão devido a um erro de protocolo.
-   `1006` indica que a conexão foi encerrada anormalmente.
-   `1009` indica que o tamanho do quadro excedeu o limite de 4 MB.
-   `1011` indica que o serviço está encerrando a conexão porque encontrou uma condição inesperada que o impede de preencher a solicitação, como um argumento inválido. O código de retorno também pode indicar que o texto de entrada era muito grande.

Se o soquete fechar com um erro, o serviço enviará ao cliente uma mensagem informativa do formulário `{ "erro": "Mensagem de erro específica" }`antes de fechar. O serviço também pode enviar mensagens de aviso não fatais para parâmetros desconhecidos.

## Exemplo de mensagens de erro e de aviso
{: #returnErrors}

Os exemplos a seguir mostram respostas de erro. Incluem uma mensagem de texto JSON e uma mensagem formatada do método de retorno de chamada `onClose` do cliente. As mensagens formatadas iniciam com o booleano `true` porque a conexão está encerrada. Também incluem o código de erro do WebSocket que causou o encerramento.

-   Esse exemplo mostra mensagens de erro para um argumento inválido para o parâmetro `accept`:

    ```javascript
    {
      "error": "Unsupported mimetype. Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   Este exemplo mostra mensagens de erro para um parâmetro `text` ausente:

    ```javascript
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

O exemplo a seguir mostra uma resposta de aviso, nesse caso, para um parâmetro desconhecido chamado `invalid-parameter`. Ele não inclui a segunda mensagem porque a conexão não foi encerrada pelo aviso.

```javascript
{
  "avisos": "Argumentos desconhecidos: invalid-parameter."
}
```
{: codeblock}

Para obter mais informações sobre os códigos de retorno do WebSocket, consulte o Internet Engineering Task Force (IETF) [Solicitação de comentários (RFC) 6455](http://tools.ietf.org/html/rfc6455){: external}.
