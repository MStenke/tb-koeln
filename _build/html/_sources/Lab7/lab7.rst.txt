.. lab7:

--------------------
Lab 7: Prism Central
--------------------

Erfahren Sie von Prism Central's Multi Cluster Verwaltung, Suche, Überwachung und Ressourcen Planung welche Ihnen dabei hilft Engpässe zu vermeiden und zukünftiges Wachstum akkurat planen zu können. Nachdem Sie in Prism Central eingeloggt sind, machen Sie sich zunächst mit der Prism Central Oberfläche vertraut, erkunden Sie die Informationen auf dem Dashboard und den Sektionen im Hauptmenü auf der linken oberen Seite.

Suchfunktion
++++++++++++
Die Prism Central Suchfunktion hilft dabei Probleme (oder auch Dokumentation) schneller identifizieren und finden zu können. Anhand ein paar einfacher Suchabfragen können die gewünschten Informationen direkt über die zentrale Suche gefunden werden - ohne langwierig in der einer Menüstruktur suchen zu müssen. Klicken Sie auf das **Help Icon** oben rechts in der Menüleiste und dann auf **Learn about search** um die umfangreichen Suchparameter einzusehen.

.. figure:: images/lab7-1.png

Testen Sie ein paar Suchabfragen um mit der Syntax vertraut zu werden:
    - vm cpu > 1
    - vm mem > 2
    - vm iops > 50
    - Hosts "cpu usage">95
    - etc.

.. note:: Der *Hotkey* um die Suche zu aktivieren ist ein **Schrägstrich** bzw. das **"/"** Symbol welches von überall in der Prism Central Oberfläche verwendet werden kann. Klicken Sie auf das **Stern** Symbol um eine Suche zu speichern.

 .. figure:: images/lab7-2.png


Reports
+++++++
Prism Central bietet Ihnen die Möglichkeit historische Auswertungen Ihrer Umgebung zu generieren. Solche Reports können u.A. Ressourcen Auslastung, ungewöhnliches VM Verhalten und andere wertvolle operationale Einblicke enthalten.

1.  In **Prism Central Hauptemnü > Operations > Reports**.
2.  Testen Sie den “Cluster   Efficiency   Summary”   oder den “Environment   Summary” Report.   Wählen Sie einen der beiden Reports aus und wählen Sie dann **Run** von dem **Actions Dropdown Menü**.
3.  Als Nächstes füllen Sie die folgenden Felder aus und klicken auf **Run**:

    - **Report instance Name** - *Initialen*-BeispielReport
    - **Time Period for Report** - Last 24 Hours
    - **Report Format** – PDF / CSV checked
    - **Recipient Format / Email Report** - diese Option wird in diesem Lab nicht verwendet.

     .. figure:: images/lab7-3.png

4.  Sobald der Report fertig ist, klicken Sie auf den Report und können die bereits ausgeführten Instanzen dieses Reports einsehen. Sie können nun Ihren Report als **PDF** oder als **CSV** Datei **herunterladen** und ansehen.

.. figure:: images/lab7-4.png

Capacity Planning
++++++++++++++++++
Nutzen Sie **Prism Central's Capacity Planning** (Kapazitäts-Planung) um mehr über Cluster Auslastungs-Planung und Empfehlungen zu erfahren.


1.  Im **Prism Central Menu > Operations > Planning > Capacity Runway**.

    .. note:: Die **Runway Summary** zeigt die übrigen Tage an, bis das CLuster in der jeweiligen Kategorie ans Limit läuft. Wie lange dauert es bis das aktuelle Cluster Memory, CPU oder Storage seitig in einen Engpass gerät? Hier ein Beispiel wie es aussehen könnte:

        .. figure:: images/lab7-5.png

3.  Wählen Sie das **Cluster** aus.

    - Die **am meisten limitierte Ressource** is auf der linken Seite hervorgehoben.
    - Klicken Sie **Storage**, **CPU** oder **Memory Runway** um das Diagramm für die Ressource anzuzeigen.
    - Klicken Sie **Optimize   Resources** um eine Liste an empfohlenden Verwaltungs-Aufgaben für eine Ressourcen Reallokation anzusehen, etwa *Optimierung von Überprovisionierten VMs*, *Löschen von inaktiven VMs* oder *Hinzufügen von weiteren Ressourcen zu limitierten VMs*.

        .. figure:: images/lab7-6.png

