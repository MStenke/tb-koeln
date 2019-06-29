.. lab6:

--------------------------
Lab 6: Data Protection
--------------------------

Nutanix bietet die Möglichkeit VM- / vDisk-level basierte Storage Snapshots anzulegen. Protection Domains (PDs) sind ein Konstrukt um VMs zu gruppieren und darauf Snapshots und Replikations-Policies anzuwenden.

**In diesem Lab werden Sie Prism Element nutzen um VM-Snapshots zu erstellen und VMs aus diesen Snapshots wiederherzustellen sowie eine Protection Domain für Ihre VMs anzulegen.**


VM-Snapshots
++++++++++++

#. In **Prism Element > VM > Table** wählen Sie Ihre *Initialen*-**Linux-VM**.

#. Wenn die VM angeschaltet sein sollte, fahren Sie die VM herunter **Guest Shutdown**.

    .. figure:: images/poweroffvm.png

#. Wählen Sie die VM und klicken Sie auf **Take Snapshot** innerhalb des Menüs unterhalb der Tabelle.

#. Geben Sie einen Namen für Ihren Snapshot an und klicken Sie auf **Submit**.

    .. figure:: images/takesnap.png

#. Klicken Sie auf den **VM Snapshots**-Tab unterhalb der Tabelle und sehen Sie sich nun die verfügbaren Snapshots für die ausgewählte VM an.

    .. figure:: images/snap-list.png

#. Unter **Actions**, klicken Sie auf **Details** um die Eigenschaften der VM zum Zeitpunkt der Erstellung des Snapshots zu sehen. 

  .. raw:: html

    <h2><strong><font color="red">Jetzt wird es Zeit die VM zu zerstören!</font></strong></h2>

7. Nun klicken Sie auf **Update** um die VM zu modifizieren. Jetzt entfernen Sie sowohl das CD-ROM Laufwerk als auch die DISK durch anklicken des **X** Symbols neben den jeweiligen Devices. Klicken Sie danach auf **Save**.

   .. figure:: images/removedisks.png

#. Starten Sie die VM (*Power on*) und öffnen Sie das Consolen Fenster (*Launch Console*).

   .. figure:: images/2048game.png

   .. note:: Wie Sie in der Abbildung sehen können, hat die VM keine Disk mehr von der sie booten kann. Sie zeigt daher das 2048ger Spiel an.

#. Schalten Sie die nun VM aus (*Power off*).

#. Unter **VM Snapshots** wählen Sie Ihren zuvor von dieser VM erstellten Snapshot aus und klicken auf **Restore** um die VM wieder in den ursprünglichen und funktionsfähigen Zustand zu versetzen. (Alternativ können Sie auch auf **Clone** klicken um einen Restore in Form einer (oder mehrerer) neuen VM(s) durchzuführen.

    .. figure:: images/vmrestored.png

#. Schalten Sie die VM nun wieder ein und verifizieren, ob die VM erfolgreich bootet.

Wie vorher erwähnt, nutzt die Nutanix-Snapshot-Technologie das `redirect-on-write <https://nutanixbible.com/#anchor-book-of-acropolis-snapshots-and-clones>`_ Verfahren, welches ohne verkettete Snapshots auskommt und dadurch höchste Performance bietet.

Protection Domains
++++++++++++++++++

#. Klicken Sie nun in **Prism Element > Data Protection > Table**, und klicken dann auf **+ Protection Domain > Async DR** um eine *Protection Domain (PD)* zu erstellen.

   .. note::
      Eine *synchrone Replikation* in Verbindung mit *Metro Availability* wird aktuell ausschließlich auf der Basis des VMware ESXi-Hypervisors unterstützt, wird aber zu einem späterem Zeitpunkt auch für AHV erwartet.

#. Geben Sie nun einen Namen für die zu erstellende Protection Domain in das Formular ein und klicken auf **Create**.

#. Suchen Sie nun durch *Filterung* oder durch *scrollen* die von Ihnen erstellten VMs im linken Teil des Fensters unter **Unprotected Entities** und wählen diese dann durch anklicken aus um sie in die PD aufzunehmen.  

#. Klicken Sie nun auf **Protect Selected Entities** links unten im Fenster und warten bis die ausgewählten VMs im linken Feld des Fensters unter **Protected Entities** auftauchen.

    .. figure:: images/pd-entities.png

   Consistency-Groups erlauben es Ihnen mehrere VMs zu gruppieren um Snapshots zum gleichen Zeitpunkt aufnehmen zu können, da die VMsz.B. zur gleichen Anwendung gehören.

   .. note:: Mit Nutanix-Snapshots können Anwendungskonsistente-Snapshots für unterstützte Betriebssysteme durchgeführt werden. Voraussetzung hierfür ist, dass die Nutanix-Guest-Tools (NGT) in den entsprechenden VMs installiert sind. Jede VM, die Anwendungskonsistente-Snapshots verwendet wird Teil ihrer eigenen Consistency Group.

#. Klick Sie nun auf **Next**.

#. Klick Sie bitte jetzt auf **New Schedule** um die *Recovery Point Objective (RPO)* sowie die *Retention Policy* zu definieren.

#. Definieren Sie Ihre gewünschte Snapshot-Frequenz, indem Sie z.B. **Repeat every 1 hour(s)** einstellen. Hierdurch wird dann jede Stunde ein Snapshot ezeugt. Stellen Sie dann noch die Start-Time ein und klicken Sie im Anschgluss daran dann auf **Create Schedule** und dann auf **Close**.

   .. note:: AHV unterstützt heute schon NearSync Snapshots mit RPOs so niedrig wie mit 1 Minute.

   .. note:: Mehrere Schedules können für die gleiche PD angewendet werden, was es Ihnen erlaubt eine X Anzahl an Snapshots stündlich, täglich oder monatlich zu erzeugen und vorzuhalten.

#. Konfigurieren Sie eine Retention Policy (z.B. die letzten 5 Snapshots behalten)

   .. note::
      Für Umgebungen bei denen Remote Nutanix Cluster angebunden wurden, lässt sich die Replikation einfach anhand der vorzuhaltenden Snapshots auf der Remote Seite definieren.

      .. figure:: images/snapshot_02.png

#. Klick auf **Create Schedule**.

#. Klick auf **Close** um das Lab abzuschließen.

Und das war's auch schon! Sie haben nun erfolgreich die nativen Data Protection Optionen in Prism konfiguriert.

Zusammenfassung
+++++++++++++++
Nutanix bietet unterschiedliche *Data-Protection-Lösungen* für virtuelle Datacenters anhand vieler verschiedener Möglichkeiten. Darunter befinden sich u. a. *one-to-one* oder *one-to-many* Replikationen. Die Möglichkeiten der Nutanix-Data-Protection-Funktionen beinhalten die VM-, File- und Volume-Group-Ebene, sodass VMs und Daten in einem geschützen und abgesicherten Zustand bleiben. VM-Level-Snapshots und Replikations-Regeln können für jeden unterstützten Hypervisor direkt aus Prism-Element heraus durchgeführt werden.
