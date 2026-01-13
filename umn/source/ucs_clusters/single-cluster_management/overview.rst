:original_name: ucs_01_0099.html

.. _ucs_01_0099:

Overview
========

The UCS console allows you to manage each cluster on each cluster console.

-  For OTC clusters (CCE standard and Turbo clusters), the operations on the cluster console of UCS are the same as those on the cluster console of CCE. For details about CCE cluster management, see `CCE User Guide <https://docs.otc.t-systems.com/cloud-container-engine/umn/clusters/cluster_overview.html#>`__.
-  For attached clusters, the cluster console allows you to manage basic Kubernetes resources, such as nodes, workloads, Services and ingresses, container storage, ConfigMaps and secrets, and namespaces.

   .. important::

      For attached clusters, you need to log in to the UCS console with a **OTC account** or as a user who has the **UCS FullAccess** permissions to add permissions on the **Permissions** page.

Accessing the Cluster Console
-----------------------------

The method for accessing the cluster console varies according to whether a cluster has been added to a fleet. The details are as follows:

-  Cluster in fleet: On the **Fleets** page, click the **Fleets** tab and click the name of the target fleet. In the navigation pane, choose **Container Clusters**. Then, click the cluster name to access the cluster console.
-  Clusters not in fleet: Switch to the **Clusters Not in Fleet** tab, locate the cluster that is not added to the fleet, and click the cluster name to access the cluster console.
