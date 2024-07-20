---
title: Verwenden Sie Best Practices beim Senden von Daten an AAM auf SPA Seiten
description: Erfahren Sie mehr über Best Practices zum Senden von Daten von Einzelseiten-Apps (SPA) an Adobe Audience Manager (AAM). Dieser Artikel konzentriert sich auf die Verwendung von Experience Platform-Tags, der empfohlenen Implementierungsmethode.
feature: Implementation Basics
topics: spa
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
topic: SPA
role: Developer, Data Engineer
level: Experienced
exl-id: 99ec723a-dd56-4355-a29f-bd6d2356b402
source-git-commit: d4874d9f6d7a36bb81ac183eb8b853d893822ae0
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# Verwenden Sie Best Practices beim Senden von Daten an AAM auf SPA Seiten {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

In diesem Dokument werden verschiedene Best Practices zum Senden von Daten von Einzelseitenanwendungen (SPA) an Adobe Audience Manager (AAM) beschrieben. Dieser Artikel konzentriert sich auf die Verwendung von [!UICONTROL Experience Platform tags], der empfohlenen Implementierungsmethode.

## Anfängliche Hinweise

* Bei den folgenden Elementen wird davon ausgegangen, dass Sie Platform-Tags verwenden, um auf Ihrer Site zu implementieren. Wenn Sie keine Platform-Tags verwenden, sind diese jedoch an Ihre Implementierungsmethode anzupassen.
* Alle SPA unterscheiden sich, sodass Sie möglicherweise einige der folgenden Elemente anpassen müssen, um Ihre Anforderungen am besten zu erfüllen. Adobe möchte jedoch einige Best Practices teilen, über die Sie nachdenken müssen, wenn Sie Daten von SPA an Audience Manager senden.

## Einfaches Diagramm zum Arbeiten mit SPA und AAM in Experience Platform-Tags (früher Launch){#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![spa für aam in tags](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Wie angegeben, ist dies ein vereinfachtes Diagramm dazu, wie SPA Seiten in einer Adobe Audience Manager-Implementierung (ohne Adobe Analytics) mit Platform-Tags verarbeitet werden. Wie Sie sehen können, ist es recht unkompliziert, wobei die große Entscheidung darin liegt, wie Sie eine Änderung der Ansicht (oder eine Aktion) an Platform-Tags weiterleiten.

## Auslösen von Tags von der SPA {#triggering-launch-from-the-spa-page}

Zwei der gängigeren Methoden zum Auslösen einer Regel in Platform-Tags (und somit zum Senden von Daten in Audience Manager) sind:

* Festlegen benutzerdefinierter JavaScript-Ereignisse (siehe Beispiel [HERE](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) mit Adobe Analytics)
* Verwenden eines [!UICONTROL Direct Call Rule]

In diesem Audience Manager verwenden Sie einen [!UICONTROL Direct Call rule] in Platform-Tags, um den Treffer in den Audience Manager Trigger. Wie Sie in den nächsten Abschnitten sehen werden, ist dies nützlich, indem Sie den [!UICONTROL Data Layer] auf einen neuen Wert setzen, damit er von den [!UICONTROL Data Element] in Platform-Tags aufgenommen werden kann.

## Demoseite {#demo-page}

Hier ist eine kleine Seite, die zeigt, wie Sie einen Wert in der Datenschicht ändern und ihn wie auf einer SPA an Audience Manager senden. Diese Funktion kann für detailliertere Änderungen modelliert werden, die erforderlich sind. Sie finden diese Demoseite [HIER](https://aam.enablementadobe.com/SPA-Launch.html).

## Festlegen der Datenschicht {#setting-the-data-layer}

Wie bereits erwähnt, muss beim Laden neuer Inhalte auf der Seite oder beim Ausführen einer Aktion auf der Site die Datenschicht dynamisch im Kopf der Seite festgelegt werden, BEVOR Platform-Tags aufgerufen werden und den Wert &quot;[!UICONTROL rules]&quot;ausführen, damit Platform-Tags die neuen Werte aus der Datenschicht aufnehmen und in den Audience Manager übertragen können.

Wenn Sie die oben aufgeführte Demosite aufrufen und sich die Seitenquelle ansehen, sehen Sie:

* Die Datenschicht befindet sich im Kopf der Seite, bevor Platform-Tags aufgerufen werden
* Der JavaScript im simulierten SPA-Link ändert die [!UICONTROL Data Layer] und ruft dann Platform-Tags auf (den `_satellite.track()` -Aufruf). Wenn Sie benutzerspezifische JavaScript-Ereignisse anstelle von [!UICONTROL Direct Call Rule] verwendet haben, ist die Lektion die gleiche. Ändern Sie zunächst die [!DNL data layer] und rufen Sie dann Platform-Tags auf.

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## Zusätzliche Ressourcen {#additional-resources}

* [SPA Diskussion auf den Adobe-Foren](https://forums.adobe.com/thread/2451022)
* [Referenzarchitektur-Sites, die zeigen, wie SPA in Platform-Tags implementiert werden](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Verwenden von Best Practices beim SPA in Adobe Analytics](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [Für diesen Artikel verwendete Demosite](https://aam.enablementadobe.com/SPA-Launch.html)
