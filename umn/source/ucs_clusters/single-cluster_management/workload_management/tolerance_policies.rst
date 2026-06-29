:original_name: ucs_01_0399.html

.. _ucs_01_0399:

Tolerance Policies
==================

A tolerance policy allows the scheduler to schedule pods to nodes with corresponding taints. This policy must be used together with node taints. One or more taints can be added to each node. For pods without node tolerance policy, the scheduler performs selective scheduling based on the taint effect to prevent pods from being allocated to inappropriate nodes.

.. note::

   In the current UCS version, the NoExecute taint policy is not supported during tolerance configuration when you create a workload.

**Configuring a Tolerance Policy on the Console**

#. Log in to the UCS console.
#. When creating a workload, click **Next: Scheduling and Differentiation**.
#. Add a tolerance policy.

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                        |
   +===================================+====================================================================================================================================================================================================+
   | Taint Key                         | Key of a node taint.                                                                                                                                                                               |
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
