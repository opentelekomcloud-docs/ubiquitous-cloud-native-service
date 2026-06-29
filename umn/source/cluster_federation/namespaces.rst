:original_name: ucs_01_0281.html

.. _ucs_01_0281:

Namespaces
==========

A namespace is an abstract integration of a group of resources and objects in a cluster. Namespace-level resource quotas limit the amount of resources available to teams or projects that use the same cluster.

.. _ucs_01_0281__section20381629121511:

Creating a Namespace
--------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its details page.

#. Choose **Namespaces** in the navigation pane and click **Create Namespace** in the upper right corner.

#. Set namespace parameters based on :ref:`Table 1 <ucs_01_0281__table5523151617575>`.

   .. _ucs_01_0281__table5523151617575:

   .. table:: **Table 1** Parameters for creating a namespace

      +-------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter   | Description                                                                                                                                                      |
      +=============+==================================================================================================================================================================+
      | Name        | Name of a namespace, which must be unique in a cluster.                                                                                                          |
      +-------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Label       | Add labels to namespaces and define different attributes in the key-value pair format. You can learn the characteristics of each namespace through these labels. |
      +-------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Annotation  | Add customized annotations to the namespace in the key-value pair format.                                                                                        |
      +-------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description | Description of the namespace.                                                                                                                                    |
      +-------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. When the configuration is complete, click **OK**.

   After the creation is complete, you can click **View YAML** to view and download the YAML file.

Using Namespaces
----------------

Namespaces can be used when creating Services, ingresses, and PVCs. The following uses workload creation as an example to describe how a namespace is used.

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.
#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its details page.
#. In the navigation pane, choose **Workloads**. On the **Deployments** tab, click **Create from Image** in the upper right corner.
#. Configure the basic information about the workload and select the namespace where the workload is located.
#. Complete the configuration.

Deleting a Namespace
--------------------

.. important::

   -  Deleting a namespace on the UCS console will delete the namespace with the same name in each cluster as well as all data resources related to the namespace. Exercise caution when performing this operation.
   -  To ensure that UCS runs properly, namespaces whose source is **System** or **Default** cannot be deleted.

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its details page.

#. Choose **Namespaces** in the navigation pane. In the namespace list, click **Delete** in the row of the target namespace.

   To delete multiple namespaces at a time, select the namespaces and click **Delete** in the upper left corner.

#. Click **Yes** as prompted.
