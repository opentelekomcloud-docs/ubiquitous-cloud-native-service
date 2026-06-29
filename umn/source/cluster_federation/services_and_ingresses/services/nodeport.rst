:original_name: ucs_01_0272.html

.. _ucs_01_0272:

NodePort
========

A NodePort Service is exposed on a node at a static port, allowing access from outside the cluster to the workloads on the node. A ClusterIP Service, to which the NodePort Service routes, is automatically created, and it transfers access requests to the backing containers. If a node in the cluster is bound to an EIP, you can also request <*EIP*>:<*NodePort*> to access the workloads from public networks.

Creating a Service
------------------

You can create a Service in either of the following ways:

-  Create one when creating a workload. For details, see :ref:`During Workload Creation <ucs_01_0272__section162656112108>`.
-  Create one after creating a workload. For details, see :ref:`After Workload Creation <ucs_01_0272__section1926571114103>`.

.. _ucs_01_0272__section162656112108:

During Workload Creation
------------------------

The procedure of creating a Service is the same for different types of workloads, such as Deployments, StatefulSets, and DaemonSets.

#. In the **Service Settings** step of :ref:`Creating a Deployment <ucs_01_0255__section146991320135316>`, :ref:`Creating a StatefulSet <ucs_01_0256__section146991320135316>`, or :ref:`Creating a DaemonSet <ucs_01_0257__section146991320135316>`, click |image1| to configure the Service.

   -  **Name**: Enter a Service name consisting of 1 to 50 characters.
   -  **Type**: Select **NodePort**.
   -  **Affinity**

      -  **Cluster-level**: The IP addresses and access ports of all nodes in a cluster can be used to access the workloads associated with the Service. However, performance loss is introduced due to hops, and source IP addresses cannot be obtained.
      -  **Node-level**: Only the IP address and access port of the node where the workload is located can be used to access the workload associated with the Service. Service access will not cause performance loss due to route redirection, and the source IP address of the client can be obtained.

   -  **Port**

      -  **Protocol**: Select **TCP** or **UDP**.
      -  **Service Port**: Port mapped to the container port at the cluster-internal IP address. The application can be accessed at <*cluster-internal IP address*>:<*access port*>. The port number range is 1-65535.
      -  **Container Port**: Port on which the workload listens, defined in the container image. For example, the Nginx application listens on port 80 (container port).
      -  **Node Port**: Specify a port to which the container port will be mapped when the node private IP address is used for accessing the application. The port number range is 30000-32767. You are advised to select **Auto**.

         -  **Auto**: The system automatically assigns a port number.
         -  **Custom**: Specify a fixed node port. The port number range is 30000-32767. Ensure that the port is unique in a cluster.

#. Click **OK**.
#. Click **Next: Set Scheduling and Differentiation** to configure the scheduling and differentiated settings for the selected clusters. After completing the settings, click **Create Workload**.
#. Obtain the access address.

   a. In the navigation pane, choose **Services and Ingresses**.
   b. On the **Services** tab, click the name of the added Service to go to its details page. Then, obtain the access address of the cluster. If a node in the cluster is bound to an EIP, you can access the backend workload through the EIP and node port of the node where the workload is deployed.

.. _ucs_01_0272__section1926571114103:

After Workload Creation
-----------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its details page.

#. In the navigation pane, choose **Services and Ingresses**.

#. On the **Services** tab, select the namespace that the Service will belong to and click **Create Service** in the upper right corner. For details about how to create a namespace, see :ref:`Creating a Namespace <ucs_01_0281__section20381629121511>`.

#. .. _ucs_01_0272__li83801855111117:

   On the **Services** tab, click **Create Service**. Then, configure the parameters.

   -  **Name**: Can be the same as the workload name.
   -  **Type**: Select **NodePort**.
   -  **Affinity**

      -  **Cluster-level**: The IP addresses and access ports of all nodes in a cluster can be used to access the workloads associated with the Service. However, performance loss is introduced due to hops, and source IP addresses cannot be obtained.
      -  **Node-level**: Only the IP address and access port of the node where the workload is located can be used to access the workload associated with the Service. Service access will not cause performance loss due to route redirection, and the source IP address of the client can be obtained.

   -  **Port**

      -  **Protocol**: Select **TCP** or **UDP**.
      -  **Service Port**: Port mapped to the container port at the cluster-internal IP address. The application can be accessed at <*cluster-internal IP address*>:<*access port*>. The port number range is 1-65535.
      -  **Container Port**: Port on which the workload listens, defined in the container image. For example, the Nginx application listens on port 80 (container port).
      -  **Node Port**: Specify a port to which the container port will be mapped when the node private IP address is used for accessing the application. The port number range is 30000-32767. You are advised to select **Auto**.

         -  **Auto**: The system automatically assigns a port number.
         -  **Custom**: Specify a fixed node port. The port number ranges from **30000** to **32767**. Ensure that the port is unique in a cluster.

   -  **Namespace**: namespace that the Service belongs to.
   -  **Selector**: Services are associated with workloads (labels) through selectors. Click **Reference Workload Label** to reference the labels of an existing workload.

      -  **Type**: Select the desired workload type.
      -  **Workload**: Select an existing workload. If your workload is not displayed in the list, click |image2| to refresh it.
      -  **Label**: After a workload is selected, its labels are displayed and cannot be modified.

#. Click **OK**. After the Service is created, you can view it in the list on the **Services** tab page.

#. Obtain the access address.

   a. In the navigation pane, choose **Services and Ingresses**.
   b. On the **Services** tab, click the name of the added Service to go to its details page. Then, obtain the access address of the cluster. If a node in the cluster is bound to an EIP, you can access the backend workload through the EIP and node port of the node where the workload is deployed.

Related Operations
------------------

You can also perform operations described in :ref:`Table 1 <ucs_01_0272__table1619535674020>`.

.. _ucs_01_0272__table1619535674020:

.. table:: **Table 1** Related operations

   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                           | Description                                                                                                                                                   |
   +=====================================+===============================================================================================================================================================+
   | Creating a Service from a YAML file | Click **Create from YAML** in the upper right corner to create a Service from an existing YAML file.                                                          |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Viewing details                     | #. Select the namespace to which the Service belongs.                                                                                                         |
   |                                     | #. (Optional) Search for a Service by its name.                                                                                                               |
   |                                     | #. Click the Service name to view its details, including the basic information and cluster deployment information.                                            |
   |                                     | #. On the **Service Details** page, click **View YAML** in the **Cluster** area to view or download YAML files of Service instances deployed in each cluster. |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Editing a YAML file                 | Click **Edit YAML** in the row where the target Service resides to view and edit the YAML file of the Service.                                                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Updating a Service                  | #. Choose **More** > **Update** in the row where the target Service resides.                                                                                  |
   |                                     | #. Modify the information by referring to :ref:`5 <ucs_01_0272__li83801855111117>`.                                                                           |
   |                                     | #. Click **OK** to submit the modified information.                                                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting a Service                  | Choose **More** > **Delete** in the row where the target Service resides, and click **Yes**.                                                                  |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting Services in batches        | #. Select the Services to be deleted.                                                                                                                         |
   |                                     | #. Click **Delete** in the upper left corner.                                                                                                                 |
   |                                     | #. Click **Yes**.                                                                                                                                             |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001554793633.png
.. |image2| image:: /_static/images/en-us_image_0000001554906629.png
