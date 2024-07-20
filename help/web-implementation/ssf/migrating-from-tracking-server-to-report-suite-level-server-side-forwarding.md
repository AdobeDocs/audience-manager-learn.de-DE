---
title: Migration vom Tracking-Server zur serverseitigen Weiterleitung auf Report Suite-Ebene
description: Erfahren Sie, wie Sie die serverseitige Weiterleitung von Adobe Analytics-Daten an den Audience Manager auf Report Suite-Ebene und nicht auf Tracking-Server-Ebene aktivieren.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
role: Developer, Data Engineer
level: Intermediate
exl-id: 08b81e52-a28a-43e4-a284-df2460a43016
source-git-commit: 4adaade180545bcf5f911b7453a7e9939e2ed178
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Migration vom Tracking-Server zur serverseitigen Weiterleitung auf Report Suite-Ebene {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

In diesem Artikel und Video erfahren Sie, wie Sie die serverseitige Weiterleitung von [!DNL Analytics] Daten an den Audience Manager auf [!UICONTROL report suite]-Ebene und nicht auf [!UICONTROL tracking server] -Ebene aktivieren.

## Einführung {#introduction}

Wenn Sie über Adobe Audience Manager UND Adobe Analytics verfügen, können Sie die serverseitige Weiterleitung der [!DNL Analytics] -Daten an Audience Manager implementieren. Anstatt also zwei Treffer von Ihrer Seite zu senden (1 an [!DNL Analytics] und 1 an den Audience Manager), kann sie einen Treffer an [!DNL Analytics] senden, und [!DNL Analytics] leitet diese Daten an den Audience Manager weiter.

Wenn Sie dies bereits ausgeführt haben und vor Oktober 2017 aktiviert/implementiert haben, basiert die serverseitige Weiterleitung möglicherweise auf Ihrem [!UICONTROL Tracking Server] -Wert, der von der Adobe-Kundenunterstützung oder Adobe Consulting aktiviert werden musste. Ab Oktober 2017 können Sie jetzt die serverseitige Weiterleitung selbst konfigurieren und sie auf Report Suite-Ebene (Weiterleitung pro Report Suite) durchführen. Dies hat erhebliche Vorteile, die im Folgenden erläutert werden.

## [!UICONTROL Tracking server] Weiterleitung {#tracking-server-forwarding}

Ihr [!UICONTROL tracking server] ist der Ort, an den Sie Ihre [!DNL Analytics] -Daten senden, sowie die Domäne, in die die Bildanforderung und das Cookie geschrieben werden. Sie sollte in DTM oder [!DNL Experience Platform Launch] oder in der Datei [!DNL AppMeasurement.js] festgelegt werden und sieht in der Regel wie folgt aus, wobei Ihr Site- oder Geschäftsname &quot;mysite&quot;ersetzt:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Wenn die serverseitige Weiterleitung auf [!UICONTROL tracking server]-Ebene für die Weiterleitung eingerichtet ist, werden alle Treffer, die an diesen [!UICONTROL tracking server] gesendet werden (WENN der Experience Cloud ID-Dienst ebenfalls aktiviert ist), an Audience Manager weitergeleitet. Dies musste durch die Adobe-Kundenunterstützung oder Adobe Consulting aktiviert werden. Es sind auch diejenigen, die es deaktivieren können, nachdem Sie auf die [!UICONTROL report suite] -Weiterleitung umgestellt haben, wie unten beschrieben.

Wenn Sie sich nicht sicher sind, ob [!DNL tracking server forwarding] für Sie aktiviert ist, wenden Sie sich an die Adobe-Kundenunterstützung oder Adobe Consulting und sie sollten Sie darüber informieren können.

## [!UICONTROL Report-suite] Serverseitige Weiterleitung {#report-suite-level-server-side-forwarding}

Einer der größten Vorteile beim Wechsel zur [!UICONTROL report suite]-Weiterleitung von der [!UICONTROL tracking server]-Weiterleitung besteht darin, dass Sie jetzt &quot;Audience Analytics&quot;verwenden können. Dies ist die Möglichkeit, Audience Manager [!UICONTROL segments] zur detaillierten Segmentanalyse zurück an Adobe Analytics zu leiten. Diese großartige Funktion wird NICHT unterstützt, wenn Sie noch die [!UICONTROL tracking server] -Weiterleitung und nicht die [!UICONTROL report suite] -Weiterleitung verwenden. Weitere Informationen zum Audience Analytics finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Wichtiger Tipp {#additional-resources}

Wie im Video oben angegeben, sollten Sie sich an die Adobe-Kundenunterstützung oder Adobe Consulting wenden, sobald Sie alle [!UICONTROL report suites] für die Weiterleitung an den Audience Manager festgelegt haben und diese die [!UICONTROL tracking server]-Weiterleitung deaktivieren lassen. Dies ist kein Notfall für Sie, da sowohl die [!UICONTROL tracking server] Weiterleitung als auch die [!UICONTROL report suite] Weiterleitung nicht zu doppelten Treffern führt. Es empfiehlt sich jedoch, nur die [!UICONTROL report suite] Weiterleitung zu verwenden.

Wenn Sie die [!UICONTROL tracking server] Weiterleitung aktivieren, werden nicht nur Daten von [!UICONTROL report suites] weitergeleitet, die Sie nicht weiterleiten möchten, sondern in Zukunft, nachdem Sie (und alle Mitarbeiter in Ihrem Unternehmen) vergessen haben, dass die [!UICONTROL tracking server] Weiterleitung aktiviert ist, können Sie denken, dass die Daten für einen bestimmten [!UICONTROL report suite] nicht weitergeleitet werden. Dies liegt daran, dass sie nicht auf Report Suite-Ebene aktiviert ist, die Daten jedoch trotzdem aufgrund des [!UICONTROL tracking server] weitergeleitet werden. Dann verschwenden Sie Zeit und Geld, um herauszufinden, warum es weiterleitet und auch für AAM Server-Aufrufe bezahlt, die Sie nicht erwartet haben. Daher ist es empfehlenswert, die [!UICONTROL tracking server]-Weiterleitung zu deaktivieren, sobald Sie alle [!UICONTROL report suites] für die Weiterleitung festgelegt haben, die für Ihre geschäftlichen Anforderungen sinnvoll sind.
