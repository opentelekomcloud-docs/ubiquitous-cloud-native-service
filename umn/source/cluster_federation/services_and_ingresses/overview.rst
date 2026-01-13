:original_name: ucs_01_0270.html

.. _ucs_01_0270:

Overview
========

UCS clusters allow workload access in different scenarios via Services and ingresses.

.. important::

   -  After a Service or ingress is created on the UCS console, a Service or ingress with the same name will be created in the cluster that each associated workload belongs to.
   -  You can modify or delete the Services and ingresses automatically created by UCS on the cluster console. However, if the Service or ingress settings on the UCS console are not modified accordingly, the modified or deleted Services or ingresses will be re-created by UCS. Therefore, you are advised to change the settings on the UCS console, not the cluster console.
   -  When there is an exception in your cluster, Services in the cluster will be migrated to a healthy cluster. When your cluster recovers, you need to manually modify the Service template to deploy the Services again.
   -  When creating a LoadBalancer Service and ingress for a non-CCE cluster, you need to specify the annotations based on the load balancer connected to the cluster. Configure the annotations based on your service requirements and vendor requirements. For details, see `Internal Load Balancer <https://kubernetes.io/docs/concepts/services-networking/service/>`__.

-  :ref:`ClusterIP <ucs_01_0271>`

   A workload can be accessed from other workloads in the same cluster through a cluster-internal domain name. A cluster-internal domain name is in the format of *<User-defined Service name>*.\ *<Namespace of the workload>*\ **.svc.cluster.local**, for example, **nginx.default.svc.cluster.local**.

-  :ref:`NodePort <ucs_01_0272>`

   A workload can be accessed from outside the cluster. A NodePort Service is exposed on each node's IP address at a static port. If a node in the cluster is bound to an EIP, workloads on the node can be accessed from public networks by requesting <*EIP*>:<*NodePort*>.

-  :ref:`LoadBalancer <ucs_01_0273>`

   A workload can be accessed from a public network through a load balancer. LoadBalancer provides higher reliability than EIP-based NodePort because the former needs no EIP. The access address is in the format of *<IP address of public network load balancer>*:*<access port>*, for example, **10.117.117.117:80**.

-  :ref:`Ingress <ucs_01_0274>`

   Enhanced load balancer is used for an ingress. Compared with Layer-4 load balancing, Layer-7 load balancing supports Uniform Resource Identifier (URI) configurations and distributes access traffic to services based on URIs. In addition, different functions are implemented based on URIs. The access address is in the format of <IP address of public network load balancer>:<access port><defined URI>, for example, **10.117.117.117:80/helloworld**.
