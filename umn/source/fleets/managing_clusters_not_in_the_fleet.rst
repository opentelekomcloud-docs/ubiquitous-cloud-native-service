:original_name: ucs_01_0155.html

.. _ucs_01_0155:

Managing Clusters Not in the Fleet
==================================

Clusters for which a fleet is not selected during registration or clusters removed from a fleet will be displayed on the **Clusters Not in Fleet** tab. This section describes how you can manage clusters that are not added to a fleet, including adding clusters to a fleet and add a permission policy for the fleet.

Registering Clusters to a Fleet
-------------------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Clusters Not in Fleet** tab, click |image1| in the upper right corner of the card view of the target cluster.

#. Select a fleet. A registered cluster will follow the fleet permissions policies, not its own ones.

#. After you select a fleet, the current permission and adjusted permission are displayed. Confirm the information and click **OK**.

   After the cluster is registered to a fleet, the cluster is displayed in the fleet and will be centrally managed by the fleet.

Adding Permissions
------------------

#. Log in to the UCS console. In the navigation pane, choose **Permissions**.
#. Select a cluster for which you want to add permissions from the drop-down list on the right.
#. Click **Add Permission** in the upper right corner.
#. In the window that slides from the right, confirm the cluster name, set **Namespace** (for example, select **All namespaces**), select the target user or user group, and set **Permission Type**.

   -  A user group can contain multiple users, and a user can be added to multiple user groups. A user has all the permissions of the user group that the user belongs to.
   -  **Namespace**: Select **All namespaces** or a specific namespace. **All namespaces** includes the existing namespace of the fleet and the namespace to be added to the fleet. If you select this option, you cannot select other namespaces. If you do not select this option, UCS provides several common namespaces, such as **default**, **kube-system**, and **kube-public**. You can also add a namespace, which should exist in the cluster.

#. Click **OK**.

Unregistering a Cluster
-----------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Clusters Not in Fleet** tab, click |image2| in the upper right corner of the card view of the target cluster.

#. In the **Unregister Cluster** dialog box, read the precautions carefully, confirm the risks, and click **OK**.

#. (Optional) After an attached cluster is unregistered, run the following command to uninstall the agent component from the destination cluster:

   **kubectl -n kube-system delete deployments/proxy-agent secret/proxy-agent-cert**

.. |image1| image:: /_static/images/en-us_image_0000002306426742.png
.. |image2| image:: /_static/images/en-us_image_0000001461556069.png
