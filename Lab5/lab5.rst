.. lab5:

------------------------------
Lab 5: Verwalten von Workloads
------------------------------
**Jetzt da wir einige VMs bereits ausgerollt haben, lassen Sie uns anhand dieser einige VM-Verwaltungsmöglichkeiten mit AHV (Power Aktionen, Klonen und Migration) testen.**

Power-Actions und Console-Zugang
++++++++++++++++++++++++++++++++++
#. In **Prism Element > VM > Table** nutzen Sie die Suche, um Ihre Linux-VM, die Sie in dem vorherigen Lab angelegt haben, zu finden (*Initialen*-LinuxVM).

 Beachten Sie, dass in der Spalte "Energiezustand" für diese VM entweder ein roter Punkt angezeigt wird, der angibt, dass die VM ausgeschaltet ist, oder ein grüner Punkt zu sehen ist, wenn die VM eingeschaltet ist.
 
#. Wählen Sie die VM aus und stellen Sie sicher, dass diese noch läuft. (Falls nicht, klicken Sie auf **Power On**).

#. Bei ausgewählter VM klicken Sie unterhalb der VM Tabelle auf **Launch Console**.

   Das HTML5 Konsolen Fenster bietet rechts oben 4 Aktionen:

    .. figure:: images/vmactionoptions.png

   - **Mount ISO**: Bietet die Option eine ISO aus dem Image Service zu mounten.

    .. figure:: images/mountiso.png

   - **CTRL-ALT-DEL**: Sendet Ctrl+Alt+Del an die VM.

   - **Take Screen Capture**: Nimmt einen Screenshot als png Datei auf.

   - **Power off / Reset VM**

    .. figure:: images/poweroffvm.png

   .. note::

     Für ESXi: Die Schritte in dieser Übung können ebenfalls aus Prism heraus durchgeführt werden wenn ein Cluster verwendet wird welches ESXi as Hypervisor verwendet und vCenter in Prism registriert hat

     .. figure:: images/manage_workloads_06.png

VM Clonen
+++++++++

#. In **Prism Element > VM > Table** wählen Sie Ihre *Initialen*-LinuxVM aus.

#. Klicken Sie auf **Clone** von der **Actions** Liste.

#. Füllen Sie die folgenden Details aus und klicken Sie auf **Save**:

   - **Number of Clones** - 2
   - **Prefix Name**  - *Initialen*-LinuxVM**-Clone**
   - **Starting Index Number** - 1

   .. figure:: images/manage_workloads_02.png

#. Lassen Sie diese **Powered Off**.

   Sowohl Nutanix Snapshots als auch Clone's verwenden ein `redirect-on-write <https://nutanixbible.com/#anchor-book-of-acropolis-snapshots-and-clones>`_ Algorithmus um schnell und effizient Kopien von VMs durch Metadata Operationen zu erstellen.

VM Migrationen
++++++++++++++
VM Live Migrationen sind ein kritisches Feature für jede virtualisierte Umgebung, da nur so VMs nahtlos zwischen Hosts innerhalb eines Clusters verschoben werden können um Infrastruktur Wartung oder Lastverteilung durchführen zu können.

#. In **Prism Element > VM > Table** wählen Sie ihre *Initialen*-LinuxVM aus.

   Sie sollten nun sehen, dass die VM keinen Eintrag in der **Host** Spalte besitzt solange diese ausgeschaltet ist.

   .. figure:: images/lab5-1.png

#. Wählen Sie die VM aus und starten Sie diese (**Powered On**). Nun sollte in der Spalte **Host** einer der Hosts im Cluster erscheinen.

   .. figure:: images/lab5-2.png

#. Klicken Sie als nächstes auf **Migrate**.

   Sie können entweder einen der Hosts in dem Cluster als Migrationsziel bestimmen oder standardmäßig AHV automatisch den passenden Hosts auswählen lassen.

   .. figure:: images/lab5-3.png

#. Klicken Sie auf **Migrate** um den Schritt abzuschließen.

   Wenn der Schritt abgeschlossen ist, stellen Sie sicher, dass Ihre VM nun auf einem anderen Host läuft als zuvor.

   .. figure:: images/lab5-4.png

