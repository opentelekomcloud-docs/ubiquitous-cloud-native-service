:original_name: ucs_01_0103.html

.. _ucs_01_0103:

Viewing Nodes in a Cluster
==========================

After a cluster is connected to UCS, you can access the cluster console from UCS to view the nodes in a cluster.

Procedure
---------

#. Access the cluster console.
#. In the navigation pane, choose **Nodes** to view the nodes in a cluster.
#. Choose **More** > **View Pods** in the **Operation** column of the target node to view pods running on the current node.
#. Click **View Events** to view node events.
#. Choose **More** > **Disable Scheduling** in the **Operation** column of the target node to set the node as non-schedulable so that new pods cannot be scheduled to this node. For details about node taints, see :ref:`Adding Labels/Taints to Nodes <ucs_01_0104>`.
