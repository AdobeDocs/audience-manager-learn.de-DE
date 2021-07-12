---
title: Identifizieren Ihrer Audience Manager-Partner-ID oder -Subdomäne
description: Bei der Implementierung einiger Experience Cloud-Funktionen müssen Sie wissen, was die "Partner-ID"Ihres Audience Managers ist (manchmal auch als "Kunden-ID"oder "Subdomäne"bezeichnet). In diesem Video zeigen wir Ihnen zwei Orte, an denen Sie diese ID in der Audience Manager-Benutzeroberfläche erhalten können.
feature: Implementierungsgrundlagen
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
role: Developer, Data Engineer
level: Intermediate
exl-id: d3f4a12d-acc5-47b7-a38a-a6a14152bf3a
source-git-commit: 4b91696f840518312ec041abdbe5217178aee405
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Identifizierung der Subdomain Ihres Audience Managers {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

Bei der Implementierung einiger Experience Cloud-Funktionen müssen Sie wissen, was Ihr Audience Manager `Subdomain` ist (auch manchmal als `client ID` oder `Partner ID` bezeichnet). In diesem Video zeigen wir Ihnen zwei Orte, an denen Sie diese Informationen in der Audience Manager-Benutzeroberfläche erhalten können.

## Das Ende verraten... {#giving-away-the-ending}

Falls Sie lieber einfach einspringen und es finden möchten, ohne dieses kurze Video anzuschauen, können Sie Ihr `Partner Subdomain` an zwei Stellen in der Benutzeroberfläche finden:

1. Wenn Sie bereits eine [!UICONTROL rule-based] [!UICONTROL trait] erstellt haben, klicken Sie auf **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] neben der  [!UICONTROL trait] in der Liste von  [!UICONTROL traits] in diesem Ordner befindet, und die URL enthält Ihre Subdomäne in die URL.
1. Wenn Sie die Oberfläche **[!UICONTROL Tools]** > **[!UICONTROL Tags]** aufrufen und für Ihren Container auf **[!UICONTROL Get code]** klicken, befindet sich die Subdomain am Ende der Akamai-Zeile

Wenn Sie es mit diesen Schnellverweisen nicht schnell finden können, ist das Video eine kurze Zeitverpflichtung. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Jedem Adobe Experience Cloud-Kunden wird eine numerische ID zugewiesen, die häufig als &quot;PID&quot;oder Partner-ID bezeichnet wird. Dies ist nicht die ID, über die wir in diesem Artikel und Video sprechen. Stattdessen ist die &quot;Partner-Subdomain&quot;, die manchmal als Partner-ID bezeichnet wird, normalerweise eine Version des Kundennamens und die Subdomäne des Servers, an den die Daten gesendet werden. Wenn Ihr Unternehmen z. B. &quot;Bob&#39;s Knobs&quot;(alles, was natürlich Türknappen enthält) ist, dann ist es wahrscheinlich, dass Ihre Partner-Subdomäne &quot;bobsknobs&quot;ist, während die &quot;PID&quot;eher &quot;12345&quot;wäre. Normalerweise müssen Sie Ihre PID nicht kennen, aber Ihre Subdomain ist wichtig, damit Sie Ihre Audience Manager-Implementierung konfigurieren können.

