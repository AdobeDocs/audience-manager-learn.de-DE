---
title: Migrieren vom Tracking-Server zur Server-seitigen Weiterleitung auf Report Suite-Ebene
description: Erfahren Sie, wie Sie die Server-seitige Weiterleitung von Adobe Analytics-Daten an Audience Manager auf einer Report Suite-Ebene anstelle einer Tracking-Server-Ebene aktivieren.
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

# Migrieren vom Tracking-Server zur Server-seitigen Weiterleitung auf Report Suite-Ebene {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

In diesem Artikel und in diesem Video erfahren Sie, wie Sie die Server-seitige Weiterleitung [!DNL Analytics] Daten an den Audience Manager auf einer [!UICONTROL report suite] statt auf einer [!UICONTROL tracking server] Ebene aktivieren.

## Einführung {#introduction}

Wenn Sie über Adobe Audience Manager UND Adobe Analytics verfügen, können Sie die Server-seitige Weiterleitung der [!DNL Analytics] an den Audience Manager implementieren. Das bedeutet, dass Ihre Seite nicht zwei Treffer (einen an [!DNL Analytics] und einen an den Audience Manager), sondern einen Treffer an [!DNL Analytics] senden kann, und [!DNL Analytics] leitet diese Daten an den Audience Manager weiter.

Wenn Sie diesen bereits eingerichtet haben und er vor Oktober 2017 aktiviert/implementiert wurde, basiert Ihre Server-seitige Weiterleitung möglicherweise auf Ihrer [!UICONTROL Tracking Server], die von der Adobe-Kundenunterstützung oder Adobe Consulting aktiviert werden musste. Seit Oktober 2017 können Sie die Server-seitige Weiterleitung jetzt selbst konfigurieren und auf Report Suite-Ebene durchführen (Weiterleitung pro Report Suite). Dies hat erhebliche Vorteile, die im Folgenden erläutert werden.

## [!UICONTROL Tracking server] {#tracking-server-forwarding}

Ihr [!UICONTROL tracking server] ist der Ort, an den Sie Ihre [!DNL Analytics] senden, sowie die Domain, in die die Bildanforderung und das Cookie geschrieben werden. Sie sollte in DTM oder [!DNL Experience Platform Launch] oder in der [!DNL AppMeasurement.js] festgelegt werden und sieht normalerweise wie folgt aus, wobei Ihr Site- oder Geschäftsname „mysite“ ersetzt:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Wenn die Server-seitige Weiterleitung für die Weiterleitung auf [!UICONTROL tracking server]-Ebene eingerichtet ist, wird jeder Treffer, der an diese [!UICONTROL tracking server] gesendet wird (wenn auch der Experience Cloud-ID-Dienst aktiviert ist), an den Audience Manager weitergeleitet. Dies musste durch die Adobe-Kundenunterstützung oder Adobe Consulting aktiviert werden. Sie sind auch diejenigen, die es deaktivieren können, NACHDEM Sie wie unten beschrieben zur [!UICONTROL report suite]-Weiterleitung gewechselt haben.

Wenn Sie sich nicht sicher sind, ob [!DNL tracking server forwarding] für Sie aktiviert ist, wenden Sie sich an die Kundenunterstützung von Adobe oder Adobe Consulting. Die Mitarbeiter sollten Ihnen in der Lage sein, dies mitzuteilen.

## Server-seitige Weiterleitung auf [!UICONTROL Report-suite] {#report-suite-level-server-side-forwarding}

Einer der größten Vorteile beim Übergang von der [!UICONTROL tracking server] zur [!UICONTROL report suite] besteht darin, dass Sie jetzt &quot;Audience Analytics&quot; verwenden können, d. h. die Möglichkeit, Audience Manager-[!UICONTROL segments] zur detaillierten Segmentanalyse zurück an Adobe Analytics weiterzuleiten. Diese großartige Funktion wird NICHT unterstützt, wenn Sie sich noch in der [!UICONTROL tracking server] und nicht in der [!UICONTROL report suite] befinden. Weitere Informationen zum Audience Analytics finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=de).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Wichtiger Tipp {#additional-resources}

Wie im obigen Video erklärt, sollten Sie sich, sobald alle [!UICONTROL report suites], die Sie an Audience Manager weiterleiten möchten, an die Adobe-Kundenunterstützung oder Adobe Consulting wenden und diese die [!UICONTROL tracking server] deaktivieren lassen. Dies ist kein Notfall, da sowohl die [!UICONTROL tracking server]- als auch die [!UICONTROL report suite] nicht zu doppelten Treffern führen. Es empfiehlt sich jedoch, nur die [!UICONTROL report suite] weiterzuleiten.

Wenn Sie die [!UICONTROL tracking server]-Weiterleitung aktiviert lassen, leitet sie möglicherweise nicht nur Daten von [!UICONTROL report suites] weiter, die Sie nicht weiterleiten möchten, sondern in Zukunft auch noch, wenn Sie (und alle Mitarbeiter in Ihrem Unternehmen) vergessen haben, dass [!UICONTROL tracking server]-Weiterleitung aktiviert ist, können Sie annehmen, dass die Daten nicht für eine bestimmte [!UICONTROL report suite] weitergeleitet werden. Dies liegt daran, dass sie auf der Report Suite-Ebene nicht aktiviert ist, aber die Daten aufgrund der [!UICONTROL tracking server] trotzdem weitergeleitet werden. Dann verschwenden Sie Zeit und Geld, um herauszufinden, warum es weiterleitet und auch für AAM-Server-Aufrufe bezahlt, die Sie nicht erwartet haben. Es empfiehlt sich daher, die [!UICONTROL tracking server] zu deaktivieren, sobald Sie über alle [!UICONTROL report suites] verfügen, die für Ihre geschäftlichen Anforderungen sinnvoll sind.
