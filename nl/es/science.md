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

# La ciencia detrás del servicio
{: #science}

El servicio {{site.data.keyword.texttospeechshort}} es un sistema de concatenación basado en un inventario de unidades acústicas de un corpus de síntesis grande para producir un discurso de salida para un texto de entrada arbitrario. Se basa en el siguiente conducto de procesos. Estos procesos facilitan una búsqueda eficiente y en tiempo real sobre este inventario de unidades seguida de un post-procesamiento de las unidades.
{: shortdesc}

-   **Modelo acústico** - Este modelo consiste en un árbol de decisiones que es el responsable de generar unidades candidatas para la búsqueda. Para cada uno de los teléfonos de una secuencia de teléfonos a sintetizar, el modelo considera el teléfono en el contexto de los dos teléfonos anteriores y posteriores. A continuación, produce un conjunto de unidades acústicas de las que la búsqueda evalúa su adecuación. Este paso reduce de forma efectiva la complejidad de la búsqueda restringiéndola a sólo aquellas unidades que cumplen algunos criterios contextuales y descartando todas las demás.
-   **Modelos de destino de prosodia** - Estos modelos consisten en redes Deep Recurrent Neural Networks (RNN). Los modelos son responsables de generar valores de destino para los aspectos prosódicos del habla (como por ejemplo la duración y la entonación) dada una secuencia de características lingüísticas que se extraen del texto de entrada. Esta lista incluye atributos como, por ejemplo, categoría léxica, acento léxico, prominencia a nivel de palabra y características de posición (por ejemplo, la posición de la sílaba o la palabra en la frase). Los modelos de destino de prosodia ayudan a guiar la búsqueda hacia aquellas unidades que cumplen los criterios prosódicos que se predicen mediante este modelo.
-   **Búsqueda** - Dada una lista de los candidatos que devuelve el modelo acústico y la prosodia de destino, este módulo realiza una búsqueda Viterbi. Esta búsqueda extrae una secuencia de unidades acústicas que minimiza una función de coste que tiene en cuenta los costes de concatenación y de destino. Como resultado, los artefactos audibles de la unión de dos unidades se minimizan, y el módulo trata de aproximarse la prosodia de destino sugerida por los modelos de destino de prosodia. Esta búsqueda también favorece los fragmentos contiguos en el corpus de síntesis para reducir más estos artefactos.
-   **Generación de onda** - Cuando la búsqueda devuelve la secuencia óptima de unidades, el sistema utiliza PSOLA (Pitch Synchronous Overlap and Add) para generar la onda de salida. PSOLA es una técnica de proceso de procesamiento de señales que se utiliza para el procesamiento del habla. Específicamente, se utiliza para la síntesis del habla. Puede modificar el paso y la duración de una señal de habla y mezclar las unidades que devuelve la búsqueda sin interrupciones.

    Para todas las características lingüísticas de los procesos de fondo anteriores, el servicio utiliza un programa frontal de procesamiento de texto para analizar el texto antes de sintetizarlo en formato de audio. El programa frontal limpia el texto de artefactos de formateo como por ejemplo etiquetas HTML. A continuación, utiliza un lenguaje registrado dirigido por reglas lingüísticas dependientes del idioma para preparar el texto y generar pronunciaciones. Este módulo normaliza las características del texto que dependen del idioma, como por ejemplo fechas, horas, números y moneda. Por ejemplo, realiza una expansión de abreviaturas a partir de un diccionario y una expansión numérica a partir de reglas para ordinales y cardinales.

    Algunas palabras tienen múltiples pronunciaciones permisibles, por lo que el programa frontal de procesamiento de texto produce una única pronunciación canónica en tiempo de ejecución. Puede ocurrir que este enfoque no refleje la pronunciación que utilizó el hablante cuando se grabó el corpus de audio. Así pues, el servicio aumenta un conjunto de pronunciaciones candidatas con formas alternativas que se inventarían en un diccionario de formas base alternativas. Permite a la búsqueda elegir formas que reduzcan el coste en términos de tono, duración y problemas y restricciones de contigüidad. Este algoritmo facilita la selección de fragmentos contiguos más largos del conjunto de datos, dando como resultado un flujo óptimo de habla en el resultado sintetizado.

El tema de sintetizar el texto a voz es inherentemente complejo, y cualquier explicación del servicio requiere más profundidad explicativa de lo que este breve resumen puede dar. Para obtener más información sobre la investigación científica detrás del servicio, consulte los documentos que aparecen en [Referencias de investigación](/docs/services/text-to-speech/references.html).
