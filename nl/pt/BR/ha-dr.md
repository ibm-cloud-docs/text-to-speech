---

copyright:
  years: 2019
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

# Alta disponibilidade e recuperação de desastre
{: #ha-dr}

O serviço {{site.data.keyword.texttospeechfull}} está altamente disponível em qualquer local do {{site.data.keyword.cloud_notm}} (por exemplo, Dallas ou Washington, DC). No entanto, a recuperação de possíveis desastres que afetam todo um local requer planejamento e preparação.
{: shortdesc}

Você é responsável por entender sua configuração, customização e uso do serviço. Você também é responsável por estar pronto para recriar uma instância do serviço em um novo local e restaurar seus dados onde quer que seja.

## Alta disponibilidade
{: #high-availability}

O serviço {{site.data.keyword.texttospeechshort}} suporta a alta disponibilidade sem nenhum ponto único de falha. O serviço obtém a alta disponibilidade de forma automática e transparente por meio do recurso de região de diversas zonas (MZR) fornecido pelo {{site.data.keyword.cloud_notm}}.

O {{site.data.keyword.cloud_notm}} permite diversas zonas que não compartilham um ponto único de falha em um único local. Também fornece o balanceamento automático de carga entre as zonas dentro de uma região.

## Recuperação de desastre
{: #disaster-recovery}

A recuperação de desastre pode se tornar um problema se um local do {{site.data.keyword.cloud_notm}} passar por uma falha significativa que inclua a possível perda de dados. Como o MZR não está disponível nos locais, caso um local fique indisponível, deve-se aguardar até que o {{site.data.keyword.IBM_notm}} retorne-o para o estado on-line. Se os serviços de dados subjacentes forem comprometidos pela falha, deve-se também aguardar até que o {{site.data.keyword.IBM_notm}} os restaure.

No caso de uma falha catastrófica, o {{site.data.keyword.IBM_notm}} pode não ser capaz de recuperar dados de backups de banco de dados. Nesse caso, é necessário restaurar seus dados para retornar sua instância de serviço para seu estado mais recente. É possível restaurar os dados para o mesmo local ou para um local diferente.

Para o serviço {{site.data.keyword.texttospeechshort}}, apenas os dados para modelos de voz customizados são armazenados no {{site.data.keyword.cloud_notm}}. Seu plano de recuperação de desastre inclui saber, preservar e estar preparado para restaurar seus modelos de voz customizados.

### Fazendo backup de modelos de voz customizados
{: #disaster-recovery-backup}

Preserve as informações a seguir sobre seus modelos de voz e entradas customizados:

-   Uma lista de todos os seus modelos de voz customizados e suas definições. Para listar informações sobre seus modelos customizados:
    -   Use o método `GET /v1/customizations` para listar informações sobre todos os modelos customizados. Para obter mais informações, consulte [Consultando todos os modelos customizados](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQueryAll).
    -   Use o método `GET /v1/customizations/{customization_id}` para listar informações sobre um modelo customizado especificado. Para obter mais informações, consulte [Consultando um modelo customizado](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery).
-   Informações sobre todas as entradas customizadas (pares de palavra/tradução) em seus modelos de voz customizados:
    -   Use o método `GET /v1/customizations/{customization_id}/words` para listar informações sobre todos os pares de palavra/tradução de um modelo customizado. Para obter mais informações, consulte [Consultando todas as palavras de um modelo customizado](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryModel).
    -   Use o método `GET /v1/customizations/{customization_id}/words/{word}` para listar informações sobre um par de palavra/tradução especificado de um modelo customizado. Para obter mais informações, consulte [Consultando uma única palavra de um modelo customizado](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordQueryModel).

Uma melhor prática é preservar essas informações em um formato que possa ser usado para recriar seus modelos de voz customizados no caso de uma falha. Manter ativamente as informações sobre seus modelos e entradas customizados e preparar antecipadamente as chamadas listadas na seção a seguir pode permitir a recuperação o mais rápido possível.

### Restaurando Modelos de Voz Customizados
{: #disaster-recovery-restore}

Se precisar se recuperar de um desastre, será possível usar as informações de backup para recriar seus modelos de voz e entradas customizados:

1.  Para recriar seus modelos de voz customizados, use o método `POST /v1/customizations`. Para obter mais informações, consulte [Criando um modelo customizado](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsCreate).
1.  Para incluir diversos pares de palavra/tradução em seus modelos de voz customizados, use o método `POST /v1/customizations/{customization_id}/words`. Para obter mais informações, consulte [Incluindo diversas palavras em um modelo customizado](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsAdd).
1.  Para incluir um par de palavra/tradução único em seus modelos de voz customizados, use o método `POST /v1/customizations/{customization_id}/words/{word}`. Para obter mais informações, consulte [Incluindo uma única palavra em um modelo customizado](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordAdd).

Todas as suas entradas customizadas podem ser incluídas de uma vez, em grupos ou individualmente.
