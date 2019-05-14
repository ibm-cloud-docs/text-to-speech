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

# Wissenswertes über die Anpassung
{: #customIntro}

Wenn Sie mit {{site.data.keyword.texttospeechfull}} aus Text synthetisch Sprache erstellen, wendet der Service sprachenabhängige Ausspracheregeln an. Durch die Anwendung der Regeln konvertiert der Service die herkömmliche (also die ortografische) Schreibweise jedes Wortes in eine phonetische Schreibweise. Die phonetische Schreibweise eines Wortes verwendet Phonemsymbole, um zu definieren, wie das Wort ausgesprochen wird. Bei diesen Symbolen handelt es sich um die verschiedenen Lauteinheiten, die Wörter in einer Sprache unterscheiden, um die Grenzen zwischen den Silben und um die Betonungszeichen für die Silben.
{: shortdesc}

Die normalen Ausspracheregeln des Service sind für gängige Wörter gut geeignet. Bei ungewöhnlichen Wörtern können sie jedoch zu mangelhaften Ergebnissen führen. Hierzu gehören Sonderbegriffe fremdsprachigen Ursprungs, Personennamen bzw. geografische Bezeichnungen und Abkürzungen oder Akronyme. Falls das Wörterbuch Ihrer Anwendung solche Wörter enthält, können Sie mit der Anpassungsschnittstelle angeben, wie sie vom Service ausgesprochen werden sollen.

Die Anpassungsschnittstelle ist als Betafunktionalität für alle Sprachen verfügbar.
{: note}

## Funktionsweise der Anpassung
{: #ciHow}

Die Anpassungsschnittstelle des {{site.data.keyword.texttospeechshort}}-Service erstellt ein Wörterverzeichnis mit Wörtern und deren Umsetzungen für eine bestimmte Sprache. Dieses Wörterverzeichnis wird als *angepasstes Sprechmodell* oder auch kurz als 'angepasstes Modell' bezeichnet. Jeder angepasste Eintrag in einem angepassten Sprechmodell besteht aus einem Paar im Format *Wort*/*Umsetzung*. Die Umsetzung eines Wortes teilt dem Service mit, wie das Wort auszusprechen ist, wenn es im Eingabetext vorkommt.

Die Anpassungsschnittstelle bietet Methoden, mit denen Sie Ihre angepassten Sprechmodelle, die vom Service permanent gespeichert werden, erstellen und verwalten können. Nachdem Sie ein angepasstes Modell erstellt haben, können Sie es während der Synthese mit jeder beliebigen Version der Methode `/v1/synthesize` verwenden. Wenn der Service aus Eingabetext synthetisch Sprache erstellt, ermittelt er die Aussprache der Wörter, die im angepassten Modell enthalten sind, durch eine direkte oder indirekte Anwendung ihrer Umsetzungen.

Die Umsetzung für ein Wort geben Sie in einem angepassten Sprechmodell als *gleich klingende Umsetzung* oder *phonetische Umsetzung* an. Sie können beide Methoden für Einträge in demselben angepassten Modell verwenden und die beiden Methoden auch innerhalb einer Umsetzung kombinieren. Für angepasste Einträge gelten eine Reihe von Regeln und Richtlinien. Weitere Informationen finden Sie im Abschnitt [Regeln für die Erstellung von angepassten Einträgen](/docs/services/text-to-speech/custom-rules.html).

## Gleich klingende Umsetzung
{: #soundsLike}

Bei der *gleich klingenden Umsetzung* werden die normalen Ausspracherregeln des Service verwendet, um die Aussprache eines Zielworts indirekt darzustellen. Eine gleich klingende Umsetzung wird aus den normalen Aussprachevarianten für eines oder mehrere Wörter gebildet. Der Service ersetzt zunächst jedes Vorkommmen des Wortes im Eingabetext durch die angegebene Umsetzung. Anschließend wendet er seine normalen Ausspracheregeln auf die Umsetzung an, wobei die Umsetzung in ihre phonetische Darstellung konvertiert und auf diese Weise die Aussprache erhalten wird.

Viele gängige Abkürzungen und Akronyme werden beispielsweise einwandfrei durch die normalen Ausspracheregeln des Service umgesetzt. Der Service spricht die Abkürzung *cm* als *centimeter* aus. Seltener verwendete Abkürzungen werden Buchstabe für Buchstabe ausgesprochen. Beispielsweise wird die Zeichenfolge *Str* (Abkürzung für *street*) als *S T R* ausgesprochen, also mit einzeln ausgesprochenen Buchstaben. Mit der Methode für die gleich klingende Umsetzung können Sie die Umsetzung *street* für die Zeichenfolge *Str* angeben.

Ein weiteres Beispiel für ein Akronym ist das Wort *IEEE*, das für 'Institute of Electrical and Electronic Engineers' steht. Dieses Akronym wird vom Service standardmäßig als *I E E E* ausgesprochen. Die gängige Aussprache des Akronyms lautet jedoch *I triple E*, was Sie ganz einfach mithilfe der einfachen gleich klingenden Umsetzung *I triple E* definieren können. Falls das Wort *IEEE* mit dieser Umsetzung in Ihrem angepasste Modell enthalten ist, ersetzt der Service jedes Vorkommen des Wortes durch die Umsetzung. Anschließend wendet er seine normalen Ausspracheregeln auf die einzelnen Wörter *I*, *triple* und *E* an, um die gängige Aussprache zu erzielen.

Die Methode der gleich klingenden Umsetzung können Sie auf mehr als nur Abkürzungen oder Akronyme anwenden. Sie funktioniert bei komplexen oder ungewöhnlichen Wörtern ebenso gut. Beispielsweise ergibt das folgende Paar von gleich klingenden Umsetzungen korrekte Aussprachen für ungewöhnliche Wörter, die durch die normalen Ausspracheregeln des Service mangelhaft verarbeitet werden. Die Ermittlung der richtigen Umsetzungen für solche Wörter kann eine größere Herausforderung als bei einfachen Abkürzungen darstellen. Bei den folgenden Umsetzungen wird die Schreibweise der Wörter unter Verwendung der normalen Ausspracheregeln geändert.

<table style="width:35%">
  <caption>Tabelle 1. Beispiel für gleich klingende Umsetzungen</caption>
  <tr>
    <th style="text-align:left">Wort</th>
    <th style="text-align:left">Umsetzung</th>
  </tr>
  <tr>
    <td>ayurvedic</td>
    <td>aayervedic</td>
  </tr>
  <tr>
    <td>gastroenteritis</td>
    <td>gastro enteritis</td>
  </tr>
</table>

Aus diesen Beispielen wird ersichtlich, dass gleich klingende Umsetzungen eher durch Versuch und Irrtum als durch ein schablonenhaftes Vorgehen entwickelt werden. Erstellen Sie aufgrund Ihrer Intuition eine mögliche Umsetzung und experimentieren Sie dann mit dem Service. Anschließend erstellen Sie aus dem Wort für die mögliche Umsetzung synthetisch Sprache als Eingabetext und hören Sie sich die resultierende Audioausgabe an. Wenn Sie mit der Aussprache zufrieden sind, können Sie die Umsetzung in Ihrem angepassten Modell verwenden. Andernfalls ändern Sie die Umsetzung und testen sie erneut.

## Phonetische Umsetzung
{: #phonetic}

Die Methode der gleich klingenden Umsetzung ist ein relativ einfaches und brauchbares Verfahren für die Festlegung einer Aussprache. Es ist jedoch nicht immer möglich, gleich klingende Umsetzungen zu entwickeln. Als direkte Alternative erscheint die phonetische Methode möglicherweise komplizierter und zeitaufwendiger, aber mit ihrer Hilfe kann für jedes beliebige Wort eine Aussprache festgelegt werden.

Bei der *phonetischen Umsetzung* wird eine Aussprache in Form von Phonemsymbolen, Betonungszeichen für Silben und optionalen Silbentrennungen angegeben, die die normalen Ausspracheregeln des Service außer Kraft setzen. Zur Angabe einer phonetischen Umsetzung verwenden Sie eines der folgenden Formate:

-   Standarddarstellung gemäß IPA (International Phonetic Alphabet)
-   {{site.data.keyword.IBM_notm}} eigenes Format 'Symbolic Phonetic Representation' (SPR)

In beiden Fällen geben Sie eine Umsetzung mithilfe eines bestimmten Phonemformats an, das auf SSML (Speech Synthesis Markup Language) basiert. SSML ist eine XML-basierte Markup-Sprache, die Annotationen von Text für Sprachsyntheseanwendungen bereitstellt. Die phonetische Umsetzung für ein Wort geben Sie mithilfe des SSML-Elements `<phoneme>` an:

<pre><code>&lt;phoneme alphabet="{ipa | ibm}" ph="{umsetzung}"&gt;&lt;/phoneme&gt;</code></pre>

Das Attribut `alphabet` gibt den Typ der phonetischen Darstellung an, also `ipa` oder `ibm`. Das Attribut `ph` gibt die Zeichenfolge für die phonetische Umsetzung an.

Dies wird nachfolgend am Beispiel des Wortes `trinitroglycerin` erläutert. Die normalen Ausspracheregeln des Service erzeugen eine andere Aussprache, als üblicherweise von Chemikern und Physikern verwendet wird. Die korrekte Aussprache kann mit einer phonetischen Umsetzung erzielt werden.

<table style="width:35%">
  <caption>Tabelle 2. Beispiel für phonetische Umsetzungen</caption>
  <tr>
    <th style="text-align:left">Alphabet</th>
    <th style="text-align:left">Umsetzung</th>
  </tr>
  <tr>
    <td>IPA</td>
    <td>t&#633;a&#618;n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n</td>
  </tr>
  <tr>
    <td>SPR</td>
    <td>trYn1YtrxglIsxrXn</td>
  </tr>
</table>

In diesen Beispielen besteht die Zeichenfolge für die phonetische Umsetzung aus Phonemsymbolen und einer einzigen Markierung für die Hauptbetonung. Die Markierung für die Hauptbetonung wird in IPA mit <code>&#712;</code> und in SPR mit `1` dargestellt. In beiden Fällen steht sie unmittelbar vor dem Symbol für den betonten Vokal. Auch wenn es in den Beispielen nicht dargestellt ist, können Sie ebenfalls Silbengrenzen und Positionen für eine Nebenbetonung in einer phonetischen Umsetzung angeben. Diese Elemente sind nicht erforderlich und werden normalerweise nicht benötigt, um eine Aussprache festzulegen. Wie gleich klingende Umsetzungen können Sie auch eine phonetische Umsetzung aus mehreren Zeichenfolgen bilden, die durch Leerzeichen voneinander abgegrenzt werden.

Umsetzungen im IPA-Format können Sie auch als IPA-Unicode-Werte angeben. Weitere Informationen enthalten der Abschnitt [IBM SPR verwenden](/docs/services/text-to-speech/SPRs.html) und die sprachspezifischen Tabellen auf den Seiten, auf die im Abschnitt [Unterstützte Sprachen](/docs/services/text-to-speech/SPRs.html#supportedLanguages) Bezug genommen wird. Ein Beispiel für eine Umsetzung, die IPA-Unicode-Werte verwendet, finden Sie unter [Element 'phoneme'](/docs/services/text-to-speech/SSML-elements.html#phoneme_element).
{: note}

### Vorhandene phonetische Umsetzung bearbeiten
{: #phoneticMethod}

Sofern Sie nicht gerade Experte auf dem Gebiet der Phonetik sind, ist die Bildung von phonetischen Umsetzungen keine einfache Aufgabe. Es ist immer leichter, eine vorhandene phonetische Umsetzung zu bearbeiten, als sie völlig neu zu erstellen. Die API des Service umfasst eine Methode `GET /v1/pronunciation`, die Sie bei der Erstellung von phonetischen Umsetzungen unterstützt. Die Methode gibt die IPA- oder SPR-Darstellung zurück, die von den normalen Ausspracheregeln des Service für ein Wort in einer angegebenen Sprache generiert wird. Sie haben außerdem die Möglichkeit, die Aussprache für ein Wort aus einem angegebenen angepassten Sprechmodell abzurufen, um die Umsetzung in der Sprache für dieses Modell anzuzeigen.

Mit der Methode `/GET v/1/pronunciation` können Sie eine erste phonetische Umsetzung für ein Wort anfordern. Anschließend können Sie die Umsetzung ändern und so die gewünschte Aussprache erzielen. Wie bei der Methode für gleich klingende Umsetzungen arbeiten Sie auch hier nach dem Prinzip von Versuch und Irrtum. Sie übergeben Ihre mögliche Umsetzung an den Service, lassen aus dem Wort synthetisch Eingabetext erstellen, hören sich die resultierende Audioausgabe an und bearbeiten die mögliche Umsetzung. Diesen Prozess können Sie wiederholen, bis Sie mit der Aussprache zufrieden sind.

Zusätzliche Angaben finden Sie im Abschnitt [Wort aus einer Sprache abfragen](/docs/services/text-to-speech/custom-entries.html#cuWordsQueryLanguage).

### Weitere Informationen zur phonetischen Umsetzung
{: #phoneticInfo}

Die folgenden Quellen bieten weitere Informationen zur phonetischen Umsetzung:

-   Näheres über die Verwendung von SSML und des Elements `<phoneme>` finden Sie unter [SSML verwenden](/docs/services/text-to-speech/SSML.html).
-   Weitere Informationen zur Angabe von SPR-Umsetzungen und ihre äquivalenten IPA-Symbole enthält der Abschnitt [IBM SPR verwenden](/docs/services/text-to-speech/SPRs.html).
-   Zusätzliche Angaben über die Verwendung von IPA-Symbolen und Tonbeispiele für die Symbole bieten Quellen im Web. Unter der Adresse [en.wikipedia.org/wiki/International_Phonetic_Alphabet ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet){: new_window} finden Sie eine ausführliche Einführung und Erläuterung.

## Gleich klingende und phonetische Umsetzung kombinieren

Sie können die Methoden für die gleich klingende und die phonetische Umsetzung in ein und derselben Umsetzung kombinieren. Dies kann die mit der Erstellung einer Umsetzung verbundene Arbeit verringern.

Nehmen wir beispielsweise an, Sie haben für den Teil eines Wortes mit der Methode für die gleich klingende Umsetzung eine zufriedenstellende Aussprache erreicht. Nun müssen Sie jedoch noch die übrigen Elemente des Wortes optimieren. Mit der phonetischen Methode können Sie die komplizierten Aspekte des Wortes angeben. Beim folgenden Beispiel wird eine kombinierte Umsetzung für das Wort `trinitroglycerin` angewendet:

<pre><code>try&lt;phoneme alphabet="ipa" ph="n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n"&gt;&lt;/phoneme&gt;</code></pre>
