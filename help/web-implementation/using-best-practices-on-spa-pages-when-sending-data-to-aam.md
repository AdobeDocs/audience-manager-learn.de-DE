---
title: Verwenden Sie Best Practices auf SPA-Seiten, wenn Sie Daten an AAM senden
description: Erfahren Sie mehr über Best Practices für das Senden von Daten von Single Page Applications (SPA) an Adobe Audience Manager (AAM). Dieser Artikel konzentriert sich auf die Verwendung von Experience Platform-Tags, der empfohlenen Implementierungsmethode.
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

# Verwenden Sie Best Practices auf SPA-Seiten, wenn Sie Daten an AAM senden {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

In diesem Dokument werden mehrere Best Practices für das Senden von Daten von Single Page Applications (SPA) an Adobe Audience Manager (AAM) beschrieben. Dieser Artikel konzentriert sich auf die Verwendung von [!UICONTROL Experience Platform tags], der empfohlenen Implementierungsmethode.

## Erste Hinweise

* Bei den folgenden Elementen wird davon ausgegangen, dass Sie Platform-Tags zur Implementierung auf Ihrer Site verwenden. Wenn Sie keine Platform-Tags verwenden, gelten die Überlegungen trotzdem, Sie müssen sie jedoch an Ihre Implementierungsmethode anpassen.
* Alle SPAs sind unterschiedlich, sodass Sie möglicherweise einige der folgenden Elemente anpassen müssen, um Ihre Anforderungen optimal zu erfüllen. Adobe möchte jedoch einige Best Practices austauschen, über die Sie beim Senden von Daten von SPA-Seiten an Audience Manager nachdenken müssen.

## Einfaches Diagramm zum Arbeiten mit SPAs und AAM in Experience Platform-Tags (ehemals Launch){#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![SPA für AAM in Tags](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Wie bereits erwähnt, ist dies ein vereinfachtes Diagramm dazu, wie SPA-Seiten in einer Adobe Audience Manager-Implementierung (ohne Adobe Analytics) mit Platform-Tags verarbeitet werden. Wie Sie sehen können, ist dies relativ einfach, wobei die große Entscheidung darin besteht, wie Sie Platform-Tags eine Änderung der Ansicht (oder eine Aktion) kommunizieren.

## Auslösen von Tags auf der SPA-Seite {#triggering-launch-from-the-spa-page}

Zwei der gebräuchlichsten Methoden zum Auslösen einer Regel in Platform-Tags (und damit zum Senden von Daten an Audience Manager) sind:

* Festlegen benutzerdefinierter JavaScript-Ereignisse (siehe Beispiel [HIER](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) mit Adobe Analytics)
* Verwenden eines [!UICONTROL Direct Call Rule]

In diesem Audience Manager-Beispiel verwenden Sie einen [!UICONTROL Direct Call rule] in Platform-Tags, um den Trigger des Treffers an Audience Manager weiterzuleiten. Wie Sie in den nächsten Abschnitten sehen werden, wird dies nützlich, indem Sie die [!UICONTROL Data Layer] auf einen neuen Wert setzen, damit sie von den [!UICONTROL Data Element] in Platform-Tags aufgenommen werden können.

## Demoseite {#demo-page}

Hier ist eine kleine Seite, die das Ändern eines Werts in der Datenschicht und das Senden an Audience Manager zeigt, wie Sie es auch auf einer SPA-Seite tun können. Diese Funktion kann für komplexere Änderungen modelliert werden, die erforderlich sind. Diese Demoseite finden Sie [HIER](https://aam.enablementadobe.com/SPA-Launch.html).

## Festlegen der Datenschicht {#setting-the-data-layer}

Wie bereits erwähnt, muss beim Laden neuer Inhalte auf der Seite oder beim Ausführen einer Aktion auf der Site durch eine Person die Datenschicht dynamisch im Kopf der Seite festgelegt werden, BEVOR Platform-Tags aufgerufen werden und die [!UICONTROL rules] ausführen, damit Platform-Tags die neuen Werte aus der Datenschicht übernehmen und in Audience Manager übertragen können.

Wenn Sie zur oben aufgeführten Demo-Site gehen und sich die Seitenquelle ansehen, sehen Sie Folgendes:

* Die Datenschicht befindet sich im Kopf der Seite, vor dem Aufruf von Platform-Tags
* Der JavaScript im simulierten SPA-Link ändert die [!UICONTROL Data Layer] und ruft dann Platform-Tags auf (den `_satellite.track()`-Aufruf). Wenn Sie benutzerdefinierte JavaScript-Ereignisse anstelle dieses [!UICONTROL Direct Call Rule] verwenden, ist die Lektion dieselbe. Ändern Sie zunächst die [!DNL data layer] und rufen Sie dann Platform-Tags auf.

>[!VIDEO](https://video.tv.adobe.com/v/38108/?quality=12&captions=ger)

## Zusätzliche Ressourcen {#additional-resources}

* [SPA in den Adobe-Foren](https://forums.adobe.com/thread/2451022)
* [Referenz-Sites zur Architektur, die zeigen, wie SPA in Platform-Tags implementiert wird](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Verwenden von Best Practices beim Tracking von SPAs in Adobe Analytics](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [Demo-Site für diesen Artikel verwendet](https://aam.enablementadobe.com/SPA-Launch.html)
