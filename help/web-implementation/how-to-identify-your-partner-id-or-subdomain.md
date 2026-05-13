---
title: So identifizieren Sie Ihre Partner-ID oder Subdomain
description: Erfahren Sie, wie Sie Ihre Partner-ID oder Subdomain identifizieren, wenn Sie einige Experience Cloud-Funktionen implementieren, und an zwei Stellen können Sie diese ID in der Audience Manager-Benutzeroberfläche erhalten.
feature: Implementation Basics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
role: Developer
level: Intermediate
exl-id: d3f4a12d-acc5-47b7-a38a-a6a14152bf3a
TQID: https://experienceleague.adobe.com/ZObq0VjU8IEiaQSL4emTTRXdTgBvjiDfzztHFc7rO-g
product_v2:
  - id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1
feature_v2:
  - id: a8b0238e-1d43-4679-a3b4-5ba1bad83baa
subfeature_v2:
  - id: f0bb1502-9f96-4d5e-a596-06876fe34ea0
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 3152e8fc51e0e06c90c17dce0aa203a27995e88d
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 0%

---

# Identifizieren der Audience Manager-Subdomain {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

Bei der Implementierung einiger Experience Cloud-Funktionen müssen Sie wissen, was Ihr Audience Manager-`Subdomain` ist (manchmal auch als Ihr `client ID` oder `Partner ID` bezeichnet). In diesem Video zeigen wir Ihnen zwei Orte, an denen Sie diese Informationen in der Audience Manager-Benutzeroberfläche erhalten.

## Das Ende verraten… {#giving-away-the-ending}

Wenn Sie lieber einfach hineinspringen und es finden möchten, ohne sich dieses kurze Video anzusehen, können Sie Ihre `Partner Subdomain` an zwei Stellen in der Benutzeroberfläche finden:

1. Wenn Sie bereits eine [!UICONTROL rule-based] Eigenschaft erstellt haben, klicken Sie auf **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] befindet sich neben der Eigenschaft in der Liste der Eigenschaften in diesem Ordner, und die URL enthält Ihre Subdomain in der URL.
1. Wenn Sie in der Benutzeroberfläche von **[!UICONTROL Tools]** > **[!UICONTROL Tags]** auf **[!UICONTROL Get code]** für Ihren Container klicken, befindet sich die Subdomain am Ende der Akamai-Zeile

Wenn Sie es mit diesen Kurzverweisen nicht schnell finden können, ist das Video ein kurzer Zeitaufwand. :)

>[!VIDEO](https://video.tv.adobe.com/v/40888/?captions=ger&quality=12)

>[!IMPORTANT]
>
>Jedem Kunden der Adobe Experience Cloud ist eine numerische ID zugewiesen. Diese wird häufig als „PID“ oder Partner-ID bezeichnet. Dies ist nicht die ID, über die wir in diesem Artikel und Video sprechen. Stattdessen ist die „Partner-Subdomain“, die manchmal auch als Partner-ID bezeichnet wird, in der Regel eine Version des Client-Namens und ist die Subdomain des Servers, an den die Daten gesendet werden. Wenn Ihr Unternehmen beispielsweise „Bob&#39;s Knobs“ ist (alle Dinge, die Türknäufe, natürlich, haha), ist es wahrscheinlich, dass Ihre Partner-Subdomain „bobsknobs“ wäre, während die „PID“ eher so etwas wie „12345“ wäre. Normalerweise müssen Sie Ihre PID nicht kennen. Ihre Subdomain ist jedoch wichtig, damit Sie Ihre Audience Manager-Implementierung konfigurieren können.
>
