:original_name: ucs_01_0282.html

.. _ucs_01_0282:

OTC Clusters
============

You can register OTC clusters (CCE standard clusters and CCE Turbo clusters) with UCS with just a few clicks. After the registration is complete, clusters can be managed automatically.

Constraints
-----------

-  Only **OTC accounts** or users with the **UCS FullAccess** permissions can register clusters.
-  If you are connecting a foreign cluster to UCS, ensure that this connection and the subsequent actions you will take comply with the local laws and regulations.
-  Ensure that your Kubernetes cluster version is 1.19 or later.

Prerequisites
-------------

You have created a CCE standard cluster or CCE Turbo cluster to be connected to UCS, and the cluster is in the **Running** state.

Procedure
---------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. In the card view of **OTC clusters**, click **Register Cluster**.

#. Select the CCE standard cluster or CCE Turbo cluster to be registered. Select a fleet and click **OK**.

   If you do not select a fleet when registering a cluster, the cluster will be displayed on the **Clusters Not in Fleet** tab after registration. You can add it to a fleet later. For details, see :ref:`Managing Clusters Not in the Fleet <ucs_01_0155>`.

   .. note::

      When registering a cluster, you cannot select a fleet with cluster federation enabled. To add your cluster to the fleet with cluster federation enabled, register your cluster with UCS first. For details about cluster federation, see :ref:`Enabling Cluster Federation <ucs_01_0018>`.
