---
title: Migrieren der Audience Manager-Implementierung Ihrer Site von Client-seitiger DIL zur Server-seitigen Weiterleitung
description: Erfahren Sie, wie Sie die Audience Manager-Implementierung Ihrer Site (AAM) von Client-seitiger DIL zur Server-seitigen Weiterleitung migrieren. Dieses Tutorial gilt, wenn Sie sowohl AAM als auch Adobe Analytics verwenden und Treffer von der Seite mithilfe von DIL (Data Integration Library)-Code an AAM senden sowie Treffer von der Seite an Adobe Analytics senden.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: tutorial
team: Technical Marketing
kt: 1778
role: Developer, Data Engineer
level: Intermediate
exl-id: bcb968fb-4290-4f10-b1bb-e9f41f182115
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '2333'
ht-degree: 0%

---

# Migrieren der Audience Manager-Implementierung Ihrer Site von Client-seitiger DIL zur Server-seitigen Weiterleitung {#migrating-your-site-s-aam-implementation-from-client-side-dil-to-server-side-forwarding}

Dieses Tutorial gilt für Sie, wenn Sie sowohl Adobe Audience Manager (AAM) als auch Adobe Analytics haben und derzeit einen Treffer von der Seite an AAM senden, indem Sie DIL ([!DNL Data Integration Library])-Code verwenden, und auch einen Treffer von der Seite an Adobe Analytics senden. Da Sie beide Lösungen haben und beide Teil von Adobe Experience Cloud sind, haben Sie die Möglichkeit, die Best Practice der Aktivierung der Server-seitigen Weiterleitung zu befolgen, mit der die [!DNL Analytics] Datenerfassungs-Server Site-Analysedaten in Echtzeit an Audience Manager weiterleiten können, anstatt Client-seitigen Code einen zusätzlichen Treffer von der Seite an AAM senden zu lassen. Dieses Tutorial führt Sie durch die Schritte, die für den Wechsel von der älteren Client-seitigen DIL-Implementierung zur neueren Server-seitigen Weiterleitungsmethode erforderlich sind.

## Client-seitig (DIL) vs. Server-seitig {#client-side-dil-vs-server-side}

Wenn Sie diese beiden Methoden vergleichen und gegenüberstellen, um Adobe Analytics-Daten in AAM zu importieren, können Sie zunächst die Unterschiede in der folgenden Abbildung visualisieren:

![Client-seitig zu Server-seitig](assets/client-side_vs_server-side_aam_implementation.png)

### Client-seitige DIL-Implementierung {#client-side-dil-implementation}

Wenn Sie diese Methode verwenden, um Adobe Analytics-Daten in AAM zu importieren, erhalten Sie zwei Treffer von Ihren Web-Seiten: einen, der zu [!DNL Analytics] geht, und einen, der zu AAM geht (nachdem die [!DNL Analytics] Daten auf der Web-Seite kopiert wurden). [!UICONTROL Segments] werden von AAM an die Seite zurückgegeben, wo sie für die Personalisierung usw. verwendet werden können. Dies wird als veraltete Implementierung betrachtet und nicht mehr empfohlen.

Abgesehen von der Tatsache, dass dies nicht den Best Practices entspricht, umfassen die Nachteile der Verwendung dieser Methode Folgendes:

* Zwei Treffer von der Seite statt nur einem
* Die Server-seitige Weiterleitung ist für die Echtzeitfreigabe von AAM-Zielgruppen an [!DNL Analytics] erforderlich, sodass Client-seitige Implementierungen diese Funktion (und möglicherweise weitere zukünftige Funktionen) nicht zulassen

Es wird empfohlen, zu einer Server-seitigen Weiterleitungsmethode der AAM-Implementierung zu wechseln.

### Server-seitige Weiterleitungsimplementierung {#server-side-forwarding-implementation}

Wie in der Abbildung oben gezeigt, kommt ein Treffer von der Web-Seite zu Adobe Analytics. [!DNL Analytics] leitet diese Daten in Echtzeit an AAM weiter, und die Besucher werden in AAM-Eigenschaften und -[!UICONTROL segments] ausgewertet, so als ob der Treffer direkt von der Seite gekommen wäre.

[!UICONTROL Segments] werden beim selben Echtzeit-Treffer an [!DNL Analytics] zurückgegeben, der die Antwort zur Personalisierung an die Web-Seite weiterleitet usw.

