.. lab1:

----------------
Lab 1: Überblick
----------------

**In diesem Lab lernen Sie Prism Element kennen und werden mit dessen Funktionen und der Benutzerführung vertraut. Sie werden Prism Element nutzen um Basis Cluster Administrations-Aufgaben (inkl. Storage und Netzwerk Verwaltung) sowie Basis VM Deployments und Management Aufgaben mit Prism und AHV durchzuführen. Zuletzt werden Sie VM Data Protection  Optionen wie Snapshots und Replikation erkunden.**

Prism Element
+++++++++++++

Der Prism Dienst stellt das Webinterface bereit um die Nutanix Cluster zu verwalten und läuft auf jeder Controller VM (CVM).
Dieser lokale Dienst, Prism Element genannt, kann durch die IP Adresse jeder einzelnen CVM oder durch die virtuelle Cluster IP Adresse (diese leitet dann zu dem aktuellem Prism Leader um) erreicht werden.

#. Rufen Sie \https://<*NUTANIX-CLUSTER-IP*>:9440 in einem neuem Browser Tab auf.

#. Melden Sie sich mit den folgenden Zugangsdaten an:

   - **username** - admin
   - **password** - <*HPOC Password*>

   .. figure:: images/nutanix_tech_overview_01.png

#. Nachdem Sie sich in Prism Element angemeldet haben, verschaffen Sie sich einen Überblick über die Prism Weboberfläche. Schauen Sie sich die Informationen auf dem **Home Screen** und unter anderen Menüpunkten in Ruhe an.

#. Identifizieren Sie auf dem **Home Screen** die folgenden Informationen:

   - Verwendeter Hypervisor
   - Hypervisor Version
   - Hardware Modell
   - Health (Gesundheitsstatus des Clusters)
   - VM Summary
   - Warning Alerts
   - Data Resiliency Status

   .. figure:: images/nutanix_tech_overview_02.png

#. Werfen Sie einen Blick auf die Cluster Hardware unter **Prism > Hardware**, Klick **Hardware**, dann Klick auf **Diagram**. Dort können Sie die Hardware Zusammenfassung & Details einsehen:

   - Blocks
   - Hosts
   - Memory
   - CPU
   - Disks

   .. figure:: images/nutanix_tech_overview_04.png

#. Schauen Sie sich die obere Toolbar nun etwas genauer an:

   .. figure:: images/nutanix_tech_overview_05.png

   - Health
   - Alarms
   - Tasks
   - Search
   - Help
   - Configuration
   - User

#. Starten Sie über das **Hilfe Symbol** in der Toolbar als nächstes das **Health Tutorial**  und machen Sich mit der Funktionsweise des Health Bereiches vertraut.

   .. figure:: images/nutanix_tech_overview_10.png

   .. figure:: images/nutanix_tech_overview_11.png


#. Schauen Sie sich nun die restlichen Hauptmenü-Einträge auch noch genauer an:

   .. figure:: images/nutanix_tech_overview_03.png

   - VM, Storage, Network, Hardware, File Server, Data Protection, Analysis, Alerts, Tasks, Settings, Self Service


Prism Element - Rückblick
+++++++++++++++++++++++++

Wie können Sie die verwendete **AOS Version** herausfinden?

.. figure:: images/nutanix_tech_overview_06.png

(Sie können dies durch einen Klick auf das **User** Dropdown und Klick auf **About Nutanix**.)

Wie würden Sie zu folgender Ansicht gelangen, welche Ihnen eine Übersicht über die **Anzahl der Hosts**, der **Cluster Kapazität** und der **Cluster Auslastung** anzeigt?

.. figure:: images/nutanix_tech_overview_07.png

(In **Prism Element > Hardware**, Klick **Hardware**, dann auf **Table**).

Wo finden Sie folgenden Screenshot mit den **Gesundheitsinformationen** zu dem Cluster?

.. figure:: images/nutanix_tech_overview_08.png

(In **Prism > Health**, Klick **Health**, dann Klick **Summary** in der rechten Spalte.)

Auf welcher Seite würden Sie die **letzte Aktivität** auf dem System einsehen? Auf dieser Seite können Sie den Fortschritt aller Tasks einsehen und erkennen welche Tasks in der Vergangenheit gelaufen sind. Kennen Sie beide Wege um dorthin zu gelangen?

.. figure:: images/nutanix_tech_overview_09.png

(In **Prism > Tasks**, Klick auf **Tasks** oder das **"Kreis-Symbol"** in der oberen Toolbar.

Zusammenfassung
+++++++++++++++
Prism Element ist die Nutanix "Management plane" / Verwaltungs-Ebene welche auf jedem Knoten läuft und ein HTML5 Webinterface für das Cluster bereitstellt. Die Oberfläche & Bedienbarkeit wurde bewusst so angelegt, dass die wichtigsten Informationen für einen Administrator intuitiv ersichtlich sind.
