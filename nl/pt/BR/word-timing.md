---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-07"

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

# Obtendo a sincronização de palavra
{: #timing}

A interface WebSocket fornece a mesma funcionalidade que os métodos HTTP `GET` e `POST /v1/synthesize`. Também é possível usar a interface WebSocket para obter informações de sincronização para locais específicos ou para todas as palavras da entrada:
{: shortdesc}

-   Inclua o elemento `<mark>` do SSML no texto de entrada para identificar o horário no qual o marcador ocorre no áudio.
-   Especifique o parâmetro `timings` de uma mensagem de texto JSON para obter informações de sincronização para todas as sequências do texto de entrada.

As informações de sincronização são úteis para sincronizar o áudio e o texto de entrada. Por exemplo, é possível coordenar os gestos de um robô com o conteúdo da fala sintetizada.

O parâmetro `timings` não é suportado para textos de entrada em japonês.
{: note}

## Como o serviço retorna as sincronizações de palavra
{: #timingHow}

Para retornar informações de sincronização de palavras ou marcas, o serviço multiplexa fluxos de texto e binários independentes para construir sua resposta:

-   Para cada elemento `<mark`>, o serviço retorna uma mensagem de texto JSON. Cada mensagem indica o horário exato do início do áudio sintetizado no qual a marca ocorre.
-   Para sincronizações de palavras para todas as sequências, o serviço retorna uma ou mais mensagens de texto JSON. Cada mensagem contém uma matriz de palavras e seus horários de início e de término desde o início do áudio sintetizado.

Os fluxos de texto e binários enviados pelo serviço são independentes. Portanto, o serviço tem pouco controle sobre o número de chunks de áudio entregues por ele e quando o usuário recebe as mensagens de texto e de áudio. Por exemplo, se o áudio é sintetizado mais rapidamente do que é compactado, todas as mensagens de texto podem chegar antes dos áudios.

Em termos práticos, o serviço pode enviar um número arbitrário de chunks de áudio, incluindo diversos chunks de áudio antes e depois de cada mensagem de texto. Também é possível que um único chunk binário contenha dados de áudio que sejam precedentes e subsequentes às informações de sincronização para uma marca ou palavra.

No entanto, a mensagem de texto que contém as informações de sincronização sempre chega antes do chunk binário que contém o áudio correspondente. Além disso, as mensagens de áudio sempre chegam em ordem, para que seja possível construir uma síntese de áudio exata do texto por meio dos resultados binários.

## Especificando uma marca do SSML
{: #mark}

O elemento `<mark>` opcional do SSML é uma tag vazia que coloca um marcador no texto a ser sintetizado. O cliente é notificado quando todo o texto que antecede o elemento `<mark>` foi sintetizado.

O elemento aceita um único atributo `name` que especifica uma sequência que identifica exclusivamente a marca. O nome deve começar com um caractere alfanumérico. O serviço retorna o nome com o horário no qual a marca ocorre do início do áudio sintetizado. É possível incluir qualquer número de marcas no texto de entrada.

O fragmento a seguir do código JavaScript inclui uma instância do elemento `<mark>`com o nome `aqui`:

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello <mark name="here"/> world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

Quando conclui a síntese do texto que antecede a marca, o serviço envia uma mensagem de texto que identifica o nome da marca e o horário, em segundos, no qual a marca ocorre no áudio:

```javascript
{
  "marks": [
    ["here", 0.5019387755102041]
  ]
}
```
{: codeblock}

A mensagem de texto que contém as informações de sincronização sempre chega antes do chunk de áudio que contém o local da marca.

## Solicitando sincronizações de palavra para todas as palavras
{: #timingRequest}

O parâmetro opcional `timings` do objeto JSON transmitido ao serviço para uma solicitação retorna as informações de sincronização para todas as sequências do texto de entrada. Essa conveniência elimina a necessidade de especificar o elemento `<mark>` do SSML para cada palavra da entrada. Transmita uma matriz que inclua a sequência `palavras`para solicitar as timings de palavra. Transmita uma matriz vazia ou omita o parâmetro para não receber informações de sincronização.

O serviço retorna as sincronizações de palavras pela conexão do WebSocket da mesma maneira que retorna informações de sincronização para elementos `<mark>` individuais. Ele retorna uma ou mais mensagens de texto JSON. Cada mensagem contém uma matriz de palavras e seus horários de início e de término, em segundos, do início do áudio sintetizado. Por exemplo, o exemplo a seguir solicita informações de sincronização de palavras:

```javascript
function onOpen(evt) {
  var message = {
    text: 'I have a pet bird.',
    accept: '*/*',
    timings: ['words']
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

Em resposta, o serviço pode retornar as mensagens de texto a seguir:

```javascript
{
  "words": [
    ["I", [0.0690258394023930, 0.1655782733012873]]
    ["have", [0.1655789302434486, 0.3722901056092351]]
    ["a", [0.3722906798320199, 0.4012192331086645]]
  ]
}
{
  "words": [
    ["pet", [0.4012195492838347, 0.5798213856109801]]
    [ "pássaro.", [0.5798218710823425, 0.7440360383928273]]
  ]
}
```
{: codeblock}

A resposta é apenas um exemplo. O serviço pode retornar uma ou mais mensagens de texto com informações de sincronização para a entrada. Além disso, as mensagens podem ser intercaladas com respostas que contêm chunks binários de áudio. Mas a mensagem de texto que contém as informações de sincronização para uma palavra sempre chega antes do chunk de áudio que contém essa palavra.

### Sincronizações para textos sem formatação
{: #timingText}

O processo de síntese do serviço envolve uma etapa de normalização de texto que soletra números, datas, horários, quantias monetárias, acrônimos e abreviações. Os resultados correspondem ao modo como essas cadeias são faladas. Por exemplo, a sequência *$200* é falada como três palavras: *two*, *hundred* e *dollars*. Como as informações de sincronização de palavra são usadas para sincronizar o áudio com o texto de entrada, o serviço retorna informações de sincronização que correspondem à ortografia não normalizada da entrada.

Por exemplo, considere o texto de entrada a seguir:

```
The coldest recorded temperature is -89.2 degrees Celsius in Antarctica on July 21, 1983!
```
{: codeblock}

O serviço retorna as sincronizações de áudio para as sequências a seguir:

"*The*", "*coldest*", "*recorded*", "*temperature*", "*is*", "*-89.2*", "*degrees*", "*Celsius*", "*in*", "*Antarctica*", "*on*", "*July*", "*21,*", "*1983!*"

Embora "*-89.2*" seja falado no áudio como cinco palavras separadas (*menos*, *oitenta*, *nove*, *ponto*, *dois*), a mensagem de texto fornece informações de sincronização para a sequência como uma única unidade com o horário de início de *menos*e o horário de encerramento de *dois*.

Como no exemplo anterior, as sequências não normalizadas também podem conter pontuação. O serviço inclui a pontuação precedente ou subsequente a uma palavra na mensagem de texto que retorna com as sincronizações. Por exemplo, as sequências "*21,*" e "*1983!*" incluem uma pontuação que o serviço retorna em sua mensagem de texto. Embora a pontuação resulte em silêncio, a sincronização de áudio para a palavra *não* inclui esse silêncio.

Por exemplo, considere o texto de entrada que contém a instrução condicional a seguir:

```
Se for ensolarado, eu vou para a praia.
```
{: codeblock}

O serviço retorna informações de sincronização para todas as sequências da entrada, incluindo "*sunny,*" e "*beach.*", que terminam com a pontuação que produz o silêncio. Mas as informações de sincronização para "*sunny,*" não incluem o silêncio produzido pela vírgula e as informações de sincronização para "*beach.*" não incluem o silêncio para o ponto. As informações refletem somente a sincronização das sequências faladas.

### Sincronizações para textos do SSML
{: #timingSSML}

O serviço retorna todos os caracteres de entrada quando sintetiza textos sem formatação, exceto espaços em branco, como parte das sequências em sua resposta de sincronização de palavra. O mesmo não acontece para o SSML, pois alguns elementos do SSML não geram áudio. A lista a seguir resume os elementos do SSML que podem impactar as informações de sincronização de palavra:

-   `<say-as>`indica como o texto que é colocado entre a abertura e o fechamento das tags `<say-as>`deve ser tratado na etapa de normalização. Os atributos especificam como o texto integrado deverá ser falado. O exemplo a seguir indica como a data deve ser falada:

    ```xml
    The baby was born on <say-as interpret-as="date" format="mdy">3/4/2016</say-as>.
    ```
    {: codeblock}

    O serviço retorna informações de sincronização para as sequências a seguir: "*The*", "*baby*", "*was*", "*born*", "*on*", "*3/4/2016.*" O serviço normaliza a sequência "*3/4/2016*" como "*march fourth two thousand sixteen*". As informações de sincronização de palavra para a sequência refletem o horário de início de "*march*" e o horário de término de "*sixteen*".

    O exemplo a seguir indica que a palavra `Hello` deve ser soletrada:

    ```xml
    <say-as interpret-as="letters">Olá</say-as>.
    ```
    {: codeblock}

    O serviço retorna informações de sincronização para a sequência "*Hello.*". Ele soletra a palavra letra por letra durante a etapa de normalização. As informações de sincronização de palavra na resposta refletem o horário de início da letra "*h*" e o horário de término da letra "*o*".
-   O`<phoneme>`fornece uma pronúncia para o texto que é colocado entre as tags `<phoneme>`de abertura e fechamento. Mas tanto o texto quanto a tag de fechamento são opcionais. O exemplo a seguir inclui um texto integrado e uma tag de fechamento:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme> was ripe.
    ```
    {: codeblock}

    O serviço retorna informações de sincronização para as sequências a seguir: "*O*", "*tomato*", "*era*", "*maduro.*"

    Por outro lado, o exemplo a seguir fornece um elemento `<phoneme>`unário sem texto incorporado e sem tag de fechamento:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo"/> was ripe.
    ```
    {: codeblock}

    Nesse caso, o serviço retorna informações de sincronização para as sequências a seguir: "*The*", "*&lt;phoneme&gt;*", "*was*", "*ripe.*"
-   `<sub>` substitui o texto incluído no atributo `alias` do elemento para o texto entre as tags de abertura e de fechamento `<sub>` no áudio falado. Por exemplo, a entrada a seguir inclui uma única tag `<sub>`:

    ```xml
    Eu trabalho na <sub alias="International Business Machines">IBM</sub>.
    ```
    {: codeblock}

    O serviço produz informações de sincronização para as sequências a seguir: "*I*", "*work*", "*at*", "*{{site.data.keyword.IBM_notm}}.*". O serviço normaliza a sequência "*{{site.data.keyword.IBM_notm}}*" como "*International Business Machines*". As informações de sincronização para a sequência refletem o horário de início de "*International*" e o horário de término de "*Machines*".
-   `<break>` insere uma pausa no texto falado. O serviço reflete o silêncio resultante na palavra timings como um intervalo entre o horário de encerramento da palavra que precede o elemento `<break>`e o horário de início da palavra que segue o elemento.
- `<paragraph>` (ou `<p>`) pode incluir o silêncio no áudio. O serviço não retorna informações de sincronização para o silêncio.
- `<sentence>` (ou `<s>`) pode incluir o silêncio no áudio. O serviço não retorna informações de sincronização para o silêncio.

Os elementos do SSML não mencionados na lista não afetam as informações de sincronização de palavra. Para obter mais informações sobre o suporte ao SSML do serviço, consulte [Usando o SSML](/docs/services/text-to-speech/SSML.html).

## Exemplos com elementos de marca
{: #timingExample}

Os exemplos a seguir mostram uma sessão simples do WebSocket entre um cliente e o serviço. Os exemplos focam na troca de dados, não no estabelecimento da conexão. O cliente envia uma mensagem de texto que inclui dois elementos `<mark>`, denominados `SIMPLE` e `EXAMPLE`, e solicita que o áudio seja retornado no formato WAV:

```javascript
{
  "text": "Esse é um exemplo de <mark name=\"SIMPLE\"/>simple <mark name=\"EXAMPLE\"/>.",
  "accept": "audio/wav"
}
```
{: codeblock}

Primeiro, o serviço envia uma mensagem para confirmar o formato de áudio. Em seguida, envia diversas mensagens com os resultados. O serviço não pode garantir o número de chunks de áudio que envia ao cliente ou a ordem na qual as mensagens de texto e de áudio são entregues.

Ambas as respostas a seguir são possíveis. Em cada caso, o serviço envia duas mensagens de texto que identificam os locais das marcas no fluxo binário. Mas ele envia um número arbitrário de mensagens binárias que contêm o áudio. As informações de sincronização para uma marca sempre chegam antes do chunk de áudio que contém o local da marca.

### Primeiro exemplo de resposta

Na primeira resposta de exemplo, as mensagens de texto são intercaladas com diversas mensagens de áudio.

```javascript
{
  "binary_streams": [
    {
      "content_type": "audio/wav"
    }
  ]
}
... um ou mais chunks de áudio binário
    todos os áudios antecedem a marca SIMPLE...
{
  "marks": [
    [
      "SIMPLE",
      0.7848991042702103
    ]
  ]
}
... um ou mais chunks de áudio binário
    o áudio pode ser precedente ou subsequente à marca SIMPLE
    todos os áudios antecedem a marca EXAMPLE...
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... um ou mais chunks de áudio binário
    o áudio pode ser precedente ou subsequente à marca EXAMPLE...
```
{: codeblock}

### Segunda resposta de exemplo

No segundo exemplo de resposta, as mensagens de texto chegam antes de qualquer uma das mensagens de áudio.

```javascript
{
  "binary_streams": [
    "content_type": "audio/wav"}
  ]
}
{
  "marks": [
    [
      "SIMPLE", 0.7848991042702103
    ]
  ]
}
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... um ou mais chunks de áudio binário...
```
{: codeblock}
