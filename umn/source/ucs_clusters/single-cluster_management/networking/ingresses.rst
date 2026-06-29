:original_name: ucs_01_0111.html

.. _ucs_01_0111:

Ingresses
=========

An ingress uses load balancers as the entry for external traffic. Compared with Layer-4 load balancing, it supports Uniform Resource Identifier (URI) configurations and distributes access traffic to the corresponding services based on the URIs. You can customize forwarding rules based on domain names and URLs to implement fine-grained distribution of access traffic. The access address is in the format of *<IP address of public network load balancer>*:*<access port><defined URI>*, for example, **10.117.117.117:80/helloworld**.

Procedure
---------

#. Access the cluster console.
#. In the navigation pane, choose **Services & Ingresses**. On the displayed page, click the **Ingresses** tab and select the namespace that the ingress belongs to. For details about how to create a namespace, see :ref:`Creating a Namespace <ucs_01_0117__en-us_topic_0167389656_section31143617514>`.
#. Click **Create Ingress** in the upper right corner and configure the parameters.

   -  **Name**: name of the ingress to be created, which can be self-defined.
   -  **Namespace**: namespace that the ingress belongs to.
   -  **TLS**:

      -  **Server Certificate**: Select the IngressTLS server certificate. If no desired certificates are available, click **Create IngressTLS Secret**. For details, see `Creating a Secret <https://docs.otc.t-systems.com/cloud-container-engine/umn/configmaps_and_secrets/creating_a_secret.html#cce-10-0153>`__. For details about how to obtain a TLS certificate, see
      -  **SNI**: Enter the domain name and select the corresponding certificate. Server Name Indication (SNI) is an extended protocol of TLS. It allows multiple TLS-based access domain names to be provided for external systems using the same IP address and port number. Different domain names can use different security certificates.

   -  **Forwarding Policy**: When the access address of a request matches the forwarding policy (a forwarding policy consists of a domain name and URL, for example, 10.117.117.117:80/helloworld), the request is forwarded to the corresponding target Service for processing. You can add multiple forwarding policies.

      -  **Domain Name**: (Optional) actual domain name. Ensure that the domain name has been registered and licensed. Once a forwarding policy is configured with a domain name specified, you must use the domain name for access.
      -  **URL**: access path to be registered, for example, **/healthz**. The access path must be the same as the URL exposed by the backend application. Otherwise, a 404 error will be returned.
      -  **Destination Service**: Select a Service name. You need to create the NodePort Service first. For details, see :ref:`NodePort <ucs_01_0110__en-us_topic_0000001258156072_section16547755192910>`.
      -  **Destination Service Port**: After you select the destination Service, the corresponding container port is automatically filled in.

   -  **Ingress Class**: You can select an existing ingress class or manually enter an ingress class name.
   -  **Annotation**: The key-value pair format is supported. Configure annotations based on your service and vendor requirements and then click **Add**.

#. Click **OK**.