Affinity Policies
+++++++++++++++++

#. In **Prism Element > VM > Table** selektieren Sie Ihre *Initialen*-LinuxVM aus.

#. Wählen Sie **Powered Off** VM, dann klicken Sie auf **Update** und **+ Set Affinity**.

#. Wählen Sie **zwei** **Hosts** aus, zu welcher die VM eine *Affinity* haben soll und klicken sie auf **Save** und **Save** um den Prozess abzuschließen.

   .. figure:: images/lab5-5.png

   .. note:: Wir selektieren mehr als einen Host, sodass die VM ein Migrationsziel hat, falls ein Host ausfallen sollte.

#. Starten Sie die VM und verifizieren Sie, dass Sie auf einem der **Host** läuft welchen sie in der *Affinity Policy* angegeben.

#. Wählen Sie die VM aus und klicken dann auf **Migrate**.

   Sie sollten nun die folgende Nachricht angezeigt bekommen:

   .. figure:: images/lab5-6.png

   - Diese VM hat eine **Host Affinity** mit 2 von 4 verfügbaren Host und kann daher nur auf diesen Host migriert werden.

#. Klicken Sie auf **Migrate**.

   Sie sollten nun sehen können wie die VM auf den anderen Host verschoben wurde.

VM-zu-Host Affinity Policies werden typischerweise genutzt um VMs auf bestimmte Host zu binden, z.B. aus Performance oder Lizenz-Gründen. AHv kann darüber hinaus auch VM-zu-VM *Anti-Affinity* Regeln erstellen, z.B. für Anwendungen bei denen man sicherstellen möchte, dass mehrere Instanzen einer Anwendungn nicht auf dem gleichen Host laufen.

High Availability & Dynamic Scheduling
++++++++++++++++++++++++++++++++++++++

Im Gegensatz zu ESXi, ist bei AHV *High Availability* standardmäßig bereits aktiviert und sorgt dafür, dass VMs im Falle eines Host Ausfalles bestmöglich (*best effort*) auf anderen Host wieder neugestarted werden. Zusätzliche Konfiguration erlaubt es Ressourcen zu reservieren, um sicherzustellen, dass auch genügend Ressourcen vorhanden sind um alle VMs neustarten zu können.

.. note::

   Um Memory Reservierungen vorzunehmen, wählen Sie **Enable HA Reservation** unter **Prism Element > Settings > Manage VM High Availability**.

   .. figure:: images/lab5-7.png

   Da Memory auf dieser Testumgebung allerdings bereits reduziert ist, aktivieren Sie bitte **keine** *HA memory reservations*.

Mit dem **Acropolis Dynamic Scheduler** (ADS) Service nimmt AHV ein intelligentes initiales Platzieren von VMs vor und kann VMs dynamisch zu anderen Host im Cluster verschieben um Performance zu optimieren. Dies läuft bereits standardmäßig (*out of the box*) ohne zusätzliche Konfiguration.

Ein Mehrwert der Nutanix AHV Lösung ist, dass VM Platzierungs-Entscheidungen nicht nur ausschließlich auf CPU & Memory Engpass-Vermeidung basiert, sondern ebenso Storage Performance miteinbeziehen kann.

Mehr Informationen bzgl. des **Acropolis Dynamic Scheduler** ist `hier <https://nutanixbible.com/#anchor-book-of-acropolis-dynamic-scheduler>`_ in der Nutanix Bible zu finden.

Zusammenfassung
+++++++++++++++
In diesem Lab haben Sie erlebt welche vielfältigen Werkzeuge und Optionen AHV bietet um VMs in dem Cluster zu verwalten. AHV bietet kritische Funktionen wie Live Migration, Hochverfügbarkeit (High Availability) und Dynamischer VM Platzierung (Dynamic VM Placement) "out-of-the-box" ohne zusätzliche Konfiguration an. AHV VMs können darüber hinaus nicht nur durch Prism verwaltet werden, sondern ebenfalls via CLI oder REST API. Es ist ebenso möglich ein ESXi Cluster in Prism zu registrieren und ein paar Basis VM Tasks ebenso direkt aus Prism heraus durchzuführen.
