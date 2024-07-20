---
title: Verwenden Sie Look-alike-Modelle, um ausverkauften Bestand aus Erstanbieterdaten zu erweitern
description: In diesem Tutorial gehen wir durch die Schritte, die Sie unternehmen sollten, um Look-alike-Modelle einzurichten und zu verwenden, sodass Sie neue Look-alike-Zielgruppen erstellen und diese als Erweiterung für Ihr Konversionssegment verkaufen können.
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

# Verwenden Sie Look-alike-Modelle, um ausverkauften Bestand aus Erstanbieterdaten zu erweitern {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

In diesem Tutorial führen wir Sie durch die Schritte, die Sie unternehmen sollten, um Look-alike [!UICONTROL Models] einzurichten und zu verwenden, damit Sie neue Look-alike-Zielgruppen erstellen und diese als Erweiterung für Ihr Konversionssegment verkaufen können.

## Anwendungsfalldetails {#use-case-details}

Sie sind ein Herausgeber von Inhalten. Wenn Sie bereits Inventar für Konverter auf Ihrer Site ausverkauft haben, können Sie denken, dass Ihre Chance dort endet. Geben Sie AAM Look-Alike [!UICONTROL Models] ein. Mit dieser Funktion können Sie den ausverkauften Bestand weiter erweitern und auch Zielgruppen von Personen verkaufen, die vielleicht noch nicht konvertiert sind, aber wie konvertierte Personen aussehen/handeln. Dieses Zielgruppensegment würde in der Regel für weniger als die tatsächlichen Konverter verkauft, ermöglicht Ihnen jedoch, zu Ihrem Endwert hinzuzufügen, indem Sie eine zusätzliche Zielgruppenoption für Advertiser bereitstellen, die Anzeigen auf Ihrer Site platzieren möchten. Der zusätzliche Vorteil dieses Anwendungsbeispiels besteht darin, dass es Sie nicht kostet, dieses Modell auf Ihren Erstanbieterdaten auszuführen.

Die Schritte in diesem Tutorial lauten wie folgt:

1. Identifizieren/Erstellen einer idealen Benutzereigenschaft (Konversion) oder eines Segments
1. Erstellen eines Modells mit dieser Konversionseigenschaft/diesem Segment als Basiselement
1. Wählen Sie [!UICONTROL First party] Datenquellen im Modell aus und führen Sie das Modell aus.
1. Erstellen Sie eine [!UICONTROL Algorithmic Trait] aus den Modellergebnissen und fügen Sie die Eigenschaft zu einem Segment hinzu
1. Angebot des Segments an interessierte Advertiser zur Erweiterung der Umrechnungssegmentverkäufe

## Identifizieren oder Erstellen einer idealen Benutzereigenschaft (Konversion) oder eines Segments {#identify-create-an-ideal-user-conversion-trait-or-segment}

Was versuchen Sie, Menschen dazu zu bringen, auf Ihrer Site zu tun? Was ist Ihr Konversionsereignis? Natürlich gibt es viele verschiedene Antworten auf diese Frage, abhängig von Ihrem Site-Typ/Ihrer Vertikale und Ihren Organisationszielen. In jedem Fall ist es in AAM üblich, eine Eigenschaft für Besucher zu erstellen, die diese Kriterien erfüllt haben.

In diesem Anwendungsfall wird dies bereits angenommen, da Sie den Bestand für Konverter verkauft haben. Für die Zwecke dieses Tutorials ist es jedoch gut, es als Referenz für den restlichen Anwendungsfall zu diskutieren.

Außerdem müssen Sie bei der Verwendung von Ereignissen zur Erstellung von Eigenschaften einen wichtigen Aspekt beachten, damit Sie nicht mehr Benutzer erfassen, als Sie in der Eigenschaft sollten. Sehen Sie sich das folgende Video für die große Anzeige an. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**HINWEIS:** Im obigen Video geht das angezeigte Beispiel davon aus, dass Sie über Adobe Analytics verfügen. Das ist offensichtlich nicht der Fall. Wenn Sie über Google Analytics (GA) verfügen, können Sie mit einem -Modul Daten an AAM senden (siehe die [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html)). Wenn Ihre Konversionsaktivität auf Ihrer Site von GA an AAM gesendet wird, können Sie daraus Ihre Konversionseigenschaft erstellen. Wenn Sie über eine andere Analyselösung (oder keine Analyselösung) verfügen, können Sie weiterhin Daten über unseren DIL-Code und die Funktion `submit` an AAM senden. (siehe die [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html)). Erstellen Sie dann erneut die Konversionseigenschaft basierend auf den Daten, die gesendet werden, wenn die Konversionsaktivität auf der Site durchgeführt wird.

## Erstellen eines Look-alike-Modells aus Erstanbieterdaten {#creating-a-look-alike-model-from-first-party-data}

In diesem Schritt erstellen wir ein Look-alike-Modell [!UICONTROL First Party]. Das bedeutet, dass wir nicht nur eine Erstanbieter-Konversionseigenschaft/ein Erstanbieter-Segment für unsere Basiseigenschaft/unser Basissegment verwenden werden (dies wäre ohnehin für die meisten Modelle normal), sondern auch nur in den Pool von Erstanbieterdaten für mehr Personen, die wie die Konverter aussehen. Wir werden keine Daten von Zweitanbietern oder Drittanbietern betrachten.

In diesem Anwendungsfall ist dies wichtig, da wir versuchen, ein Segment von Benutzern auf unserer Site zu erstellen, die wie Konverter aussehen, aber noch nicht konvertiert wurden, sodass wir dieses Look-alike-Segment an interessierte Advertiser verkaufen können.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Erstellen einer algorithmischen Eigenschaft {#creating-an-algorithmic-trait}

Als Nächstes müssen wir einen [!UICONTROL Algorithmic Trait] erstellen, damit die Ergebnisse des Modells verwendet werden können. Ohne eine Eigenschaft zu erstellen, ist das Modell nutzlos. Nachdem das Modell ausgeführt wurde, gehen Sie also in das Eigenschaftsdialogfeld und erstellen Sie eine [!UICONTROL Algorithmic Trait]. Das folgende Video führt Sie durch und zeigt einige Tipps.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## Anzeigen von [!UICONTROL Algorithmic Segment] {#offering-the-algorithmic-segment-to-advertisers}

Nachdem Sie den Wert &quot;[!UICONTROL Algorithmic Trait]&quot;erstellt haben, können Sie ein neues Segment erstellen, um ihn einzufügen, sodass Sie die Daten aktivieren können (Sie können eine Eigenschaft nicht aktivieren, sondern ein neues Segment mit einer Eigenschaft mit dem Wert &quot;[!UICONTROL Algorithmic Trait]&quot;erstellen, damit Sie das Segment aktivieren (verwenden) können.

Nachdem Sie ein Segment mit Erstanbieterbesuchern erstellt haben, die im Look-alike-Modell einen hohen Wert erreicht haben (d. h., die wie Konverter aussehen, aber noch nicht konvertiert wurden), können Sie dieses Segment Werbetreibenden auf Ihrer Site anbieten, selbst wenn Sie Ihren gesamten Bestand an tatsächlichen Konvertern auf Ihrer Site ausverkauft haben. Dies ist eine großartige Möglichkeit, diese Zielgruppe zu erweitern und durch die Verwendung von Look-Alike [!UICONTROL Models] im Audience Manager weiterhin zusätzlichen Umsatz zu sehen.
