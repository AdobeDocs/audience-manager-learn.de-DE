---
title: ROAS durch Verwendung von algorithmischen (Lookalike-)Modellen erhöhen
description: Die Lookalike-Modellierung von Audience Manager bietet die echte Leistung, wenn Sie Ihre Grundlinie anhand einer hochwertigen, brandneuen Benutzergruppe aus Datenquellen von 2 und 3 Parteien erweitern möchten. In diesem Tutorial lernen Sie die Schritte zum Erstellen eines Modells aus diesen Daten kennen.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 25188.jpg
kt: 1849
role: User, Developer, Admin, Leader
level: Intermediate
exl-id: 6626ae11-8709-4302-9e03-0d55878d2409
TQID: https://experienceleague.adobe.com/rQ-djjfEOZDjR3IdvvJnO1Hb2tu6IUhz0uFhp-xuZq8
product_v2: id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1
feature_v2: id: c814092e-2730-45e8-a12d-e084529f52cbid: d8f86c1e-15ad-457f-9d6f-5e756573fad4
subfeature_v2: id: d921db59-bd4a-43dc-97e6-4ff4611f1ae8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 3152e8fc51e0e06c90c17dce0aa203a27995e88d
workflow-type: tm+mt
source-wordcount: 943
ht-degree: 0%

---

# Erhöhen des ROAS durch die Verwendung von algorithmischen (Lookalike-)Modellen in Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

Die Lookalike-[!UICONTROL Modeling] von Audience Manager erzielen Sie, wenn Sie Ihre Grundlinie anhand einer hochwertigen, brandneuen Benutzergruppe aus Datenquellen von Zweitanbietern und Drittanbietern erweitern möchten. In diesem Tutorial lernen Sie die Schritte kennen, die zum Erstellen eines Modells aus diesen Daten erforderlich sind.

## Aktivieren von Datenströmen von Zweitanbietern oder Drittanbietern aus Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Um Zweit- und Drittanbieterdaten in einem Lookalike-Modell zu verwenden, müssen wir diese Daten zunächst in Ihrer Audience Manager-Oberfläche aktivieren. Adobe verfügt über eine große Anzahl von Zweit- und Drittanbietern, aus denen Sie auswählen können. Diese sind in einer Self-Service-Oberfläche in AAM über die Audience Marketplace verfügbar. Navigieren Sie zur Audience Marketplace und durchsuchen Sie die verschiedenen Möglichkeiten. Das folgende Video zeigt Ihnen, wie Sie dies tun können, einschließlich der Aktivierung kostenloser Streams, die Sie vor dem Kauf ausprobieren können, damit Sie sich auf die Daten konzentrieren können, die für Ihr Unternehmen am nützlichsten sind, bevor Sie sich zur Preisgestaltung des Datenanbieters verpflichten.

