---
title: Aktualisierung auf Adobe Audience Manager DIL Version 8.0 (oder höher)
description: In diesem Artikel finden Sie Anweisungen und Empfehlungen zum Aktualisieren des Adobe Audience Manager (AAM) Data Integration Library (DIL)-Codes auf Version 8.0 oder höher. Dies bezieht sich auf die „Client-seitige“ DIL-Implementierung und nicht auf die Server-seitige Weiterleitung von Adobe Analytics-Daten. Es umfasst DTM, Launch durch Adobe und Implementierungen ohne Adobe Tag Manager-Lösung.
feature: DIL Implementation
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1841
role: Developer, Data Engineer
level: Intermediate
exl-id: 8c1e6ed5-0f21-427b-a681-0ecb020a0e60
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Aktualisierung auf Adobe Audience Manager DIL Version 8.0 (oder höher) {#updating-to-adobe-audience-manager-s-dil-version-or-greater}

In diesem Artikel finden Sie Anweisungen und Empfehlungen zum Aktualisieren des Adobe Audience Manager (AAM) [!DNL Data Integration Library] (DIL)-Codes auf Version 8.0 oder höher. Dies bezieht sich auf die „Client-seitige“ DIL-Implementierung und nicht auf die Server-seitige Weiterleitung von Adobe Analytics-Daten. Es umfasst DTM, Launch durch Adobe und Implementierungen ohne Adobe Tag Manager-Lösung.

## Überblick {#overview}

Mit dem [!DNL Data Integration Library]-Code (DIL) von Audience Manager können Sie AAM auf Ihrer Website implementieren*. Bei der Implementierung früherer Versionen von DIL war es nicht erforderlich, auch den Experience Cloud ID Service (ECID) von Adobe zu implementieren (obwohl dies eine sehr gute Idee war). Ab DIL Version 8.0 besteht eine feste Abhängigkeit von ECID Version 3.3 oder höher. Wenn Sie DIL 8.0 oder höher ohne ECID 3.3 oder mit einer früheren Version implementieren, wird eine Fehlermeldung angezeigt und die Implementierung funktioniert nicht. Da Sie AAM auf verschiedene Weise implementieren können, haben wir diese Seite erstellt, auf der Sie einige Schritte sowie Empfehlungen finden. Nachfolgend finden Sie diese Schritte und Empfehlungen aufgeschlüsselt nach Plattform/Implementierungsmethode. Weitere Informationen zu DIL finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=de).

* Wie auf der Beschreibung dieser Seite angegeben, umfasst dies nur „Client-seitige“ DIL-Implementierungen, die von AAM-Kunden ohne Adobe Analytics verwendet werden. Wenn Sie über Adobe Analytics verfügen, sollten Sie die Server-seitige Weiterleitungsmethode zur Implementierung von AAM verwenden. Diese Methode wird in der [Dokumentation](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html?lang=de) beschrieben.

## Duplizierte und veraltete Elemente und Methoden {#duplicate-and-deprecated-elements-and-methods}

In früheren Versionen von DIL und ECID gab es doppelte Methoden (Methoden, die sowohl in DIL als auch in ECID dieselbe Funktion ausführen), was zu Verwirrung hinsichtlich der zu verwendenden führte. In der Regel mussten Sie beide verwenden und abgleichen, und diese Botschaft wurde unseren Kunden nicht gut vermittelt. Ab DIL 8.0 sind diese doppelten Methoden und Elemente in DIL veraltet. Es wird empfohlen, die ECID-Version zu verwenden.

Beispiel:

