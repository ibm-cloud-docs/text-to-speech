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

# Criando e gerenciando entradas customizadas
{: #customWords}

Quando houver um modelo customizado, a próxima etapa será incluir entradas customizadas no formato de pares de palavra/tradução para definir como as palavras especificadas devem ser pronunciadas durante a síntese. As definições substituem as regras de pronúncia regular padrão do serviço. É possível incluir e consultar traduções para uma ou mais palavras por vez e excluir palavras individuais que não são mais necessárias. Assim que estiver familiarizado com a interface de customização, manipular diversas palavras de uma vez será mais conveniente do que trabalhar com somente uma palavra por vez. Deve-se usar credenciais para a instância do serviço que possui um modelo customizado para usar qualquer método que requeira o ID de customização.
{: shortdesc}

## Incluindo uma única palavra em um modelo customizado
{: #cuWordAdd}

Para incluir um par de palavra/tradução único em um modelo customizado, use o método `PUT /v1/customizations/{customization_id}/words/{word}`. Você especifica a palavra a ser incluída na URL do método. Você fornece a tradução para a palavra como um objeto JSON com um único atributo `translation`. A inclusão de uma nova tradução para uma palavra que já existe em um modelo sobrescreve sua tradução existente.

É possível fornecer uma tradução usando o método fonético ou de semelhança (ou uma combinação dos dois). Para traduções fonéticas, é possível usar o Alfabeto Fonético Internacional (IPA) ou o formato do {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). Os exemplos a seguir usam abordagens diferentes para incluir traduções equivalentes para a palavra `IEEE` em um modelo customizado.

-   **Sons-tipo:**Para este exemplo, o método de sons semelhantes é a abordagem mais simples:

    ```bash
    curl -X PUT -u "apikey: { apikey }"
    -- header "Content-Type: application / json"
    --data "{ \" conversão \": \" I triple E \" }"
    "https: //stream.watsonplatform.net/text-to-speech/api/v1/customizations/ { customization_id } /words/IEEE"
    ```
    {: pre}

-   **IPA Phonetic:**O IPA requer o uso do elemento `<phoneme>`com o atributo `alfabeto`configurado para `ipa`e o atributo `ph`definido no formato IPA:

    <pre><code class="language-bash">curl -X PUT -u "apikey: { apikey }"
    --header "Content-Type: application/json"
    --data \" { ": \" &lt; nome do alfabeto = \ \\" ipa \\\" ph = \ \\" & # 618; .t & #712; & #616; p & #601; l. & #712; i \\\" &gt;&lt;/phoneme&gt;\" }"
    "https: //stream.watsonplatform.net/text-to-speech/api/v1/customizations/ { customization_id } /words/IEEE"</code></pre>

-   **{{site.data.keyword.IBM_notm}}SPR:**SPR fonética usa o elemento `<phoneme>`com o atributo `alfabeto`configurado como `ibm`e o atributo `ph`definido no formato SPR:

    ```bash
    curl -X PUT -u "apikey: { apikey }"
    -- header "Content-Type: application / json"
    --data "{ \" translação \": \" < foneme alfabeto = \ \\" ibm \\\" ph= \\\ "1Y.tr1Ipxl.1i \\\" >< /phoneme>\" }"
    "https: //stream.watsonplatform.net/text-to-speech/api/v1/customizations/ { customization_id } /words/IEEE"
    ```
    {: pre}

## Incluindo Várias Palavras em um Modelo Customizado
{: #cuWordsAdd}

Para incluir uma ou mais palavras em um modelo customizado de uma vez, use o método `POST /v1/customizations/{customization_id}/words`. Você especifica as entradas a serem incluídas no modelo customizado como uma matriz JSON de pares de palavra/tradução. O exemplo a seguir inclui traduções semelhantes comuns para as palavras `NCAA` e `iPhone` em um modelo customizado:

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

O conteúdo JSON enviado no corpo da solicitação é igual ao seguinte:

```javascript
{
  "words": [
    {"word":"NCAA", "translation":"N C double A"},
    {"word":"iPhone", "translation":"I phone"}
  ]
}
```
{: codeblock}

Conforme mencionado em [Atualizando um modelo customizado](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsUpdate), também é possível usar o método `POST /v1/customizations/{customization_id}` para incluir palavras em um modelo customizado. O exemplo a seguir usa esse método para incluir as mesmas duas palavras que o exemplo anterior e não faz mudanças nos metadados do modelo. Com a exceção da URL, os dois métodos são idênticos.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

## Incluindo palavras em um modelo customizado em japonês
{: #cuJapaneseAdd}

Considerações adicionais e um campo `part_of_speech` adicional se aplicam ao criar entradas para palavras em um modelo customizado em japonês. Para obter mais informações, consulte [Trabalhando com entradas em japonês](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes). Especifique uma parte do discurso para uma entrada customizada em japonês da seguinte forma:

-   Para o método `PUT /v1/customizations/{customization_id}/words/{word}`, transmita um objeto JSON do seguinte formato:

    ```javascript
    {
      "conversão": "value",
      "part_of_discurso": "valor"
    }
    ```
    {: codeblock}

-   Para os métodos `POST /v1/customizations/{customization_id}/words` e `POST customizations/{customization_id}`, transmita um objeto JSON como o seguinte:

    ```javascript
    {
      "words": [
        {
          "word": "value",
          "translation": "value",
          "part_of_speech": "value"
        }
        . . .
      ]
    }
    ```
    {: codeblock}

Os exemplos a seguir do método `PUT /v1/customizations/ { customization_id } /words/ { word }`traduzem a sequência de caracteres codificados por URL para `NY`para o nome (`Mesi`) <code>& #12491; & #12517; & #12540; & #12463;</code>(`New York`em inglês). Se essa tradução customizada não estiver definida, a sequência será lida como `enu wai`.

-   **Semelhante:**

    <pre><code>curl -X PUT -u "apikey: { apikey }"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **IPA fonético:**

    <pre><code>curl -X PUT -u "apikey: { apikey }"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#626;&#623;&#720;&#106;&#111;&#720;&#107;&#623;\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **{{site.data.keyword.IBM_notm}} SPR fonético:**

    <pre><code>curl -X PUT -u "apikey: { apikey }"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

## Consultando uma única palavra em um modelo customizado
{: #cuWordQueryModel}

Para consultar a tradução de uma única palavra de um modelo customizado, use o método `GET /v1/customizations/{customization_id}/words/{word}`. Você especifica a palavra na URL do método. A conversão é retornada como está definida no modelo customizado (sons-como ou fonética).

O exemplo a seguir consulta um modelo customizado em busca da tradução da palavra `IEEE`:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

Se a palavra tiver a tradução semelhante no modelo, o exemplo retornará a saída JSON a seguir:

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

## Consultando todas as palavras de um modelo customizado
{: #cuWordsQueryModel}

Para ver as traduções de todas as palavras definidas em um modelo customizado, use o método `GET /v1/customizations/{customization_id}/words`. O exemplo a seguir usa o método para listar as entradas de um modelo customizado que contém traduções semelhantes para três palavras:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

O método retorna uma matriz JSON com os dados a seguir. Para modelos customizados em japonês, a saída inclui a parte do discurso das palavras individuais.

```javascript
{
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

Conforme descrito em [Consultando um modelo customizado](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery), também é possível usar o método `GET /v1/customizations/{customization_id}` para ver os metadados e as palavras de um modelo customizado:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

O método retorna a saída JSON do formulário a seguir. Como esse exemplo e o anterior especificam o mesmo modelo customizado, a matriz de palavras em sua saída é idêntica.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T19:15:17.926Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T19:46:01.387Z",
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

## Consultando uma palavra de um idioma
{: #cuWordsQueryLanguage}

Para consultar a pronúncia de uma palavra, use o método `GET /v1/pronunciation`. Especifique uma voz para obter a pronúncia no idioma dessa voz. Por padrão, o método retorna a pronúncia com base nas regras de pronúncia regular do serviço, mas também é possível solicitar a pronúncia para um modelo de voz customizado que tenha sido especificado. O método inclui quatro parâmetros de consulta que permitem que você especifique as informações que devem ser retornadas:

-   O parâmetro `text` necessário especifica a palavra cuja pronúncia deve ser retornada.
-   O parâmetro `voice` opcional permite especificar o idioma da pronúncia. Ao especificar um dos modelos de voz (por exemplo, `en-US_LisaVoice`) para indicar o idioma desejado, todas as vozes para o mesmo idioma (por exemplo, `en-US`) retornarão a mesma pronúncia. Por padrão, a pronúncia é retornada para o inglês americano.
-   O parâmetro `format` opcional permite especificar o formato fonético da pronúncia, `ipa` ou `ibm`. Por padrão, a pronúncia é retornada no formato do IPA.
-   O parâmetro `customization_id` opcional permite especificar um modelo de voz customizado para o qual a pronúncia deve ser retornada. Se a palavra não estiver definida no modelo de voz especificado, o serviço retornará a pronúncia padrão para o idioma do modelo. Omita o parâmetro para ver a tradução para a voz especificada sem a customização. Não especifique uma voz e um modelo de voz customizado.

Esse método é útil porque permite consultar uma palavra de qualquer idioma e, porque não requer um ID de customização, não coloca restrições sobre as palavras que podem ser vistas. Ele pode ser especialmente útil ao compor uma tradução fonética para uma nova palavra, pois é possível usá-lo para obter a pronúncia para uma palavra existente e, em seguida, como a base de sua nova tradução, o que é muito mais conveniente do que criá-la do zero.

O exemplo a seguir obtém a pronúncia para a palavra `IEEE`no formato IPA padrão.

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=IEEE"
```
{: pre}

<pre><code data-copy="false" class="language-javascript">{
  "pronunciation": ".&#712;a&#618; .&#712;i .&#712;i .&#712;i"
}</code></pre>

O exemplo a seguir insere uma tradução semelhante para a palavra `IEEE` e obtém o equivalente fonético no formato do {{site.data.keyword.IBM_notm}} SPR. Obter a pronúncia fonética para uma tradução semelhante é uma abordagem especialmente interessante para compor uma tradução fonética. Os espaços da palavra são codificados com URL no exemplo.

```bash
curl -X GET -u "apikey: { apikey }" "https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=i%20triple%20e&format=ibm "
```
{: pre}

```javascript
{
  "pronunciation": "1Y.tr1Ipxl.1i"
}
```
{: codeblock}

## Excluindo uma palavra de um modelo customizado
{: #cuWordDelete}

Para excluir uma palavra de um modelo customizado, use o método `DELETE /v1/customizations/{customization_id}/words/{word}`. Você especifica a palavra a ser excluída na URL do método. Não é possível excluir diversas palavras e palavras que não sejam individuais com um único método.

O exemplo a seguir excluirá a palavra `IEEE` do modelo customizado que foi especificado:

```bash
curl -X DELETE -u "apikey: { apikey }" "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE "
```
{: pre}
