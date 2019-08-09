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

# Creación y gestión de modelos de voz personalizados
{: #customModels}

El primer paso para trabajar con cualquier modelo personalizado es crearlo. Una vez que existe, puede gestionar el modelo consultando o actualizando sus metadatos y entradas, y suprimirlo si ya no se necesita. Antes de empezar, revise la siguiente información de uso general sobre modelos personalizados.
{: shortdesc}

## Notas de uso
{: #customGuidelines}

Tenga en cuenta las siguientes directrices al trabajar con la interfaz de personalización.

### Propiedad de los modelos de voz personalizados
{: #customOwner}

Un modelo de voz personalizado es propiedad de la instancia del servicio {{site.data.keyword.texttospeechshort}} cuyas credenciales se han utilizado para crearlo. Debe utilizar las credenciales para dicha instancia de servicio con los métodos de la interfaz de personalización para cualquier trabajo que realice con el modelo personalizado.

Todas las credenciales obtenidas para la misma instancia del servicio {{site.data.keyword.texttospeechshort}} comparten el acceso a todos los modelos personalizados creados para esa instancia de servicio. Para restringir el acceso a un modelo personalizado, cree una instancia de servicio aparte y utilice únicamente las credenciales de esa instancia de servicio para crear y trabajar con el modelo. Las credenciales de otras instancias de servicio no pueden afectar al modelo personalizado.

Una ventaja de compartir la propiedad entre las credenciales es que se puede cancelar un conjunto de credenciales, por ejemplo, si están en riesgo. A continuación, puede crear nuevas credenciales para la misma instancia de servicio y seguir manteniendo la propiedad y el acceso a los modelos personalizados creados con las credenciales originales.

### Registro de solicitudes y privacidad de datos
{: #customLogging}

La forma en que el servicio maneja el registro de solicitudes para las llamadas a la interfaz de personalización depende de la solicitud:

-   El servicio *no* registra los datos (palabras y conversiones) que se utilizan para crear modelos de voz personalizados. No es necesario que defina la cabecera de la solicitud `X-Watson-Learning-Opt-Out` cuando utilice la interfaz de personalización para gestionar las palabras y las conversiones en un modelo personalizado. Los datos de entrenamiento nunca se utilizan para mejorar los modelos base del servicio.
-   El servicio *si* registra los datos cuando se utiliza un modelo personalizado con una solicitud de síntesis. Debe establecer la cabecera de solicitud `X-Watson-Learning-Opt-Out` a `true` para evitar que se registren las solicitudes de síntesis.

Para obtener más información, consulte [Control del registro de solicitud para servicios de {{site.data.keyword.watson}}](/docs/services/watson?topic=watson-gs-logging-overview).

### Seguridad de la información
{: #customSecurity}

El servicio le permite asociar un ID de cliente con los datos que se añaden o actualizan para los modelos de voz personalizados. Puede asociar un ID de cliente a palabras personalizadas pasando la cabecera `X-Watson-Metadata` con los métodos siguientes:

-   `POST /v1/customizations/{customization_id}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word}`

Si es necesario, después puede suprimir los datos asociados al ID de cliente utilizando el método `DELETE /v1/user_data`. Para obtener más información, consulte [Seguridad de la información](/docs/services/text-to-speech?topic=text-to-speech-information-security).

## Crear un modelo personalizado
{: #cuModelsCreate}

Para crear un modelo personalizado nuevo, utilice el método `POST /v1/customizations`. Un modelo nuevo siempre está vacío en el momento en que se crea. Se deben utilizar otros métodos para llenarlo con pares de palabra/conversión. El nuevo modelo personalizado es propiedad de la instancia de servicio cuyas credenciales se han utilizado para crearlo. Para obtener más información, consulte [Propiedad de los modelos de voz personalizados](#customOwner).

Se pasan los atributos siguientes como un objeto JSON con el cuerpo de la solicitud.

<table>
  <caption>Tabla 1. Parámetros del método <code>POST /v1/customizations</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parámetro</th>
    <th style="text-align:center; width:12%">Tipo de datos</th>
    <th style="text-align:left">Descripción</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>Obligatorio</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      Un nombre definido por el usuario para el nuevo modelo personalizado. El nombre se utiliza para etiquetar el modelo y así poder identificarlo fácilmente. El nombre debe ser exclusivo entre todos los modelos personalizados de los que sea propietario.
    </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      Un identificador del idioma del modelo personalizado. El valor predeterminado es <code>en-US</code> para inglés de Estados Unidos. El modelo personalizado se puede utilizar con cualquier voz, estándar o neuronal, que esté disponible en el idioma especificado.
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      Una descripción del nuevo modelo. Aunque es opcional, se recomienda especificar una descripción.
    </td>
  </tr>
</table>

El siguiente mandato `curl` de ejemplo crea un nuevo modelo personalizado denominado `curl Test`. La cabecera `Content-Type` identifica el tipo de entrada como `application/json`.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test\", \"language\":\"en-US\", \"description\":\"Customization test via curl\"}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

El método devuelve un objeto JSON que contiene un identificador exclusivo global (GUID) para el nuevo modelo. El GUID se utiliza como el parámetro `customization_id` en las llamadas para acceder al modelo, como por ejemplo, para consultar, modificar y utilizar el modelo y sus palabras.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

## Consultar un modelo personalizado
{: #cuModelsQuery}

Para consultar información sobre un modelo personalizado existente, utilice el método `GET /v1/customizations/{customization_id}`. Esta es la forma más directa de ver toda la información sobre un modelo, tanto sus metadatos como los pares de palabra/conversión que contiene.

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

El método devuelve sus resultados como un objeto JSON con el formato siguiente:

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

Además de la información especificada al crear el modelo, la salida incluye las credenciales del propietario del modelo, el idioma del modelo y las horas en las que se creó el modelo y se modificó por última vez. Dado que el modelo no se ha modificado desde su creación, en el ejemplo las dos horas son la misma.

La salida también incluye una matriz `words` que enumera las entradas personalizadas del modelo. Dado que el modelo todavía no se ha actualizado, en el ejemplo la matriz está vacía.

## Consultar todos los modelos personalizados
{: #cuModelsQueryAll}

Para ver información sobre todos los modelos personalizados de los que es propietario, utilice el método `GET /v1/customizations`:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

El método devuelve una matriz JSON que incluye un objeto para cada modelo personalizado propiedad del solicitante. En el campo `owner` se muestran las credenciales del propietario.

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

Las horas de `created` y `last_modified` del primer modelo son la misma porque todavía no se ha actualizado. En el segundo modelo las horas son distintas, lo que indica que se ha modificado desde su creación. La información no incluye las entradas personalizadas definidas para los modelos.

## Actualizar un modelo personalizado
{: #cuModelsUpdate}

Para actualizar la información sobre un modelo personalizado, utilice el método `POST /v1/customizations/{customization_id}`. Debe especificar las actualizaciones como un objeto JSON. Además de modificar el nombre y la descripción, también puede utilizar este método para añadir o actualizar pares de palabra/conversión en el modelo. No se puede cambiar el idioma de un modelo una vez que se ha creado.

En el ejemplo siguiente se actualiza el nombre y la descripción de un modelo personalizado. Se envía una matriz JSON vacía con el parámetro `words` para indicar que las entradas del modelo se mantienen sin cambios.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test Update\", \"description\":\"Customization test update via curl\", \"words\":[]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

Para obtener información sobre cómo actualizar las palabras de un modelo, consulte [Añadir varias palabras a un modelo personalizado](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsAdd).

## Suprimir un modelo personalizado
{: #cuModelsDelete}

Para descartar un modelo personalizado que ya no se necesita, utilice el método `DELETE /v1/customizations/{customization_id}`. Utilice este método sólo si está seguro de que ya no necesita el modelo, ya que la supresión es permanente.

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}
