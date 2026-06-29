:original_name: ucs_01_0375.html

.. _ucs_01_0375:

Overview
========

Why MCS?
--------

A `Service <https://kubernetes.io/docs/concepts/services-networking/service/>`__ in Kubernetes is an object that defines a logical set of pods and a policy to access the pods. The Service provides a stable IP address and DNS name for accessing pods. The Service lets you discover and access available pods in a single cluster. However, sometimes you might want to split applications into multiple clusters, to address data sovereignty, state management, and scalability requirements. With MCS, you can create applications that span multiple clusters.

MCS is a cross-cluster Service discovery and invocation mechanism that leverages the existing Service object. Services enabled with this feature are discoverable and accessible across clusters.

Using MCS provides you with the following benefits:

-  Application DR: Running the same Service across clusters in multiple regions provides you with improved fault tolerance. If a Service in a cluster is unavailable, the request can fail over and be served from other clusters.
-  Service sharing: Instead of each cluster requiring its own local Service replica, MCS makes it easier to set up common shared Services (such as monitoring and logging) in a separate cluster that all functional clusters use.
-  Application migration: MCS provides you with a mechanism to help bridge the communication between Services, making it easier to migrate your applications. This is especially helpful as you can deploy the same Service to two different clusters and traffic is allowed to shift from one cluster or application to another.

There are north-south MCS and east-west MCS.

-  North-south MCS allows you to create a multi-cluster Service of the LoadBalancer type to route traffic to ports at Layer 4.
-  East-west MCS allows you to create a multi-cluster Service of the CrossCluster type to enable service discovery across clusters.

How MCS Works
-------------

MCS functions are implemented by the control plane component karmada-controller-manager. karmada-controller-manager monitors Service and MCS changes in real time, parses rules defined by MCS objects, and forwards requests to backend services.

.. _ucs_01_0375__fig5369712001:

.. figure:: /_static/images/en-us_image_0000001801477477.png
   :alt: **Figure 1** Working principle of MCS

   **Figure 1** Working principle of MCS

:ref:`Figure 1 <ucs_01_0375__fig5369712001>` shows the working principle of MCS. The details are as follows:

#. A user creates a workload on the federation control plane and deploys Service **foo** in cluster B for the workload.
#. The user creates an MCS object on the federation control plane and configures an access rule. In the rule, the Service is delivered to cluster B and a user can access the Service from cluster A.
#. karmada-controller-manager monitors the changes of the Service and MCS object, delivers the Service to cluster B, and collects and sends endpoint slices of cluster B to cluster A.
#. When a user accesses the Service from cluster A, the request is routed to the service backend of cluster B. This is how cross-cluster service discovery and access occur.

Process of Using MCS
--------------------

:ref:`Figure 2 <ucs_01_0375__fig1563824751320>` shows the process of using MCS. The details are as follows:

#. Check the connectivity of both cluster nodes and containers. If they cannot communicate with each other, connect them as required. For details, see :ref:`Configuring the Cluster Network <ucs_01_0377>`.
#. Deploy available workloads and Services in the federation in advance. For details, see :ref:`Preparations <ucs_01_0378__section3746123012276>`.
#. Create an MCS object and configure an access rule. For details, see :ref:`Creating an MCS Object Using kubectl <ucs_01_0378__section7746559101919>`.
#. Simulate cross-cluster access. This means the Service delivered to one cluster will be accessed by the other cluster configured in MCS. For details, see :ref:`Cross-Cluster Access <ucs_01_0378__section687594962717>`.

.. _ucs_01_0375__fig1563824751320:

.. figure:: /_static/images/en-us_image_0000001749257256.png
   :alt: **Figure 2** Process of using MCS

   **Figure 2** Process of using MCS
