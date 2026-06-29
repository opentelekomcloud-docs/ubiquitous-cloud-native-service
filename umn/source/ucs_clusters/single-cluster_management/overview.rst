:original_name: ucs_01_0099.html

.. _ucs_01_0099:

Overview
========

The UCS console allows you to manage each cluster on each cluster console.

-  For T Cloud clusters (CCE standard and Turbo clusters), the operations on the cluster console of UCS are the same as those on the cluster console of CCE. For details about CCE cluster management, see `CCE User Guide <https://docs.otc.t-systems.com/cloud-container-engine/umn/clusters/cluster_overview.html#>`__.
-  For attached clusters, the cluster console allows you to manage basic Kubernetes resources, such as nodes, workloads, Services and ingresses, container storage, ConfigMaps and secrets, and namespaces.

   .. important::

      The console permissions of attached clusters are separately managed by UCS. You need to use **a T Cloud account** or have the **UCS FullAccess** permissions to configure the required permissions on the **Permissions** page of the UCS console.

Accessing the Cluster Console
-----------------------------

For a cluster in a fleet and a cluster not in a fleet, the methods for accessing the cluster console are different. The details are as follows:

-  Cluster in a fleet: On the **Fleets** page, click the **Fleets** tab and click the name of the target fleet. In the navigation pane, choose **Container Clusters**. Click the cluster name to access the cluster console.
-  Cluster not in a fleet: On the **Clusters Not in Fleet** tab, locate the cluster that is not added to any fleet and click the cluster name to access the cluster console.
