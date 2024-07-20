---
title: Validierung der globalen Geräte-ID
description: Erfahren Sie mehr über die Validierung von Geräte-IDs, die zur korrekten Formatierung an die globalen Datenquellen gesendet werden, und über Fehlermeldungen, wenn IDs falsch formatiert sind.
feature: Data Governance & Privacy
topics: mobile
activity: implement
doc-type: article
team: Technical Marketing
kt: 2977
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 0ff3f123-efb3-4124-bdf9-deac523ef8c9
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# Validierung der globalen Geräte-ID {#global-device-id-validation}

Geräte-Advertising-IDs (d. h. iDFA, GAID, Roku-ID) verfügen über Formatierungsstandards, die eingehalten werden müssen, damit sie im digitalen Werbe-Ökosystem verwendet werden können. Kunden und Partner können heute IDs in beliebige Formate in unsere globalen Datenquellen hochladen, ohne darüber informiert zu werden, ob die ID korrekt formatiert ist. Diese Funktion führt zur Validierung von Geräte-IDs, die zur korrekten Formatierung an die globalen Datenquellen gesendet werden, und bietet Fehlermeldungen, wenn IDs falsch formatiert sind. Wir unterstützen die Validierung für [!DNL iDFA], [!DNL Google Advertising] und [!DNL Roku IDs] beim Start.

## Übersicht über die Formatstandards {#overview-of-format-standards}

Im Folgenden finden Sie die globalen Geräte-Advertising-ID-Pools, die derzeit von AAM erkannt und unterstützt werden. Diese sind als freigegebene [!UICONTROL Data Sources] -Variablen implementiert, die von jedem Kunden oder Datenpartner verwendet werden können, der mit Daten arbeitet, die an Benutzer dieser Plattformen gebunden sind.

<table>
  <tr>
   <td>Plattform </td>
   <td>Source ID AAM Data </td>
   <td>ID-Format </td>
   <td>AAM PID </td>
   <td>Hinweise </td>
  </tr>
  <tr>
   <td>Google Android (GAID)</td>
   <td>20914</td>
   <td>32 Hexadezimalzahlen, im Allgemeinen als Beispiel 8-4-4-4-12<em>dargestellt, 97987bca-ae59-4c7d-94ba-ee4f19ab8c21<br/> </em> </td>
   <td>1352</td>
   <td>Diese ID muss in einer rohen/ungehashten/unveränderten Formularreferenz erfasst werden - <a href="https://play.google.com/about/monetization-ads/ads/ad-id/">https://play.google.com/about/monetization-ads/ads/ad-id/</a></td>
  </tr>
  <tr>
   <td>Apple iOS (IDFA)</td>
   <td>20915</td>
   <td>32 Hexenzahlen, allgemein als Beispiel 8-4-4-4-12 <em>angegeben, 6D92078A-8246-4BA4-AE5B-76104861E7DC<br /> </em> </td>
   <td>3560</td>
   <td>Diese ID muss in einer rohen/ungehashten/unveränderten Formularreferenz erfasst werden - <a href="https://support.apple.com/en-us/HT205223">https://support.apple.com/en-us/HT205223</a></td>
  </tr>
  <tr>
   <td>Roku (RIDA)</td>
   <td>121963</td>
   <td>32 Hexadezimalzahlen, im Allgemeinen als Beispiel 8-4-4-4-12 <em>dargestellt, </em> <em>fcb2a29c-315a-5e6b-bcfd-d889ba19aada</em></td>
   <td>11536</td>
   <td>Diese ID muss in einer rohen/ungehashten/unveränderten Formularreferenz erfasst werden - <a href="https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework">https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework</a> </td>
  </tr>
  <tr>
   <td>Microsoft Advertising ID (MAID)</td>
   <td>389146</td>
   <td>Numerische Zeichenfolge des Alphas</td>
   <td>14593</td>
   <td>Diese ID muss in einer rohen/ungehashten/unveränderten Formularreferenz erfasst werden - <a href="https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid">https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid</a><br/><a href="https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx">https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx</a></td>
  </tr>
  <tr>
   <td>Samsung DUID</td>
   <td>404660</td>
   <td>Beispiel für numerische Alpha-Zeichenfolge 7XCBNROQJQPYW</td>
   <td>15950</td>
   <td>Diese ID muss in einer rohen/ungehashten/unveränderten Formularreferenz erfasst werden - <a href="https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api">https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api</a> </td>
  </tr>
