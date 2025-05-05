---
title: ROAS durch Verwendung von algorithmischen (Lookalike-)Modellen erhöhen
description: Die Lookalike-Modellierung von Audience Manager bietet die echte Leistung, wenn Sie Ihre Grundlinie mit einer hochwertigen, brandneuen Benutzergruppe aus Datenquellen von 2 und 3 Anbietern erweitern möchten. In diesem Tutorial lernen Sie die Schritte zum Erstellen eines Modells aus diesen Daten kennen.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 25188.jpg
kt: 1849
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6626ae11-8709-4302-9e03-0d55878d2409
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Erhöhen des ROAS durch Verwendung von algorithmischen (Lookalike-)Modellen im Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

Die Lookalike-[!UICONTROL Modeling] von Audience Manager bietet die echte Leistung, wenn Sie Ihre Grundlinie anhand einer hochwertigen, brandneuen Benutzergruppe aus Datenquellen von Zweitanbietern und Drittanbietern erweitern möchten. In diesem Tutorial lernen Sie die Schritte kennen, die zum Erstellen eines Modells aus diesen Daten erforderlich sind.

## Aktivieren von Datenströmen von Zweitanbietern oder Drittanbietern von der Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Um Zweit- und Drittanbieterdaten in einem Lookalike-Modell zu verwenden, müssen wir diese Daten zunächst in Ihrer Audience Manager-Oberfläche aktivieren. Adobe verfügt über eine große Anzahl von Zweit- und Drittanbietern, aus denen Sie auswählen können. Diese stehen Ihnen in einer Self-Service-Oberfläche in AAM über die Audience Marketplace zur Verfügung. Navigieren Sie zur Audience Marketplace und durchsuchen Sie die verschiedenen Möglichkeiten. Das folgende Video zeigt Ihnen, wie Sie dies tun können, einschließlich der Aktivierung kostenloser Streams, die Sie vor dem Kauf ausprobieren können, damit Sie sich auf die Daten konzentrieren können, die für Ihr Unternehmen am nützlichsten sind, bevor Sie sich zur Preisgestaltung des Datenanbieters verpflichten.

Außerdem ist eine hervorragende Ressource die [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/), um Sie bei der Suche und Entscheidung zu unterstützen, welcher Datenanbieter verwendet werden soll.

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identifizieren oder erstellen Sie ein ideales Benutzermerkmal (Konversion) oder Segment {#identify-create-an-ideal-user-conversion-trait-or-segment}

Was versuchen Sie, die Leute auf Ihrer Seite zu tun? Was ist Ihr Konversionsereignis? Natürlich gibt es viele verschiedene Antworten auf diese Frage, abhängig von Ihrem Site-Typ/Vertikal und Ihren Unternehmenszielen. In jedem Fall ist es in AAM üblich, eine Eigenschaft für Besuchende zu erstellen, die diese Kriterien erfüllt haben.

Im folgenden Video zeige ich Ihnen, wie Sie ein Konversionsmerkmal erstellen, das Sie im Laufe dieses Tutorials anwenden und ein ähnliches Modell erstellen sollten.

Außerdem müssen Sie bei der Verwendung von Adobe Analytics-Ereignissen zum Erstellen von Eigenschaften ein großes Problem beachten, damit Sie nicht mehr Benutzende erfassen, als Sie für die Eigenschaft erfassen sollten. Sehen Sie sich das folgende Video für die große Enthüllung an. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**HINWEIS:** Im obigen Video wird im gezeigten Beispiel davon ausgegangen, dass Sie über Adobe Analytics verfügen. Das ist offensichtlich nicht der Fall. Wenn Sie Google Analytics (GA) haben, verfügen wir über ein Modul, mit dem Sie Daten an AAM senden können (siehe [documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html?lang=de)). Wenn Ihre Konversionsaktivität auf Ihrer Site per GA an AAM gesendet wird, können Sie daraus Ihr Konversionsmerkmal erstellen. Wenn Sie eine andere Analyselösung haben (oder keine Analyselösung), können Sie dennoch Daten über unseren DIL-Code und die `submit` usw. an AAM senden. (Siehe die [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=de)). Erstellen Sie dann das Konversionsmerkmal basierend auf den Daten, die bei der Durchführung der Konversionsaktivität auf der Site gesendet werden.

## Erstellen eines Lookalike-Modells aus Daten von Zweitanbietern oder Drittanbietern {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Nach Abschluss der oben genannten Schritte sind wir nun bereit, ein algorithmisches (Lookalike-)Modell zu erstellen. Bei der Einrichtung des Modells verwenden wir das Konversionsmerkmal als Grundeigenschaft (wichtige Besucher, die wir duplizieren möchten) und verwenden den aktivierten Drittanbieter-Datenstrom als Pool von Personen, aus dem wir Daten abrufen können.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Eine wichtige Best Practice {#an-important-best-practice}

Wenn wir das algorithmische Modell im Audience Manager erstellen, wollen wir natürlich, dass das Modell so effektiv wie möglich ist. Da das Modell alle Eigenschaften berücksichtigt, zu denen die Mitglieder Ihrer Basiseigenschaft/Ihres Segments gehören, ist es für das Modell nicht hilfreich, wenn ALLE Personen in einer Eigenschaft/einem Segment sind. Wenn Sie also über generische Supereigenschaften verfügen (z. B. für alle Benutzer Ihrer Site oder für alle Benutzer, die eine Anzeige von Ihnen erhalten haben usw.), stellen Sie sicher, dass die Datenquelle, zu der sie gehören, NICHT in den Datenquellen Ihres Modells enthalten ist. In diesem Anwendungsfall ist es unwahrscheinlich, dass Sie dies tun, da wir uns auf die Suche nach Drittanbieterdaten für unsere neuen Lookalikes konzentrieren. Es ist jedoch trotzdem erwähnenswert, und gilt für ALLE Ihre algorithmischen Modelle.

## Erstellen eines [!UICONTROL Algorithmic Trait] {#creating-an-algorithmic-trait}

Als Nächstes müssen wir eine [!UICONTROL Algorithmic Trait] erstellen, damit die Ergebnisse des Modells verwendet werden können. Ohne das Erstellen einer Eigenschaft ist das Modell nutzlos. Gehen Sie daher nach der Ausführung des Modells unbedingt in das Dialogfeld „Eigenschaft“ und erstellen Sie eine [!UICONTROL Algorithmic Trait]. Das folgende Video erläutert dies und zeigt einige Tipps.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Segment aus den Modelldaten erstellen und an DSP senden {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Nachdem Sie ein [!UICONTROL Algorithmic Trait] erstellt haben, können Sie ein neues Segment erstellen, um es einzufügen, damit Sie die Daten aktivieren können (Sie können keine Eigenschaft aktivieren, sondern stattdessen ein neues Segment mit einer Eigenschaft und den darin enthaltenen [!UICONTROL Algorithmic Trait] erstellen, damit Sie das Segment aktivieren (verwenden) können).

Nachdem Sie ein Segment aus dieser algorithmischen Eigenschaft erstellt haben, haben Sie eine Zielgruppe potenzieller Kunden, die wie Personen aussehen, die bereits auf Ihrer Site konvertiert sind. Jetzt können Sie dieses Segment jedem Ihrer DSP-Ziele in Audience Manager zuordnen. Sie können Ihr Marketing auf die Lookalikes ausrichten, die mit höherer Wahrscheinlichkeit auf Ihrer Site konvertieren als nur auf die normale Öffentlichkeit, was Ihre Rendite auf Werbeausgaben erhöht.