Außerdem ist eine hervorragende Ressource die [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/), um Sie bei der Suche und Entscheidung zu unterstützen, welcher Datenanbieter verwendet werden soll.

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identifizieren oder erstellen Sie ein ideales Benutzermerkmal (Konversion) oder Segment {#identify-create-an-ideal-user-conversion-trait-or-segment}

Was versuchen Sie, die Leute auf Ihrer Seite zu tun? Was ist Ihr Konversionsereignis? Natürlich gibt es viele verschiedene Antworten auf diese Frage, abhängig von Ihrem Site-Typ/Vertikal und Ihren Unternehmenszielen. In jedem Fall ist es in AAM üblich, eine Eigenschaft für Besuchende zu erstellen, die diese Kriterien erfüllt haben.

Im folgenden Video zeige ich Ihnen, wie Sie ein Konversionsmerkmal erstellen, das Sie im Laufe dieses Tutorials anwenden und ein ähnliches Modell erstellen sollten.

Außerdem müssen Sie bei der Verwendung von Adobe Analytics-Ereignissen zum Erstellen von Eigenschaften ein großes Problem beachten, damit Sie nicht mehr Benutzende erfassen, als Sie für die Eigenschaft erfassen sollten. Sehen Sie sich das folgende Video für die große Enthüllung an. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**HINWEIS:** Im obigen Video wird im gezeigten Beispiel davon ausgegangen, dass Sie über Adobe Analytics verfügen. Das ist offensichtlich nicht der Fall. Wenn Sie über Google Analytics (GA) verfügen, können Sie mithilfe eines Moduls Daten an AAM senden (siehe [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html)). Wenn Ihre Konversionsaktivität auf Ihrer Site über GA an AAM gesendet wird, können Sie daraus Ihr Konversionsmerkmal erstellen. Wenn Sie eine andere Analyselösung haben (oder keine Analyselösung), können Sie weiterhin Daten über unseren DIL-Code und die `submit` usw. an AAM senden (siehe [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html)). Erstellen Sie dann das Konversionsmerkmal basierend auf den Daten, die bei der Durchführung der Konversionsaktivität auf der Site gesendet werden.

## Erstellen eines Lookalike-Modells aus Daten von Zweitanbietern oder Drittanbietern {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Nach Abschluss der oben genannten Schritte sind wir nun bereit, ein algorithmisches (Lookalike-)Modell zu erstellen. Bei der Einrichtung des Modells verwenden wir das Konversionsmerkmal als Grundeigenschaft (wichtige Besucher, die wir duplizieren möchten) und verwenden den aktivierten Drittanbieter-Datenstrom als Pool von Personen, aus dem wir Daten abrufen können.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Eine wichtige Best Practice {#an-important-best-practice}

Bei der Erstellung des algorithmischen Modells in Audience Manager ist es offensichtlich, dass wir wollen, dass das Modell so effektiv wie möglich ist. Da das Modell alle Eigenschaften berücksichtigt, zu denen die Mitglieder Ihrer Basiseigenschaft/Ihres Segments gehören, ist es für das Modell nicht hilfreich, wenn ALLE Personen in einer Eigenschaft/einem Segment sind. Wenn Sie also über generische Supereigenschaften verfügen (z. B. für alle Benutzer Ihrer Site oder für alle Benutzer, die eine Anzeige von Ihnen erhalten haben usw.), stellen Sie sicher, dass die Datenquelle, zu der sie gehören, NICHT in den Datenquellen Ihres Modells enthalten ist. In diesem Anwendungsfall ist es unwahrscheinlich, dass Sie dies tun, da wir uns auf die Suche nach Drittanbieterdaten für unsere neuen Lookalikes konzentrieren. Es ist jedoch trotzdem erwähnenswert, und gilt für ALLE Ihre algorithmischen Modelle.

## Erstellen eines [!UICONTROL Algorithmic Trait] {#creating-an-algorithmic-trait}

Als Nächstes müssen wir eine [!UICONTROL Algorithmic Trait] erstellen, damit die Ergebnisse des Modells verwendet werden können. Ohne das Erstellen einer Eigenschaft ist das Modell nutzlos. Gehen Sie daher nach der Ausführung des Modells unbedingt in das Dialogfeld „Eigenschaft“ und erstellen Sie eine [!UICONTROL Algorithmic Trait]. Das folgende Video erläutert dies und zeigt einige Tipps.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Erstellen eines Segments aus den Modelldaten und Senden an DSPs {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Nachdem Sie ein [!UICONTROL Algorithmic Trait] erstellt haben, können Sie ein neues Segment erstellen, um es einzufügen, damit Sie die Daten aktivieren können (Sie können keine Eigenschaft aktivieren, sondern stattdessen ein neues Segment mit einer Eigenschaft und den darin enthaltenen [!UICONTROL Algorithmic Trait] erstellen, damit Sie das Segment aktivieren (verwenden) können).

Nachdem Sie ein Segment aus dieser algorithmischen Eigenschaft erstellt haben, haben Sie eine Zielgruppe potenzieller Kunden, die wie Personen aussehen, die bereits auf Ihrer Site konvertiert sind. Jetzt können Sie dieses Segment jedem Ihrer DSP-Ziele in Audience Manager zuordnen. Sie können Ihr Marketing auf die Lookalikes ausrichten, die mit höherer Wahrscheinlichkeit auf Ihrer Site konvertieren als nur auf die normale Öffentlichkeit, was Ihre Rendite auf Werbeausgaben erhöht.
