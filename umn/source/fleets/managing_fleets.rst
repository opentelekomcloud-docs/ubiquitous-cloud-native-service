:original_name: ucs_01_0004.html

.. _ucs_01_0004:

Managing Fleets
===============

This section describes how to create a fleet, add clusters to the fleet, adding a permission policy for the fleet, remove clusters from the fleet, unregister clusters from the fleet, and delete the fleet.

Creating a Fleet
----------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**. On the **Fleets** tab, click **Create Fleet**.
#. Enter the fleet information.

   -  **Fleet Name**: Enter a name, starting with a lowercase letter and not ending with a hyphen (-). Only lowercase letters, digits, and hyphens (-) are allowed.
   -  **Add Cluster**: Clusters not in the fleet are displayed in the list. You can add clusters when creating a fleet or after the fleet is created. If you do not select any cluster, an empty fleet will be created. After the fleet is created, see :ref:`Adding a Cluster <ucs_01_0004__section590712161108>`.
   -  **Description**: description of the fleet to which the cluster is added

   .. note::

      A registered cluster will follow the fleet permissions policies, not its own ones.

#. Click **OK**.

.. _ucs_01_0004__section590712161108:

Adding a Cluster
----------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. In the card view of the target fleet, click **Add Cluster**, or click |image1| in the upper right corner.

   You can also click the fleet name to access the fleet console. In the navigation pane, choose **Container Clusters**. On the displayed page, click **Add Cluster** in the upper right corner.

#. Select one or more existing clusters. A cluster can only be added to one fleet. The clusters displayed in the list are those that do not been added to any fleet.

   .. note::

      -  Only clusters not added to a fleet can be added. To add a cluster from another fleet, remove the cluster from that fleet first.
      -  After a cluster is added to a fleet, the cluster will follow the fleet permission policies, not its own ones.

#. Click **OK**.

Adding Permissions
------------------

#. Log in to the UCS console. In the navigation pane, choose **Permissions**.

#. Select a cluster or fleet for which you want to add permissions from the drop-down list on the right.

#. Click **Add Permission** in the upper right corner.

#. In the window that slides from the right, confirm the cluster or fleet name, set **Namespace** (for example, select **All namespaces**), select the target user or user group, and set **Permission Type**.

   -  **User/User Group**: A user group can contain multiple users, and a user can be added to multiple user groups. A user has all the permissions of the user group that the user belongs to.
   -  **Namespace**: You can select **All namespaces** or other namespaces. **All namespaces** includes the existing namespace of the fleet and the namespace to be added to the fleet. If you select this option, you cannot select other namespaces. If you do not select this option, UCS provides several common namespaces, such as **default**, **kube-system**, and **kube-public**. You can also add a namespace, which should exist in the cluster.

#. Click **OK**.


   .. figure:: /_static/images/en-us_image_0000002240667777.png
      :alt: **Figure 1** Adding permissions for a fleet

      **Figure 1** Adding permissions for a fleet

.. _ucs_01_0004__section171856259306:

Removing a Cluster from a Fleet
-------------------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the fleet name to access the fleet console.

#. In the navigation pane, choose **Container Clusters**. In the card view of the target cluster, click |image2| in the upper right corner.

#. Read the precautions carefully and confirm the risks. Then click **OK**.

   After a cluster is removed from a fleet, it is displayed on the **Clusters Not in Fleet** tab. You can add the cluster to the fleet again. For details, see :ref:`Managing Clusters Not in the Fleet <ucs_01_0155>`.

Unregistering a Cluster from a Fleet
------------------------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the fleet name to access the fleet console.

#. In the navigation pane, choose **Container Clusters**. In the card view of the target cluster, click |image3| in the upper right corner.

#. In the **Unregister Cluster** dialog box, read the precautions carefully, confirm the risks, and click **OK**.

#. (Optional) After an attached cluster is unregistered, run the following command to uninstall the agent component from the destination cluster:

   **kubectl -n kube-system delete deployments/proxy-agent secret/proxy-agent-cert**

Deleting a Fleet
----------------

If a fleet is no longer used, you can delete it. There are two restrictions on deletion: there is no cluster in the fleet and cluster federation has been disabled for the fleet. If there are clusters in the fleet, you can :ref:`remove the clusters from the fleet <ucs_01_0004__section171856259306>` and then add them to another fleet. If cluster federation has been enabled for the fleet, disable it following :ref:`Disabling Cluster Federation <ucs_01_0018__section88211316259>`.

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.
#. On the **Fleets** tab, locate the target fleet and click |image4| in the upper right corner.
#. In the dialog box displayed, click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001277812325.png
.. |image2| image:: /_static/images/en-us_image_0000001411282188.png
.. |image3| image:: /_static/images/en-us_image_0000001875972418.png
.. |image4| image:: /_static/images/en-us_image_0000001875805610.png