* Bei Verwendung von [!DNL DIL.create] werden einige Elemente nicht mehr unterstützt, stattdessen sollten Sie die ECID-Elemente verwenden. Diese Elemente werden in der (Dokumentation[[!DNL DIL.create]  beschrieben](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html?lang=de).
* Die Methode auf [!DNL idSync]-Instanzebene wird ebenfalls nicht mehr unterstützt, wie in der (Dokumentation[ der Methode ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-instance-methods.html?lang=de).

## ID mit einer Kunden-ID synchronisieren {#id-syncing-with-a-customer-id}

In AAM können Sie Ihre UUID (anonyme eindeutige Benutzer-ID) auf dem Computer mit einer Kunden-ID synchronisieren, sodass Sie Offline-Daten über diesen Kunden hochladen und mit seinem Online-Verhalten verknüpfen können, um Ihre Kunden besser zu verstehen. In der Vergangenheit geschah dies auf eine von zwei Arten:

* Die Methode auf Instanzebene [!DNL idSync]
* Das [!DNL declaredId] Element in [!DNL DIL.create]

Wenn Sie eine dieser älteren Methoden zur Synchronisierung mit einer Kunden-ID verwendet haben, wird dringend empfohlen, auf die Verwendung der [!DNL setCustomerIDs]-Methode zu aktualisieren, die Teil des ECID-Service ist. Weitere Informationen zu [!DNL setCustomerIDs] finden Sie in der [ der Methode ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=de).

**Schnelltipp:** Sie zuvor eine der oben genannten Methoden verwendet haben, haben Sie auf den AAM-[!UICONTROL Data Source] mit der [!UICONTROL Data Source]-ID (auch „DPID“ genannt) verwiesen. Bei der Aktualisierung auf [!DNL setCustomerIDs] müssen Sie stattdessen das &quot;[!UICONTROL Data Source]&quot; des AAM-[!UICONTROL Integration Code] verwenden. Er verweist immer noch auf denselben [!UICONTROL Data Source], ist aber nur eine andere Kennung. Dies wird im folgenden Video gezeigt.

>[!VIDEO](https://video.tv.adobe.com/v/23873/?quality=12)

In den folgenden Abschnitten werden die Schritte und Empfehlungen für die Aktualisierung auf DIL 8.0 auf Grundlage Ihrer Implementierungsmethode aufgeführt:

## Aktualisieren auf DIL 8.0 in Adobe Experience Platform-Tags {#updating-to-dil-in-experience-platform-launch}

Grundlegende Schritte zum Aktualisieren auf DIL 8.0

1. Wenn Sie DIL vor Version 8.0 verwenden, wechseln Sie vor dem Upgrade zur DIL-Konfiguration in der AAM-Erweiterung, und notieren Sie sich alle erweiterten Optionen, die Sie verwenden (zur Verwendung in einem nachfolgenden Schritt).
1. Aktualisieren Sie Ihre AAM-Erweiterung auf Version 8.0 oder höher.
1. Stellen Sie sicher, dass Ihre Experience Cloud ID Service-Erweiterung Version 3.3.0 oder höher ist.
1. Aktivieren Sie für alle veralteten Methoden/Elemente (z. B. `disableIDSyncs`), die sich in Ihrer AAM-Erweiterung vor 8.0 oder in benutzerdefiniertem Code für DIL befanden, die ECID-Methoden in der ECID-Erweiterung.

   1. (DIL) `disableDestinationPublishingIframe` -> (ECID) `disableIdSyncs`
   1. (DIL) `disableIDSyncs` -> (ECID) `disableIdSyncs`
   1. (DIL) `iframeAkamaiHTTPS` -> (ECID) `dSyncSSLUseAkamai`
   1. (DIL) `declaredId` -> (ECID) `setCustomerIDs`

1. Veröffentlichen Sie die Änderungen.

>[!VIDEO](https://video.tv.adobe.com/v/23874/?quality=12)

## Aktualisieren auf DIL 8.0 in Adobe DTM {#updating-to-dil-in-adobe-dtm}

1. Aktualisieren Sie Ihr AAM-Tool auf Version 8.0 oder höher. Diese Versionseinstellung befindet sich im Abschnitt „Allgemein“ des AAM-Tools.
1. Notieren Sie sich veraltete Methoden/Elemente (z. B. `disableIDSyncs`) im benutzerdefinierten Code des AAM-Tools von vor 8.0 für DIL (damit Sie sie dem ECID-Tool hinzufügen können) und entfernen Sie sie dann aus dem benutzerdefinierten [!DNL DIL code] im AAM-Tool.
1. Aktualisieren Sie Ihre Experience Cloud ID Service-Erweiterung auf Version 3.3.0 oder höher
1. Fügen Sie die erweiterten Optionen zum ECID-Tool hinzu, das Sie aus dem benutzerdefinierten Code des AAM-Tools entfernt haben.
1. Veröffentlichen der Änderungen

## Aktualisierung auf DIL 8.0 ohne Adobe Tag Management-Lösung {#additional-resources}

Wenn Sie Ihren Code direkt auf der Seite aktualisieren, können Sie ältere Elemente einfach durch neuere Elemente ersetzen. Dies gilt nicht für Fälle, in denen Sie, wie oben beschrieben, Methoden/Elemente von DIL in ECID verschieben müssen. In diesem Fall ersetzen Sie einfach die alte Methode/das alte Element am DIL-Speicherort durch die ECID-Methode/das alte Element am ECID-Speicherort.

Dasselbe gilt für Tag-Manager, die nicht mit Adobe arbeiten. Wenn Sie die alten Versionen in dieser Tag-Management-Lösung haben, ersetzen Sie sie durch den neuen Code, wie in den folgenden Schritten beschrieben.

1. Aktualisieren Sie Ihre DIL-Bibliothek auf die neueste Version (8.0 oder höher). Sie benötigen den neuesten DIL-Code von der Adobe Consulting- oder Adobe-Kundenunterstützung, da er derzeit nicht an einem öffentlichen Speicherort verfügbar ist. Ersetzen Sie dann einfach den alten DIL-Bibliotheks-Code durch den neuen DIL-Bibliotheks-Code und fahren Sie mit dem nächsten Schritt fort (hören Sie jetzt nicht auf oder Sie stoßen auf Probleme, ha).
1. Installieren Sie [!DNL ECID Service] oder aktualisieren Sie Ihre vorhandene Version auf 3.3.0 oder höher. Sie können die neueste Version des Experience Cloud ID-Service [von unserer GitHub-Seite) ](https://github.com/Adobe-Marketing-Cloud/id-service/releases). Wenn Sie dabei Hilfe benötigen, lesen Sie die [Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de) oder wenden Sie sich an einen Adobe-Berater.

1. Stellen Sie sicher, dass veraltete Methoden oder Elemente, die sich in Ihrem benutzerdefinierten Code für DIL befinden, in die ECID-Methoden verschoben werden:

   1. (DIL) `disableDestinationPublishingIframe` -> (ECID) `disableIdSyncs`

      [Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/disableidsync.html?lang=de)

   1. (DIL) `disableIDSyncs` -> (ECID) `disableIdSyncs`

      [Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/disableidsync.html?lang=de)

   1. (DIL) `iframeAkamaiHTTPS` -> (ECID) `idSyncSSLUseAkamai`

      [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html?lang=de)

   1. (DIL) `declaredId` -> (ECID) `setCustomerIDs`

      [Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=de)