</table>

## Festlegen einer Advertising-ID in der App {#setting-an-advertising-identifier-in-the-app}

Das Festlegen der Advertiser-ID in der App ist in Wahrheit ein zweistufiger Prozess, der zunächst die Advertiser-ID abruft und dann an die Experience Cloud sendet. Nachstehend finden Sie Links zur Durchführung dieser Schritte.

1. ID abrufen
   1. [!DNL Apple] Informationen über den [!DNL advertising ID] finden Sie [HIER](https://developer.apple.com/documentation/adsupport/asidentifiermanager).
   1. Einige Informationen zum Festlegen des [!DNL advertiser ID] für [!DNL Android] -Entwickler finden Sie [HIER](http://android.cn-mirrors.com/google/play-services/id.html).
1. Senden Sie es mit der [!DNL setAdvertisingIdentifier] -Methode im SDK an die Experience Cloud.
   1. Informationen zur Verwendung von `setAdvertisingIdentifier` finden Sie in der [Dokumentation](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#set-an-advertising-identifier) für sowohl [!DNL iOS] als auch [!DNL Android].

`// iOS (Swift) example for using setAdvertisingIdentifier:`
`ACPCore.setAdvertisingIdentifier([AdvertisingId]) // ...where [AdvertisingId] is replaced by the actual advertising ID`

## DCS-Fehlernachrichten für falsche IDs  {#dcs-error-messaging-for-incorrect-ids}

Wenn eine falsche globale Geräte-ID (IDFA, GAID usw.) in Echtzeit an Audience Manager gesendet wird, wird beim Treffer ein Fehlercode zurückgegeben. Im Folgenden finden Sie ein Beispiel für einen zurückgegebenen Fehler, da die ID als [!DNL Apple IDFA] gesendet wird, der nur Großbuchstaben enthalten soll, und trotzdem gibt es in der ID eine Kleinbuchstabe &#39;x&#39;.

![Fehlerbild](assets/image_4_.png)

Eine Liste der Fehlercodes finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-error-codes.html?lang=en#api-and-sdk-code) .

## Onboarding globaler Geräte-IDs {#onboarding-global-device-ids}

Zusätzlich zur Echtzeit-Übermittlung globaler Geräte-IDs können Sie auch &quot;[!DNL onboard]&quot;-Daten (Upload) für die IDs verwenden. Dieser Vorgang ist mit dem Onboarding von Daten für Ihre Kunden-IDs (normalerweise über Schlüssel/Wert-Paare) identisch. Sie würden jedoch einfach die richtigen Data Source IDs verwenden, damit die Daten der globalen Geräte-ID zugewiesen werden. Die Dokumentation zum Onboarding-Prozess finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/sending-audience-data/batch-data-transfer-process/batch-data-transfer-overview.html?lang=en#implementation-integration-guides). Denken Sie daran, je nach verwendeter Plattform die globale Datenquellen-ID zu verwenden.

Wenn beim Onboarding-Prozess falsche globale Geräte-IDs gesendet werden, werden die Fehler im [[!DNL Onboarding Status Report]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reporting/onboarding-status-report.html?lang=en#reporting) angezeigt.

Im Folgenden finden Sie ein Beispiel eines Fehlers, der durch diesen Bericht ausgegeben wird:

![Fehlerbild](assets/image_5_.png)
