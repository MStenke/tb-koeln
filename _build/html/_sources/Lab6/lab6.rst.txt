.. lab6:

--------------------------
Lab 6: Data Protection
--------------------------

Nutanix bietet die Möglichkeit VM / vDisk-level basierte Storage Snapshots anzulegen. Protection Domains (PDs) sind ein Konstrukt um VM's zu gruppieren und darauf Snapshots und Replikations-Policies anzuwenden.

**In diesem Lab werden Sie Prism Element nutzen um VM Snapshots zu erstellen und VM's aus diesen Snapshots wiederherzustellen, sowie eine Protection Domain für Ihre VMs anzulegen.**


VM Snapshots
++++++++++++

#. In **Prism Element > VM > Table**, wählen Sie Ihre *Initialen*-**Linux_VM** VM.

#. Wenn die VM angeschaltet sein sollte, führen sie eine **Guest Shutdown** Power Aktion durch.

    .. figure:: images/poweroffvm.png

#. Wählen Sie die VM und klicken Sie **Snapshot** von dem Menü unterhalb der Tabelle.

#. Geben Sie einen Namen für Ihren Snapshot an und klicken Sie auf **Submit**.

    .. figure:: images/takesnap.png

#. Wählen Sie **VM Snapshots** Tab unterhalb der Tabelle und sehen Sie sich die verfügbaren Snapshots für die ausgewählte VM an.

    .. figure:: images/snap-list.png

#. Unter **Actions**, klicken Sie auf **Details** um alle VM Eigenschaften zum Zeitpunkt des Snapshots zu sehen. Wie Sie sehen enthält der Snapshot den VM Zustand neben den reinen Storage Daten.

  .. raw:: html

    <h2><strong><font color="red">Jetzt wird es Zeit die VM zu zerstören!</font></strong></h2>

7. Klicken Sie auf **Update** um die VM zu modifizieren und entfernen Sie sowohl das CD-ROM Laufwerk als auch die DISK durch klicken auf das **X** Symbol neben dem jeweiligen Eintrag. Klicken Sie danach auf **Save**.

   .. figure:: images/removedisks.png

#. Versuchen Sie die VM zu starten (*Power on*) und öffnen Sie das Consolen Fenster (*Launch Console*).

   .. figure:: images/2048game.png

   .. note:: Wie Sie sehen, hat die VM keine Disk mehr von welcher diese booten kann und zeigt daher das 2048 Spiel an.

#. Schalten Sie die VM aus (*Power off*).

#. Unter **VM Snapshots** wählen Sie Ihren Snapshot aus und klicken auf **Restore** um die VM wieder in einen funktionsfähigen Zustand zu versetzen. (Alternativ können Sie auch auf **Clone** klicken um einen Restore in Form einer (oder mehrerer) neuen VM(s) durchzuführen.

    .. figure:: images/vmrestored.png

#. Verifizieren Sie, dass die VM erfolgreich bootet.

Wie vorher erwähnt nutzen Nutanix Snapshots ein `redirect-on-write <https://nutanixbible.com/#anchor-book-of-acropolis-snapshots-and-clones>`_ Ansatz, welcher nicht unter Performance Verlusten durch verkettete Snapshots wie in anderen Hypervisoren leidet.

Protection Domains
++++++++++++++++++

#. In **Prism Element > Data Protection > Table**, klick **+ Protection Domain > Async DR** um eine PD zu erstellen.

   .. note::
      Synchrone Replikation (Metro Availability) ist aktuell nur mit ESXi unterstützt and wird zu einem späterem Zeitpunkt mit AHV unterstützt.

#. Geben Sie einen Namen für die Protection Domain an und klicken auf **Create**.

#. Filtern oder scrollen Sie um die von Ihnen erstellten VMs zu selektieren die in die PD aufgenommen werden sollen.

#. Klick auf **Protect Selected Entities** und stellen Sie sicher, dass die VMs in der rechten Spalte unter **Protected Entities** auftauchen.

    .. figure:: images/pd-entities.png

   Consistency Groups erlauben es Ihnen mehrere VMs zu gruppieren um Snapshots zum gleichen Zeitpunkt aufzunehmen, z.B. wenn die VMs zu einer gleichen Anwendung gehören.

   .. note:: Nutanix Snapshots können Anwendungs konsistente Snapshots für unterstützte Betriebssysteme durchführen auf welchen die Nutanix Guest Tools (NGT) installiert sind. Jede VM die Anwendungs konsistente Snapshots verwendet wird Teil Ihrer eigenen Consistency Group.

#. Klick auf **Next**.

#. Klick auf **New Schedule** um die Recovery Point Objective (RPO) und Retention Policy zu definieren.

#. Definieren Sie Ihre gewünschte Snapshot Frequenz (z.B. jede Stunde 1x)

   .. note:: AHV unterstützt heute schon NearSync Snapshots mit RPOs so niedrig wie mit 1 Minute.

   .. note:: Mehrere Schedules können für die gleiche PD angewendet werden, was es Ihnen erlaubt eine X Anzahl an Snapshots stündlich, täglich oder monatlich zu erzeugen und vorzuhalten.

#. Konfigurieren Sie eine Retention Policy (z.B. die letzten 5 Snapshots behalten)

   .. note::
      Für Umgebungen bei denen Remote Nutanix Cluster angebunden wurden, lässt sich die Replikation einfach anhand der vorzuhaltenden Snapshots auf der Remote Seite definieren.

      .. figure:: images/snapshot_02.png

#. Klick auf **Create Schedule**.

#. Klick auf **Close** um das Lab abzuschließen.

Das war's - Sie haben erfolgreich die nativen Data Protection Optionen in Prism konfiguriert.

Zusammenfassung
+++++++++++++++
Nutanix bietet Data Protection Lösungen für virtuelle Datacenter anhand vieler verschiedener Möglichkeiten darunter u.a. "one-to-one" oder "one-to-many" Replikation. Die Nutanix Data Protection Möglichkeiten umfassen Funktionen auf VM, File und Volume Group Ebene, sodass VM's und Daten in einem sicheren Zustand bleiben. VM Level Snapshots und Replikations-Regeln können direkt aus Prism heraus für jeden unterstützten Hypervisor vorgenommen werden.
