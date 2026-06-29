:original_name: ucs_01_0280.html

.. _ucs_01_0280:

Creating a PVC
==============

.. important::

   -  After a PVC is created on the UCS console, a PVC with the same name is automatically created in your cluster. Also a PersistentVolume (PV) is created and bound with the PVC.

   -  You can modify or delete the PVCs automatically created by UCS on the cluster console. However, if the PVC settings on the UCS console are not modified accordingly, the modified or deleted PVCs will be re-created by UCS. You are advised to change the settings on the UCS console.

   -  For a non-T Cloud cluster, when PVCs are used to mount cloud storage volumes, the cluster provider must support storage classes for dynamically creating PVs. Run the following command to query the storage class configuration and the interconnected backend storage resources of the cluster. For more information about storage classes, see `Storage Classes <https://kubernetes.io/docs/concepts/storage/storage-classes/>`__.

      .. code-block::

         kubectl get storageclass


Creating a PVC
--------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its console.

#. In the navigation pane, choose **Storage**. On the **PersistentVolumeClaims (PVCs)** tab, click **Create PVC** in the upper right corner.

#. .. _ucs_01_0280__li2054518163575:

   Specify basic information.

   -  **Name**: Enter a unique name of a PVC to be added.
   -  **Namespace**: namespace that the PVC will belong to. If this parameter is not specified, the default namespace is used.
   -  **Cluster**: Click |image1| to select the cluster where the PVC is to be deployed.

      -  For details about the parameters for adding a T Cloud cluster, see :ref:`Table 1 <ucs_01_0280__table68391084401>`.
      -  For details about the parameters for adding a non-T Cloud cluster, see :ref:`Table 2 <ucs_01_0280__table1057124594410>`.

         .. important::

            When creating a PVC for an attached cluster, you need to specify the corresponding annotations based on the actually interconnected with the cluster for the PVC to take effect. For more information, see `Annotations <https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/>`__ and `kubectl annotate <https://kubernetes.io/docs/reference/kubectl/generated/kubectl_annotate/>`__.

   .. _ucs_01_0280__table68391084401:

   .. table:: **Table 1** Parameters for adding a T Cloud cluster

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                               |
      +===================================+===========================================================================================================================================================================+
      | Cluster                           | Select a T Cloud cluster.                                                                                                                                                 |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Storage Class                     | -  **csi-disk**: EVS disk. Specify the AZ and disk type.                                                                                                                  |
      |                                   |                                                                                                                                                                           |
      |                                   |    -  **AZ**: Specify the AZ where the EVS disk is located. The supported EVS disk types may vary in different AZs.                                                       |
      |                                   |    -  **EVS Disk Type**: Available disk types are common I/O, high I/O, and ultra-high I/O, and the storage pools corresponding to the disk types are SATA, SAS, and SSD. |
      |                                   |                                                                                                                                                                           |
      |                                   | -  **csi-nas**: indicates SFS.                                                                                                                                            |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Access Mode                       | -  If **csi-disk** is selected, **Access Mode** must be set to **ReadWriteOnce**. This means the volume can be mounted as read-write by only a single node.               |
      |                                   | -  If **csi-nas** (file storage) is selected, **Access Mode** must be set to **ReadWriteMany**. This means the volume can be mounted as read-write by multiple nodes.     |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Capacity (GiB)                    | The capacity of the created PVC cannot be less than 10 GiB.                                                                                                               |
      |                                   |                                                                                                                                                                           |
      |                                   | Set this parameter only when **csi-disk** (EVS disk) or **csi-nas** (file storage) is selected.                                                                           |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. _ucs_01_0280__table1057124594410:

   .. table:: **Table 2** Parameters for adding a non-T Cloud cluster

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                 |
      +===================================+=============================================================================================================================================================================================================+
      | Cluster                           | Select a non-T Cloud cluster.                                                                                                                                                                               |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Storage Class                     | The storage classes supported by a cluster depend on the actual environment of the registered cluster. For details, see `Storage Classes <https://kubernetes.io/docs/concepts/storage/storage-classes/>`__. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Access Mode                       | -  **ReadWriteOnce** (RWO): The PVC can be mounted as read-write only by a single node.                                                                                                                     |
      |                                   | -  **ReadWriteMany** (RWX): The PVC can be mounted as read-write by multiple nodes.                                                                                                                         |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Capacity (GiB)                    | The capacity of the created PVC cannot be less than 10 GiB.                                                                                                                                                 |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Annotation                        | Set the key and value and click **Add**. Annotations are attached to PVCs in the form of key-value pairs.                                                                                                   |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Add more key-value pairs to specify differentiated settings for each cluster.

#. Click **OK**. After the PVC is successfully created, you can click the PVC name to view the details.

Related Operations
------------------

You can also perform operations described in :ref:`Table 3 <ucs_01_0280__table1619535674020>`.

.. _ucs_01_0280__table1619535674020:

.. table:: **Table 3** Related operations

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                         | Description                                                                                                                                           |
   +===================================+=======================================================================================================================================================+
   | Creating a PVC from a YAML file   | Click **Create from YAML** in the upper right corner to create a PVC from an existing YAML file.                                                      |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Viewing details                   | #. Select the namespace that the PVC will belong to.                                                                                                  |
   |                                   | #. (Optional) Search for a PVC by its name.                                                                                                           |
   |                                   | #. Click the PVC name to view its details, including the basic information and deployment information of each cluster.                                |
   |                                   | #. On the **PVC Details** page, click **View YAML** in the **Cluster** area to view or download YAML files of PVCs deployed in each cluster.          |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Viewing the YAML file             | Click **View YAML** next to the PVC name to view the YAML file of the current PVC.                                                                    |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Update (Expanding a PVC)          | #. Choose **More** > **Update** in the row where the target PVC resides.                                                                              |
   |                                   | #. Modify the cluster deployment parameters based on the :ref:`PVC parameters <ucs_01_0280__li2054518163575>`, or click **Expand** to expand the PVC. |
   |                                   | #. Click **OK** to submit the modified information.                                                                                                   |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting a PVC                    | Choose **More** > **Delete** in the row where the target PVC resides, and click **Yes**.                                                              |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting PVCs in batches          | #. Select PVCs to be deleted.                                                                                                                         |
   |                                   | #. Click **Delete** in the upper left corner.                                                                                                         |
   |                                   | #. Click **Yes**.                                                                                                                                     |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001504164728.png
