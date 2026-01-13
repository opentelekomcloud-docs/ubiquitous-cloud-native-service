:original_name: ucs_01_0277.html

.. _ucs_01_0277:

Overview
========

You can configure a storage class in the **Add Container** step of creating a workload.

Local Storage
-------------

You can mount the file directory of the host where a container is located to a specified container path (corresponding to hostPath in Kubernetes). Alternatively, you can leave the source path empty (corresponding to emptyDir in Kubernetes). If the source path is left empty, a temporary directory of the host will be mounted to the mount point of the container. A specified source path is used when data needs to be persistently stored on the host, while emptyDir is used when temporary storage is needed. A ConfigMap is a type of resource that stores configuration information required by a workload. Its content is user-defined. A secret is a type of resource that holds sensitive data, such as authentication and key information, required by a workload. Its content is user-defined. For details, see :ref:`Mounting a Local Volume <ucs_01_0278>`.

PVCs
----

You can create PVs and mount them to a container path. When containers are migrated, cloud storage volumes are mounted to new containers to ensure data reliability. For details, see :ref:`Mounting a PV <ucs_01_0279>`. You are advised to select PVCs when creating a workload and store pod data in corresponding cloud storage volumes. If you store pod data in a local volume, the data cannot be restored when the node becomes faulty.

-  UCS can automatically create EVS, OBS, and SFS volumes and mount them to the container path of a OTC cluster.

   -  EVS offers scalable block storage with high reliability, high performance, and extensive specifications for containers. EVS stores binary data and cannot store files directly. This storage class is applicable when data needs to be stored permanently.
   -  SFS provides high-performance file storage (NAS) that can be expanded on demand. It provides shared file access for containers and is used for persistent storage in ReadWriteMany scenarios, including media processing, content management and web services, and big data and application analysis.
   -  OBS provides unlimited storage capacity for objects/files in any format. It is mainly designed for scenarios involving storage and analysis of massive data, query of historical data details, analysis on a large number of behavior logs, and statistical analysis on public transactions.

-  For a non-OTC cluster, when PVCs are used to mount cloud storage volumes, the cluster provider must support storage classes. For details, see `Storage Classes <https://kubernetes.io/docs/concepts/storage/storage-classes/>`__.
