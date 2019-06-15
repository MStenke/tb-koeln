.. lab1:

---------------------
Lab 1: Nutanix Technology Überblick
---------------------

**In diesem Lab werden Sie Prism Element kennenlernen und mit den FUnktionen und der Navigationen vertraut. Sie werden Prism nutzen um typische Cluster Administrations Aufgaben, wie etwa Storage und Netzwerk, durchzuführen. Sie werden auch einfache VM Deployment und Verwaltungsaufgaben mit Prism und AHV erlernen. Zu guter Letzt werden Sie VM Data Protection inkl. Snapshots und Replikation erkunden.**

Prism Element
-------------

The Prism service provides the web UI for managing Nutanix clusters and runs on every Controller VM (CVM). This local Prism service, referred to Prism Element, can be accessed via the IP of any individual CVM, or via the virtual IP for the cluster, which will redirect to the current Prism leader.

#. Open \https://<*NUTANIX-CLUSTER-IP*>:9440 in a new browser tab.

#. Log in using the following credentials:

   - **Username** - admin
   - **Password** - *HPOC Password*

   .. figure:: images/nutanix_tech_overview_01.png

#. After you log in to Prism Element, familiarize yourself with the Prism UI. Explore the information on the **Home** screen, as well as the other screens.

#. Review the Home screen, and identify the following items:

   - Hypervisor
   - Version
   - Hardware Model
   - Health
   - VM Summary
   - Warning Alerts
   - Data Resiliency Status

   .. figure:: images/nutanix_tech_overview_02.png

#. Review the UI navigation options.

   .. figure:: images/nutanix_tech_overview_03.png

#. Examine the cluster hardware under **Prism > Hardware**, click **Hardware**, then click **Diagram**.

#. Review the hardware summary information:

   - Blocks
   - Hosts
   - Memory
   - CPU
   - Disks

   .. figure:: images/nutanix_tech_overview_04.png

#. Review the other sections, and do a quick walk through:

   - VM
   - Health
   - Network
   - Data Protection
   - Storage
   - Alerts
   - Etc.

#. Review other sections of the Prism UI

   - Health :fa:`heartbeat`
   - Alarms :fa:`bell`
   - Tasks :fa:`circle-o`
   - Search :fa:`search`
   - Help :fa:`question`
   - Configuration :fa:`cog`
   - User :fa:`user`

   .. figure:: images/nutanix_tech_overview_05.png

Prism Element UI Review
.......................

Where would you locate the version of AOS you are running?

.. figure:: images/nutanix_tech_overview_06.png

You can do this by clicking on the **User** drop down :fa:`user`, and clicking **About Nutanix**.

How would you get to the following screen to view a summary of the number of hosts (or nodes) and the resource capacity and current utilization?

.. figure:: images/nutanix_tech_overview_07.png

In **Prism > Hardware**, click **Hardware**, then click **Table**.

How would you get the following screen to see the health of your cluster?

.. figure:: images/nutanix_tech_overview_08.png

In **Prism > Health**, click **Health**, then click **Summary** in the right pane.

What page would show you the latest activity in the system? On this page, you can monitor the progress of any task and keep track of what has been done in the past using time stamps. Can you figure out two different ways to get there?

.. figure:: images/nutanix_tech_overview_09.png

Browse to **Prism > Tasks** and click **Tasks**, or click the :fa:`circle-o` icon in the toolbar.
