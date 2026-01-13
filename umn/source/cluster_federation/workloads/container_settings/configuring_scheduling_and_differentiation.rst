:original_name: ucs_01_0037.html

.. _ucs_01_0037:

Configuring Scheduling and Differentiation
==========================================

Scheduling Policies
-------------------

Currently, there are two scheduling policies: cluster weights and automatic balancing.

**Configuring a Scheduling Policy on the Console**

#. Log in to the UCS console.
#. When creating a workload, click **Next: Scheduling and Differentiation**.
#. Add a scheduling policy.

   .. table:: **Table 1** Scheduling policies

      +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Policy          | Description                                                                                                                                                     |
      +=================+=================================================================================================================================================================+
      | Cluster weights | You need to select clusters and configure their weights. Pods are allocated to clusters based on the :ref:`cluster weights <ucs_01_0037__section042702214566>`. |
      +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Auto balancing  | The system automatically selects clusters to allocate pods based on the number of remaining pods. No extra configuration is required.                           |
      +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ucs_01_0037__section042702214566:

Calculation Method Based on Cluster Weights
-------------------------------------------

**Calculation Method**

After you set the weight of each cluster, the number of pods allocated to each cluster is calculated as follows:

#. Formula for calculating the number of pods allocated to each cluster by cluster weight (The calculation result is rounded down.)

   Number of pods allocated to each cluster = (Total number of pods x Weight of a cluster)/Total weight of clusters

#. Formula for calculating the number of remaining pods

   Number of remaining pods = Total number of pods - Total number of pods allocated to each cluster

#. If there are any pods remaining, they will continue to be allocated by cluster weight in ascending order (one pod allocated at a time). If any clusters have the same weight, a cluster will be selected at random.

**Example**

There are seven pods that are assigned to three clusters named member1, member2, and member3. The clusters have weights of 2, 1, and 1, respectively.

#. The number of pods allocated to each cluster is calculated as follows:

   Number of pods allocated to member1 = 7 x 2/4 (rounded down to 3)

   Number of pods allocated to member2 = 7 x 1/4 (rounded down to 1)

   Number of pods allocated to member3 = 7 x 1/4 (rounded down to 1)

   In this initial allocation, three pods are allocated to member1, one pod to member2, and one pod to member3.

#. The number of remaining pods is calculated as follows:

   Number of remaining pods = 7 - 3 - 1 - 1 = 2

#. The remaining pods are allocated by cluster weight in ascending order.

   One pod is first allocated to member1 and the remaining pod to member2 or member3 at random.

Tolerance Policies
------------------

A tolerance policy allows the scheduler to schedule pods to clusters with corresponding taints. This policy must be used together with cluster taints.

**Using the Default Tolerance Policy**

When you create a workload, UCS configures a default tolerance policy for your workload. The default tolerance policy adds taints listed in :ref:`Table 2 <ucs_01_0037__table7136162420189>` to a faulty cluster. If the tolerance duration is exceeded, all pods in the cluster will be automatically evicted.

.. _ucs_01_0037__table7136162420189:

.. table:: **Table 2** Taints for faulty clusters

   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Taint Key                      | Tolerance Policy                                                                                                                                                  |
   +================================+===================================================================================================================================================================+
   | cluster.karmada.io/not-ready   | When the cluster is not ready, this taint is automatically added. If the tolerance duration is exceeded, all pods in the cluster will be automatically evicted.   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster.karmada.io/unreachable | When the cluster is unavailable, this taint is automatically added. If the tolerance duration is exceeded, all pods in the cluster will be automatically evicted. |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Configuring a Tolerance Policy on the Console**

#. Log in to the UCS console.
#. When creating a workload, click **Next: Scheduling and Differentiation**.
#. Add a tolerance policy.

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                        |
   +===================================+====================================================================================================================================================================================================+
   | Taint Key                         | Taint key of the cluster.                                                                                                                                                                          |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operator                          | -  **Equal**: matches the nodes with the specified taint key (mandatory) and value. If the taint value is left blank, all taints with the key the same as the specified taint key will be matched. |
   |                                   | -  **Exists**: matches the nodes with the specified taint key. In this case, the taint value cannot be specified. If the taint key is left blank, all taints will be tolerated.                    |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Taint Value                       | -  If the value of **Operator** is **Exists**, the value attribute can be omitted.                                                                                                                 |
   |                                   | -  If the value of **Operator** is **Equal**, the relationship between the key and value is **Equal**.                                                                                             |
   |                                   | -  If **Operator** is not specified, the default value is **Equal**.                                                                                                                               |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Taint Policy                      | -  **All**: All taint policies are matched.                                                                                                                                                        |
   |                                   | -  **NoSchedule**: Only the **NoSchedule** taint is matched.                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