4.  Schließen Sie die **Capacity Runway** Ansicht.

What If Planning
++++++++++++++++
Wie planen Sie typischerweise ob und welchen Workload Sie zu Ihrer bestehenden Umgebung noch ergänzen können - wann laufen Sie durch den zusätzlichen Workload in Engpässe? Um diese Planungsaufgaben einfacher zu gestalten, bietet Prism Central eine sog. **What If Planning** Funktion an, die dabei hilft theoretische Planung von weiterem Workload auf Ihrer bestehenden Umgebung zu simulieren um zu schauen wie Sich Ihre Umgebung mit diesen neuen hypothetischen Workload verhält.

1.  In **Prism Central Menu > Operations > Planning > Scenarios** dann auf **New Scenario** klicken.
2.  Als nächstes füllen Sie die folgenden Felder aus:

    - **Cluster** - Wählen Sie Ihr Cluster aus.
    - **Target** - 6 months

3.	Jetzt lassen Sie uns **150 neue Citrix XenDesktop Anwender** hinzufügen. Klicken Sie auf **Add/Adjust** und fügen Sie die folgenden Felder wie folgt aus:

    - **Workload** – VDI
    - **Vendor** - XenDesktop
    - **User Type** - Power User
    - **Provision Type** - Machine Creation Services
    - **Number of Users** - 150
    - **On** - One Month from today

5.	Speichern Sie dieses **Scenario** und inspizieren Sie die **Runway Veränderungen** für *CPU*, *Memory* und *Storage*.

        .. figure:: images/lab7-7.png

    .. note:: Wiederholen Sie diesen Prozess (Workload hinzufügen) oder passen Sie den VDI Workload an, bis Sie insgesamt unter 6 Monate Runway gelangen.

6.	Werfen Sie einen Blick auf die **Resource Sektion**  welche die aktuelle Hardware anzeigt.

7.	Klicken Sie auf **Recommend** um zu sehen welche NX Konfiguration dem Cluster hinzugefügt werden kann, um die **Runway** zu verlängern.

        .. figure:: images/lab7-8.png

        .. note:: Experimentieren Sie gerne ein wenig mit weiterem Workload und sehen Sie welche Workload Veränderungen weitere Auswirkungen auf die **Runway** und die **Resource Recommendation** haben, z.B.  fügen sie weiter 150 VDI Nutzer in 3 Monaten hinzu, etc.


8.	Generieren Sie ein **PDF Report** um detailierte Kapazitäts-Planungs-Informationen zu erhalten, die als Grundlage für weitere Workload Planungen verwendet werden können.

        .. figure:: images/lab7-9.png

Zusammenfassung
+++++++++++++++

Die Prism Central Report Funktionalität bietet Ihnen die Möglichkeit Auswertung, die aktuelle und historische Daten umfassen, nach Ihren zeitlichen Vorgaben bequem regelmäßig per E-Mail zu empfangen. Die **Capacity Runway** Ansicht in dem Planungs-Dashboard zeigt & aggregiert kombinierte **Resource Runway** Information für alle registrierten Cluster an. Die **Scenario View** Ansicht in dem **Planning Dashboard** eröffnet Ihnen die Möglichkeit "What If" Szenarien für zukünftige Workloads (nach Ihren Vorgaben) zu evaluieren, um so zukünftigen Ressourcenbedarf vorrauszuplanen.
 
.. note:: Ein paar der vorgestellten Funktionen benötigen eine **Prism Central PRO Lizenz**. Und auch darüber hinaus gibt es noch weitere interessante Mehrwerte die Nutanix mit Prism Central erbringen kann, so kommt z.B. Machine Learning zum EInsatz (**Nutanix X-Fit**) um **Anomalie Erkennung** oder auch **Automatisierung von Routine Tasks mit X-Play** anzugehen, etc.
