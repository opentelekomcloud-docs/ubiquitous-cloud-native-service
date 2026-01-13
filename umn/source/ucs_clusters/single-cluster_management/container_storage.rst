:original_name: ucs_01_0112.html

.. _ucs_01_0112:

Container Storage
=================

To mount a PVC to a cluster, the cluster provider must support the StorageClass resource to dynamically create storage volumes. You can choose **Storage** on the cluster console and click the **Storage Classes** tab to view the storage classes supported by the cluster. For more information about StorageClass, see `Storage Classes <https://kubernetes.io/docs/concepts/storage/storage-classes/>`__.

Creating a PVC
--------------

#. Access the cluster console.
#. In the navigation pane, choose **Storage**. On the displayed page, click the **PVCs** tab. Then click **Create from YAML** in the upper right corner.
#. Write a YAML file for the PVC.
#. Click **OK**.
