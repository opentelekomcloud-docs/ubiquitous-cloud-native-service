:original_name: ucs_01_0371.html

.. _ucs_01_0371:

Overview
========

Why MCI?
--------

Traditionally, each Kubernetes cluster has its load balancer and ingress, which brings complexities around load balancing and traffic routing across clusters and regions. UCS Multi Cluster Ingress (MCI) abstracts away such complexities and improves the availability and reliability of applications.

MCI accepts traffic coming from the Internet and routes it to pods running in clusters based on forwarding rules. With MCI, you can create custom forwarding rules to provide fine-grained control over how your load balancer behaves. The following diagram shows how traffic flows from MCI to two clusters. Traffic from **foo.example.com** flows to the pods that have the **app:foo** label across both clusters. Traffic from **goo.example.com** flows to the pods that have the **app:goo** label across both clusters.


.. figure:: /_static/images/en-us_image_0000001756494569.png
   :alt: **Figure 1** MCI diagram

   **Figure 1** MCI diagram

MCI has the following advantages:

-  Multi-cluster load balancing: MCI provides an ingress for traffic routing across multiple clusters, without the need to know cluster locations.
-  Traffic routing: MCI allows you to customize forwarding rules based on different conditions (such as URLs, HTTP headers, and source IP addresses) to flexibly route traffic across clusters.
-  High availability: MCI supports health checks and automatic traffic switchover for multi-cluster and regional high availability.
-  Scalability: MCI discovers and manages application resources in multiple clusters for automatic application expansion and deployment.
-  Security: MCI supports TLS security policies and certificate management for application security.

How MCI Works
-------------

MCI Controller acts as an executor for request forwarding and enables MCI functions. MCI Controller is deployed on the federation control plane to monitor resource object changes in real time, parse rules defined for MCI objects, and forward requests to backend services.

.. _ucs_01_0371__fig5369712001:

.. figure:: /_static/images/en-us_image_0000001772226485.png
   :alt: **Figure 2** Working principle of MCI Controller

   **Figure 2** Working principle of MCI Controller

MCI Controller allows you to configure different domain names, ports, and forwarding rules for the same load balancer. :ref:`Figure 2 <ucs_01_0371__fig5369712001>` shows the working principle.

#. The deployment personnel create a workload on the federation control plane and configure a Service object for the workload.
#. The deployment personnel create an MCI object on the federation control plane and configure a traffic access rule that consists of the load balancer, URL, and backend service and port.
#. When detecting that the MCI object changes, MCI Controller reconfigures the listener and backend server route on the ELB side according to the traffic access rule.
#. When a user accesses workloads, the traffic is forwarded to the corresponding backend service over the port based on the configured forwarding policy, and then forwarded to each associated workload through the Service.
