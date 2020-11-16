---
title: Identifizieren der Partner-ID oder Subdomäne Ihres Audience Managers
description: Bei der Implementierung einiger Experience Cloud-Funktionen müssen Sie wissen, was Ihr Audience Manager "Partner-ID"ist (auch als "Client-ID"oder "Subdomäne"bezeichnet). In diesem Video zeigen wir Ihnen zwei Orte, an denen Sie diese ID in der Benutzeroberfläche des Audience Managers abrufen können.
feature: implementation basics
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
translation-type: tm+mt
source-git-commit: a108c51fdad66f4e7974eb96609b6d8f058cb6ff
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---


# Identifizieren der Subdomäne des Audience Managers {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

Bei der Implementierung einiger Experience Cloud-Funktionen müssen Sie wissen, was Ihr Audience Manager `Subdomain` ist (auch als Ihre `client ID` oder `Partner ID`). In diesem Video zeigen wir Ihnen zwei Orte, an denen Sie diese Informationen in der Benutzeroberfläche des Audience Managers abrufen können.

## Das Ende verraten... {#giving-away-the-ending}

Falls Sie lieber einfach einspringen und es ohne dieses kurze Video finden möchten, können Sie Ihre `Partner Subdomain` an zwei Stellen in der Benutzeroberfläche finden:

1. Wenn Sie bereits eine [!UICONTROL rule-based] erstellt haben, klicken Sie auf [!UICONTROL trait]**[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] neben dem Ordner [!UICONTROL trait] in der Liste von [!UICONTROL traits] in diesem Ordner und die URL enthält Ihre Subdomäne in der URL.
1. Wenn Sie auf der **[!UICONTROL Tools]** >- **[!UICONTROL Tags]** Oberfläche auf **[!UICONTROL Get code]** Ihren Container klicken, wird die Subdomäne an das Ende der Akamai-Zeile ausgerichtet

Wenn Sie es mit diesen schnellen Referenzen nicht schnell finden können, ist das Video eine kurze Zeitverpflichtung. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Jedem Kunden des Adobe Experience Cloud wird eine numerische ID zugewiesen, die oft als &quot;PID&quot;oder Partner-ID bezeichnet wird. Dies ist nicht die ID, über die wir in diesem Artikel und Video sprechen. Stattdessen handelt es sich bei der &quot;Partner-Subdomäne&quot;, die manchmal auch als Partner-ID bezeichnet wird, in der Regel um eine Version des Kundennamens und die Subdomäne des Servers, an den die Daten gesendet werden. Wenn Ihre Firma z. B. &quot;Bob&#39;s Knobs&quot; ist (alle Dinge Türklinken, natürlich haha), dann ist es wahrscheinlich, dass Ihre Partner-Subdomäne &quot;bobsknobs&quot; wäre, während die &quot;PID&quot; eher &quot;12345&quot; wäre. Normalerweise müssen Sie Ihre PID nicht kennen, aber Ihre Subdomäne ist wichtig zu wissen, damit Sie Ihre Audience Manager-Implementierung konfigurieren können.
