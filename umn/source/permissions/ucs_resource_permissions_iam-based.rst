:original_name: ucs_01_0156.html

.. _ucs_01_0156:

UCS Resource Permissions (IAM-based)
====================================

UCS cluster- and fleet-level permissions are assigned based on IAM system-defined policies and custom policies. You can use user groups to assign permissions to IAM users.

.. caution::

   -  Cluster- and fleet-level permissions are configured only for cluster- and fleet-related resources (such as resources for the cluster management, fleet management, add-on management, policy center, configuration management, traffic distribution, container intelligent analysis, and other functions). You must also configure :ref:`Kubernetes resource permissions <ucs_01_0011>` to perform operations on Kubernetes resources (such as workloads and Services in a cluster).
   -  When you view a cluster or fleet on the UCS console, the information displayed depends on the Kubernetes resource permissions. If the Kubernetes resource permissions are not configured, you cannot view the resources in the cluster or fleet.

Prerequisites
-------------

-  A user with the Security Administrator role (for example, your account) has all IAM permissions except role switching. Only these users can view user groups and their permissions on the **Permissions** page on the UCS console.

Configuration Description
-------------------------

On the UCS console, when you choose **Permissions** > **Add Permission** to create a user or user group, you will be directed to the IAM console to complete the process. After the user or user group is created and its permissions are configured, you can view the information on the **Permissions** page. This section describes the operations on IAM.

Process Flow
------------


.. figure:: /_static/images/en-us_image_0000002304425873.png
   :alt: **Figure 1** Process for assigning UCS permissions

   **Figure 1** Process for assigning UCS permissions

#. .. _ucs_01_0156__li10176121316284:

   `Create a user group and assign permissions <https://docs.otc.t-systems.com/identity-access-management/umn/user_guide/user_groups_and_authorization/creating_a_user_group_and_assigning_permissions.html#en-us-topic-0046611269>`__.

   On the IAM console, create a user group and grant it UCS permissions (UCS ReadOnlyAccess as an example).

   .. note::

      UCS is a global service deployed in all physical regions. When granting permissions, set the authorization scope to **All resources**.

#. `Create a user and add it to the user group <https://docs.otc.t-systems.com/identity-access-management/umn/user_guide/iam_users/creating_a_user.html#en-us-topic-0046611303>`__.

   Create a user on the IAM console and add it to the user group created in :ref:`1 <ucs_01_0156__li10176121316284>`.

#. `Log in <https://docs.otc.t-systems.com/identity-access-management/umn/user_guide/iam_users/logging_in_as_an_iam_user.html#iam-01-0552>`__ and verify permissions.

   Log in to the console as the created user and verify the permissions. (Assume that the user has only the **UCS ReadOnlyAccess** permissions.)

   -  Choose **Ubiquitous Cloud Native Service** from the service list. In the navigation pane, choose **Infrastructure** > **Fleets**. If a message indicating that you do not have the access permissions is displayed when you create a fleet or register a cluster, the **UCS ReadOnlyAccess** permissions have taken effect.
   -  Choose another service (such as Elastic Cloud Server) from the service list. If a message indicating insufficient permissions is displayed, the **UCS ReadOnlyAccess** permissions have taken effect.

System-defined Roles
--------------------

Roles are a type of coarse-grained authorization mechanism that defines service-level permissions based on user responsibilities. Only a limited number of service-level roles are available for authorization. However, roles are not an ideal choice for fine-grained authorization and secure access control.

The preset system role for UCS in IAM is **UCS Administrator**. When assigning this role to a user group, you must also select other roles and policies on which this role depends, such as **Tenant Guest**, **Server Administrator**, **ELB Administrator**, **OBS Administrator**, **SFS Administrator**, **APM FullAccess**, and **SWR Admin**.

.. _ucs_01_0156__section19693172419122:

System-defined Policies
-----------------------

The system-defined policies preset for UCS in IAM include **UCS FullAccess**, **UCS CommonOperations**, and **UCS ReadOnlyAccess**.

-  **UCS FullAccess**: UCS administrator with full permissions, including creating permission policies and security policies

   .. important::

      **UCS FullAccess** does not have the RBAC permissions of CCE clusters. You need to go to the **Permissions** page to grant permissions for CCE clusters.

