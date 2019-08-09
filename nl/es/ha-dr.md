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

# Alta disponibilidad y recuperación tras desastre
{: #ha-dr}

El servicio de {{site.data.keyword.texttospeechfull}} está altamente disponible dentro de cualquier ubicación {{site.data.keyword.cloud_notm}} (por ejemplo, Dallas o Washington, DC). No obstante, la recuperación de desastres potenciales que afecten a toda una ubicación requiere planificación y preparación.
{: shortdesc}

Usted es responsable de comprender la configuración, personalización y uso del servicio. También es responsable de estar preparado para volver a crear una instancia del servicio en una nueva ubicación y de restaurar los datos en cualquier ubicación.

## Alta disponibilidad
{: #high-availability}

El servicio {{site.data.keyword.texttospeechshort}} admite la alta disponibilidad sin un solo punto de anomalía. El servicio consigue una alta disponibilidad de forma automática y transparente mediante la característica de región multizona (MZR) proporcionada por {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloud_notm}} habilita varias zonas que no comparten un único punto de anomalía dentro de una única ubicación. También proporciona equilibrio de carga automático entre las zonas dentro de una región.

## Recuperación tras desastre
{: #disaster-recovery}

La recuperación tras desastre puede convertirse en un problema si una ubicación de {{site.data.keyword.cloud_notm}} sufre un fallo significativo que incluye la pérdida potencial de datos. Debido a que MZR no está disponible en las ubicaciones, debe esperar a que {{site.data.keyword.IBM_notm}} vuelva a poner una ubicación en línea si no está disponible. Si los servicios de datos subyacentes se ven afectados por el fallo, también debe esperar a que {{site.data.keyword.IBM_notm}} restaure estos servicios de datos.

En el caso de que se produzca un error catastrófico, puede que {{site.data.keyword.IBM_notm}} no pueda recuperar los datos de las copias de seguridad de bases de datos. En tal caso, deberá que restaurar los datos para devolver la instancia de servicio a su estado más reciente. Puede restaurar los datos a la misma ubicación o a una ubicación distinta.

Para el servicio {{site.data.keyword.texttospeechshort}}, sólo se almacenan los datos de los modelos de voz personalizados en {{site.data.keyword.cloud_notm}}. El plan de recuperación tras desastre incluye el conocimiento, la conservación y la preparación para restaurar los modelos de voz personalizados.

### Copia de seguridad de modelos de voz personalizados
{: #disaster-recovery-backup}

Conserve la siguiente información sobre los modelos de voz personalizados y sus entradas personalizadas:

-   Una lista de todos los modelos de voz personalizados y sus definiciones. Para listar la información sobre los modelos personalizados:
    -   Utilice el método `GET /v1/customizations` para listar la información sobre todos los modelos personalizados. Para obtener más información, consulte [Consulta de todos los modelos personalizados](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQueryAll).
    -   Utilice el método `GET /v1/customizations/{customization_id}` para listar información sobre un modelo personalizado especificado. Para obtener más información, consulte [Consulta de un modelo personalizado](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery).
-   Información sobre todas las entradas personalizadas (pares de palabra/conversión) en los modelos de voz personalizados:
    -   Utilice el método `GET /v1/customizations/{customization_id}/words` para listar información sobre todos los pares de palabra/conversión de un modelo personalizado. Para obtener más información, consulte [Consulta de todas las palabras de un modelo personalizado](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryModel).
    -   Utilice el método `GET /v1/customizations/{customization_id}/words/{word}` para listar información sobre un par de palabra/conversión especificado de un modelo personalizado. Para obtener más información, consulte [Consulta de una palabra de un modelo personalizado](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordQueryModel).

Una práctica recomendada consiste en conservar esta información en un formato que se puede utilizar para volver a crear los modelos de voz personalizados en caso de que se produzca un error. Realizar de forma activa un mantenimiento de la información sobre los modelos personalizados y las entradas personalizadas, y preparar de forma anticipada las llamadas que se listan en la siguiente sección, puede permitirle recuperar la información lo más rápido posible.

### Restauración de modelos de voz personalizados
{: #disaster-recovery-restore}

Si tiene que recuperarse de un desastre, puede utilizar la información de copia de seguridad para volver a crear los modelos de voz personalizados y sus entradas personalizadas:

1.  Para volver a crear los modelos de voz personalizados, utilice el método `POST /v1/customizations`. Para obtener más información, consulte [Creación de un modelo personalizado](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsCreate).
1.  Para añadir varios pares de palabra/conversión a los modelos de voz personalizados, utilice el método `POST /v1/customizations/{customization_id}/words`. Para obtener más información, consulte [Añadir varias palabras a un modelo personalizado](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsAdd).
1.  Para añadir un par de palabra/conversión individuales a los modelos de voz personalizados, utilice el método `POST /v1/customizations/{customization_id}/words/{word}`. Para obtener más información, consulte [Añadir una palabra a un modelo personalizado](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordAdd).

Puede añadir todas las entradas personalizadas a la vez, en grupos, o de una en una.