Es gibt keinen zeitlichen Nachteil bei der Umstellung auf Server-seitige Weiterleitung. Adobe empfiehlt dringend, dass jeder, der sowohl Audience Manager als auch [!DNL Analytics] hat, diese Implementierungsmethode verwendet.

## Sie haben zwei Hauptaufgaben {#you-have-two-main-tasks}

Es gibt eine ganze Menge Informationen auf dieser Seite, und es ist natürlich alles wichtig. Es **sich jedoch auf zwei wichtige Dinge, die Sie tun müssen**:

1. Ändern Sie den Code von Client-seitigem DIL-Code in serverseitigen Weiterleitungscode
1. Wechseln Sie in der [!DNL Analytics] [!DNL Admin Console], um die tatsächliche Weiterleitung von Daten zu starten (pro [!UICONTROL report suite])

Wenn Sie eine dieser Aufgaben überspringen, funktioniert die Server-seitige Weiterleitung nicht ordnungsgemäß. Diesem Dokument wurden Schritte und zusätzliche Daten hinzugefügt, damit Sie diese beiden Schritte für Ihr Setup korrekt ausführen können.

## Implementierungsoptionen {#implementation-options}

Wenn Sie von der Client- zur Server-seitigen Weiterleitung wechseln, besteht eine der Aufgaben darin, den Code in den neuen Server-seitigen Weiterleitungs-Code zu ändern. Dies geschieht mithilfe einer der folgenden Optionen:

* Adobe Experience Platform Tags - Adobes empfohlene Implementierungsoption für Web-Eigenschaften. Sie werden sehen, dass dies eine einfache Aufgabe ist, da Platform Tags die ganze harte Arbeit für Sie erledigt hat.
* Auf der Seite - Sie können den neuen SSF-Code auch direkt in die `doPlugins` in Ihrer `appMeasurement.js`-Datei einfügen, wenn Sie Adobe Launch (noch) nicht verwenden
* Andere Tag-Manager : Diese können wie die vorherige Option (auf der Seite) behandelt werden, da der SSF-Code weiterhin in `doPlugins` abgelegt wird, wo auch immer der andere Tag-Manager den [!DNL AppMeasurement]-Code speichert

Wir werden die einzelnen unten stehenden Schritte im Abschnitt _Aktualisieren des Codes_ ansehen.

## Implementierungsschritte {#implementation-steps}

Die folgenden Schritte beschreiben die Implementierung.

### Schritt 0: Voraussetzung: Experience Cloud ID Service (ECID) {#step-prerequisite-experience-cloud-id-service-ecid}

Die wichtigste Voraussetzung für die Umstellung auf die Server-seitige Weiterleitung ist die Implementierung des Experience Cloud ID-Service. Dies ist am einfachsten, wenn Sie Experience Platform Launch verwenden. In diesem Fall installieren Sie einfach die ECID-Erweiterung und sie erledigt den Rest.

