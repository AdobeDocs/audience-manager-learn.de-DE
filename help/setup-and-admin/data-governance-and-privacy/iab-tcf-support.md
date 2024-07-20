---
title: IAB TCF 2.0-Unterstützung
description: Erfahren Sie mehr über das Audience Manager-Plugin für IAB TCF und wie es mit dem Opt-in-Objekt von Adobe und Ihrem Consent Management Provider (CMP) funktioniert.
feature: Data Governance & Privacy
activity: implement
doc-type: technical video
team: Technical Marketing
thumbnail: 26434.jpg
kt: 5027
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 04b4e786-0457-4dcc-bcf9-a79eda67bb2e
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# IAB TCF 2.0-Unterstützung in Audience Manager {#iab-tcf-support-in-audience-manager}

Adobe bietet Ihnen die Möglichkeit, die Datenschutzoptionen Ihrer Benutzer über die Opt-in-Funktion und die Audience Manager-Plug-in-Unterstützung für IAB Transparency and Consent Framework 2.0 (TCF 2.0) zu verwalten und zu übermitteln. Dieser Artikel arbeitet mit der Dokumentation zusammen, um Ihnen zu helfen, das Audience Manager-Plug-in für IAB TCF zu verstehen und wie es mit dem Opt-in-Objekt von Adobe und Ihrem Consent Management Provider (CMP) funktioniert. Weitere Informationen zum IAB finden Sie auf ihrer Website unter [https://www.iabeurope.eu/](https://www.iabeurope.eu/).

## Erster Schritt: Grundlegendes zur Experience Cloud ID-Anmeldung {#first-step-understand-ecid-s-opt-in}

Um zu verstehen, wie Sie mit dem IAB TCF arbeiten, müssen Sie zunächst die Funktion [!DNL Opt-in] verstehen, die Teil der Experience Cloud ID-Dienst-Bibliothek (ECID) ist. Wenn Sie nicht genau wissen, wie das Opt-in funktioniert, lesen Sie zuerst [diesen hilfreichen Artikel](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/id-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.html). Sie sollten auch die Opt-in [Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) lesen. Kehren Sie nach Durchsicht dieser Ressourcen zu dieser Seite zurück und fahren Sie fort.

## Das Audience Manager-Plug-in für IAB TCF {#the-audience-manager-plug-in-for-iab-tcf}

Da Sie jetzt mindestens über ein grundlegendes Verständnis der Funktionsweise des Opt-in-Dienstes verfügen, kann der Audience Manager auf die [!DNL IAB Transparency and Consent Framework (TCF)]-Unterstützung übertragen, was über ein Plug-in im Opt-in-Objekt erfolgt.

Das Audience Manager-Plug-in für IAB TCF erweitert die Opt-in-Funktionalität und ermöglicht es AAM Kunden, Datenschutzoptionen von Benutzern gemäß IAB TCF zu bewerten, zu berücksichtigen und an nachgelagerte Partner weiterzuleiten. Es bietet einen Standard, den Datenverantwortliche (Sie als Adobe-Kunde) und Anbieter (DMPs, DSP, SSPs, Anzeigenserver usw.) kann verwenden, um die Zustimmung in der gesamten Zustimmungslandschaft zu verstehen.

## IAB TCF aktivieren {#enabling-iab-tcf}

Die Aktivierung des Audience Manager-Plug-ins für IAB TCF ist einfach, wenn Sie Adobe Experience Platform Launch verwenden, da es sich um ein einfaches Kontrollkästchen handelt, wie im folgenden kurzen Video gezeigt:

>[!VIDEO](https://video.tv.adobe.com/v/26433/?quality=12)

Wenn Sie Launch nicht verwenden, können Sie auch `isIabContext=true` verwenden, um es zu aktivieren, wenn Sie den Experience Cloud-Besucher instanziieren. Dadurch wird der IAB-TCF-Fluss initiiert, d. h. ein weiterer Schritt zur Einverständniserfassung hinzugefügt. Dabei wird der IAB-TCF verwendet, um die IAB-TC-Zeichenfolge abzufragen, und der Opt-in wird zurückgegeben, der wiederum mit den Experience Cloud-Lösungen kommuniziert.

## IAB TC-Zeichenfolge {#iab-tcf-consent-string}

Eine der Standards, die IAB bereitstellt, ist eine &quot;Zustimmungszeichenfolge&quot;(auch &quot;DaisyBit&quot;genannt), die eigentlich aus zwei Listen besteht:

1. Zweck: **Was** wird genehmigt?
1. Anbieter: **Wer** erhält die Einwilligung?

### Zweck {#purposes}

Mit IAB TCF 2.0 gibt es zehn &quot;Zwecke&quot;, für die eine Einwilligung eingeholt werden kann (was Anbieter mit den Besucherdaten tun können). Adobe Audience Manager benötigt nicht alle zehn, sondern nur die Zustimmung für die folgenden Zwecke zusätzlich zur Zustimmung des Anbieters:

* **Zweck 1:** Informationen auf einem Gerät speichern und/oder darauf zugreifen;
* **Zweck 10:** Produkte entwickeln und verbessern;
* **Sonderzweck 1:** Gewährleistung von Sicherheit, Vermeidung von Betrug und Fehlerbehebung.

Dies ist der erste Teil der IAB-TC-Zeichenfolge und wird nur als 1 und 0 aufgezeichnet und bestimmt, ob dieser Zweck/diese Aktivität genehmigt ist.

>[!NOTE]
>
>Gemäß den IAB-Vorschriften wird dem Sonderzweck 1 (Sicherheit gewährleisten, Betrug verhindern und Debugging) immer zugestimmt und Benutzer können keine Einwände dagegen erheben.

### Anbieter {#vendors}

Ein weiterer Teil der IAB TC-Zeichenfolge ist eine lange Liste mit mehreren hundert Anbietern, sodass Besuchern eine Liste der jeweiligen Anbieter angezeigt werden kann, die Tags auf der Site haben und entscheiden können, welche Anbieter verwendet werden sollen. Anbieter behalten ihren Platz auf der Liste bei. Beispielsweise lautet die Anbieternummer von Adobe Audience Manager auf dieser Liste 565. Wenn die Nummer in der Liste den Wert &quot;1&quot;hat, kann der Audience Manager die genehmigten Zwecke von der Vorderseite der Liste aus durchführen. Wenn AAM Spot den Wert &quot;0&quot;hat, kann er keine Daten verarbeiten.

**Damit Audience Manager eine Benutzeroberfläche bereitstellt, über die Kunden das IAB TCF zur Auswahl dieser Zwecke und Anbieter verwenden oder alle Aktivitäten genehmigen/ablehnen können, müssen Sie einen CMP-Partner verwenden, der beim IAB TCF registriert ist oder einen erstellen, der IAB TCF unterstützt und beim IAB TCF registriert ist.**

## Opt-in: Übersetzung zwischen IAB- und Adobe-Anwendungen {#opt-in-translating-between-iab-and-adobe-solutions}

Einer der Vorteile der Verwendung des IAB TCF besteht darin, dass die oben aufgeführten Standardzwecke dem Endbenutzer wahrscheinlich eine bessere Vorstellung davon geben, was er genehmigt, als eine Liste von Adobe-Lösungen. Endbenutzer wissen möglicherweise nicht, was es bedeutet, Audience Manager oder [!DNL Target] zu &quot;genehmigen&quot;, aber &quot;Informationen auf einem Gerät speichern und/oder aufrufen&quot;oder &quot;Produkte entwickeln und verbessern&quot;ist für sie wahrscheinlich einfacher zu verstehen und zuzustimmen.

Damit der Audience Manager genehmigt werden kann (d.h. Damit die Übersetzung von IAB-Zwecken für Opt-in AAM &quot;Ja&quot; abstimmen kann, müssen die oben aufgeführten Zwecke 1 und 10 vom Endnutzer genehmigt werden. Wenn eine dieser Optionen nicht genehmigt ist oder ein Anbieter nicht genehmigt wurde, führen AAM keine Pixellöcher aus oder setzen keine Cookies. Es ist auch gut zu wissen, dass viele Kunden dem Endbenutzer einfach eine &quot;alles oder nichts&quot;-Benutzeroberfläche bereitstellen, die natürlich die Verwendung von Audience Manager (und den anderen Experience Cloud-Lösungen) zulassen oder verbieten würde.

In der [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=en) finden Sie einige großartige Informationen darüber, wie das Audience Manager-Plug-in für IAB TCF-Fluss sowohl für Publisher- als auch für Advertiser-Anwendungsfälle gilt.

## IAB: Zustimmungsversand nachgelagert {#iab-sending-consent-downstream}

Wenn das Audience Manager-Plug-in für IAB TCF verwendet wird, werden die Zustimmungsoptionen des Benutzers auch an die ID-Synchronisationen auf Plattformebene (Drittanbieter) für Partner gesendet, die in der Global Vendor List vorhanden sind, sodass der Partner über die Informationen zur Benutzerzustimmung verfügt und auch darauf reagieren kann. Diese Informationen werden in zwei Variablen gesendet:

* gdpr = 1
* gdpr_consent = [kodierte Zustimmungszeichenfolge]

Der Nachteil besteht darin, dass der Audience Manager die IAB-TC-Zeichenfolge überhaupt nicht erfasst und die Aufrufe daher abbricht, wenn er sich im IAB-Kontext befindet und keine Zustimmung erteilt (oder eine negative Zustimmung erteilt). In diesem Fall also...keine Weitergabe der Zustimmung nachgelagert.

## Demo {#demo}

Im folgenden Video sehen Sie, wie Cookies und Beacons von ECID und Lösungen von der Auswahl der IAB-Benutzer beeinflusst werden.

>[!VIDEO](https://video.tv.adobe.com/v/26434/?quality=12)

Weitere Informationen zum Audience Manager-Plug-in für IAB TCF 2.0, einschließlich Implementierung und Test, Anwendungsfällen und Workflows, finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).
