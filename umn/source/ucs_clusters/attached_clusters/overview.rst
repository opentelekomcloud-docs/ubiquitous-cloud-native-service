:original_name: ucs_01_0162.html

.. _ucs_01_0162:

Overview
========

Attached clusters refer to third-party Kubernetes clusters that comply with the Cloud Native Computing Foundation (CNCF) standard, such as AWS EKS clusters, Google Cloud GKE clusters, and Kubernetes clusters that are deployed and run by third parties.

:ref:`Figure 1 <ucs_01_0162__fig1037664362220>` shows the attached cluster management process.

.. _ucs_01_0162__fig1037664362220:

.. figure:: /_static/images/en-us_image_0000001433849600.png
   :alt: **Figure 1** Attached cluster management process

   **Figure 1** Attached cluster management process

Access Mode
-----------

Cluster providers or on-premises data centers have different inbound port rules for attached clusters to prevent inbound traffic from ports other than the specific ones. UCS uses the cluster network agent to access clusters. You do not need to enable any inbound port on the firewall. Instead, only the cluster agent program is required to establish sessions with UCS in the outbound direction.

There are two methods with different advantages for attached clusters to connect to UCS:

-  :ref:`Over a public network <ucs_01_0005>`: flexibility, cost-effectiveness, and easy access
-  :ref:`Over a private network <ucs_01_0006>`: high speed, low latency, stability, and security

.. important::

   The list and create permissions of RBAC are required for fine-grained permissions control when an attached cluster is registered with and connected to UCS.

   RBAC permissions include the following four resources: Roles, RoleBindings, ClusterRoles, and ClusterRoleBindings.
