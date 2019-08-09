---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-04"

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

# Segurança de Informações
{: #information-security}

A {{site.data.keyword.IBM}} está comprometida em fornecer aos nossos clientes e parceiros as soluções inovadoras de privacidade de dados, segurança e controle.
{: shortdesc}

Os clientes são responsáveis por garantir sua própria conformidade com diversas leis e regulamentações, incluindo o Regulamento Geral sobre a Proteção de Dados da União Europeia. Os clientes são os únicos responsáveis por obter conselhos de aconselhamento jurídico competente quanto à identificação e interpretação de quaisquer leis e regulamentos relevantes que possam afetar os negócios dos clientes e quaisquer ações que os clientes possam precisar tomar para cumprir tais leis e regulamentos.
{: important}

Os produtos, serviços e outros recursos descritos neste documento não são adequados para todas as situações do cliente e podem ter disponibilidade restrita. A {{site.data.keyword.IBM_notm}} não fornece aconselhamento jurídico, de contabilidade ou de auditoria e nem representa ou garante que seus serviços ou produtos garantirão que os clientes estejam em conformidade com qualquer lei ou regulamentação.

Se precisar solicitar o suporte ao GDPR para recursos do {{site.data.keyword.cloud}}{{site.data.keyword.watson}} que são criados

-   Na União Europeia (UE), consulte [Solicitando o suporte para recursos do {{site.data.keyword.cloud_notm}} Watson criados na União Europeia](/docs/services/watson?topic=watson-gdpr-sar#request-EU).
-   Fora da UE, consulte [Solicitando o suporte para recursos fora da União Europeia](/docs/services/watson?topic=watson-gdpr-sar#request-non-EU).

## Regulamento Geral sobre a Proteção de Dados (GDPR) da União Europeia
{: #gdpr}

A {{site.data.keyword.IBM_notm}} está comprometida em fornecer aos nossos clientes e parceiros as soluções inovadoras de privacidade de dados, segurança e controle para auxiliá-los em sua jornada para a conformidade com o GDPR.

Saiba mais sobre a jornada de preparação para o GDPR da própria {{site.data.keyword.IBM_notm}} e sobre nossos recursos e ofertas do GDPR para suportar sua jornada de conformidade [aqui](http://www.ibm.com/gdpr){: external}.

## Rotulando e excluindo dados no serviço Text to Speech
{: #gdpr-text-to-speech}

O serviço {{site.data.keyword.texttospeechfull}} permite excluir todos os dados associados a solicitações de síntese de discurso e a modelos de voz customizados. Para excluir dados, é necessário fazer o seguinte:

1.  Use o cabeçalho `X-Watson-Metadata` para associar um ID do cliente aos dados que serão transmitidos por uma solicitação ao serviço e, para isso, consulte [Especificando um ID do cliente](#specify-customer-id).
1.  Use o método `DELETE /v1/user_data` para excluir todos os dados associados a um ID de cliente especificado e, para isso, consulte [Excluindo dados](#delete-pi).

Por padrão, nenhum ID do cliente está associado aos dados.

Os recursos experimentais e beta não são destinados para uso com um ambiente de produção e, portanto, não são garantidos para funcionar conforme o esperado ao rotular e excluir dados. Os recursos experimentais e beta não devem ser usados ao implementar uma solução que requer a rotulagem e a exclusão de dados.
{: note}

### Especificando um ID do cliente
{: #specify-customer-id}

Para associar um ID do cliente aos dados, inclua o cabeçalho `X-Watson-Metadata` na solicitação que transmite as informações. Você transmite a sequência `customer_id={id}` como o argumento do cabeçalho. O exemplo a seguir associa o ID do cliente `my_ID` aos dados transmitidos com uma solicitação `POST /v1/synthesize`:

```bash
curl -X POST -u "apikey:{apikey}"
--header "X-Watson-Metadata: customer_id=my_ID"
--header "Content-Type: application/json"
--header "Accept: audio/wav"
--data "{\"text\":\"hello world\"}"
--output hello_world.wav
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```

Um ID do cliente pode incluir quaisquer caracteres, exceto o `;` (ponto e vírgula) e o `=` (sinal de igual). Especifique uma sequência aleatória ou genérica para o ID do cliente e não especifique uma sequência pessoal identificável, como um endereço de e-mail ou um ID do Twitter. É possível especificar diferentes IDs do cliente com solicitações diferentes. Um ID do cliente especificado será associado à instância do serviço cujas credenciais são usadas com a solicitação e somente credenciais para essa instância do serviço podem excluir dados associados ao ID.

Use o cabeçalho `X-Watson-Metadata` com os métodos a seguir:

-   Com solicitações de HTTP:
    -   `POST /v1/synthesize`
    -   `GET /v1/synthesize`

    O ID do cliente está associado aos dados enviados com a solicitação.

-   Com solicitações WebSocket:
    -   `/v1/synthesize`

    Você especifica o ID do cliente com o parâmetro de consulta `x-watson-metadata` para associar o ID aos dados enviados com a solicitação. Deve-se codificar com URL o argumento para o parâmetro de consulta, por exemplo, `customer_id%3dmy_ID`.

-   Com solicitações para incluir palavras customizadas em modelos de voz customizados:
    -   `POST /v1/customizations/{customization_id}`
    -   `POST /v1/customizations/{customization_id}/words`
    -   `PUT /v1/customizations/{customization_id}/words/{word}`

    O ID do cliente está associado às palavras customizadas incluídas ou atualizadas pela solicitação.

### Excluindo dados
{: #delete-pi}

Para excluir todos os dados associados a um ID do cliente, use o método `DELETE /v1/user_data`. Você passa a sequência `customer_id={id}` como um parâmetro de consulta com a solicitação. O exemplo a seguir exclui todos os dados do ID do cliente `my_ID`:

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/user_data?customer_id=my_ID"
```

O método `/v1/user_data`exclui todos os dados que estão associados com o ID do cliente especificado, independentemente do método pelo qual as informações foram incluídas. O método não terá efeito se nenhum dado estiver associado ao ID de cliente. Deve-se emitir a solicitação com as credenciais para a mesma instância de serviço usada para associar o ID do cliente aos dados.
