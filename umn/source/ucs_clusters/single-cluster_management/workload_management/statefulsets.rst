:original_name: ucs_01_0136.html

.. _ucs_01_0136:

StatefulSets
============

.. _ucs_01_0136__section311016411651:

Creating a StatefulSet
----------------------

#. (Optional) If you create a workload using the image pulled from SWR, push your image to SWR first. For details about how to push an image, see `Image Management <https://docs.otc.t-systems.com/software-repository-container/umn/image_management/index.html>`__. If you create a workload using an open source image, you do not need to push the image to SWR.

#. On the cluster details page, choose **Workloads** > **StatefulSets** and click **Create from Image**.

#. Set basic workload parameters as described in :ref:`Table 1 <ucs_01_0136__en-us_topic_0150272097_en-us_topic_0150272097_table12741447488>`. The parameters marked with an asterisk (*) are mandatory.

   .. _ucs_01_0136__en-us_topic_0150272097_en-us_topic_0150272097_table12741447488:

   .. table:: **Table 1** Basic workload parameters

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                          |
      +===================================+======================================================================================================================================================================================================================================================+
      | \*Workload Name                   | Name of a workload, which must be unique.                                                                                                                                                                                                            |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Cluster Name                      | Cluster to which the workload belongs. You do not need to set this parameter.                                                                                                                                                                        |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | \*Namespace                       | In a single cluster, data in different namespaces is isolated from each other. This enables applications to share the Services of the same cluster without interfering each other. If no namespace is set, the **default** namespace is used.        |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | \*Pods                            | Number of pods in the workload. A workload can have one or more pods. You can set the number of pods. The default value is **2** and can be set to **1**.                                                                                            |
      |                                   |                                                                                                                                                                                                                                                      |
      |                                   | Each workload pod consists of the same containers. Configuring multiple pods for a workload ensures that the workload can still run properly even if a pod is faulty. If only one pod is used, a node or pod exception may cause service exceptions. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Description of the workload.                                                                                                                                                                                                                         |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Time Zone Synchronization         | If this parameter is enabled, the containers and the node use the same time zone, and disks of the hostPath type will be automatically added and listed in the **Data Storage** > **Local Volumes** area. Do not modify or delete the disks.         |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Configure the container settings for the workload.

   Multiple containers can be configured in a pod. You can click **Add Container** on the right to configure multiple containers for the pod.

   -  **Container Information**: Click **Add Container** on the right to configure multiple containers for the pod.

      -  **Basic Info**: See :ref:`Table 2 <ucs_01_0136__ucs_01_0106_en-us_topic_0150272097_en-us_topic_0000001236922598_table6496632151617>`.

         .. _ucs_01_0136__ucs_01_0106_en-us_topic_0150272097_en-us_topic_0000001236922598_table6496632151617:

         .. table:: **Table 2** Basic information parameters

            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Parameter                         | Description                                                                                                                                                                                                                                                                              |
            +===================================+==========================================================================================================================================================================================================================================================================================+
            | Container Name                    | Name the container.                                                                                                                                                                                                                                                                      |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Image Name                        | Click **Select Image** and select the image used by the container.                                                                                                                                                                                                                       |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | -  **My Images**: images in the image repository of the current region. If no image is available, click **Upload Image** to upload an image.                                                                                                                                             |
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
            |                                   | For details about **Request** and **Limit** of CPU or memory, see :ref:`Setting Container Specifications <ucs_01_0147>`.                                                                                                                                                                 |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Init Container                    | Select whether to use the container as an init container.                                                                                                                                                                                                                                |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | An init container is a special container that runs before app containers in a pod. For details, see `Init Containers <https://kubernetes.io/docs/concepts/workloads/pods/init-containers/>`__.                                                                                           |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Privileged Container              | Programs in a privileged container have certain privileges.                                                                                                                                                                                                                              |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | If **Privileged Container** is enabled, the container is assigned privileges. For example, privileged containers can manipulate network devices on the host machine and modify kernel parameters.                                                                                        |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

      -  **Lifecycle**: The lifecycle callback functions can be called in specific phases of the container. For example, if you want the container to perform a certain operation before stopping, set the corresponding function. Currently, lifecycle callback functions, such as startup, post-start, and pre-stop are provided. For details, see :ref:`Setting Container Lifecycle Parameters <ucs_01_0148>`.

      -  **Health Check**: Set health check parameters to periodically check the health status of the container during container running. For details, see :ref:`Setting Health Check for a Container <ucs_01_0149>`.

      -  **Environment Variable**: Environment variables affect the way a running container will behave. Configuration items set by environment variables will not change if the pod lifecycle ends. For details, see :ref:`Setting Environment Variables <ucs_01_0150>`.

      -  **Data Storage**: Store container data using **Local Volumes** and **PersistentVolumeClaims (PVCs)**. You are advised to use PVCs to store workload pod data on a cloud volume. If you store pod data on a local volume and a fault occurs on the node, the data cannot be restored. For details about container storage, see :ref:`Container Storage <ucs_01_0112>`.

      -  **Security Context**: Set container permissions to protect the system and other containers from being affected. Enter a user ID and the container will run with the user permissions you specify.

   -  **Image Access Credential**: Select the credential for accessing the image repository. This credential is used only for accessing a private image repository. If the selected image is a public image, you do not need to select a secret. For details on how to create a secret, see :ref:`Creating a Secret <ucs_01_0115>`.

