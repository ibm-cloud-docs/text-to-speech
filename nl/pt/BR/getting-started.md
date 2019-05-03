---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-14"

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# Tutorial de introdução
{: #gettingStarted}

O serviço {{site.data.keyword.texttospeechfull}} converte o texto escrito em discurso semelhante ao natural para fornecer recursos de síntese de discurso para aplicativos. Esse tutorial baseado em curl pode ajudá-lo a começar rapidamente a usar o serviço. Os exemplos mostram como chamar os métodos `POST` e `GET /v1/synthesize` do serviço para solicitar um fluxo de áudio.
{: shortdesc}

O tutorial usa as chaves de API do {{site.data.keyword.cloud}} Identity and Access Management (IAM) para a autenticação. As instâncias de serviço mais antigas podem continuar usando o `{username}` e o `{password}` de suas credenciais de serviço existentes do Cloud Foundry para a autenticação. Autentique-se usando a abordagem ideal para sua instância de serviço. Para obter mais informações sobre o uso da autenticação do IAM pelo serviço, consulte a [Atualização de serviço de 30 de outubro de 2018](/docs/services/text-to-speech/release-notes.html#October2018) nas notas sobre a liberação.
{: important}

## Antes de começar
{: #before-you-begin}

- {: hide-dashboard}  Crie uma instância do serviço:
    1.  {: hide-dashboard} Acesse a página [{{site.data.keyword.texttospeechshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/text-to-speech){: new_window} no {{site.data.keyword.cloud_notm}} Catalog.
    1.  {: hide-dashboard} Inscreva-se para obter uma conta gratuita do {{site.data.keyword.cloud_notm}} ou efetue login.
    1.  {: hide-dashboard} Clique em **Criar**.
-   Copie as credenciais para autenticar sua instância de serviço:
    1.  {: hide-dashboard} No painel do [{{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/dashboard/apps){: new_window}, clique em sua instância de serviço do {{site.data.keyword.texttospeechshort}} para acessar a página do painel do serviço {{site.data.keyword.texttospeechshort}}.
    1.  Na página **Gerenciar**, clique em **Mostrar** para visualizar suas credenciais.
    1.  Copie os valores de `API Key` e `URL`.
-   Certifique-se de que você tenha o comando `curl`.
    -   Os exemplos usam o comando `curl` para chamar métodos da interface HTTP. Instale a versão para o seu sistema operacional por meio de [curl.haxx.se ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://curl.haxx.se/){: new_window}. Instale a versão que suporta o protocolo Secure Sockets Layer (SSL). Certifique-se de incluir o arquivo binário instalado em sua variável de ambiente `PATH`.

Ao inserir um comando, substitua `{apikey}` e `{url}` por sua URL e chave de API reais. Omita as chaves, que indicam um valor de variável, do comando. Um valor real é semelhante ao exemplo a seguir:
{: hide-dashboard}

```bash
curl -X POST -u "apikey :L_HALhLVIksh1b73l97LSs6R_3gLo4xkujAaxm7i-b9x"
. . .
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```
{:pre}
{: hide-dashboard}

É possível usar um navegador ou outras ferramentas para reproduzir os arquivos de áudio produzidos pelos exemplos nesse tutorial. Para obter mais informações, consulte [Reproduzindo um arquivo de áudio](/docs/services/text-to-speech/audio-formats.html#formatsPlay).
{: note}

## Etapa 1: sintetizar textos em inglês americano
{: #synthesizeEnglish}

Os comandos a seguir usam o método `POST /v1/synthesize` para sintetizar a entrada em inglês americano para arquivos de áudio em dois formatos diferentes. Ambas as solicitações usam a voz padrão em inglês americano, `en-US_MichaelVoice`.

1.  Emita o comando a seguir para sintetizar a sequência "hello world" e produzir um arquivo WAV denominado `hello_world.wav`.
    -   {: hide-dashboard} Substitua `{apikey}` e `{url}` por sua URL e chave de API.

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

1.  Emita o comando a seguir para sintetizar o mesmo texto, mas produzir um arquivo Ogg (o formato padrão) denominado `hello_world.ogg`.
    -   {: hide-dashboard} Substitua `{apikey}` e `{url}` por sua URL e chave de API.

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

## Etapa 2: sintetizar textos em espanhol
{: #synthesizeSpanish}

O comando a seguir usa o método `GET /v1/synthesize` para sintetizar uma entrada em espanhol para um arquivo de áudio.

1.  Emita o comando a seguir para sintetizar a sequência "hola mundo" e produzir um arquivo WAV denominado `hola_mundo.wav`. O texto de entrada é codificado com URL. O método inclui os parâmetros de consulta `accept`para especificar o formato de áudio e a `voz`para especificar uma voz espanhola, `es-ES_EnriqueVoice`.
    -   {: hide-dashboard} Substitua `{apikey}` e `{url}` por sua URL e chave de API.

    ```bash
    curl -X GET -u "apikey:{apikey}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## Próximas etapas

-   Saiba mais sobre a interface HTTP do serviço em [A interface HTTP](/docs/services/text-to-speech/http.html).
-   Saiba mais sobre a interface WebSocket do serviço em [A interface WebSocket](/docs/services/text-to-speech/websockets.html).
-   Obtenha informações detalhadas sobre os métodos da interface do serviço na [Referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/text-to-speech){: new_window}.
