---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-09"

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

# SSML expressivo
{: #expressive}

Por padrão, o serviço {{site.data.keyword.texttospeechfull}}sintetiza texto em um estilo declarativo neutro. O serviço estende SSML com um elemento `<express-as>`que produz expressividade convertendo texto para discurso sintetizado em vários estilos de fala. O elemento é análogo ao elemento `<say-as>` do SSML, que especifica a normalização de texto para o texto formatado, como datas, horários e números.
{: shortdesc}

## Suporte ao idioma
{: #languages-expressive}

O serviço suporta a expressividade somente para voz em inglês americano Allison (`en-US_AllisonVoice`). A expressividade não é suportada com a voz `en-US_AllisonV2Voice`. O uso do elemento com uma voz não suportada retorna um erro.

## O elemento express-as

É possível aplicar o elemento `<express-as>`para o corpo inteiro do texto, uma sentença ou um fragmento, como uma frase ou uma palavra. O elemento aceita um atributo necessário, `type`, que descreve o tipo de expressão a ser usado para o texto especificado: `GoodNews`, `Apology` ou `Uncertainty`.

### GoodNews
{: #goodnews}

O `GoodNews` expressa uma mensagem positiva e animadora.

```xml
<express-as type="GoodNews">
  Tenho o prazer de informar que sua requisição de empréstimo de hipoteca foi aprovada.
< /express-as>

<express-as type="GoodNews">
  Tenho boas notícias: fui capaz de reduzir os pagamentos em sua conta mensal!
< /express-as>

< express-as type="GoodNews">
  Parabéns pelo noivado! Vocês são perfeitos um para o outro!
< /express-as>

<express-as type="GoodNews">
  Uau, parabéns por sua promoção! É uma posição de grande prestígio!
< /express-as>
```
{: codeblock}

### Apology
{: #apology}

O `Apology` expressa uma mensagem negativa.

```xml
<express-as type="Apology">
  Infelizmente, o próximo vôo sairá apenas após mais cinco horas.
< /express-as>

<express-as type="Apology">
  Sinto muito pela qualidade do serviço que você recebeu.
< /express-as>

<express-as type="Apology">
  Sinto muito por ter excluído seus arquivos. Foi um acidente.
< /express-as>

<express-as type="Apology">
  Há alguma forma de recompensar você?
< /express-as>
```
{: codeblock}

### Uncertainty
{: #uncertainty}

O `Uncertainty` transmite uma mensagem de incerteza e interrogação.

```xml
<express-as type="Uncertainty">
  Será que ela ainda está no escritório? Ela me disse que poderia sair mais cedo.
< /express-as>

<express-as type="Uncertainty">
  Acho que não ouvi bem. Você disse sexta ou sábado?
< /express-as>

<express-as type="Uncertainty">
  Você pode explicar novamente? Não sei se realmente entendi.
< /express-as>

<express-as type="Uncertainty">
  Desculpe, não entendi seu nome. Você pode repetir?
< /express-as>
```
{: codeblock}

## Exemplos expressivos

Os exemplos a seguir demonstram o uso de todas as três formas de expressividade no atributo `text` do método `POST /v1/synthesize`. O texto a ser sintetizado está localizado dentro do período do elemento `<speak>`da raiz SSML.

```xml
{
  "text": "<speak>
    Fui designado para manipular sua solicitação de status do pedido.
    <express-as type=\"Apology\">
      Lamento informar que os itens solicitados estão temporariamente indisponíveis.
      Sinto muito pela inconveniência.
    </express-as>
    <express-as type=\"Uncertainty\">
      Não sabemos quando os itens estarão novamente disponíveis. Talvez na próxima semana,
      Mas não temos certeza neste momento.
    </express-as>
    <express-as type=\"GoodNews\">
      No entanto, como gostaríamos que você se sentisse satisfeito, forneceremos
      um desconto de 50% em seu pedido!
    </express-as>
  </speak>"
}
```
{: codeblock}
