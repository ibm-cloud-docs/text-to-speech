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

# Seguridad de la información
{: #information-security}

{{site.data.keyword.IBM}} se compromete a proporcionar a nuestros clientes y socios soluciones innovadoras de privacidad de datos, seguridad y gobierno.
{: shortdesc}

Los clientes son responsables de garantizar el cumplimiento de las leyes y normativas aplicables, incluyendo el Reglamento general de protección de datos de la Unión Europea. Los clientes son los únicos responsables de obtener asesoramiento de un asesor jurídico competente en cuanto a la identificación e interpretación de las leyes y reglamentos pertinentes que puedan afectar a los negocios de los clientes y a cualquier medida que los clientes puedan necesitar para cumplir con esas leyes y reglamentos.
{: important}

Los productos, los servicios y otras prestaciones que se describen en el presente documento no son adecuados para todos los casos de cliente y pueden tener una disponibilidad restringida. {{site.data.keyword.IBM_notm}} no proporciona asesoramiento legal, contable ni de auditoría, ni garantiza que sus servicios o productos vayan a asegurarse de que los clientes cumplan cualquier normativa o ley.

Si tiene que solicitar soporte de GDPR para los recursos de {{site.data.keyword.cloud}} {{site.data.keyword.watson}} que se crean

-   En la Unión Europea (UE), consulte [Solicitud de soporte para recursos de {{site.data.keyword.cloud_notm}} Watson creados en la Unión Europea](/docs/services/watson?topic=watson-gdpr-sar#request-EU).
-   Fuera de la Unión Europea, consulte [Solicitud de soporte para recursos fuera de la Unión Europea](/docs/services/watson?topic=watson-gdpr-sar#request-non-EU).

## Reglamento General de Protección de Datos de la Unión Europea (GDPR)
{: #gdpr}

{{site.data.keyword.IBM_notm}} se ha comprometido a proporcionar a nuestros clientes y socios soluciones innovadoras de privacidad de datos, seguridad y gobierno para ayudarles en su camino hacia la conformidad con GDPR.

Obtenga más información sobre el camino de {{site.data.keyword.IBM_notm}} hacia la conformidad con GDPR y sobre nuestras prestaciones y ofertas relacionadas con GDPR para darle soporte en su camino hacia esta conformidad [aquí](http://www.ibm.com/gdpr){: external}.

## Etiquetado y supresión de datos en el servicio Text to Speech
{: #gdpr-text-to-speech}

El servicio {{site.data.keyword.texttospeechfull}} permite suprimir todos los datos asociados a las solicitudes de síntesis de voz y a los modelos de voz personalizados. Para suprimir datos, debe hacer lo siguiente:

1.  Utilice la cabecera `X-Watson-Metadata` para asociar un ID de cliente con los datos que se pasan por una solicitud al servicio; consulte [Especificación de un ID de cliente](#specify-customer-id).
1.  Utilice el método `DELETE /v1/user_data` para suprimir todos los datos asociados a un ID de cliente especificado; consulte [Supresión de datos](#delete-pi).

De forma predeterminada, no hay ningún ID de cliente asociado a los datos.

Las características experimentales y beta no están pensadas para su uso con un entorno de producción y, por lo tanto, no se garantiza que funcionen como se espera cuando se etiquetan o se suprimen datos. Las características experimentales y beta no deben utilizarse al implementar una solución que requiera el etiquetado y la supresión de datos.
{: note}

### Especificar un ID de cliente
{: #specify-customer-id}

Para asociar un ID de cliente a unos datos, incluya la cabecera `X-Watson-Metadata` con la solicitud que pasa la información. Pase la serie `customer_id={id}` como argumento de la cabecera. En el ejemplo siguiente se asocia el ID de cliente `my_ID` con los datos pasados con una solicitud `POST /v1/synthesize`:

```bash
curl -X POST -u "apikey:{apikey}"
--header "X-Watson-Metadata: customer_id=my_ID"
--header "Content-Type: application/json"
--header "Accept: audio/wav"
--data "{\"text\":\"hello world\"}"
--output hello_world.wav
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```

Un ID de cliente puede incluir cualquier carácter excepto `;` (punto y coma) y `=` (signo de igual). Especifique una serie aleatoria o genérica para el ID de cliente; no especifique información de identificación personal, como por ejemplo una dirección de correo electrónico o un ID de Twitter. Puede especificar diferentes ID de cliente con diferentes solicitudes. El ID de cliente que especifica se asocia a la instancia del servicio cuyas credenciales se utilizan con la solicitud; sólo las credenciales para dicha instancia del servicio pueden suprimir los datos asociados al ID.

Utilice la cabecera `X-Watson-Metadata` con los métodos siguientes:

-   Con las solicitudes HTTP:
    -   `POST /v1/synthesize`
    -   `GET /v1/synthesize`

    El ID de cliente se asocia a los datos que se envían con la solicitud.

-   Con las solicitudes WebSocket:
    -   `/v1/synthesize`

    El ID de cliente se especifica con el parámetro de consulta `x-watson-metadata` para asociar el ID a los datos que se envían con la solicitud. Debe codificar como URL del argumento en el parámetro de consulta, por ejemplo, `customer_id%3dmy_ID`.

-   Con las solicitudes para añadir palabras personalizadas a modelos de voz personalizados:
    -   `POST /v1/customizations/{customization_id}`
    -   `POST /v1/customizations/{customization_id}/words`
    -   `PUT /v1/customizations/{customization_id}/words/{word}`

    El ID de cliente se asocia a las palabras personalizadas que la solicitud añade o actualiza.

### Supresión de datos
{: #delete-pi}

Para suprimir todos los datos asociados a un ID de cliente, utilice el método `DELETE /v1/user_data`. Pase la serie `customer_id={id}` como parámetro de consulta con la solicitud. En el ejemplo siguiente se suprimen todos los datos del ID de cliente `mi_ID`:

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/user_data?customer_id=my_ID"
```

El método `/v1/user_data` suprime todos los datos asociados al ID de cliente especificado, independientemente del método por el que se haya añadido la información. Este método no tiene ningún efecto si el ID de cliente no tiene datos asociados. Debe emitir la solicitud con las credenciales para la misma instancia del servicio que se ha utilizado para asociar el ID de cliente a los datos.