-  **UCS CommonOperations**: common operation permissions for UCS. Users with these permissions can create workloads and perform other operations.
-  **UCS ReadOnlyAccess**: read-only permissions for UCS services

You can check the content of a system-defined policy to learn about its supported actions. An action is in the format of *{service-name}*:*{resource-type}*:*{action}*. The wildcard (``*``) is allowed, indicating all actions.

The following is an example of the **UCS FullAccess** policy. This policy contains all permissions for UCS, Cloud Container Engine (CCE), and SoftWare Repository for Container (SWR), and operation permissions on some resources of Application Operations Management (AOM), Simple Message Notification (SMN), Domain Name Service (DNS), and other services.

.. code-block::

   {
       "Version": "1.1",
       "Statement": [
           {
               "Action": [
                   "ucs:*:*",
                   "cce:*:*",
                   "swr:*:*",
                   "aom:*:get",
                   "aom:*:list",
                   "smn:*:list",
                   "dns:*:get*",
                   "dns:*:list*",
                   "dns:*:get",
                   "dns:*:list",
                   "dns:recordset:create",
                   "dns:recordset:delete",
                   "dns:recordset:update",
                   "dns:tag:get",
                   "lts:*:get",
                   "lts:*:list",
                   "apm:*:get",
                   "apm:*:list",
                   "vpcep:epservices:*",
                   "vpcep:connections:*",
                   "vpcep:endpoints:*",
                   "elb:*:get",
                   "elb:*:list",
                   "vpc:*:get",
                   "vpc:*:list",
                   "ief:*:get",
                   "ief:*:list",
                   "cgs:images:operate",
                   "cgs:*:get",
                   "cgs:*:list"
               ],
               "Effect": "Allow"
           }
       ]
   }

Least-Privilege Permissions Required by Each UCS Function
---------------------------------------------------------

Services on OTC are interdependent, so UCS depends on other cloud services to implement some functions (such as image repository and domain name resolution). The preceding four :ref:`system-defined policies <ucs_01_0156__section19693172419122>` are often used together with the roles or policies of other cloud services for refined authorization. When granting permissions to IAM users, the administrator must comply with the principle of least privilege. :ref:`Table 1 <ucs_01_0156__table7597629178>` lists the least-privilege permissions required by the Administrator, Operator, and Viewer roles to use each UCS function.

.. important::

   -  If your OTC account is used to log in to the UCS console for the first time, you need to grant permissions to the account. Then, UCS will create an agency named **ucs_admin_trust** for you in IAM. Do not delete or modify the agency.
   -  If the user group that an IAM user belongs to is not granted any permissions, you cannot access the UCS console. Grant permissions by referring to :ref:`Table 1 <ucs_01_0156__table7597629178>`.
   -  UCS FullAccess does not have the RBAC permissions of CCE clusters. You need to go to the **Permissions** page to grant permissions for CCE clusters as described in the following table.

.. _ucs_01_0156__table7597629178:

