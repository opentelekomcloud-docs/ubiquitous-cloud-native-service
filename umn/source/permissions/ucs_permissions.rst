:original_name: ucs_01_0010.html

.. _ucs_01_0010:

UCS Permissions
===============

UCS permissions management allows you to grant permissions to IAM users and user groups under your tenant accounts. UCS combines the advantages of IAM and Kubernetes RBAC to provide a variety of authorization methods, including IAM fine-grained and token authorization and cluster-, fleet-, cluster namespace-, and fleet namespace-level authorization.

UCS allows you to manage permissions on related resources at a finer granularity, for example, to control the access of employees in different departments to cloud resources.

This section describes the UCS permissions management mechanism and related concepts. If your account has met your service requirements, you can skip the configurations in this section.

.. note::

   -  Permissions management applies to single clusters and fleets with cluster federation enabled. To use permissions management, :ref:`enable cluster federation for your fleet <ucs_01_0018>`.
   -  UCS supports IAM authorization but does not support enterprise project authorization.


.. figure:: /_static/images/en-us_image_0000002202216004.png
   :alt: **Figure 1** Permissions design

   **Figure 1** Permissions design

UCS Permissions Management
--------------------------

UCS permissions management involves UCS resource permissions and Kubernetes resource permissions in a cluster.

-  **UCS resource permissions** are based on IAM system-defined policies and include cluster-level permissions and fleet-level permissions.
-  **Kubernetes resource permissions in a cluster** are based on Kubernetes RBAC and include cluster namespace-level permissions and fleet namespace-level permissions.

UCS permissions are described as follows:

-  **Cluster-level permissions**: You can grant cluster-level permissions to allow some user groups to perform operations on clusters (such as registering and deregistering clusters and managing cluster add-ons) and allow some user groups to only view clusters.

-  **Fleet-level permissions**: You can grant fleet-level permissions to allow some user groups to perform operations on fleets (such as creating and deleting fleets, adding clusters to fleets, and deleting clusters from fleets) and allow some user groups to only view fleets.

   UCS resource permissions involve UCS non-fleet APIs and Kubernetes APIs and support fine-grained IAM policies and enterprise project management. Fleet-level permissions are configured for fleet-related resources (such as fleets and federations), and cluster-level permissions are configured for cluster-related resources (such as clusters and nodes). You must also configure namespace-level permissions to perform operations on fleet resources and Kubernetes resources (such as workloads, Services, and routes). Fleet-level permissions and cluster-level permissions are independent of each other.

-  **Cluster namespace-level permissions**: You can regulate users' or user groups' access to Kubernetes resources (such as workloads, jobs, Services, and other native Kubernetes resources) based on their Kubernetes RBAC roles.

-  **Fleet namespace-level permissions**: You can regulate users' or user groups' access to fleet resources (such as workloads, Services, MCI, distribution policies, and other native fleet resources) based on their fleet RBAC roles.

   Kubernetes resource permissions in a cluster involve UCS Kubernetes APIs and are enhanced based on the Kubernetes RBAC capabilities. These permissions can be granted to IAM users or user groups for authentication and authorization, but are independent of fine-grained IAM policies.

   In general, you can configure UCS permissions in two scenarios. The first is creating and managing clusters and fleets, as well as their related resources, such as nodes. The second is using Kubernetes resources in a cluster and fleet resources, such as workloads and Services.


   .. figure:: /_static/images/en-us_image_0000002269702534.png
      :alt: **Figure 2** Illustration on UCS permissions

      **Figure 2** Illustration on UCS permissions

.. _ucs_01_0010__section322351221619:

UCS Resource Permissions (IAM-based) and Kubernetes Resource Permissions in a Cluster (Kubernetes RBAC-based)
-------------------------------------------------------------------------------------------------------------

Users with different UCS resource permissions have different Kubernetes resource permissions in a cluster. :ref:`Table 1 <ucs_01_0010__table413216578166>` describes the Kubernetes resource permissions in a cluster for different users.

.. _ucs_01_0010__table413216578166:

.. table:: **Table 1** Kubernetes resource permissions in a cluster for different users

   +---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | User Type                                                                 | UCS Resource Permissions                                                                          | Kubernetes Resource Permissions in a Cluster                                                                                                                  |
   +===========================================================================+===================================================================================================+===============================================================================================================================================================+
   | Users with the **Tenant Administrator** or **UCS FullAccess** permissions | Operation permissions for clusters, fleets, add-ons, policy center, traffic distribution, and CIA | All namespace permissions                                                                                                                                     |
   |                                                                           |                                                                                                   |                                                                                                                                                               |
   |                                                                           |                                                                                                   | .. note::                                                                                                                                                     |
   |                                                                           |                                                                                                   |                                                                                                                                                               |
   |                                                                           |                                                                                                   |    **UCS FullAccess** does not have the RBAC permissions of CCE clusters. Users need to go to the **Permissions** page to grant permissions for CCE clusters. |
   +---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Users with the **UCS CommonOperations** permissions                       | Read-only permissions for clusters, fleets, traffic distribution, add-ons, and policy center      | RBAC authorization                                                                                                                                            |
   +---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IAM users with the **UCS ReadOnlyAccess** permissions                     | Read-only permissions on UCS resources                                                            | RBAC authorization                                                                                                                                            |
   +---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IAM users with the **UCS CIAOperations** permissions                      | Operation permissions for CIA instances in UCS                                                    | RBAC authorization                                                                                                                                            |
   +---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IAM users with the **Tenant Guest** permissions                           | Read-only permissions on UCS resources                                                            | RBAC authorization                                                                                                                                            |
   +---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+

Permissions Management Flow
---------------------------

The following figure shows the permissions management flow of a new IAM user.


.. figure:: /_static/images/en-us_image_0000002237255937.png
   :alt: **Figure 3** Permissions management flow

   **Figure 3** Permissions management flow

Basic Concepts
--------------

:ref:`Figure 4 <ucs_01_0010__fig136064712176>` shows the relationships between the following basic concepts:

-  **User:** You can use your administrator account to create IAM users and grant permissions on specific resources. Each IAM user has their own identity credentials (password and access keys) and uses cloud resources based on granted permissions.
-  **User group:** You can use user groups to grant permissions to IAM users. IAM users added to a user group automatically obtain the permissions granted to the group. For example, after the administrator grants the **UCS FullAccess** permissions to a user group, users in the user group have the administrator permissions of UCS. If a user is added to multiple user groups, the user inherits the permissions granted to all these groups.
-  **Namespace**: A namespace is a collection of resources and objects. You can create multiple namespaces in the same cluster. Data is isolated by namespace so that multiple namespaces can share the services of the same cluster without any interference with each other. For example, you can deploy workloads in a development environment into one namespace, and deploy workloads in a testing environment into another namespace.
-  **Permission types:** The UCS administrator defines the scope of operations performed by one or more users on Kubernetes resources in a cluster. There are several common permission types on UCS, including **Administrator**, **O&M**, **Developer**, and **Viewer**. You can also create custom permissions. For details, see .
-  **Fleet:** A fleet contains multiple clusters. An administrator can use fleets to classify associated clusters. An administrator can also use a fleet for the unified management of multiple clusters, including permissions management, security policy configuration, and multi-cluster orchestration.

.. _ucs_01_0010__fig136064712176:

.. figure:: /_static/images/en-us_image_0000002225124869.png
   :alt: **Figure 4** Permission relationships

   **Figure 4** Permission relationships
