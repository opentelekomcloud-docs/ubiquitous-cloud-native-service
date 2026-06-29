:original_name: ucs_01_0018.html

.. _ucs_01_0018:

Enabling Cluster Federation
===========================


Enabling Cluster Federation
---------------------------

You can enable cluster federation for a fleet with just a few clicks.

Enabling cluster federation involves two phases: enabling cluster federation and adding clusters to the federation. Enabling cluster federation for a fleet will federate the registered clusters in the fleet.

There is a quota limit for enabling cluster federation, and there are constraints on clusters in a fleet. Before enabling cluster federation, **read the following constraints** to avoid failures.

.. table:: **Table 1** Cluster constraints

   +-----------------------------------+-----------------------------------------------------------------------------------------------------+
   | Item                              | Constraint                                                                                          |
   +===================================+=====================================================================================================+
   | Cluster version                   | The versions of all clusters in the fleet must be 1.19 or later.                                    |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+
   | Cluster status                    | All clusters in the fleet must be in the **Running** status.                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+
   | Cluster network                   | -  OTC cluster: An EIP must be associated with the cluster.                                         |
   |                                   | -  Other types of clusters: Ensure that the clusters connect to UCS.                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+
   | Quota                             | The cluster federation quota is 1. This means cluster federation can be enabled only for one fleet. |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, locate the target fleet displayed with **Federation not enabled**. Click **Enable**.

#. In the displayed dialog box, click **OK**. Then, wait until cluster federation is enabled.

   If the clusters in the fleet do not meet the constraints, an error message will be displayed. Modify the clusters as prompted and enable cluster federation again.

   It takes about 10 minutes to enable cluster federation. You can click the federation status to view the detailed enabling progress. After cluster federation is enabled, a message will be displayed.

Adding Clusters
---------------

After cluster federation is enabled for a fleet, you can continue to add clusters to the fleet. The new clusters are automatically connected to the federation of the fleet. A federation can have up to 20 clusters.

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. In the card view of the target fleet, click **Add Cluster**, or click |image1| in the upper right corner.

   You can also click the fleet name to access the fleet console. In the navigation pane, choose **Container Clusters**. On the displayed page, click **Add Cluster** in the upper right corner.

#. Select one or more existing clusters. A cluster can only be added to one fleet. The clusters displayed in the list are those that do not been added to any fleets.

#. Click **OK**.

Managing Federation
-------------------

After cluster federation is enabled for a fleet, the **Federation** module on the fleet console is automatically unlocked.

Next, you can create federated resources such as federated workloads, Services, and storage for deploying your service. You can also perform advanced operations such as multi-active DR and auto scaling for multi-cluster applications.

.. _ucs_01_0018__section88211316259:

Disabling Cluster Federation
----------------------------

If you do not need to use cluster federation, you can disable it. After cluster federation is disabled, services running on the workloads are not affected.

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.
#. On the **Fleets** tab, locate the target fleet and click **Disable Federation** in the upper right corner.
#. In the displayed dialog box, click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001416896654.png
