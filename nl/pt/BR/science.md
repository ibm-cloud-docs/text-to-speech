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

# A ciência por trás do serviço
{: #science}

O serviço {{site.data.keyword.texttospeechshort}} é um sistema concatenativo que conta com um inventário de unidades acústicas de um grande corpus de síntese para produzir discurso de saída para texto de entrada arbitrário. Ele é baseado no pipeline de processos a seguir. Esses processos facilitam uma procura eficiente em tempo real sobre esse inventário de unidades seguidas por um pós-processamento de unidades.
{: shortdesc}

-   **Modelo acústico** - Esse modelo consiste em uma árvore de decisão responsável por gerar as unidades candidatas para a procura. Para cada fonema em uma sequência de fonemas a serem sintetizados, o modelo o considera no contexto do anterior e do seguinte. Em seguida, ele produz um conjunto de unidades acústicas que a procura avalia em busca de adequação. Essa etapa reduz efetivamente a complexidade da procura, restringindo-a apenas àquelas unidades que atendem a alguns critérios contextuais e descartando todas as outras.
-   **Modelos de destino de prosódia** - Esses modelos consistem em Deep Recurrent Neural Networks (RNNs). Os modelos são responsáveis por gerar valores de destino para aspectos prosódicos do discurso (como duração e entonação), dada uma sequência de recursos linguísticos extraídos do texto de entrada. Essa lista inclui atributos como parte do discurso, acento lexical, proeminência de nível de palavra e recursos posicionais (por exemplo, a posição da sílaba ou palavra na sentença). Os modelos de destino de prosódia ajudam a orientar a procura por aquelas unidades que atendem aos critérios prosódicos previstos por esse modelo.
-   **Procurar** - Dada a lista de candidatos retornada pelo modelo acústico e a prosódia de destino, esse módulo executa uma procura do Viterbi. A procura extrai uma sequência de unidades acústicas que minimiza uma função de custo e que considera os custos de concatenação e de destino. Como resultado, os artefatos audíveis da junção de duas unidades são minimizados e o módulo tenta aproximar a prosódia de destino sugerida pelos modelos de destino de prosódia. Essa procura também favorece chunks contíguos no corpus de síntese para reduzir ainda mais tais artefatos.
-   **Geração de Waveform**-Quando a procura retorna a sequência ideal de unidades, o sistema usa Pitch Síncrono Sobreposição e Inclusão (PSOLA) de tempo de tempo para gerar a forma de saída de saída. PSOLA é uma técnica de processamento de sinalização digital que é usada para processamento de fala. Especificamente, ela é usada para a síntese de discurso. Ela pode modificar o tom e a duração de um sinal de discurso e misturar as unidades retornadas pela procura de maneira contínua.

    Para todos os recursos linguísticos nos processos de back-end anteriores, o serviço usa um front-end de processamento de texto para analisar o texto antes de sintetizá-lo em forma de áudio. O front-end limpa o texto de qualquer artefato de formatação, como tags HTML. Em seguida, usa uma linguagem proprietária acionada por regras linguísticas dependentes do idioma para preparar o texto e gerar pronúncias. Esse módulo normaliza os recursos dependentes de idioma do texto, como datas, horários, números e moeda. Por exemplo, executa a expansão de abreviação de um dicionário e a expansão numérica de regras para ordinais e cardinais.

    Algumas palavras têm diversas pronúncias permitidas, portanto, o front-end de processamento de texto primeiro produz uma pronúncia única e canônica no tempo de execução. Essa abordagem pode não refletir a pronúncia que o falante usou quando o corpus de áudio foi registrado. Portanto, o serviço aumenta um conjunto candidato de pronúncias com formatos alternativos que são colocados em forma de inventário em um dicionário de formato base alternativo. Ele permite que a procura escolha os formatos que reduzem o custo em termos de tom, duração, preocupações e restrições de contiguidade. Esse algoritmo facilita a seleção de chunks contíguos mais longos do conjunto de dados, resultando em um fluxo ideal de fala no resultado sintetizado.

O tópico de sintetizar texto para discurso é inerentemente complexo, e qualquer explicação do serviço requer mais profundidade de explicação do que este breve resumo pode acomodar. Para obter mais informações sobre a pesquisa científica por trás do serviço, consulte os documentos listados em [Referências de pesquisa](/docs/services/text-to-speech/references.html).
