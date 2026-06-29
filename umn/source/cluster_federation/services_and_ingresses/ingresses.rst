:original_name: ucs_01_0274.html

.. _ucs_01_0274:

Ingresses
=========

An ingress uses load balancers as the entry for external traffic. Compared with Layer-4 load balancing, it supports Uniform Resource Identifier (URI) configurations and distributes access traffic to services based on URIs. You can create custom forwarding rules based on domain names and URLs for the fine-grained distribution of access traffic. The access address is in the format of <IP address of public network load balancer>:<access port><defined URI>, for example, **10.117.117.117:80/helloworld**.

Prerequisites
-------------

A workload is available. If no workload is available, create one by following the procedure described in :ref:`Workloads <ucs_01_0254>`.

Creating an Ingress
-------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its console.

#. In the navigation pane, choose **Services and Ingresses**. Then, click the **Ingresses** tab.

#. Select the namespace that the ingress will belong to and click **Create Ingress** in the upper right corner. For details about how to create a namespace, see :ref:`Creating a Namespace <ucs_01_0281__section20381629121511>`.

#. .. _ucs_01_0274__li18105124262:

   Configure ingress parameters.

   -  **Ingress Name**: name of the ingress to be created.
   -  **Namespace**: namespace that the ingress belongs to.
   -  **Interconnect with Nginx**: There are ELB Ingress Controller and Nginx Ingress Controller. Both of them are supported in UCS. ELB Ingress Controller forwards traffic through ELB. Nginx Ingress Controller uses the templates and images maintained by the Kubernetes community to forward traffic through the Nginx component.

      -  ELB Ingress: Do not enable **Interconnect with Nginx**.
      -  Nginx Ingress: Click |image1| to enable **Interconnect with Nginx**.

   -  **Listener**: Select an external protocol. **HTTP** and **HTTPS** are supported. If you select **HTTPS**, select an IngressTLS server certificate. If no desired certificate is available, click **Create IngressTLS Secret** to create an IngressTLS secret. For details, see :ref:`Secrets <ucs_01_0268>`.

      -  **SNI**: Server Name Indication (SNI) is an extended protocol of TLS. It allows multiple TLS-based access domain names to be provided for external systems using the same IP address and port number. Different domain names can use different security certificates.

   -  **Forwarding Policy**: When the access address of a request matches the forwarding policy (a forwarding policy consists of a domain name and URL, for example, 10.117.117.117:80/helloworld), the request is forwarded to the corresponding target Service for processing. You can add multiple forwarding policies.

      -  **Domain Name**: (optional) actual domain name. Ensure that the domain name has been registered and licensed. Once a forwarding policy is configured with a domain name specified, you must use the domain name for access.
      -  **URL**: access path to be registered, for example, **/healthz**. The access path must be the same as the URL exposed by the backend application. Otherwise, a 404 error will be returned.
      -  **Backend Service**: Select a Service name. You need to create the NodePort Service first. For details, see :ref:`NodePort <ucs_01_0272>`.
      -  **Backend Service Port**: After you select the backend Service, the corresponding container port is automatically filled in.

   -  **Cluster**: Select the cluster where the ingress is to be deployed.

      -  CCE cluster:

         -  **Exposed Port**: port opened on the load balancer, which can be specified randomly.
         -  **Load Balancer**: Only load balancers in the VPC where the cluster resides are supported. If no load balancer is available, click **Create Load Balancer**. After the load balancer is created, click the refresh button.

            .. caution::

               When creating an Nginx Ingress, you do not need to manually select a load balancer because a load balancer has been associated during add-on installation.

      -  Other clouds

         -  **Ingress Class**: You can select an existing ingress class or manually enter an ingress class name. For details, see `Ingress <https://kubernetes.io/docs/concepts/services-networking/ingress/>`__.
         -  **Annotation**: Enter an annotation in a key-value pair based on your service and vendor requirements.

      -  To create an internal load balancer, add the annotation based on the cloud service provider of your cluster. For details, see `Internal load balancer <https://kubernetes.io/docs/concepts/services-networking/service/>`__.

#. Click **OK**. After the ingress is created, you can view it in the list on the **Ingresses** tab.

#. Obtain the access address.

   a. In the navigation pane, choose **Services and Ingresses**. Then, click the **Ingresses** tab.
   b. Click the name of the created ingress. On the **Ingress Details** page displayed, view the load balancer and listener port configurations. You can access a backend pod using the EIP of the load balancer, listener port, and URL, for example, **10.117.117.117:8088/helloworld**.

Related Operations
------------------

You can also perform operations described in :ref:`Table 1 <ucs_01_0274__table1619535674020>`.

.. _ucs_01_0274__table1619535674020:

.. table:: **Table 1** Related operations

   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                            | Description                                                                                                                                                   |
   +======================================+===============================================================================================================================================================+
   | Creating an ingress from a YAML file | Click **Create from YAML** in the upper right corner to create an ingress from an existing YAML file.                                                         |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Viewing details                      | #. Select the namespace that the ingress belongs to.                                                                                                          |
   |                                      | #. (Optional) Search for an ingress by its name.                                                                                                              |
   |                                      | #. Click the ingress name to view its details, including the basic information and cluster deployment information.                                            |
   |                                      | #. On the **Ingress Details** page, click **View YAML** in the **Cluster** area to view or download YAML files of ingress instances deployed in each cluster. |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Editing a YAML file                  | Click **Edit YAML** in the row where the target ingress resides to view and edit the YAML file of the ingress.                                                |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Updating an ingress                  | #. Choose **More** > **Update** in the row where the target ingress resides.                                                                                  |
   |                                      | #. Modify the information by referring to :ref:`5 <ucs_01_0274__li18105124262>`.                                                                              |
   |                                      | #. Click **OK** to submit the modified information.                                                                                                           |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting an ingress                  | Choose **More** > **Delete** in the row where the target ingress resides. Then, click **Yes**.                                                                |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting ingresses in batches        | #. Select the ingresses to be deleted.                                                                                                                        |
   |                                      | #. Click **Delete** in the upper left corner.                                                                                                                 |
   |                                      | #. Click **Yes**.                                                                                                                                             |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001834789605.png
