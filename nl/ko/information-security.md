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

# 정보 보안
{: #information-security}

{{site.data.keyword.IBM}}은 고객 및 파트너에게 혁신적인 데이터 개인정보 보호, 보안 및 통제 솔루션을 제공하려 노력하고 있습니다.
{: shortdesc}

고객은 유럽 연합 일반 개인정보 보호법률(General Data Protection Regulation)을 포함한
다양한 법령과 규정을 준수해야 할 책임이 있습니다. 고객은 고객의 비즈니스에 영향을 줄 수 있는 관련 법령 및 규정에 대한 확인과 해석,
그러한 법령 및 규정의 준수를 위해 필요한 고객의 모든 조치와 관련하여 적절한 법률 자문을 받아야 할 단독 책임이 있습니다.
{: important}

여기에서 설명하는 제품, 서비스 및 기타 기능은 일부 고객의 상황에는 해당되지 않을 수 있으며
그 가용성이 제한될 수 있습니다. {{site.data.keyword.IBM_notm}}은 법률, 회계 또는 감사 관련 자문을 제공하지 않으며, IBM의 서비스나 제품 사용이 고객의 관련 법령이나 규정 준수를
보장한다는 진술이나 보증을 제공하지 않습니다.

작성된 {{site.data.keyword.cloud}} {{site.data.keyword.watson}} 리소스에 대한 GDPR 지원을 요청해야 하는 경우

-   유럽 연합(EU)에서 작성된 경우 [유럽 연합에서 작성된 {{site.data.keyword.cloud_notm}} Watson 리소스에 대한 지원 요청](/docs/services/watson?topic=watson-gdpr-sar#request-EU)을 참조하십시오.
-   유럽 연합(EU) 외부에서 작성된 경우 [유럽 연합 외부의 리소스에 대한 지원 요청](/docs/services/watson?topic=watson-gdpr-sar#request-non-EU)을 참조하십시오.

## 유럽 연합 일반 개인정보 보호법률(GDPR)
{: #gdpr}

{{site.data.keyword.IBM_notm}}은 고객 및 파트너가 GDPR 준수에 대비하는 데 도움을 줄 수 있도록 혁신적인 데이터 개인정보 보호, 보안 및 통제 솔루션을 제공하려 노력하고 있습니다.

{{site.data.keyword.IBM_notm}}의 자체 GDPR 대비 과정 및 규정 준수 과정을 지원하기 위한 당사의 GDPR 기능과 오퍼링에 관한 자세한 정보는 [여기](http://www.ibm.com/gdpr){: external}를 참조하십시오.

## 문자-음성 변환 서비스의 데이터 레이블 지정 및 삭제
{: #gdpr-text-to-speech}

{{site.data.keyword.texttospeechfull}} 서비스를 통해 음성 합성 요청과 사용자 정의 음성 모델과 연관된 모든 데이터를 삭제할 수 있습니다. 데이터를 삭제하려면 다음을 수행해야 합니다.

1.  `X-Watson-Metadata` 헤더를 사용하여 요청에 따라 서비스로 전달되는 데이터와 고객 ID를 연관시키십시오. [고객 ID 지정](#specify-customer-id)을 참조하십시오.
1.  `DELETE /v1/user_data` 메소드를 사용하여 지정된 고객 ID와 연관된 모든 데이터를 삭제하십시오. [데이터 삭제](#delete-pi)를 참조하십시오.

기본적으로 고객 ID는 데이터와 연관되지 않습니다.

시범 및 베타 기능은 프로덕션 환경에서 사용하도록 개발된 것이 아니므로 데이터 레이블 지정 및 삭제 시 예상대로 작동하지 않을 수 있습니다. 시범 및 베타 기능은 데이터 레이블 지정 및 삭제가 필요한 솔루션 구현 시 사용하면 안 됩니다.
{: note}

### 고객 ID 지정
{: #specify-customer-id}

고객 ID를 데이터와 연관시키려면 정보를 전달하는 요청에 따라 `X-Watson-Metadata` 헤더를 포함시키십시오. 헤더의 인수로 문자열 `customer_id={id}`를 전달합니다. 다음 예에서는 `POST /v1/synthesize` 요청과 함께 전달되는 데이터와 고객 ID `my_ID`를 연관시킵니다.

```bash
curl -X POST -u "apikey:{apikey}"
--header "X-Watson-Metadata: customer_id=my_ID"
--header "Content-Type: application/json"
--header "Accept: audio/wav"
--data "{\"text\":\"hello world\"}"
--output hello_world.wav
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```

고객 ID에는 `;`(세미콜론) 및 `=`(등호)를 제외한 모든 문자가 포함될 수 있습니다. 고객 ID에 무작위 또는 일반 문자열을 지정하십시오. 개인 식별 문자열(예: 이메일 주소 또는 Twitter ID)은 지정하지 마십시오. 요청마다 다른 고객 ID를 지정할 수 있습니다. 지정하는 고객 ID는 인증 정보가 요청에 사용되는 서비스의 인스턴스와 연관됩니다. 서비스의 해당 인스턴스에 대한 인증 정보만 ID와 연관된 데이터를 삭제할 수 있습니다.

다음 메소드를 사용하여 `X-Watson-Metadata` 헤더를 사용하십시오.

-   HTTP 요청 사용:
    -   `POST /v1/synthesize`
    -   `GET /v1/synthesize`

    고객 ID는 요청에 따라 전송되는 데이터와 연관됩니다.

-   WebSocket 요청 사용:
    -   `/v1/synthesize`

    ID가 요청에 따라 전송되는 데이터와 연관되도록 `x-watson-metadata` 조회 매개변수를 사용하여 고객 ID를 지정합니다. 조회 매개변수에 대한 인수를 URL로 인코딩해야 합니다(예: `customer_id%3dmy_ID`).

-   사용자 정의 단어를 사용자 정의 음성 모델에 추가하기 위한 요청 사용:
    -   `POST /v1/customizations/{customization_id}`
    -   `POST /v1/customizations/{customization_id}/words`
    -   `PUT /v1/customizations/{customization_id}/words/{word}`

    고객 ID는 요청에 따라 추가되거나 업데이트되는 사용자 정의 단어와 연관됩니다.

### 데이터 삭제
{: #delete-pi}

고객 ID와 연관된 모든 데이터를 삭제하려면 `DELETE /v1/user_data` 메소드를 사용하십시오. 요청에 따라 조회 매개변수로 문자열 `customer_id={id}`를 전달합니다. 다음 예에서는 고객 ID `my_ID`에 대한 모든 데이터를 삭제합니다.

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/user_data?customer_id=my_ID"
```

`/v1/user_data` 메소드는 정보를 추가한 메소드에 관계 없이 지정된 고객 ID와 연관되는 모든 데이터를 삭제합니다. 데이터가 고객 ID와 연관되지 않으면 메소드는 작동하지 않습니다. 고객 ID를 데이터와 연관시키는 데 사용된 서비스의 동일한 인스턴스에 대한 인증 정보를 사용하여 요청을 발행해야 합니다.