#. Configure the headless Service parameters for the workload.

   StatefulSet pods discover each other through headless Services. No cluster IP is allocated for a headless Service, and the DNS records of all pods are returned during query. In this way, the IP addresses of all pods can be queried.

   -  **Service Name**: Name of the Service corresponding to the workload for mutual access between workloads in the same cluster. This Service is used for internal discovery of pods, and does not require an independent IP address or load balancing.
   -  **Port**

      -  **Port**: Name of the container port. You are advised to enter a name that indicates the function of the port.
      -  **Service Port**: Port of the Service.
      -  **Container Port**: Listening port of the container.

#. (Optional) Click |image1| in the **Service Settings** area to configure a Service for the workload.

   If your workload will be reachable to other workloads or public networks, add a Service to define the workload access type. The workload access type determines the network attributes of the workload. Workloads with different access types can provide different network capabilities. For details, see :ref:`Services <ucs_01_0110>`.

   You can also create a Service after creating a workload. For details, see :ref:`ClusterIP <ucs_01_0110__en-us_topic_0000001258156072_section3959435152917>` and :ref:`NodePort <ucs_01_0110__en-us_topic_0000001258156072_section16547755192910>`.

   -  **Service Name**: name of the Service to be added. It is customizable and must be unique.
   -  **Service Type**

      -  **ClusterIP**: The Service is only reachable from within the cluster.
      -  **NodePort**: The Service can be accessed from any node in the cluster.
      -  **LoadBalancer**: The workload is accessed from the public network using a load balancer.

   -  **Service Affinity** (for NodePort and LoadBalancer only)

      -  **Cluster-level**: The IP addresses and access ports of all nodes in a cluster can be used to access the workloads associated with the Service. However, performance loss is introduced due to hops, and source IP addresses cannot be obtained.
      -  **Node-level**: Only the IP address and access port of the node where the workload is located can be used to access the workload associated with the Service. Service access will not cause performance loss due to route redirection, and the source IP address of the client can be obtained.

   -  **Port**

      -  **Protocol**: Select **TCP** or **UDP**.
      -  **Service Port**: Port mapped to the container port at the cluster-internal IP address. The application can be accessed at *<cluster-internal IP address>*:*<access port>*. The port number range is 1-65535.
      -  **Container Port**: Port on which the workload listens, defined in the container image. For example, the Nginx application listens on port 80 (container port).
      -  **Node Port** (for NodePort only): Port to which the container port will be mapped when the node private IP address is used for accessing the application. The port number range is 30000-32767. You are advised to select **Auto**.

         -  **Auto**: The system automatically assigns a port number.
         -  **Custom**: Specify a fixed node port. The port number range is 30000-32767. Ensure that the port is unique in a cluster.

   -  **Annotation**: The key-value pair format is supported. Configure annotations based on your service and vendor requirements and then click **Add**.

