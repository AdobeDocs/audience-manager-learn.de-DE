---
title: Identifizieren Ihrer Partner-ID oder Subdomäne
description: Erfahren Sie, wie Sie bei der Implementierung einiger Experience Cloud-Funktionen Ihre Partner-ID oder -Subdomäne identifizieren und an zwei Stellen diese ID in der Audience Manager-Benutzeroberfläche erhalten.
feature: Implementation Basics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
role: Developer, Data Engineer
level: Intermediate
exl-id: d3f4a12d-acc5-47b7-a38a-a6a14152bf3a
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Identifizierung der Subdomain Ihres Audience Managers {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

Bei der Implementierung einiger Experience Cloud-Funktionen müssen Sie wissen, was Ihr Audience Manager `Subdomain` ist (auch manchmal als Ihr `client ID` oder `Partner ID` bezeichnet). In diesem Video zeigen wir Ihnen zwei Orte, an denen Sie diese Informationen in der Audience Manager-Benutzeroberfläche erhalten können.

## Das Ende verraten... {#giving-away-the-ending}

Falls Sie lieber einfach reinspringen und es finden möchten, ohne dieses kurze Video anzuschauen, können Sie Ihr `Partner Subdomain` an zwei Stellen in der Benutzeroberfläche finden:

1. Wenn Sie bereits eine [!UICONTROL rule-based] -Eigenschaft erstellt haben, klicken Sie auf **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] befindet sich neben der Eigenschaft in der Liste der Eigenschaften in diesem Ordner und die URL enthält Ihre Subdomäne in die URL.
1. Wenn Sie in die Oberfläche **[!UICONTROL Tools]** > **[!UICONTROL Tags]** gehen und für Ihren Container auf **[!UICONTROL Get code]** klicken, befindet sich die Subdomäne am Ende der Akamai-Zeile.

Wenn Sie es mit diesen Schnellverweisen nicht schnell finden können, ist das Video eine kurze Zeitverpflichtung. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Jedem Adobe Experience Cloud-Kunden wird eine numerische ID zugewiesen, die häufig als &quot;PID&quot;oder Partner-ID bezeichnet wird. Dies ist nicht die ID, über die wir in diesem Artikel und Video sprechen. Stattdessen ist die &quot;Partner-Subdomain&quot;, die manchmal als Partner-ID bezeichnet wird, normalerweise eine Version des Kundennamens und die Subdomäne des Servers, an den die Daten gesendet werden. Wenn Ihr Unternehmen z. B. &quot;Bob&#39;s Knobs&quot;(alles, was natürlich Türknappen enthält) ist, dann ist es wahrscheinlich, dass Ihre Partner-Subdomäne &quot;bobsknobs&quot;ist, während die &quot;PID&quot;eher &quot;12345&quot;wäre. Normalerweise müssen Sie Ihre PID nicht kennen, aber Ihre Subdomain ist wichtig, damit Sie Ihre Audience Manager-Implementierung konfigurieren können.
>
