---
title: IAB TCF 2.2-Unterstützung
description: Erfahren Sie mehr über das Audience Manager-Plug-in für IAB TCF und wie es mit dem Opt-in-Objekt von Adobe und Ihrem Einverständnisverwaltungsanbieter (CMP) funktioniert.
feature: Data Governance & Privacy
thumbnail: 26434.jpg
kt: 5027
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 04b4e786-0457-4dcc-bcf9-a79eda67bb2e
source-git-commit: f9708e705d95b43084ff11e342dc54ff11d6326c
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# IAB TCF 2.2-Unterstützung in Audience Manager {#iab-tcf-support-in-audience-manager}

Adobe bietet Ihnen die Möglichkeit, die Datenschutzentscheidungen Ihrer Benutzenden über die Opt-in-Funktion und über das Audience Manager Plug-in zu IAB Transparency and Consent Framework 2.2 (TCF 2.2)-Unterstützung zu verwalten und zu kommunizieren. Dieser Artikel hilft Ihnen zusammen mit der Dokumentation, das Audience Manager-Plug-in für IAB TCF zu verstehen und wie es mit dem Opt-in-Objekt von Adobe und Ihrem Einverständnisverwaltungsanbieter (CMP) zusammenarbeitet. Weitere Informationen zum IAB finden Sie auf seiner Website unter [https://www.iabeurope.eu/](https://www.iabeurope.eu/).

## Erster Schritt: Grundlegendes zum Opt-in mit der Experience Cloud ID {#first-step-understand-ecid-s-opt-in}

Um zu verstehen, wie Sie mit dem IAB TCF arbeiten, müssen Sie zunächst [!DNL Opt-in] Funktionalität verstehen, die Teil der Bibliothek des Experience Cloud ID Service (ECID) ist. Wenn Sie nicht mit der Funktionsweise des Opt-in vertraut sind, lesen Sie zunächst [diesen hilfreichen Artikel](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/id-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.html). Lesen Sie auch die Dokumentation zum Opt-in [](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html). Kehren Sie nach der Bearbeitung der Ressourcen zu dieser Seite zurück und fahren Sie fort.

## Das Audience Manager-Plug-in für IAB TCF {#the-audience-manager-plug-in-for-iab-tcf}

Nachdem Sie nun mindestens ein grundlegendes Verständnis davon haben, wie der Opt-in-Dienst funktioniert, kann Audience Manager [!DNL IAB Transparency and Consent Framework (TCF)] Unterstützung darauf schichten, was über ein Plug-in in das Opt-in-Objekt erfolgt.

Das Audience Manager-Plug-in für IAB TCF erweitert die Funktionalität des Opt-ins und ermöglicht es AAM-Kunden, Datenschutzentscheidungen von Benutzern zu bewerten, zu berücksichtigen und gemäß IAB TCF an nachgelagerte Partner weiterzuleiten. Sie bietet einen Standard, den Datenverantwortliche (d. h. Sie als Adobe-Kunde) und Anbieter (DMPs, DSPs, SSPs, Werbeserver usw.) verwenden können, um das Einverständnis in der gesamten Einverständnisumgebung zu verstehen.

## IAB-TCF aktivieren {#enabling-iab-tcf}

Die Aktivierung des Audience Manager-Plug-ins für IAB TCF ist einfach, wenn Sie Adobe Experience Platform Launch verwenden, da es sich um ein einfaches Kontrollkästchen handelt, wie im folgenden kurzen Video gezeigt:

>[!VIDEO](https://video.tv.adobe.com/v/26433/?quality=12)

Wenn Sie Launch nicht verwenden, können Sie es alternativ mit `isIabContext=true` aktivieren, wenn Sie den Experience Cloud-Besucher instanziieren. Dadurch wird der IAB-TCF-Ablauf initiiert, d. h. ein weiterer Schritt zur Einverständniserfassung hinzugefügt, wobei der IAB-TCF verwendet wird, um die IAB-TC-Zeichenfolge abzufragen, und der Opt-in-Vorgang wird zurückgegeben, der dann wiederum mit den Experience Cloud-Lösungen kommuniziert.

## IAB TC-Zeichenfolge {#iab-tcf-consent-string}

Einer der Standards, den IAB bereitstellt, ist eine „Einverständniszeichenfolge“ (auch als „DaisyBit“ bezeichnet), bei der es sich in Wirklichkeit um zwei zusammengestellte Listen handelt:

1. Zweck: **Was** wird die Einwilligung erteilt?
1. Anbieter: **Wer** wird eingewilligt?

### Zwecke {#purposes}

Mit IAB TCF 2.2 gibt es zehn „Zwecke“, für die ein Einverständnis eingeholt werden muss (was Anbieter mit den Daten des Besuchers tun können). Adobe Audience Manager erfordert nicht alle zehn, sondern erfordert zusätzlich zum Einverständnis des Anbieters nur das Einverständnis für die folgenden Zwecke:

* **Zweck 1:** von Informationen auf einem Gerät speichern und/oder darauf zugreifen;
* **Zweck 10:** Entwicklung und Verbesserung von Produkten;
* **Sonderzweck 1:** Gewährleistung der Sicherheit, Verhinderung von Betrug und Fehlerbehebung.

Dies ist der erste Teil der IAB-TC-Zeichenfolge und wird einfach als 1 und 0 aufgezeichnet, was angibt, ob dieser Zweck/diese Aktivität genehmigt wurde oder nicht.

>[!NOTE]
>
>Gemäß den IAB-Vorschriften ist Special Purpose 1 (Gewährleistung der Sicherheit, Verhinderung von Betrug und Debugging) immer einverstanden, und die Benutzer können keine Einwände dagegen erheben.

### Anbieter {#vendors}

Ein weiterer Teil der IAB TC-Zeichenfolge ist eine lange Liste von mehreren hundert Anbietern, sodass Besuchern eine Liste der entsprechenden Anbieter präsentiert werden kann, die Tags auf der Website haben, und sie auswählen können, welche Anbieter verwendet werden sollen. Anbieter behalten ihren Platz auf der Liste. Beispielsweise lautet die Anbieternummer von Adobe Audience Manager auf dieser Liste 565. Wenn die Nummer in der Liste eine „1“ aufweist, kann Audience Manager die genehmigten Zwecke von vorne auf der Liste ausführen. Wenn der Spot in AAM eine „0“ hat, kann er mit den Daten nichts anfangen.

**Damit Audience Manager eine Benutzeroberfläche bereitstellt, über die Kunden den IAB TCF zum Auswählen dieser Zwecke und Anbieter verwenden können, oder um alle Aktivitäten zu genehmigen bzw. nicht zu genehmigen, müssen Sie einen CMP-Partner verwenden, der beim IAB TCF registriert ist, oder einen CMP-Partner erstellen, der den IAB TCF unterstützt und beim IAB TCF registriert ist.**

## Opt-in: Übersetzen zwischen IAB- und Adobe-Anwendungen {#opt-in-translating-between-iab-and-adobe-solutions}

Einer der Vorteile der Verwendung des IAB-TCF besteht darin, dass die oben aufgeführten Standardzwecke dem Endbenutzer wahrscheinlich eher eine Vorstellung davon vermitteln, was er genehmigt, als eine Liste von Adobe-Lösungen. Die Endbenutzer wissen möglicherweise nicht, was es bedeutet, Audience Manager oder [!DNL Target] zu „genehmigen“, aber „Informationen auf einem Gerät zu speichern und/oder darauf zuzugreifen“ oder „Produkte entwickeln und verbessern“ ist für sie wahrscheinlich leichter zu verstehen und zuzustimmen.

Damit Audience Manager genehmigt werden kann (d.h. Damit die IAB-Zwecke für das Opt-in übersetzt werden können, um AAM ein „Ja“-Votum zu erteilen), müssen die oben aufgeführten Zwecke 1 und 10 vom Endbenutzer genehmigt werden. Wenn einer dieser Schritte nicht genehmigt ist oder ein Anbieter nicht genehmigt ist, führt AAM keine Pixelfeuer aus und setzt keine Cookies. Es ist auch gut zu wissen, dass sich viele Kunden einfach dafür entscheiden, dem Endbenutzer eine „Alles-oder-Nichts“-Benutzeroberfläche bereitzustellen, die natürlich die Verwendung von Audience Manager (und den anderen Experience Cloud-Lösungen) erlauben oder verbieten würde.

Die [Dokumentation) enthält einige wichtige Informationen darüber](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=en) wie der Audience Manager Plug-In für IAB TCF-Ablauf sowohl für Publisher- als auch für Advertiser-Anwendungsfälle gilt.

## IAB: Einverständnis nachgelagert senden {#iab-sending-consent-downstream}

Wenn das Audience Manager-Plug-in für IAB TCF verwendet wird, werden die Einverständnisentscheidungen des Benutzers auch an die ID-Synchronisierungen auf Plattformebene (Drittanbieter) für Partner gesendet, die auf der globalen Anbieterliste vorhanden sind, sodass der Partner über die Einverständnisinformationen des Benutzers verfügt und auch darauf reagieren kann. Diese Informationen werden in zwei Variablen gesendet:

* DSGVO = 1
* DSGVO_CONSENT = [codierte Einverständniszeichenfolge]

Der Nachteil besteht darin, dass Audience Manager die IAB-TC-Zeichenfolge überhaupt nicht erfasst und daher die Aufrufe ignoriert, wenn sich der Benutzer im IAB-Kontext befindet und kein Einverständnis erteilt (oder ein negatives Einverständnis erteilt). Also, in diesem Fall… keine Weitergabe der Zustimmung nachgelagert.

## Demo {#demo}

Im folgenden Video sehen Sie, wie Cookies und Beacons von ECID und Lösungen durch die Auswahl der IAB-Benutzer beeinflusst werden.

>[!VIDEO](https://video.tv.adobe.com/v/26434/?quality=12)

Weitere Informationen zum Audience Manager-Plug-in für IAB TCF 2.2, einschließlich Implementieren und Testen, Anwendungsfällen und Workflows, finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).
