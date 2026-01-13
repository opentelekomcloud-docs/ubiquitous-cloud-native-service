:original_name: ucs_01_0104.html

.. _ucs_01_0104:

Adding Labels/Taints to Nodes
=============================

UCS allows you to add different labels to nodes to define different node attributes. By using these labels, you can quickly understand the characteristics of each node.

Taints enable a node to repel specific pods to prevent these pods from being scheduled to the node, achieving reasonable allocation of workloads on nodes.

Node Label Usage Scenarios
--------------------------

Node labels are mainly used in the following scenarios:

-  Node classification: Node labels are used to classify nodes.
-  Affinity and anti-affinity:

   -  If a workload consumes too much CPU, memory, or I/O on a node, other workloads on the node may not run normally. You can add labels to nodes. This way, when you deploy workloads, you can configure workload affinity and anti-affinity based on the node labels.
   -  An application may contain multiple modules, each with multiple microservices. To make O&M efficient, you can add a module label to each node so that microservices of the same module can be deployed on the same node. This way, modules do not interfere with each other and microservices can be easily maintained.

Inherent Node Labels
--------------------

After a node is created, UCS adds labels to the node. These inherent labels cannot be edited or deleted. :ref:`Table 1 <ucs_01_0104__en-us_topic_0155106002_table83962234533>` lists the inherent labels of a node.

.. _ucs_01_0104__en-us_topic_0155106002_table83962234533:

.. table:: **Table 1** Inherent labels of a node

   +------------------------------------------+----------------------------------------------------------------------------------------------------+
   | Key                                      | Value                                                                                              |
   +==========================================+====================================================================================================+
   | failure-domain.beta.kubernetes.io/region | Indicates the region where the node is located.                                                    |
   +------------------------------------------+----------------------------------------------------------------------------------------------------+
   | failure-domain.beta.kubernetes.io/zone   | Indicates the AZ where the node is located.                                                        |
   +------------------------------------------+----------------------------------------------------------------------------------------------------+
   | beta.kubernetes.io/arch                  | Indicates the processor architecture of the node.                                                  |
   |                                          |                                                                                                    |
   |                                          | For example, **amd64** indicates a AMD64-bit processor.                                            |
   +------------------------------------------+----------------------------------------------------------------------------------------------------+
   | beta.kubernetes.io/os                    | Indicates the operating system of the node.                                                        |
   |                                          |                                                                                                    |
   |                                          | For example, **linux** indicates that the node uses Linux as its operating system.                 |
   +------------------------------------------+----------------------------------------------------------------------------------------------------+
   | kubernetes.io/availablezone              | Indicates the AZ where the node is located.                                                        |
   +------------------------------------------+----------------------------------------------------------------------------------------------------+
   | kubernetes.io/hostname                   | Indicates the host name of the node.                                                               |
   +------------------------------------------+----------------------------------------------------------------------------------------------------+
   | os.architecture                          | Indicates the processor architecture of the node.                                                  |
   |                                          |                                                                                                    |
   |                                          | For example, **amd64** indicates a AMD64-bit processor.                                            |
   +------------------------------------------+----------------------------------------------------------------------------------------------------+
   | os.name                                  | Indicates the operating system name of the node.                                                   |
   |                                          |                                                                                                    |
   |                                          | For example, **EulerOS_2.0_SP2** indicates that the node uses EulerOS 2.2 as its operating system. |
   +------------------------------------------+----------------------------------------------------------------------------------------------------+
   | os.version                               | Indicates the kernel version of the node.                                                          |
   +------------------------------------------+----------------------------------------------------------------------------------------------------+

.. _ucs_01_0104__en-us_topic_0155106002_section1987385718113:

Taint
-----

Taints are in the format of **Key=Value:Effect**. **Key** and **Value** are the labels of a taint. **Value** can be empty. **Effect** is used to describe the effect of taints. The following options are supported for **Effect**:

-  **NoSchedule**: No pod will be able to schedule onto the node unless it has a matching toleration, but existing pods will not be evicted from the node.
-  **NoExecute**: Pods that cannot tolerate this taint cannot be scheduled onto the node, and existing pods will be evicted from the node.

Toleration
----------

Tolerations are applied to pods, and allow (not forcibly) the pods to schedule onto nodes with matching taints.

Taints and tolerations work together to ensure that pods are not scheduled onto inappropriate nodes. One or more taints are applied to a node. This marks that the node should not accept any pods that do not tolerate the taints.

Example:

.. code-block::

   apiVersion: v1
   kind: Pod
   metadata:
     name: nginx
     labels:
       env: test
   spec:
     containers:
     - name: nginx
       image: nginx
       imagePullPolicy: IfNotPresent
     tolerations:
     - key: "key1"
       operator: "Equal"
       value: "value1"
       effect: "NoSchedule"

In the preceding toleration label, **key** is **key1**, **value** is **value1**, and **effect** is **NoSchedule**. Therefore, the pod can be scheduled to the corresponding node.

The tolerance can also be set as follows, indicating that when a taint whose **key** is **key1** and **effect** is **NoSchedule** exists on a node, the pod can also be scheduled to the corresponding node.

.. code-block::

   tolerations:
   - key: "key1"
     operator: "Exists"
     effect: "NoSchedule"

Managing Node Labels/Taints
---------------------------

#. Access the cluster console.
#. In the navigation pane, choose **Nodes**, select the target node, and click **Manage Labels and Taints**.
#. Click |image1| to add a node label or taint. You can add a maximum of 10 operations at a time.

   -  Choose **Add/Update** or **Delete**.
   -  Set the operation object to **Kubernetes Label** or **Taint**.
   -  Specify **Key** and **Value**.
   -  If you choose **Taint**, select a taint effect. For details, see :ref:`Taint <ucs_01_0104__en-us_topic_0155106002_section1987385718113>`.

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001377241982.png
