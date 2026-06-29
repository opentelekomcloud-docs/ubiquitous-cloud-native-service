:original_name: ucs_01_0110.html

.. _ucs_01_0110:

Services
========

Services provide fixed modes for accessing workloads in a cluster. You can create the following Services on the cluster console:

-  :ref:`ClusterIP <ucs_01_0110__en-us_topic_0000001258156072_section3959435152917>`

   A workload can be accessed from other workloads in the same cluster through a cluster-internal domain name. A cluster-internal domain name is in the format of <*User-defined Service name*>.<*Namespace of the workload*>\ **.svc.cluster.local**, for example, **nginx.default.svc.cluster.local**.

-  :ref:`NodePort <ucs_01_0110__en-us_topic_0000001258156072_section16547755192910>`

   A workload can be accessed from outside the cluster. A NodePort Service is exposed on each node's IP address at a static port. If a node in the cluster is bound to an elastic IP address (EIP), you can use <*EIP*>:<*NodePort*> to access the workload from a public network.

-  :ref:`LoadBalancer <ucs_01_0110__en-us_topic_0000001258156072_section11397004379>`

   A workload can be accessed from a public network through a load balancer. This access type is applicable to Services that need to be exposed to a public network in the system. The access address is in the format of <*IP address of public network load balancer*>:<*access port*>, for example, **10.117.117.117:80**.

.. _ucs_01_0110__en-us_topic_0000001258156072_section3959435152917:

ClusterIP
---------

#. Log in to the UCS console and access the cluster console.
#. In the navigation pane, choose **Services and Ingresses**. Click the **Services** tab and select the namespace that the Service belongs to. For details about how to create a namespace, see :ref:`Creating a Namespace <ucs_01_0117__en-us_topic_0167389656_section31143617514>`.
#. Click **Create Service** in the upper right corner and configure the parameters.

   -  **Service**: Enter a custom Service name, which can be the same as the workload name.
   -  **Service Type**: Select **ClusterIP**.
   -  **Namespace**: Set it to the namespace that the workload belongs to.
   -  **Selector**: Add a label and click **Add**. A Service selects a pod based on the added label. You can also click **Reference Workload Label** to reference the label of an existing workload. In the dialog box that is displayed, select a workload and click **OK**.
   -  **Port**

      -  **Protocol**: Select a protocol used by the Service.
      -  **Service Port**: Port mapped to the container port at the cluster-internal IP address. The workload can be accessed at <*cluster-internal IP address*>:<*access port*>. The port number range is 1-65535.
      -  **Container Port**: Port on which the workload listens. For example, the Nginx application listens on port 80 (container port).

#. Click **OK**.

.. _ucs_01_0110__en-us_topic_0000001258156072_section16547755192910:

NodePort
--------

#. Log in to the UCS console and access the cluster console.
#. In the navigation pane, choose **Services and Ingresses**. Click the **Services** tab and select the namespace that the Service belongs to. For details about how to create a namespace, see :ref:`Creating a Namespace <ucs_01_0117__en-us_topic_0167389656_section31143617514>`.
#. Click **Create Service** in the upper right corner and configure the parameters.

   -  **Service**: Enter a custom Service name, which can be the same as the workload name.
   -  **Service Type**: Select **NodePort**.
   -  **Service Affinity**

      -  **Cluster-level**: The IP addresses and access ports of all nodes in a cluster can be used to access the workload associated with the Service. However, performance loss is introduced due to hops, and source IP addresses cannot be obtained.
      -  **Node-level**: Only the IP address and access port of the node where the workload is located can be used to access the workload associated with the Service. Service access will not cause performance loss due to route redirection, and the source IP address of the client can be obtained.

   -  **Namespace**: Set it to the namespace that the workload belongs to.
   -  **Selector**: Add a label and click **Add**. A Service selects a pod based on the added label. You can also click **Reference Workload Label** to reference the label of an existing workload. In the dialog box that is displayed, select a workload and click **OK**.
   -  **Port**

      -  **Protocol**: Select a protocol used by the Service.
      -  **Service Port**: Port mapped to the container port at the cluster-internal IP address. The application can be accessed at <*cluster-internal IP address*>:<*access port*>. The port number range is 1-65535.
      -  **Container Port**: Port on which the workload listens, defined in the container image. For example, the Nginx application listens on port 80 (container port).
      -  **Node Port**: port to which the container port will be mapped when the node private IP address is used for accessing the application. The port number range is 30000-32767. You are advised to select **Auto**.

         -  **Auto**: The system automatically assigns a port number.
         -  **Custom**: Specify a fixed node port. The port number range is 30000-32767. Ensure that the port is unique in a cluster.

#. Click **OK**.

.. _ucs_01_0110__en-us_topic_0000001258156072_section11397004379:

LoadBalancer
------------

#. Log in to the UCS console and access the cluster console.
#. In the navigation pane, choose **Services and Ingresses**. Click the **Services** tab and select the namespace that the Service belongs to. For details about how to create a namespace, see :ref:`Creating a Namespace <ucs_01_0117__en-us_topic_0167389656_section31143617514>`.
#. Click **Create Service** in the upper right corner and configure the parameters.

   -  **Service**: Enter a custom Service name, which can be the same as the workload name.
   -  **Service Type**: Select **LoadBalancer**.
   -  **Service Affinity**

      -  **Cluster-level**: The IP addresses and access ports of all nodes in a cluster can be used to access the workload associated with the Service. However, performance loss is introduced due to hops, and source IP addresses cannot be obtained.
      -  **Node-level**: Only the IP address and access port of the node where the workload is located can be used to access the workload associated with the Service. Service access will not cause performance loss due to route redirection, and the source IP address of the client can be obtained.

   -  **Namespace**: Set it to the namespace that the workload belongs to.
   -  **Selector**: Add a label and click **Add**. A Service selects a pod based on the added label. You can also click **Reference Workload Label** to reference the label of an existing workload. In the dialog box that is displayed, select a workload and click **OK**.
   -  **Port**

      -  **Protocol**: Select a protocol used by the Service.
      -  **Service Port**: Port mapped to the container port at the cluster-internal IP address. The application can be accessed at <*cluster-internal IP address*>:<*access port*>. The port number range is 1-65535.
      -  **Container Port**: Port on which the workload listens, defined in the container image. For example, the Nginx application listens on port 80 (container port).

   -  **Annotation**: The key-value pair format is supported. Configure annotations based on your service and vendor requirements and then click **Add**.

#. Click **OK**.