#. (Optional) Click **Expand** to set advanced settings for the workload.

   -  **Upgrade**: Upgrade mode of the StatefulSet, including **Replace upgrade** and **Rolling upgrade**. For details, see :ref:`Configuring a Workload Upgrade Policy <ucs_01_0151>`.

      -  **Rolling upgrade**: An old pod is gradually replaced with a new pod. During the upgrade, service traffic is evenly distributed to the old and new pods to ensure service continuity.
      -  **Replace upgrade**: You need to delete old pods manually before new pods are created. Services will be interrupted during a replace upgrade.

   -  **Pod Management Policies**

      -  **OrderedReady**: The StatefulSet will launch, terminate, or scale pods sequentially. It will wait for the state of the pods to change to Running and Ready or completely terminated before it launches or terminates another pod.
      -  **Parallel**: The StatefulSet will launch or terminate all pods in parallel. It will not wait for the state of the pods to change to Running and Ready or completely terminated before it launches or terminates another pod.

   -  **Scheduling**: You can set affinity and anti-affinity to implement planned scheduling for pods. For details, see :ref:`Scheduling Policy (Affinity/Anti-affinity) <ucs_01_0152>`.
   -  **Labels and Annotations**: You can click **Confirm** to add a label or annotation for the pod. The key of the new label or annotation cannot be the same as that of an existing one.
   -  **Toleration**: When the node where the workload pods are located is unavailable for the specified amount of time, the pods will be rescheduled to other available nodes. By default, the toleration time window is 300s.

      -  Using both taints and tolerations allows (not forcibly) the pod to be scheduled to a node with the matching taints, and controls the pod eviction policies after the node where the pod is located is tainted. For details, see `Example Tutorial <https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/>`__.
      -  Click |image2| to add a policy. For details about related parameters, see :ref:`Tolerance Policies <ucs_01_0399>`.

#. After the configuration is complete, click **Create Workload**. You can view the StatefulSet status in the StatefulSet List.

   If the StatefulSet is in the **Running** status, the StatefulSet is successfully created.

Related Operations
------------------

On the cluster console, you can also perform the operations described in :ref:`Table 3 <ucs_01_0136__ucs_01_0106_en-us_topic_0150272097_table1619535674020>`.

.. _ucs_01_0136__ucs_01_0106_en-us_topic_0150272097_table1619535674020:

.. table:: **Table 3** Related operations

   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                            | Description                                                                                                                                                                     |
   +======================================+=================================================================================================================================================================================+
   | Creating a workload from a YAML file | Click **Create from YAML** in the upper right corner to create a workload from an existing YAML file.                                                                           |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Viewing pod details                  | Click the name of a workload. You can view pod details on the **Pods** tab.                                                                                                     |
   |                                      |                                                                                                                                                                                 |
   |                                      | -  **View Events**: You can set search criteria, such as the time segment during which an event is generated or the event name, to view related events.                         |
   |                                      | -  **View Container**: You can view the container name, status, image, and restarts of the pod.                                                                                 |
   |                                      | -  **View YAML**: You can view the YAML file of the pod.                                                                                                                        |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Editing a YAML file                  | Click **Edit YAML** in the row where the target workload resides to edit its YAML file.                                                                                         |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Upgrade                              | #. Click **Upgrade** in the row where the target workload resides.                                                                                                              |
   |                                      | #. Modify information about the workload.                                                                                                                                       |
   |                                      | #. Click **Upgrade Workload** to submit the modified information.                                                                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Rollback                             | Choose **More** > **Roll Back** in the row where the target workload resides, and select the target version for rollback.                                                       |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Redeploy                             | Choose **More** > **Redeploy** in the row where the target workload resides, and click **Yes** in the dialog box displayed. Redeployment will restart all pods in the workload. |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Disabling upgrade                    | Choose **More** > **Disable Upgrade** in the row where the workload resides, and click **Yes** in the dialog box displayed.                                                     |
   |                                      |                                                                                                                                                                                 |
   |                                      | -  After a workload is marked "Upgrade disabled", its upgrade will not be applied to the pods.                                                                                  |
   |                                      | -  Any ongoing rolling upgrade will be suspended.                                                                                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Delete                               | Choose **More** > **Delete** in the row where the workload resides, and click **Yes** in the dialog box displayed.                                                              |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting workloads in batches        | #. Select the target workloads to be deleted.                                                                                                                                   |
   |                                      | #. Click **Delete** in the upper left corner.                                                                                                                                   |
   |                                      | #. Click **Yes**.                                                                                                                                                               |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001317957925.png
.. |image2| image:: /_static/images/en-us_image_0000001804415254.png
