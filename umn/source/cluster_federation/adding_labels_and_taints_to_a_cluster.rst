:original_name: ucs_01_0318.html

.. _ucs_01_0318:

Adding Labels and Taints to a Cluster
=====================================

UCS allows you to add different labels to clusters to define different attributes. By using these cluster labels, you can quickly understand the characteristics of each cluster. Taints enable a cluster to repel specific pods to prevent these pods from being scheduled to the cluster, achieving reasonable allocation of workloads on clusters.

Labels
------

You can add different labels to clusters to classify and manage clusters.

.. _ucs_01_0318__en-us_topic_0155106002_section1987385718113:

Taints
------

Taints are in the format of **Key=Value:Effect**. **Key** and **Value** are the labels of a taint. **Value** can be empty. **Effect** is used to describe the effect of taints. The following option is supported for **Effect**:

-  **NoSchedule**: No pod will be able to schedule onto the cluster unless it has a matching toleration, but existing pods will not be evicted from the cluster.

.. note::

   Currently, UCS does not support pod eviction using the NoExecute taint policy.

Managing Cluster Labels and Taints
----------------------------------

#. Log in to the UCS console.
#. Click the name of the fleet where the target cluster is located. In the navigation pane, choose **Container Clusters**, locate the target cluster, and click |image1| in the upper right corner to go to the **Manage Labels and Taints** page.
#. Click |image2| to add a node label or taint. You can add a maximum of 10 operations at a time.

   -  Choose **Add** or **Delete**.
   -  Set the operation object to **Kubernetes Label** or **Taint**.
   -  Specify **Key** and **Value**.
   -  If you choose **Taint**, select a taint effect. For details, see :ref:`Taints <ucs_01_0318__en-us_topic_0155106002_section1987385718113>`.

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001568318244.png
.. |image2| image:: /_static/images/en-us_image_0000001568637180.png
