:original_name: ucs_01_0114.html

.. _ucs_01_0114:

Creating a ConfigMap
====================

A ConfigMap is a type of resource that stores configuration information required by a workload. Its content is user-defined. After creating ConfigMaps, you can use them as files or environment variables in a workload.

ConfigMaps allow you to decouple configuration files from container images to enhance the portability of workloads.

ConfigMaps provide the following benefits:

-  Manage configurations for different environments and services.
-  Deploy workloads in different environments. Multiple versions are supported for configuration files so that you can update and roll back workloads easily.
-  Quickly import configurations in the form of files to containers.


Creating a ConfigMap
--------------------

#. Access the cluster console. In the navigation pane, choose **ConfigMaps and Secrets**. Then, click the **ConfigMaps** tab. You can create a ConfigMap directly or using YAML. If you want to create a ConfigMap using YAML, go to :ref:`4 <ucs_01_0114__en-us_topic_0160121210_li2731182712159>`.

#. Select the namespace that the ConfigMap will belong to.

#. Create a ConfigMap directly by clicking **Create ConfigMap**.

   Configure the parameters as described in :ref:`Table 1 <ucs_01_0114__table16321825732>`.

   .. _ucs_01_0114__table16321825732:

   .. table:: **Table 1** Parameters for creating a ConfigMap

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                              |
      +===================================+==========================================================================================================================================================================================================+
      | Name                              | Name of the ConfigMap you create, which must be unique in a namespace.                                                                                                                                   |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Namespace                         | Namespace that the ConfigMap belongs to. The current namespace is used by default.                                                                                                                       |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Description of the ConfigMap.                                                                                                                                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | ConfigMap Data                    | The workload configuration data can be used in a container or used to store the configuration data.                                                                                                      |
      |                                   |                                                                                                                                                                                                          |
      |                                   | Click |image1| and enter the key and value. **Key** indicates the configuration name, and **Value** indicates the configuration content.                                                                 |
      |                                   |                                                                                                                                                                                                          |
      |                                   | .. note::                                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                          |
      |                                   |    ConfigMaps can be used to create workload storage volumes and configure workload environment variables. When configuring workload environment variables, ensure that the ConfigMap data is not empty. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Label                             | Labels are attached to objects such as workloads, nodes, and Services in key-value pairs.                                                                                                                |
      |                                   |                                                                                                                                                                                                          |
      |                                   | Labels define the identifiable attributes of these objects and are used to manage and select the objects.                                                                                                |
      |                                   |                                                                                                                                                                                                          |
      |                                   | a. Enter the key and value.                                                                                                                                                                              |
      |                                   | b. Click **Confirm**.                                                                                                                                                                                    |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. .. _ucs_01_0114__en-us_topic_0160121210_li2731182712159:

   Create a ConfigMap from a YAML file by clicking **Create from YAML**.

   .. note::

      To create a resource by uploading a file, ensure that the resource description file has been created. UCS supports files in JSON or YAML format. For details, see :ref:`ConfigMap Resource File Configuration <ucs_01_0114__en-us_topic_0160121210_section66903416102>`.

   You can import or directly write the file content in YAML or JSON format.

   -  Method 1: Import an orchestration file.

      Click **Import** to import a YAML or JSON file. The content of the YAML or JSON file is displayed in the orchestration content area.

   -  Method 2: Directly orchestrate the content.

      In the orchestration content area, enter the content of the YAML or JSON file.

#. When the configuration is complete, click **OK**.

   The new ConfigMap is displayed in the ConfigMap list.

.. _ucs_01_0114__en-us_topic_0160121210_section66903416102:

ConfigMap Resource File Configuration
-------------------------------------

A ConfigMap resource file can be in JSON or YAML format, and the file size cannot exceed 2 MB.

-  JSON format

   The file name is **configmap.json** and the configuration example is as follows:

   .. code-block::

      {
        "kind": "ConfigMap",
        "apiVersion": "v1",
        "metadata": {
          "name": "paas-broker-app-017",
          "namespace": "test"
        },
        "data": {
          "context": "{\"applicationComponent\":{\"properties\":{\"custom_spec\":{}},\"node_name\":\"paas-broker-app\",\"stack_id\":\"0177eae1-89d3-cb8a-1f94-c0feb7e91d7b\"},\"softwareComponents\":[{\"properties\":{\"custom_spec\":{}},\"node_name\":\"paas-broker\",\"stack_id\":\"0177eae1-89d3-cb8a-1f94-c0feb7e91d7b\"}]}"
        }
      }

-  YAML format

   The file name is **configmap.yaml** and the configuration example is as follows:

   .. code-block::

      apiVersion: v1
      kind: ConfigMap
      metadata:
        name: test-configmap
        namespace: default
      data:
        data-1: "value-1"
        data-2: "value-2"

Related Operations
------------------

On the cluster console, you can also perform the operations described in :ref:`Table 2 <ucs_01_0114__en-us_topic_0160121210_table1619535674020>`.

.. _ucs_01_0114__en-us_topic_0160121210_table1619535674020:

.. table:: **Table 2** Related operations

   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Operation                         | Description                                                                               |
   +===================================+===========================================================================================+
   | Viewing details                   | Click the ConfigMap name to view its details.                                             |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Editing a YAML file               | Click **Edit YAML** in the row where the target ConfigMap resides to edit its YAML file.  |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Updating a ConfigMap              | #. Click **Update** in the row where the target ConfigMap resides.                        |
   |                                   | #. Modify the ConfigMap data according to :ref:`Table 1 <ucs_01_0114__table16321825732>`. |
   |                                   | #. Click **OK** to submit the modified information.                                       |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Deleting a ConfigMap              | Click **Delete** in the row where the target ConfigMap resides, and click **Yes**.        |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Deleting ConfigMaps in batches    | #. Select the ConfigMap to be deleted.                                                    |
   |                                   | #. Click **Delete** in the upper left corner.                                             |
   |                                   | #. Click **Yes**.                                                                         |
   +-----------------------------------+-------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000002069472218.png
