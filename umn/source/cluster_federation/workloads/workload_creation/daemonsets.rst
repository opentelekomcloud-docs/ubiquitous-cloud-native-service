:original_name: ucs_01_0257.html

.. _ucs_01_0257:

DaemonSets
==========

A DaemonSet ensures that a pod runs on all (or some) nodes in a cluster. When a new node is added to the cluster, a pod will be automatically deployed on it. When a node is removed from the cluster, the pod on the node is also reclaimed. A typical use of a DaemonSet is running a log collection daemon on every node in the cluster. If a DaemonSet is deleted, all pods created by it will be deleted.

.. _ucs_01_0257__section146991320135316:

Creating a DaemonSet
--------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its console.

#. In the navigation pane, choose **Workloads**. On the displayed page, click the **DaemonSets** tab. Then, click **Create from Image** in the upper right corner.

   .. note::

      To use an existing YAML file to create a DaemonSet, click **Create from YAML** in the upper right corner.

      If "ApplyPolicyFailed" is generated after an application is created, check whether "ApplyPolicySucceed" is generated. If yes, ignore "ApplyPolicyFailed". If no, contact the UCS on-call personnel for support.

#. Configure basic information about the workload.

   -  **Type**: Select **DaemonSet**.
   -  **Name**: name of the workload, which must be unique.
   -  **Namespace**: namespace that the workload belongs to. For details about how to create a namespace, see :ref:`Creating a Namespace <ucs_01_0281__section20381629121511>`.
   -  **Description**: description of the workload.

#. Configure the container settings for the workload.

   Multiple containers can be configured in a pod. You can click **Add Container** on the right to configure multiple containers for the pod.

   -  **Basic Info**

      .. table:: **Table 1** Basic information parameters

         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                                                                                                                                                                              |
         +===================================+==========================================================================================================================================================================================================================================================================================+
         | Container Name                    | Name the container.                                                                                                                                                                                                                                                                      |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Image Name                        | Click **Select Image** and select the image used by the container.                                                                                                                                                                                                                       |
         |                                   |                                                                                                                                                                                                                                                                                          |
         |                                   | -  **My Images**: images in the image repository of the current region. If no images are available, click **Upload Image**.                                                                                                                                                              |
         |                                   | -  **Open Source Images**: official images in the open source image repository.                                                                                                                                                                                                          |
         |                                   | -  **Shared Images**: private images shared by another account. For details, see `Sharing Private Images <https://docs.otc.t-systems.com/software-repository-container/umn/image_management/sharing_private_images.html#swr-01-0026>`__.                                                 |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Image Tag                         | Select the image tag to be deployed.                                                                                                                                                                                                                                                     |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Pull Policy                       | Image update or pull policy. If you select **Always**, the image is pulled from the image repository each time. If you do not select **Always**, the existing image of the node is preferentially used. If the image does not exist in the node, it is pulled from the image repository. |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | CPU Quota                         | -  **Request**: minimum number of CPU cores required by a container. The default value is 0.25 cores.                                                                                                                                                                                    |
         |                                   | -  **Limit**: maximum number of CPU cores available for a container. Do not leave **Limit** unspecified. Otherwise, intensive use of container resources will occur and your workload may exhibit unexpected behavior.                                                                   |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Memory Quota                      | -  **Request**: minimum amount of memory required by a container. The default value is 512 MiB.                                                                                                                                                                                          |
         |                                   | -  **Limit**: maximum amount of memory available for a container. When memory usage exceeds the specified memory limit, the container will be terminated.                                                                                                                                |
         |                                   |                                                                                                                                                                                                                                                                                          |
         |                                   | For details about **Request** and **Limit** of CPU or memory, see :ref:`Setting Container Specifications <ucs_01_0260>`.                                                                                                                                                                 |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Init Container                    | Select whether to use the container as an init container.                                                                                                                                                                                                                                |
         |                                   |                                                                                                                                                                                                                                                                                          |
         |                                   | An init container is a special container that runs before app containers in a pod. For details, see `Init Containers <https://kubernetes.io/docs/concepts/workloads/pods/init-containers/>`__.                                                                                           |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   -  **Lifecycle**: The lifecycle callback functions can be called in specific phases of the container. For example, if you want the container to perform a certain operation before stopping, set the corresponding function. Currently, lifecycle callback functions, such as startup, post-start, and pre-stop functions, are provided. For details, see :ref:`Setting Container Lifecycle Parameters <ucs_01_0261>`.
   -  **Health Check**: Set health check parameters to periodically check the health status of the container during container running. For details, see :ref:`Setting Health Check for a Container <ucs_01_0262>`.
   -  **Environment Variable**: Environment variables affect the way a running container will behave. Configuration items set by environment variables will not change if the pod lifecycle ends. For details, see :ref:`Setting Environment Variables <ucs_01_0263>`.
   -  **Data Storage**: Store container data using **Local Volumes** and **PersistentVolumeClaims (PVCs)**. You are advised to use PVCs to store workload pod data on a cloud volume. If you store pod data on a local volume and a fault occurs on the node, the data cannot be restored. For details about container storage, see :ref:`Storage <ucs_01_0276>`.
   -  **Security Context**: Set container permissions to protect the system and other containers from being affected. Enter a user ID and the container will run with the user permissions you specify.

   -  **Image Access Credential**: Select the credential for accessing the image repository. This credential is used only for accessing a private image repository. If the selected image is a public image, you do not need to select a secret. For details on how to create a secret, see :ref:`Creating a Secret <ucs_01_0268__section129181141173214>`.