Wenn Sie ein Nicht-Adobe-TMS oder gar kein TMS verwenden, implementieren Sie ECID, um (**)** anderen Adobe-Lösungen auszuführen. Weitere Informationen finden Sie in [ECID](https://experienceleague.adobe.com/docs/id-service/using/home.html)Dokumentation. Die einzige weitere Voraussetzung betrifft die Code-Versionen. Wenn Sie also in den folgenden Schritten einfach die neuesten Versionen des Codes anwenden, ist alles in Ordnung.

>[!NOTE]
>
>Bitte lesen Sie dieses gesamte Dokument, bevor Sie implementieren. Der folgende Abschnitt „Timing“ enthält wichtige Informationen dazu *wann* jedes Element implementiert werden sollte, einschließlich ECID (falls noch nicht implementiert).

### Schritt 1: Zeichnen Sie die aktuell verwendeten Optionen aus DIL Code auf {#step-record-currently-used-options-from-dil-code}

Wenn Sie bereit sind, von Client-seitigem DIL-Code zur Server-seitigen Weiterleitung zu wechseln, besteht der erste Schritt darin, alles zu identifizieren, was Sie mit DIL-Code tun, einschließlich benutzerdefinierter Einstellungen und Daten, die an AAM gesendet werden. Zu den zu beachtenden Dingen gehören:

* Normale [!DNL Analytics] mit dem `siteCatalyst.init` DIL-Modul - Sie müssen sich darüber keine Gedanken machen, da die Aufgabe darin besteht, die normalen [!DNL Analytics] einfach zu senden, und das geschieht, indem die Server-seitige Weiterleitung aktiviert ist.
* Partner-Subdomain - Notieren Sie sich in der `DIL.create` den `partner`. Diese wird als „Partner-Subdomain“ oder manchmal auch „Partner-ID“ bezeichnet und wird benötigt, wenn Sie den neuen Server-seitigen Weiterleitungs-Code platzieren.
* [!DNL Visitor Service Namespace] - Wird auch als &quot;[!DNL Org ID]&quot; oder &quot;[!DNL IMS Org ID]&quot; bezeichnet. Sie benötigen diese ebenfalls, wenn Sie den neuen Server-seitigen Weiterleitungs-Code einrichten. Notieren Sie sich das.
* containerNSID, uuuidCookie und andere erweiterte Optionen - Notieren Sie sich alle zusätzlichen erweiterten Optionen, die Sie verwenden, damit Sie sie auch im Server-seitigen Weiterleitungs-Code festlegen können.
* Zusätzliche Seitenvariablen : Wenn von der Seite aus andere Variablen an AAM gesendet werden (zusätzlich zu den normalen [!DNL Analytics], die von SiteCatalyst.init verarbeitet werden), müssen Sie diese notieren, damit sie über die Server-seitige Weiterleitung gesendet werden können (Spoiler-Warnhinweis: über [!DNL contextData]).

### Schritt 2: Code aktualisieren {#step-updating-the-code}

In [Implementierungsoptionen](#implementation-options) (oben) werden mehrere Optionen dafür angegeben, wie und wo Sie die Server-seitige Weiterleitung implementieren. Damit dieser Abschnitt effektiv ist, müssen wir ihn in diese Abschnitte unterteilen (von denen zwei kombiniert sind). Navigieren Sie zur Methode in diesem Abschnitt, die Ihre Anforderungen am besten beschreibt.

#### Adobe Experience Platform-Tags {#launch-by-adobe}

Sehen Sie sich das folgende Video an, um zu erfahren, wie Sie Implementierungsoptionen von Client-seitigem DIL-Code in die Server-seitige Weiterleitung in Experience Platform Launch verschieben.

>[!VIDEO](https://video.tv.adobe.com/v/26310/?quality=12)

#### „Auf der Seite“ oder Tag-Manager anderer Hersteller als Adobe {#on-the-page-or-non-adobe-tag-manager}

Sehen Sie sich das folgende Video an, um zu erfahren, wie Sie Implementierungsoptionen von Client-seitigem DIL-Code in die Server-seitige Weiterleitung in [!DNL AppMeasurement]-Code verschieben, der sich entweder in einer -Datei oder in einem Tag-Management-System außerhalb von Adobe befindet.

>[!VIDEO](https://video.tv.adobe.com/v/26312/?quality=12)

### Schritt 3: Aktivieren der Weiterleitung (pro [!UICONTROL Report Suite]) {#step-enabling-the-forwarding-per-report-suite}

Bisher haben wir in diesem Tutorial unsere gesamte Zeit darauf verwendet, den Code von Client-seitigem DIL-Code zur Server-seitigen Weiterleitung zu wechseln. Das ist gut so, weil es der schwierigere Teil ist. Dieser Abschnitt, obwohl Sie sehen werden, ist super einfach, ist genauso wichtig wie die Aktualisierung des Codes. In diesem Video erfahren Sie, wie Sie den Umschalter umkehren, der die tatsächliche Weiterleitung von Daten von Analytics an Audience Manager ermöglicht.

>[!VIDEO](https://video.tv.adobe.com/v/26355/?quality-12)

**HINWEIS:** Wie im Video erklärt, denken Sie daran, dass es bis zu 4 Stunden dauern wird, bis die Aktivierung der Weiterleitung vollständig im Experience Cloud-Backend implementiert ist.

## Timing {#timing}

Zur Erinnerung: Es gibt zwei Hauptaufgaben beim Übergang von Client-seitiger DIL zur Server-seitigen Weiterleitung:

1. Code aktualisieren
1. Den Schalter in der [!DNL Analytics] [!DNL Admin Console] umlegen

Aber die Frage ist, welches macht man zuerst? Spielt das eine Rolle? OK, Entschuldigung, das waren zwei Fragen. Aber die Antworten sind… es kommt darauf an, und ja, es *kann* von Bedeutung sein. Was soll das für vage sein? Brechen wir es auf. Aber zuerst eine zusätzliche Frage, die aufkommen kann, wenn Sie ein großes Unternehmen mit zahlreichen Websites: Muss ich alles auf einmal tun? Das da ist ein bisschen einfacher. Nein. Du kannst es Stück für Stück machen.

### Ein wenig tiefer tauchen {#a-little-deeper-dive}

Timing und Reihenfolge sind deshalb wichtig, weil die Weiterleitung _wirklich_ funktioniert, was in den folgenden technischen Fakten zusammengefasst werden kann:

* Wenn Sie den Experience Cloud ID Service (ECID) implementiert haben und der Schalter im [!DNL Analytics]-[!DNL Admin Console] („Schalter„) aktiviert ist, werden die Daten von [!DNL Analytics] an AAM weitergeleitet, auch wenn Sie den Code noch nicht aktualisiert haben.
* Wenn Sie keine ECID implementiert haben, werden die Daten nicht weitergeleitet, auch wenn Sie den Schalter eingeschaltet haben und den Server-seitigen Weiterleitungs-Code haben.
* Der Server-seitige Weiterleitungs-Code (ob in Platform-Tags oder auf der Seite) verarbeitet die Antwort wirklich und ist erforderlich, um die Migration abzuschließen.
* Beachten Sie, dass der Umschalter für die Server-seitige Weiterleitung vom [!UICONTROL report suite] aktiviert wird, der Code jedoch von der -Eigenschaft in Platform-Tags oder von der [!DNL AppMeasurement]-Datei verarbeitet wird, wenn Sie Platform-Tags nicht verwenden.

### Best Practices {#best-practices}

Basierend auf diesen technischen Details finden Sie hier die Empfehlungen für den Zeitpunkt, was zu tun ist und wann:

#### Wenn Sie die ECID noch NICHT implementiert haben {#if-you-do-not-have-ecid-yet-implemented}

1. Schalten Sie den Switch [!DNL Analytics] für jede [!UICONTROL report suite] um, die Sie für die Server-seitige Weiterleitung aktivieren möchten.

   1. Die Weiterleitung wird noch nicht gestartet, da Sie keine ECID haben.

1. Aktualisieren Sie Ihren Code pro Site von Client-seitiger DIL zu Server-seitiger Weiterleitung (dies könnte in Platform-Tags sein) oder auf der Seite, wie in einem anderen Abschnitt oben beschrieben).

   1. Die Weiterleitung erfolgt jetzt (wie Sie ECID hinzugefügt haben), und Sie sollten auch eine korrekte JSON-Antwort für Ihr [!DNL Analytics]-Beacon erhalten (siehe den Abschnitt Validierung und Fehlerbehebung unten für weitere Details).

#### Wenn Sie ECID implementiert haben {#if-you-do-have-ecid-implemented}

1. Vorbereiten und planen Sie , damit Sie bereit sind, Ihren Code von DIL für die Server-seitige Weiterleitung PER [!UICONTROL report suite] zu aktualisieren, die Sie für die Server-seitige Weiterleitung aktivieren werden:

   1. Schalten Sie den Switch [!DNL Analytics] um, um die Server-seitige Weiterleitung zu aktivieren.

      1. Die Weiterleitung wird gestartet, da die ECID aktiviert ist.

   1. Aktualisieren Sie Ihren Code so bald wie möglich von Client-seitiger DIL zu einseitiger Weiterleitung (dies kann sich in Platform-Tags oder auf der Seite befinden, wie in einem anderen Abschnitt oben beschrieben).

      1. Sie sollten eine geeignete JSON-Antwort auf Ihr [!DNL Analytics]-Beacon erhalten (weitere Informationen finden Sie [ Abschnitt „Validierung und ](#validation-and-troubleshooting)&quot; weiter unten).

>[!NOTE]
>
>Es ist wichtig, diese beiden Schritte so nahe beieinander wie möglich auszuführen, da zwischen den Schritten 1 und 2 oben doppelte Daten in AAM eingehen. Mit anderen Worten: Bei der einseitigen Weiterleitung werden Daten von [!DNL Analytics] an AAM gesendet, und da sich DIL-Code noch auf der Seite befindet, wird auch ein Treffer direkt von der Seite an AAM gesendet, wodurch die Daten verdoppelt werden. Sobald Sie den Code von DIL zur Server-seitigen Weiterleitung aktualisieren, wird dies gelindert.

>[!NOTE]
>
>Wenn Sie lieber eine kleine Diskrepanz in den Daten anstatt einer kleinen Duplizierung von Daten haben möchten, können Sie die Reihenfolge der Schritte 1 und 2 oben ändern. Wenn Sie den Code von DIL auf die Server-seitige Weiterleitung verschieben, wird der Datenfluss in AAM angehalten, bis Sie den Schalter umlegen können, um die Server-seitige Weiterleitung für die [!UICONTROL report suite] zu aktivieren. Normalerweise würden Kunden lieber eine kleine Verdoppelung der Daten haben, als zu verpassen, dass Besucher Eigenschaften und [!UICONTROL segments] kennenlernen.

#### Migrationszeitpunkt, wenn viele Sites und [!UICONTROL report suites] vorhanden sind {#migration-timing-when-you-have-many-sites-and-report-suites}

Dieses Thema wird in den vorherigen Abschnitten kurz angesprochen, da die Hauptstrategie wie folgt zusammengefasst werden kann:

Migrieren Sie jeweils nur eine Site/[!UICONTROL report suite] (oder eine Gruppe von Sites/[!UICONTROL report suites]).

Dies kann jedoch auf der Grundlage einiger möglicher Szenarien etwas kompliziert werden:

* Sie haben eine Site, die mehrere unterschiedliche [!UICONTROL report suites] enthält
* Sie haben eine [!UICONTROL report suite], die mehrere Sites enthält (z. B. eine globale [!UICONTROL report suite])
* Sie verwenden eine Platform Tags-Eigenschaft, um mehrere Sites abzudecken
* Sie haben verschiedene Entwicklungs-Teams für verschiedene Sites

Aufgrund dieser Dinge kann es etwas kompliziert werden. Die besten Dinge, die ich vorschlagen kann, sind:

* Nehmen Sie sich etwas Zeit, um eine Strategie für die Migration zur Server-seitigen Weiterleitung auf der Grundlage der oben erläuterten Dinge zu entwickeln
* Da eine einzelne Eigenschaft in Platform-Tags (oder eine einzelne [!DNL AppMeasurement]-Datei) in der Regel einem oder zwei verschiedenen [!UICONTROL report suites] zugeordnet ist, können Sie wahrscheinlich einen Plan erstellen, der diese verschiedenen Gruppen einzeln bearbeitet, wodurch Ihr Unternehmen auf die Server-seitige Weiterleitung aktualisiert wird
* Wenn Sie mit Adobe Consulting arbeiten, sprechen Sie mit ihm über Ihren Migrationsplan, damit er Ihnen bei Bedarf helfen kann

## Validierung und Fehlerbehebung {#validation-and-troubleshooting}

Überprüfen Sie vor allem, ob die Server-seitige Weiterleitung ausgeführt wird, indem Sie sich die Antwort auf alle Adobe Analytics-Treffer ansehen, die von der App kommen.

Wenn Sie keine Server-seitige Weiterleitung von Daten von [!DNL Analytics] an Audience Manager durchführen, gibt es wirklich keine Antwort auf das [!DNL Analytics] Beacon (außer einem 2x2 Pixel). Wenn Sie jedoch Server-seitige Weiterleitung durchführen, können Sie in der [!DNL Analytics] Anfrage und Antwort Elemente überprüfen, die Ihnen mitteilen, dass [!DNL Analytics] ordnungsgemäß mit Audience Manager kommuniziert, den Treffer weiterleitet und eine Antwort erhält.

>[!VIDEO](https://video.tv.adobe.com/v/26359/?quality=12)

>[!WARNING]
>
>Vorsicht vor dem falschen „Erfolg“. Wenn es eine Antwort gibt und alles zu funktionieren scheint, stellen Sie sicher, dass Sie das `stuff` -Objekt in der Antwort haben. Wenn nicht, wird möglicherweise eine Meldung angezeigt, die `"status":"SUCCESS"` lautet. So verrückt das klingt, ist das ein Beweis dafür, dass es NICHT richtig funktioniert.
>
>Wenn Sie dies sehen, bedeutet dies, dass Sie die Code-Aktualisierung in Platform-Tags oder -[!DNL AppMeasurement] abgeschlossen haben, die Weiterleitung in der [!DNL Analytics]-[!DNL Admin Console] jedoch noch nicht abgeschlossen ist. In diesem Fall müssen Sie sicherstellen, dass Sie die Server-seitige Weiterleitung in der [!DNL Analytics]-[!DNL Admin Console] für Ihre [!UICONTROL report suite] aktiviert haben. Wenn Sie dies getan haben, und es sind noch nicht 4 Stunden vergangen, seien Sie geduldig, da es so lange dauern kann, bis alle notwendigen Änderungen am Backend vorgenommen werden.


![Erfolg](assets/falsesuccess.png)

Weitere Informationen zur Server-seitigen Weiterleitung finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html).
