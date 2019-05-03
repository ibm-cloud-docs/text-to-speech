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

# Criando e gerenciando modelos de voz customizados
{: #customModels}

A primeira etapa para trabalhar com qualquer modelo customizado é criá-lo. Quando isso for feito, será possível gerenciar o modelo consultando ou atualizando seus metadados e entradas e excluindo-o, caso ele não seja mais necessário. Antes de começar, revise as informações de uso geral a seguir sobre modelos customizados.
{: shortdesc}

## Observações de uso
{: #customGuidelines}

Considere as diretrizes a seguir ao trabalhar com a interface de customização.

### Propriedade de modelos de voz customizados
{: #customOwner}

Um modelo de voz customizado é de propriedade da instância de serviço do {{site.data.keyword.texttospeechshort}} cujas credenciais são usadas para criá-lo. Deve-se usar as credenciais de serviço criadas para essa instância de serviço com os métodos da interface de customização para trabalhar com o modelo customizado.

Todas as credenciais de serviço obtidas para a mesma instância do {{site.data.keyword.texttospeechshort}}serviço compartilham acesso a todos os modelos customizados criados para essa instância de serviço. Para restringir o acesso a um modelo customizado, crie uma instância separada do serviço e use somente as credenciais para essa instância de serviço para criar e trabalhar com o modelo. Credenciais para outras instâncias de serviço não afetam o modelo customizado.

Uma vantagem de compartilhar a propriedade entre as credenciais de serviço é que é possível cancelar um conjunto de credenciais, por exemplo, se ficarem comprometidas. Em seguida, será possível criar novas credenciais para a mesma instância de serviço e ainda manter a propriedade e o acesso aos modelos customizados criados com as credenciais originais.

### Solicitar a criação de log e a privacidade de dados
{: #customLogging}

A maneira como o serviço manipula a criação de log de solicitação para chamadas para a interface de customização depende da solicitação:

-   O serviço *não* registra dados (palavras e traduções) usados para construir modelos de voz customizados. Não é necessário configurar o cabeçalho de solicitação `X-Watson-Learning-Opt-Out` ao usar a interface de customização para gerenciar palavras e traduções em um modelo customizado. Seus dados de treinamento nunca são usados para melhorar os modelos base do serviço.
-   O serviço *registra* os dados de log quando um modelo customizado é usado com uma solicitação de sintetização. Deve-se configurar o cabeçalho de solicitação `X-Watson-Learning-Opt-Out` para `true` para evitar a criação de log para solicitações de sintetização.

Para obter mais informações, consulte [Controlando a criação de log de solicitação para serviços {{site.data.keyword.watson}}](/docs/services/watson/getting-started-logging.html).

### Segurança de Informações
{: #customSecurity}

O serviço permite associar um ID do cliente aos dados incluídos ou atualizados para modelos de voz customizados. É possível associar um ID do cliente com palavras customizadas transmitindo o cabeçalho `X-Watson-Metadata` com os métodos a seguir:

-   `POST /v1/customizations/{customization_id}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word}`

Se necessário, será possível excluir os dados associados ao ID do cliente em seguida, usando o método `DELETE /v1/user_data`. Para obter mais informações, consulte [Segurança de informações](/docs/services/text-to-speech/information-security.html).

## Criando um modelo customizado
{: #cuModelsCreate}

Para criar um novo modelo customizado, use o método `POST /v1/customizations`. Como novo modelo está sempre vazio ao criá-lo pela primeira vez, deve-se usar outros métodos para preenchê-lo com pares de palavra/tradução. O novo modelo customizado é de propriedade do usuário cujas credenciais de serviço são usadas para criá-lo. Para obter mais informações, consulte [Propriedade de modelos de voz customizados](#customOwner).

Você transmite os atributos a seguir como um objeto JSON com o corpo da solicitação.

<table>
  <caption>Tabela 1. Parâmetros do método <code>POST /v1/customizations</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parâmetro</th>
    <th style="text-align:center; width:12%">Tipo de dados</th>
    <th style="text-align:left">Descrição</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>Necessário</em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Um nome definido pelo usuário para o novo modelo customizado. O nome é usado para rotular o modelo para fácil identificação. O nome deve ser exclusivo entre todos os modelos customizados possuídos.
    </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Um identificador para o idioma do modelo customizado. O padrão é <code>en-US</code> para inglês americano.
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Uma descrição do novo modelo. Embora seja opcional, uma descrição é altamente recomendada.
    </td>
  </tr>
</table>

O comando `curl` de exemplo a seguir cria um novo modelo customizado chamado `curl Test`. O cabeçalho `Content-Type` identifica o tipo da entrada como `application/json`.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{ \" name \": \"curl Test \", \" language \" \" :\"en-US \", \" description \": \" Teste de customização via curl \ "}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

O método retorna um objeto JSON que contém um identificador exclusivo global (GUID) para o novo modelo. O GUID é usado como o parâmetro `customization_id` em chamadas para acessar o modelo, como aqueles para consulta, modificação e uso do modelo e suas palavras.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

## Consultando um modelo customizado
{: #cuModelsQuery}

Para consultar informações sobre um modelo customizado existente, use o método `GET /v1/customizations/{customization_id}`. Esse é o meio mais direto de ver todas as informações sobre um modelo, seus metadados e os pares de palavra/tradução que ele contém.

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

O método retorna seus resultados como um objeto JSON do seguinte formato:

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T18:12:31.743Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T18:12:31.743Z",
  "words": []
}
```
{: codeblock}

Além das informações inseridas quando o modelo foi criado, a saída inclui as credenciais de serviço de seu proprietário, seu idioma e os horários nos quais ele foi criado e modificado pela última vez. Como o modelo não foi modificado desde sua criação, os dois horários no exemplo são iguais.

A saída também inclui uma matriz `words` que lista as entradas customizadas do modelo. Como o modelo ainda não foi atualizado, a matriz no exemplo está vazia.

## Consultando todos os modelos customizados
{: #cuModelsQueryAll}

Para ver informações sobre todos os modelos customizados que você possui, use o método `GET /v1/customizations`:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

O método retorna uma matriz JSON que inclui um objeto para cada modelo customizado pertencente ao solicitante. As credenciais de serviço do proprietário são mostradas no campo `owner`.

```javascript
{
  "customizations": [
    {
      "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T19:15:17.926Z",
      "name": "curl Test",
      "language": "en-US",
      "description": "Customization test via curl",
      "last_modified": "2016-07-15T19:15:17.926Z"
    },
    {
      "customization_id": "63f5807f-a4f2-5766-914e-7abb1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T18:12:31.743Z",
      "name": "curl Test Two",
      "language": "en-US",
      "description": "Second customization test via curl",
      "last_modified": "2016-07-15T18:23:50.912Z"
    }
  ]
}
```
{: codeblock}

Os horários `created` e `last_modified` para o primeiro modelo são iguais porque ele ainda precisa ser atualizado. Os horários para o segundo modelo são diferentes, indicando que ele foi modificado desde sua criação inicial. As informações não incluem as entradas customizadas que foram definidas para os modelos.

## Atualizando um modelo customizado
{: #cuModelsUpdate}

Para atualizar informações sobre um modelo customizado, use o método `POST /v1/customizations/{customization_id}`. Você especifica as atualizações como um objeto JSON. Além de modificar seu nome e descrição, também é possível usar esse método para incluir ou atualizar pares de palavra/tradução no modelo. Não é possível mudar o idioma de um modelo quando ele é criado.

O exemplo a seguir atualiza o nome e a descrição de um modelo customizado. Uma matriz JSON vazia é enviada com o parâmetro `words` para indicar que as entradas do modelo devem permanecer sem mudanças.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test Update\", \"description\":\"Customization test update via curl\", \"words\":[]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

Para obter informações sobre como atualizar as palavras em um modelo, consulte [Incluindo diversas palavras em um modelo customizado](/docs/services/text-to-speech/custom-entries.html#cuWordsAdd).

## Excluindo um modelo customizado
{: #cuModelsDelete}

Para descartar um modelo customizado que não é mais necessário, use o método `DELETE /v1/customizations/{customization_id}`. Use esse método somente se tiver certeza de que não precisa mais do modelo, pois a exclusão é permanente.

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}
