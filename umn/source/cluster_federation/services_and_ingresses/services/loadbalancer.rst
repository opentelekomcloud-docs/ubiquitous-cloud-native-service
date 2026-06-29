:original_name: ucs_01_0273.html

.. _ucs_01_0273:

LoadBalancer
============

A workload can be accessed from a public network through a load balancer. This access type is applicable to Services that need to be exposed to a public network in the system. The access address is in the format of <IP address of public network load balancer>:<access port>, for example, **10.117.117.117:80**.

Prerequisites
-------------

A workload is available. If no workload is available, create one by following the procedure described in :ref:`Workloads <ucs_01_0254>`.

Creating a Service
------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its console.

#. In the navigation pane, choose **Services and Ingresses**.

#. On the **Services** tab, select the namespace that the Service will belong to and click **Create Service** in the upper right corner. For details about how to create a namespace, see :ref:`Creating a Namespace <ucs_01_0281__section20381629121511>`.

#. .. _ucs_01_0273__li3476651017144:

   On the **Services** tab, click **Create Service**. Then, configure the parameters.

   -  **Name**: Enter a Service name consisting of 1 to 50 characters.
   -  **Type**: Select **LoadBalancer**.
   -  **Affinity**

      -  **Cluster**: The IP addresses and access ports of all nodes in a cluster can be used to access the workload associated with the Service. However, performance loss is introduced due to hops, and source IP addresses cannot be obtained.
      -  **Node**: Only the IP address and access port of the node where the workload is located can be used to access the workload associated with the Service. Service access will not cause performance loss due to route redirection, and the source IP address of the client can be obtained.

   -  **Port**

      -  **Protocol**: Select **TCP** or **UDP**.
      -  **Service Port**: Specify a port to map a container port to the load balancer. The port range is 1-65535. The port will be used when the application is accessed through the load balancer.
      -  **Container Port**: port on which the workload listens, defined in the container image. For example, the Nginx application listens on port 80 (container port).

   -  **Cluster**: Add a cluster where load balancers are to be deployed and complete differentiated load balancer settings.

      -  CCE cluster:

         -  **Load Balancer**: Only load balancers in the VPC where the cluster resides are supported.

         -  **Algorithm**

            **Weighted round robin**: Distributes requests to backend servers based on weights.

            **Weighted least connections**: Distributes requests to backend servers with the smallest ratio (current connections divided by weight).

            **Source IP hash**: Allocates requests from the client IP address to a fixed server, allowing the entire session to be processed by the same server.

         -  **Sticky Session**: This function is disabled by default. You can select **Source IP**. Listeners ensure session stickiness based on IP addresses. Requests from the same IP address will be routed to the same backend server.

         -  **Health Check**: This function is disabled by default. You can select either HTTP or TCP to enable health checks for your load balancer. For details about the parameters, see :ref:`Table 1 <ucs_01_0273__table14802612204814>`.

            .. _ucs_01_0273__table14802612204814:

            .. table:: **Table 1** Health check parameters

               +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
               | Parameter             | Description                                                                                                                                                                                   | Example               |
               +=======================+===============================================================================================================================================================================================+=======================+
               | Check Path            | This parameter is available if you have selected **HTTP** for **Health Check**. Specify the URL for health checks. The check path must start with a slash (/) and contain 1 to 80 characters. | /                     |
               +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
               | Port                  | Health check port. The port number ranges from 1 to 65535.                                                                                                                                    | 80                    |
               |                       |                                                                                                                                                                                               |                       |
               |                       | By default, the Service ports (node port and container port of the NodePort Service) are used.                                                                                                |                       |
               +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
               | Check Interval (s)    | Maximum time between health checks, in seconds.                                                                                                                                               | 5                     |
               |                       |                                                                                                                                                                                               |                       |
               |                       | The value ranges from 1 to 50.                                                                                                                                                                |                       |
               +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
               | Timeout (s)           | Maximum time required for waiting for a response from the health check, in seconds.                                                                                                           | 10                    |
               |                       |                                                                                                                                                                                               |                       |
               |                       | The value ranges from 1 to 50.                                                                                                                                                                |                       |
               +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
               | Max. Retries          | Maximum number of health check retries. The value ranges from 1 to 10.                                                                                                                        | 5                     |
               +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

      -  Other clouds

         -  **Ingress Class**: You can select an existing ingress class or manually enter an ingress class name. For details, see `Ingress <https://kubernetes.io/docs/concepts/services-networking/ingress/>`__.
         -  **Annotation**: Enter an annotation in a key-value pair based on your service and vendor requirements.

      -  To create an internal load balancer, add the annotation based on the cloud service provider of your cluster. For details, see `Internal load balancer <https://kubernetes.io/docs/concepts/services-networking/service/>`__.

   -  **Namespace**: namespace that the Service belongs to.
   -  **Selector**: Services are associated with workloads (labels) through selectors. Click **Reference Workload Label** to reference the labels of an existing workload.

      -  **Type**: Select the desired workload type.
      -  **Workload**: Select an existing workload. If your workload is not displayed in the list, click |image1| to refresh it.
      -  **Label**: After a workload is selected, its labels are displayed and cannot be modified.

#. Click **OK**.

#. Obtain the access address.

   a. In the navigation pane, choose **Services and Ingresses**.
   b. On the **Services** tab, click the name of the added Service to go to its details page. Then, obtain the access address of the cluster. You can access a backend pod using the EIP and port number of the load balancer.

Related Operations
------------------

You can also perform operations described in :ref:`Table 2 <ucs_01_0273__table1619535674020>`.

.. _ucs_01_0273__table1619535674020:

.. table:: **Table 2** Related operations

   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                           | Description                                                                                                                                                   |
   +=====================================+===============================================================================================================================================================+
   | Creating a Service from a YAML file | Click **Create from YAML** in the upper right corner to create a Service from an existing YAML file.                                                          |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Viewing details                     | #. Select the namespace that the Service belongs to.                                                                                                          |
   |                                     | #. (Optional) Search for a Service by its name.                                                                                                               |
   |                                     | #. Click the Service name to view its details, including the basic information and cluster deployment information.                                            |
   |                                     | #. On the **Service Details** page, click **View YAML** in the **Cluster** area to view or download YAML files of Service instances deployed in each cluster. |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Editing a YAML file                 | Click **Edit YAML** in the row where the target Service resides to view and edit the YAML file of the Service.                                                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Updating a Service                  | #. Choose **More** > **Update** in the row where the target Service resides.                                                                                  |
   |                                     | #. Modify the information by referring to :ref:`5 <ucs_01_0273__li3476651017144>`.                                                                            |
   |                                     | #. Click **OK** to submit the modified information.                                                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting a Service                  | Choose **More** > **Delete** in the row where the target Service resides, and click **Yes**.                                                                  |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting Services in batches        | #. Select the Services to be deleted.                                                                                                                         |
   |                                     | #. Click **Delete** in the upper left corner.                                                                                                                 |
   |                                     | #. Click **Yes**.                                                                                                                                             |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001554906629.png
