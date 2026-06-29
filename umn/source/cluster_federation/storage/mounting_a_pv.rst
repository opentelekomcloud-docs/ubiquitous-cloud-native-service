:original_name: ucs_01_0279.html

.. _ucs_01_0279:

Mounting a PV
=============

A PVC provides persistent storage management for containers in multiple clouds. The cloud storage can be mounted to containers based on actual requirements, ensuring high reliability of applications.

.. important::

   -  After a PVC is created on the UCS console, a PVC with the same name is automatically created in your cluster. Also a PersistentVolume (PV) is created and bound with the PVC.

   -  You can modify or delete the PVCs automatically created by UCS on the cluster console. However, if the PVC settings on the UCS console are not modified accordingly, the modified or deleted PVCs will be re-created by UCS. You are advised to change the settings on the UCS console.

   -  For a non-T Cloud cluster, when PVCs are used to mount cloud storage volumes, the cluster provider must support storage classes for dynamically creating PVs. Run the following command to query the storage class configuration and the interconnected backend storage resources of the cluster. For more information about storage classes, see `Storage Classes <https://kubernetes.io/docs/concepts/storage/storage-classes/>`__.

      .. code-block::

         kubectl get storageclass

Using a PVC to Mount a Cloud Storage Volume
-------------------------------------------

#. Set the basic container information by referring to :ref:`Creating a Deployment <ucs_01_0255__section146991320135316>`, :ref:`Creating a StatefulSet <ucs_01_0256__section146991320135316>`, or :ref:`Creating a DaemonSet <ucs_01_0257__section146991320135316>`. After setting the basic container information, click **Data Storage**. On the **PersistentVolumeClaims (PVCs)** tab, click |image1|.
#. Select the target PVC. If no PVC is available, click **Create PVC**. For details about related parameters, see :ref:`Creating a PVC <ucs_01_0280>`. Click **OK**.
#. Set the container mount options.

   -  Set **Mount Path** to a path to which the data volume is mounted.

      .. important::

         -  The container path cannot be a system directory, such as **/** or /**var/run**. Otherwise, the container may not function normally. Select an empty directory. If the directory is not empty, ensure that the directory does not contain any files that affect container startup. Otherwise, the files will be replaced, and the container cannot start normally. As a result, the workload may not be deployed.
         -  If a volume is mounted to a high-risk directory, use an account with minimum permissions to start the container. Otherwise, high-risk files on the host may be damaged.

   -  Set **Subpath** to a path of the data volume in the Kubernetes. It is the subpath of the volume instead of the root path. If this parameter is left blank, the root path is used.
   -  Set permissions.

      -  **Read-only**: You can only read the data in the mounted volume.
      -  **Read-write**: You can modify the volume mounted to the path. Newly written data will not be migrated if the container is migrated, which may cause data loss.

#. You can add multiple PVCs.

.. |image1| image:: /_static/images/en-us_image_0000001504004280.png