.. table:: **Table 1** Least-privilege permissions required by each UCS function

   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | Function           | Permission Type | Permissions                                                                                                                                                                      | Least-Privilege Permissions                                                                   |
   +====================+=================+==================================================================================================================================================================================+===============================================================================================+
   | Fleets             | Administrator   | -  Creating and deleting a fleet                                                                                                                                                 | UCS FullAccess                                                                                |
   |                    |                 | -  Registering an OTC cluster (CCE standard cluster or CCE Turbo cluster) or an attached cluster                                                                                 |                                                                                               |
   |                    |                 | -  Unregistering a cluster                                                                                                                                                       |                                                                                               |
   |                    |                 | -  Adding a cluster to or removing a cluster from a fleet                                                                                                                        |                                                                                               |
   |                    |                 | -  Adding permissions for a cluster or fleet                                                                                                                                     |                                                                                               |
   |                    |                 | -  Enabling cluster federation and performing federation management operations (such as creating a workload and creating a DNS policy)                                           |                                                                                               |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   |                    | Viewer          | Querying the list or details of clusters or fleets                                                                                                                               | UCS ReadOnlyAccess                                                                            |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | OTC clusters       | Administrator   | Read-write permissions on OTC clusters and all Kubernetes resource objects (including nodes, workloads, jobs, and Services)                                                      | UCS FullAccess + CCE Administrator                                                            |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   |                    | Developer       | Read-write permissions on OTC clusters and most Kubernetes resource objects and read-only permissions on Kubernetes resource objects such as namespaces and resource quotas      | UCS CommonOperations + CCE Administrator                                                      |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   |                    | Viewer          | Read-only permissions on OTC clusters and all Kubernetes resource objects (including nodes, workloads, jobs, and Services)                                                       | UCS ReadOnlyAccess + CCE Administrator                                                        |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | Attached clusters  | Administrator   | Read-write permissions on attached clusters and all Kubernetes resource objects (such as nodes, workloads, jobs, and Services)                                                   | UCS FullAccess                                                                                |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   |                    | Developer       | Read-write permissions on attached clusters and most Kubernetes resource objects and read-only permissions on Kubernetes resource objects such as namespaces and resource quotas | UCS CommonOperations + UCS RBAC permissions (The list permission for namespaces is required.) |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   |                    | Viewer          | Read-only permissions on attached clusters and all Kubernetes resource objects (such as nodes, workloads, jobs, and Services)                                                    | UCS ReadOnlyAccess + UCS RBAC permissions (The list permission for namespaces is required.)   |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | Image Repositories | Administrator   | All permissions on SWR, including creating organizations, pushing images, viewing the image list or details, and pulling images                                                  | SWR Administrator                                                                             |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | Permissions        | Administrator   | -  Creating and deleting permissions                                                                                                                                             | UCS FullAccess + IAM ReadOnlyAccess                                                           |
   |                    |                 | -  Viewing the permission list or details                                                                                                                                        |                                                                                               |
   |                    |                 |                                                                                                                                                                                  |                                                                                               |
   |                    |                 | .. note::                                                                                                                                                                        |                                                                                               |
   |                    |                 |                                                                                                                                                                                  |                                                                                               |
   |                    |                 |    When creating permissions, you need to grant the **IAM ReadOnlyAccess** permissions (read-only permissions on IAM) to IAM users to obtain the IAM user list.                  |                                                                                               |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   |                    | Viewer          | Viewing the permission list or details                                                                                                                                           | UCS ReadOnlyAccess + IAM ReadOnlyAccess                                                       |
   +--------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+

Custom Policies
---------------

Custom policies can be created as a supplement to the system-defined policies of UCS.

You can create custom policies in either of the following ways:

-  Visual editor: Select cloud services, actions, resources, and request conditions without the need to know policy syntax.
-  JSON: Create a JSON policy or edit an existing one.

The following lists examples of common UCS custom policies.

**Examples**

-  Example 1: Creating a cluster

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "ucs:clusters:create"
                  ]
              }
          ]
      }

-  Example 2: Denying cluster deletion

   A policy with only "Deny" permissions must be used with other policies. If the permissions assigned to a user contain both "Allow" and "Deny", the "Deny" permissions take precedence over the "Allow" permissions.

   If you want to grant the **UCSFullAccess** permissions to a user but prevent the user from deleting clusters (**ucs:clusters:delete**), you can create a custom policy that denies cluster deletion. Then, attach this policy with the **UCSFullAccess** policy to the user. Since an explicit denial in any policy takes precedence over any allowances, the user will have permissions to perform all operations on clusters except for deleting them. The following is an example policy that denies cluster deletion:

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Deny",
                  "Action": [
                      "ucs:clusters:delete"
                  ]
              }
          ]
      }

-  Example 3: Creating a custom policy containing multiple actions

   A custom policy can contain the actions of multiple services that are of the global or project-level type. The following is an example policy containing actions of multiple services:

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "ucs:clustergroups:create",
                      "ucs:ciaEvents:update",
                      "ucs:addonTemplates:delete"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "obs:bucket:GetBucketInventoryConfiguration",
                      "obs:bucket:CreateBucket"
                  ]
              }
          ]
      }
