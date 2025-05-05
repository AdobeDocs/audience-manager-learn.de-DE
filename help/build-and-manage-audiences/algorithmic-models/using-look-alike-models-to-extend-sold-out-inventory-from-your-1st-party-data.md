---
title: Verwenden von Look-alike-Modellen, um ausverkaufte Inventardaten aus First-Party-Daten zu erweitern
description: In diesem Tutorial führen wir die Schritte durch, die Sie zum Einrichten und Verwenden von Look-alike-Modellen ausführen sollten, damit Sie neue Look-alike-Zielgruppen erstellen und sie als Erweiterung für Ihr Konversionssegment verkaufen können.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 23523.jpg
kt: 1688
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6820528e-3211-4a1d-be05-50f1292179d2
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Verwenden von Look-alike-Modellen, um ausverkaufte Inventardaten aus First-Party-Daten zu erweitern {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

In diesem Tutorial werden wir die Schritte erläutern, die Sie zum Einrichten und Verwenden von Lookalike-[!UICONTROL Models] ausführen sollten, damit Sie neue Lookalike-Zielgruppen erstellen und sie als Erweiterung für Ihr Konversionssegment verkaufen können.

## Details zum Anwendungsfall {#use-case-details}

Sie sind ein Inhaltsherausgeber. Wenn Sie bereits einen ausverkauften Bestand an Konvertern auf Ihrer Site haben, könnten Sie denken, dass Ihre Opportunity dort endet. Geben Sie die Lookalike-[!UICONTROL Models] der AAM ein. Mithilfe dieser Funktion können Sie den ausverkauften Bestand weiter erweitern und auch Zielgruppen von Personen verkaufen, die vielleicht noch nicht konvertiert sind, aber wie Menschen aussehen/sich verhalten, die konvertiert haben. Dieses Zielgruppensegment würde in der Regel für weniger als die tatsächlichen Konverter verkauft, ermöglicht es Ihnen jedoch, Ihren Gewinn zu steigern, indem Sie eine zusätzliche Zielgruppenoption für Werbetreibende bereitstellen, die Anzeigen auf Ihrer Site platzieren möchten. Der zusätzliche Vorteil dieses Anwendungsfalls besteht darin, dass die Ausführung dieses Modells mit Erstanbieterdaten keine Kosten verursacht.

Die Schritte in diesem Tutorial sind wie folgt:

1. Identifizieren/Erstellen eines idealen Benutzermerkmals (Konversion) oder Segments
1. Erstellen Sie ein Modell mit diesem Konversionseigenschaft/Segment als Basiselement
1. [!UICONTROL First party] Datenquelle(n) im Modell auswählen und das Modell ausführen
1. Erstellen eines [!UICONTROL Algorithmic Trait] aus den Modellergebnissen und Hinzufügen der Eigenschaft zu einem Segment
1. Interessenten das Segment anbieten, um den Umsatz des Konversionssegments zu erweitern

## Identifizieren oder erstellen Sie ein ideales Benutzermerkmal (Konversion) oder Segment {#identify-create-an-ideal-user-conversion-trait-or-segment}

Was versuchen Sie, die Leute auf Ihrer Seite zu tun? Was ist Ihr Konversionsereignis? Natürlich gibt es viele verschiedene Antworten auf diese Frage, abhängig von Ihrem Site-Typ/Vertikal und Ihren Unternehmenszielen. In jedem Fall ist es in AAM üblich, eine Eigenschaft für Besuchende zu erstellen, die diese Kriterien erfüllt haben.

In diesem Anwendungsfall wird dies bereits angenommen, da Sie das Inventar für Personen ausverkauft haben, die Konvertierer sind. Für die Zwecke dieses Tutorials ist es jedoch sinnvoll, dies als Referenz für den Rest des Anwendungsfalls zu besprechen.

Außerdem müssen Sie bei der Verwendung von Ereignissen zum Erstellen von Eigenschaften einen wichtigen Aspekt beachten, damit Sie nicht mehr Benutzende erfassen, als Sie für die Eigenschaft erfassen sollten. Sehen Sie sich das folgende Video für die große Enthüllung an. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**HINWEIS:** Im obigen Video wird im gezeigten Beispiel davon ausgegangen, dass Sie über Adobe Analytics verfügen. Das ist offensichtlich nicht der Fall. Wenn Sie Google Analytics (GA) haben, verfügen wir über ein Modul, mit dem Sie Daten an AAM senden können (siehe [documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=de)). Wenn Ihre Konversionsaktivität auf Ihrer Site per GA an AAM gesendet wird, können Sie daraus Ihr Konversionsmerkmal erstellen. Wenn Sie eine andere Analyselösung haben (oder keine Analyselösung), können Sie dennoch Daten über unseren DIL-Code und die `submit` usw. an AAM senden. (Siehe die [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html?lang=de)). Erstellen Sie dann erneut das Konversionsmerkmal basierend auf den Daten, die gesendet werden, als die Konversionsaktivität auf der Site ausgeführt wird.

## Erstellen eines Lookalike-Modells aus First-Party-Daten {#creating-a-look-alike-model-from-first-party-data}

In diesem Schritt erstellen wir ein [!UICONTROL First Party] Look-alike-Modell. Das bedeutet, dass wir nicht nur eine First-Party-Konversionseigenschaft/ein First-Party-Segment für unsere Basis-Eigenschaft/unser -Segment verwenden werden (das wäre bei den meisten Modellen ohnehin normal), sondern dass wir auch nur den Pool von First-Party-Daten für weitere Personen untersuchen werden, die wie die Konverter aussehen. Wir werden keine Daten von Zweitanbietern oder Drittanbietern berücksichtigen.

In diesem Anwendungsbeispiel ist dies wichtig, da wir versuchen, ein Segment von Benutzern auf unserer Website zu erstellen, die wie Konverter aussehen, aber noch nicht konvertiert sind, damit wir dieses Lookalike-Segment an interessierte Werbetreibende verkaufen können.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Algorithmische Eigenschaft erstellen {#creating-an-algorithmic-trait}

Als Nächstes müssen wir eine [!UICONTROL Algorithmic Trait] erstellen, damit die Ergebnisse des Modells verwendet werden können. Ohne das Erstellen einer Eigenschaft ist das Modell nutzlos. Gehen Sie also nach der Ausführung des Modells unbedingt zum Dialogfeld „Eigenschaft“ und erstellen Sie eine [!UICONTROL Algorithmic Trait]. Das folgende Video erläutert dies und zeigt einige Tipps.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## Den [!UICONTROL Algorithmic Segment] Werbetreibenden anbieten {#offering-the-algorithmic-segment-to-advertisers}

Nachdem Sie ein [!UICONTROL Algorithmic Trait] erstellt haben, können Sie ein neues Segment erstellen, um es einzufügen, damit Sie die Daten aktivieren können. (Sie können keine Eigenschaft aktivieren, sondern stattdessen ein neues Segment mit einer Eigenschaft und den darin enthaltenen [!UICONTROL Algorithmic Trait] erstellen, damit Sie das Segment aktivieren (verwenden) können.

Nachdem Sie ein Segment von Erstanbieter-Besuchern erstellt haben, die im Look-alike-Modell einen hohen Wert erreicht haben (d. h. die wie Konverter aussehen, aber noch nicht konvertiert haben), können Sie dieses Segment Advertisern auf Ihrer Site anbieten, selbst wenn Sie Ihren gesamten Bestand an tatsächlichen Konvertern auf Ihrer Site ausverkauft haben. Dies ist eine hervorragende Möglichkeit, diese Zielgruppe zu erweitern und durch die Verwendung von Lookalike-[!UICONTROL Models] im Audience Manager weiterhin zusätzliche Umsätze zu erzielen.