#. (Optional) Click |image1| in the **Service Settings** area to configure a Service for the workload.

   If your workload will be reachable to other workloads or public networks, add a Service to define the workload access type. The workload access type determines the network attributes of the workload. Workloads with different access types can provide different network capabilities. For details, see :ref:`Services and Ingresses <ucs_01_0269>`.

   You can also create a Service after creating a workload. For details, see :ref:`ClusterIP <ucs_01_0271>` and :ref:`NodePort <ucs_01_0272>`.

   -  **Name**: name of the Service to be added. It is user-defined and must be unique.
   -  **Type**

      -  **ClusterIP**: The Service is only reachable from within the cluster.
      -  **NodePort**: The Service can be accessed from any node in the cluster.

   -  **Affinity** (for node access only)

      -  **Cluster**: The IP addresses and access ports of all nodes in a cluster can be used to access the workload associated with the Service. However, performance loss is introduced due to hops, and source IP addresses cannot be obtained.
      -  **Node**: Only the IP address and access port of the node where the workload is located can be used to access the workload associated with the Service. Service access will not cause performance loss due to route redirection, and the source IP address of the client can be obtained.

   -  **Port**

      -  **Protocol**: Select **TCP** or **UDP**.
      -  **Service Port**: port mapped to the container port at the cluster-internal IP address. The application can be accessed at <*cluster-internal IP address*>:<*access port*>. The port number range is 1-65535.
      -  **Container Port**: port on which the workload listens, defined in the container image. For example, the Nginx application listens on port 80 (container port).
      -  **Node Port** (for NodePort only): port to which the container port will be mapped when the node private IP address is used for accessing the application. The port number ranges from **30000** to **32767**. You are advised to select **Auto**.

         -  **Auto**: The system automatically assigns a port number.
         -  **Custom**: Specify a fixed node port. The port number ranges from 30000 to 32767. Ensure that the port is unique in a cluster.

#. (Optional) Click **Show more** to specify advanced settings for the workload.

   -  **Upgrade Policy**: upgrade mode of the DaemonSet. You can set **Upgrade Mode** to **Replace** or **Rolling**. For details, see :ref:`Configuring a Workload Upgrade Policy <ucs_01_0264>`.

      -  **Rolling**: An old pod is gradually replaced with a new pod. During the upgrade, service traffic is evenly distributed to the old and new pods to ensure service continuity.
      -  **Replace**: You need to delete old pods manually before new pods are created. Services will be interrupted during a replace upgrade.

   -  **Scheduling**: You can set affinity and anti-affinity to implement planned scheduling for pods. For details, see :ref:`Configuring a Scheduling Policy (Affinity/Anti-affinity) <ucs_01_0265>`.
   -  **Labels and Annotations**: You can click **Confirm** to add a label or annotation for the pod. The key of the new label or annotation cannot be the same as that of an existing one.

#. Click **Next: Scheduling and Differentiation**. After selecting clusters to which the workload can be scheduled, configure the differentiated settings for the containers.

   -  **Scheduling Policy**

      -  **Scheduling Mode**

         -  **Replication**: The workload will be deployed in all clusters selected below.

      -  **Cluster**: Click to select clusters to which the workload can be scheduled. The number of clusters depends on your service requirements.

   -  **Differentiated Settings**

      When deploying a workload in multiple clusters, you can specify differentiated settings for these clusters. Click |image2| in the upper right corner of the target cluster to specify differentiated settings. The settings take effect only for this cluster.

      For parameter description, see :ref:`Container Settings <ucs_01_0255__li102351132171611>`.

#. Click **Create Workload**.

.. |image1| image:: /_static/images/en-us_image_0000001554286565.png
.. |image2| image:: /_static/images/en-us_image_0000001503446844.png
