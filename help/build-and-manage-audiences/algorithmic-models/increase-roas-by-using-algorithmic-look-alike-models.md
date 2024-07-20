---
title: Steigerung des ROAS durch Verwendung algorithmischer (Look-alike) Modelle
description: Die wahre Stärke der Look-alike-Modellierung von Audience Manager liegt darin, dass Sie versuchen, Ihre Grundzielgruppe gegenüber einer qualitativ hochwertigen, brandneuen Benutzergruppe aus 2nd- und Drittanbieter-Datenquellen zu erweitern. In diesem Tutorial erfahren Sie, wie Sie anhand dieser Daten ein Modell erstellen.
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

# Steigerung des ROAS durch Verwendung algorithmischer (Look-alike) Modelle in Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

Die wahre Stärke von Audience Managers Look-alike [!UICONTROL Modeling] kommt, wenn Sie versuchen, Ihre Grundzielgruppe mit einer hochwertigen, brandneuen Benutzergruppe aus Datenquellen von Zweitanbietern und Drittanbietern zu erweitern. In diesem Tutorial erfahren Sie, wie Sie anhand dieser Daten ein Modell erstellen.

## Aktivieren von Daten-Streams von Zweitanbietern oder Drittanbietern über die Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Um Daten von Zweitanbietern und Drittanbietern in einem Look-alike-Modell zu verwenden, müssen wir diese Daten zunächst in Ihrer Audience Manager-Oberfläche aktivieren. Adobe verfügt über eine große Anzahl von Zweitanbieter- und Drittanbieter für Daten, von denen Sie wählen können. Diese sind für Sie in einer Self-Service-Oberfläche in AAM über die Audience Marketplace verfügbar. Navigieren Sie zur Audience Marketplace und durchsuchen Sie die Möglichkeiten. Im folgenden Video erfahren Sie, wie Sie dies tun, einschließlich der Aktivierung kostenloser Streams vom Typ &quot;try before you buy&quot;, sodass Sie die Daten einbinden können, die für Ihre Organisation am nützlichsten sind, bevor Sie sich zu den Preisen des Datenanbieters verpflichten.

Um Ihnen bei der Suche und Auswahl des Datenanbieters zu helfen, ist eine großartige Ressource die [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identifizieren oder Erstellen einer idealen Benutzereigenschaft (Konversion) oder eines Segments {#identify-create-an-ideal-user-conversion-trait-or-segment}

Was versuchen Sie, Menschen dazu zu bringen, auf Ihrer Site zu tun? Was ist Ihr Konversionsereignis? Natürlich gibt es viele verschiedene Antworten auf diese Frage, abhängig von Ihrem Site-Typ/Ihrer Vertikale und Ihren Organisationszielen. In jedem Fall ist es in AAM üblich, eine Eigenschaft für Besucher zu erstellen, die diese Kriterien erfüllt haben.

Im folgenden Video zeige ich Ihnen, wie Sie eine Konversionseigenschaft erstellen, die Sie während des gesamten Tutorials erhalten und ein Look-alike-Modell erstellen möchten.

Wenn Sie Adobe Analytics-Ereignisse zum Erstellen von Eigenschaften verwenden, müssen Sie außerdem einen wichtigen Aspekt beachten, damit Sie nicht mehr Benutzer erfassen, als Sie in der Eigenschaft sollten. Sehen Sie sich das folgende Video für die große Anzeige an. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**HINWEIS:** Im obigen Video geht das angezeigte Beispiel davon aus, dass Sie über Adobe Analytics verfügen. Das ist offensichtlich nicht der Fall. Wenn Sie über Google Analytics (GA) verfügen, können Sie mit einem -Modul Daten an AAM senden (siehe die [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html)). Wenn Ihre Konversionsaktivität auf Ihrer Site von GA an AAM gesendet wird, können Sie daraus Ihre Konversionseigenschaft erstellen. Wenn Sie über eine andere Analyselösung (oder keine Analyselösung) verfügen, können Sie weiterhin Daten über unseren DIL-Code und die Funktion `submit` an AAM senden. (siehe die [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html)). Erstellen Sie dann die Konversionseigenschaft basierend auf den Daten, die gesendet werden, wenn die Konversionsaktivität auf der Site durchgeführt wird.

## Erstellen eines Look-alike-Modells aus Daten von Zweitanbietern oder Drittanbietern {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Nach Abschluss der oben genannten Schritte können wir nun ein algorithmisches (Look-alike-)Modell erstellen. Während wir das Modell einrichten, verwenden wir die Konversionseigenschaft als unsere Basiseigenschaft (wichtige Besucher, die wir duplizieren möchten) und verwenden den aktivierten Datenstrom von Drittanbietern als unseren Pool von Personen, von denen wir abrufen können.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Ein wichtiger Best Practice {#an-important-best-practice}

Beim Erstellen des algorithmischen Modells in Audience Manager möchten wir natürlich, dass das Modell so effektiv wie möglich ist. Da das Modell alle Eigenschaften berücksichtigt, zu denen die Mitglieder Ihrer Basiseigenschaft/Ihres Segments gehören, hilft es dem Modell nicht, wenn sich ALLE Personen in einer Eigenschaft/einem Segment befinden. Wenn Sie also über superallgemeine Eigenschaften verfügen (z. B. alle, die Ihre Site besucht haben oder alle, die eine Anzeige von Ihnen erhalten haben usw.), stellen Sie sicher, dass die Datenquelle, zu der sie gehören, NICHT in den Datenquellen Ihres Modells enthalten ist. Im Anwendungsfall dieses Artikels ist es unwahrscheinlich, dass Sie dies tun, da wir uns darauf konzentrieren, Daten von Drittanbietern für unsere neuen Look-alikes zu betrachten. Es lohnt sich jedoch, auf jeden Fall zu erwähnen, und gilt für all Ihre algorithmischen Modelle.

## Erstellen eines [!UICONTROL Algorithmic Trait] {#creating-an-algorithmic-trait}

Als Nächstes müssen wir einen [!UICONTROL Algorithmic Trait] erstellen, damit die Ergebnisse des Modells verwendet werden können. Ohne eine Eigenschaft zu erstellen, ist das Modell nutzlos. Nachdem das Modell ausgeführt wurde, gehen Sie also in das Eigenschaftsdialogfeld und erstellen Sie eine &quot;[!UICONTROL Algorithmic Trait]&quot;. Das folgende Video führt Sie durch und zeigt einige Tipps.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Erstellen Sie ein Segment aus den Modelldaten und senden Sie es an DSP {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Nachdem Sie den Wert &quot;[!UICONTROL Algorithmic Trait]&quot;erstellt haben, können Sie ein neues Segment erstellen, um ihn einzufügen, sodass Sie die Daten aktivieren können (Sie können eine Eigenschaft nicht aktivieren, sondern ein neues Segment mit einer Eigenschaft mit dem Wert &quot;[!UICONTROL Algorithmic Trait]&quot;erstellen, damit Sie das Segment aktivieren (verwenden) können.

Nachdem Sie ein Segment aus dieser algorithmischen Eigenschaft erstellt haben, haben Sie eine Zielgruppe potenzieller Kunden, die aussehen wie Personen, die bereits auf Ihrer Site konvertiert wurden. Jetzt können Sie dieses Segment jedem Ihrer DSP in Audience Manager zuordnen. Sie können Ihr Marketing auf die Look-alikes ausrichten, die auf Ihrer Site mit höherer Wahrscheinlichkeit als nur die normale Öffentlichkeit konvertieren und so Ihren Return on Ad Spend steigern.
