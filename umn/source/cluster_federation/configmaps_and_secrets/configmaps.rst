:original_name: ucs_01_0267.html

.. _ucs_01_0267:

ConfigMaps
==========

ConfigMaps allow you to decouple configuration files from container images to enhance the portability of workloads.

ConfigMaps allow you to:

-  Manage configurations for different environments and services.
-  Deploy workloads in different environments. Multiple versions are supported for configuration files so that you can update and roll back workloads easily.
-  Quickly import configurations in the form of files to containers.

.. note::

   -  After a ConfigMap is created on the UCS console, it is in the undeployed state by default. You need to mount the ConfigMap when creating or updating a workload. For details, see :ref:`ConfigMap <ucs_01_0278__section15788171316334>`.
   -  After a ConfigMap is mounted to a workload, a ConfigMap with the same name is created in each cluster to which the workload belongs.

Creating a ConfigMap
--------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its console.

#. Choose **ConfigMaps and Secrets** in the navigation pane and click the **ConfigMaps** tab.

#. Select the namespace for which you want to create a ConfigMap and click **Create ConfigMap** in the upper right corner.

#. Set the parameters listed in :ref:`Table 1 <ucs_01_0267__table16321825732>`.

   .. _ucs_01_0267__table16321825732:

   .. table:: **Table 1** Parameters for creating a ConfigMap

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                              |
      +===================================+==========================================================================================================================================+
      | Name                              | Name of a ConfigMap, which must be unique in a namespace.                                                                                |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
      | Namespace                         | Namespace that the ConfigMap belongs to. The current namespace is used by default.                                                       |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Description of the ConfigMap.                                                                                                            |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
      | ConfigMap Data                    | The workload configuration data can be used in a container or used to store the configuration data.                                      |
      |                                   |                                                                                                                                          |
      |                                   | Click |image1| and enter the key and value. **Key** indicates the configuration name, and **Value** indicates the configuration content. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
      | Label                             | Labels are attached to objects such as workloads, nodes, and Services in key-value pairs.                                                |
      |                                   |                                                                                                                                          |
      |                                   | Labels define identified attributes of these objects and can be used to manage and select objects.                                       |
      |                                   |                                                                                                                                          |
      |                                   | a. Enter the label key and value.                                                                                                        |
      |                                   | b. Click **Confirm**.                                                                                                                    |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

Using a ConfigMap
-----------------

After a ConfigMap is created, you can mount the ConfigMap to a container for storage during workload creation. Then, you can read the ConfigMap data from the mount path of the container. For details, see :ref:`ConfigMap <ucs_01_0278__section15788171316334>`.

Related Operations
------------------

You can also perform operations described in :ref:`Table 2 <ucs_01_0267__table1619535674020>`.

.. _ucs_01_0267__table1619535674020:

.. table:: **Table 2** Related operations

   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Operation                             | Description                                                                                            |
   +=======================================+========================================================================================================+
   | Creating a ConfigMap from a YAML file | Click **Create from YAML** in the upper right corner to create a ConfigMap from an existing YAML file. |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Viewing details                       | Click the ConfigMap name to view its details.                                                          |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Editing a YAML file                   | Click **Edit YAML** in the row where the target ConfigMap resides to edit its YAML file.               |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Updating a ConfigMap                  | #. Choose **More** > **Update** in the **Operation** column of the target ConfigMap.                   |
   |                                       | #. Modify the ConfigMap information according to :ref:`Table 1 <ucs_01_0267__table16321825732>`.       |
   |                                       | #. Click **OK** to submit the modified information.                                                    |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Deleting a ConfigMap                  | Choose **More** > **Delete** in the row where the target ConfigMap resides, and click **Yes**.         |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Deleting ConfigMaps in batches        | #. Select the ConfigMaps to be deleted.                                                                |
   |                                       | #. Click **Delete** in the upper left corner.                                                          |
   |                                       | #. Click **Yes**.                                                                                      |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001503824204.png
