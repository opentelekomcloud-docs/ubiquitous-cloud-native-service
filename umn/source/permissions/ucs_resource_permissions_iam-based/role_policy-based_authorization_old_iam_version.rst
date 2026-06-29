:original_name: ucs_01_0156.html

.. _ucs_01_0156:

Role/Policy-based Authorization (Old IAM Version)
=================================================

System-defined permissions in role/policy-based authorization provided by `Identity and Access Management (IAM) <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0026.html>`__ let you control access to UCS. With IAM, you can:

-  Create IAM users for personnel based on your enterprise's organizational structure. Each IAM user has their own identity credentials for accessing UCS resources.
-  Grant users only the permissions required to perform a given task based on their job responsibilities.
-  Entrust an account or a cloud service to perform efficient O&M on your UCS resources.

If your account meets your permissions requirements, you can skip this section.

:ref:`Figure 1 <ucs_01_0156__fig151981527191516>` shows the process flow of role/policy-based authorization.

Prerequisites
-------------

-  A user with the **Security Administrator** role (for example, your account) has all IAM permissions except role switching. Only these users can view user groups and their permissions on the **Permissions** page on the UCS console.

Configuration Description
-------------------------

On the UCS console, when you choose **Permissions** > **Add Permission** to create a user or user group, you will be directed to the IAM console to complete the process. After the user or user group is created and the permissions are configured, you can view the information on the **Permissions** page of the cluster or fleet. This section describes the operations in IAM.

Process Flow
------------

.. _ucs_01_0156__fig151981527191516:

.. figure:: /_static/images/en-us_image_0000002492426226.png
   :alt: **Figure 1** Process of granting UCS permissions

   **Figure 1** Process of granting UCS permissions

#. .. _ucs_01_0156__li10176121316284:

   `Create a user group and grant it permissions <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0030.html>`__.

   On the IAM console, create a user group and grant it UCS read-only permissions (**UCS ReadOnlyAccess** as an example).

#. `Create an IAM user and add it to the user group. <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0031.html>`__

   On the IAM console, create a user and add it to the user group created in :ref:`1 <ucs_01_0156__li10176121316284>`.

#. `Log in as the IAM user <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0032.html>`__ and verify permissions.

   In the authorized region, perform the following operations:

   -  Choose **Service List** > **Ubiquitous Cloud Native Service**. In the navigation pane, choose **Infrastructure** > **Fleets**. Create a fleet or register a cluster. If a message appears indicating that you have insufficient permissions to perform the operation, the **UCS ReadOnlyAccess** policy is in effect.
   -  Choose another service (such as Elastic Cloud Server) from **Service List**. If a message appears indicating that you have insufficient permissions to access the service, the **UCS ReadOnlyAccess** policy is in effect.

.. _ucs_01_0156__section19693172419122:

System-defined Policies
-----------------------

The system-defined policies preset for UCS in IAM include **UCS FullAccess**, **UCS CommonOperations**, and **UCS ReadOnlyAccess**.

-  **UCS FullAccess**: administrator permissions for UCS. Users with these permissions can perform all operations on UCS, including creating permission policies and security policies.

   .. important::

      **UCS FullAccess** does not have the RBAC permissions of CCE clusters. Users need to go to the **Permissions** page to grant permissions for CCE clusters.

-  **UCS CommonOperations**: common operation permissions for UCS. Users with these permissions can create workloads and perform other operations.
-  **UCS ReadOnlyAccess**: read-only permissions for UCS.

You can check the content of a system-defined policy to learn about its supported actions. An action is in the format of *{service-name}*:*{resource-type}*:*{action}*. The wildcard (``*``) is allowed, indicating all actions.

The following shows the content of the **UCS FullAccess** policy. This policy contains all permissions for UCS, Cloud Container Engine (CCE), and SoftWare Repository for Container (SWR), and operation permissions on some resources of Application Operations Management (AOM), Simple Message Notification (SMN), Domain Name Service (DNS), and other services.

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

Least-Privilege Permissions for UCS Functions
---------------------------------------------

Services on T Cloud are interdependent, so UCS depends on other cloud services to implement some functions (such as image repositories and domain name resolution). The preceding four :ref:`system-defined policies <ucs_01_0156__section19693172419122>` are often used together with the roles or policies of other cloud services for refined authorization. When granting permissions to IAM users, the administrator must comply with the principle of least privilege. :ref:`Table 1 <ucs_01_0156__table7597629178>` lists the least-privilege permissions required by the Administrator, Operator, and Viewer roles to use UCS functions.

.. important::

   -  If your T Cloud account logs in to the UCS console for the first time, you need to grant permissions to the account. UCS will create an agency named **ucs_admin_trust** for you in IAM. Do not delete or modify the agency.
   -  If no permissions are granted to the user group that an IAM user belongs to, access to the UCS console will be denied. Grant permissions by referring to :ref:`Table 1 <ucs_01_0156__table7597629178>`.
   -  UCS FullAccess does not have the RBAC permissions of CCE clusters. You need to go to the **Permissions** page to grant permissions for CCE clusters as described in the following table.

.. _ucs_01_0156__table7597629178:

.. table:: **Table 1** Least-privilege permissions for UCS functions

   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | Function           | Permission Type | Permissions                                                                                                                                                                                      | Least-Privilege Permissions                                               |
   +====================+=================+==================================================================================================================================================================================================+===========================================================================+
   | Fleets             | Administrator   | -  Creating and deleting a fleet                                                                                                                                                                 | UCS FullAccess                                                            |
   |                    |                 | -  Registering a T Cloud cluster (CCE standard cluster or CCE Turbo cluster) or an attached cluster                                                                                              |                                                                           |
   |                    |                 | -  Unregistering a cluster                                                                                                                                                                       |                                                                           |
   |                    |                 | -  Adding a cluster to or removing a cluster from a fleet                                                                                                                                        |                                                                           |
   |                    |                 | -  Adding permissions for a cluster or fleet                                                                                                                                                     |                                                                           |
   |                    |                 | -  Enabling cluster federation and managing the federation (such as creating a workload and creating a domain name access policy)                                                                |                                                                           |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   |                    | Viewer          | Querying the list of clusters or fleets, or details about a cluster or fleet                                                                                                                     | UCS ReadOnlyAccess                                                        |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | T Cloud clusters   | Administrator   | Read-write permissions on T Cloud clusters and all Kubernetes resource objects (such as nodes, workloads, jobs, and Services) in the clusters                                                    | UCS FullAccess + CCE Administrator                                        |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   |                    | Developer       | Read-write permissions on T Cloud clusters and most Kubernetes resource objects in the clusters and read-only permissions on Kubernetes resource objects such as namespaces and resource quotas  | UCS CommonOperations + CCE Administrator                                  |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   |                    | Viewer          | Read-only permissions on T Cloud clusters and all Kubernetes resource objects (such as nodes, workloads, jobs, and Services) in the clusters                                                     | UCS ReadOnlyAccess + CCE Administrator                                    |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | Attached clusters  | Administrator   | Read-write permissions on attached clusters and all Kubernetes resource objects (such as nodes, workloads, jobs, and Services) in the clusters                                                   | UCS FullAccess                                                            |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   |                    | Developer       | Read-write permissions on attached clusters and most Kubernetes resource objects in the clusters and read-only permissions on Kubernetes resource objects such as namespaces and resource quotas | UCS CommonOperations + UCS RBAC (permissions to list namespaces required) |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   |                    | Viewer          | Read-only permissions on attached clusters and all Kubernetes resource objects (such as nodes, workloads, jobs, and Services) in the clusters                                                    | UCS ReadOnlyAccess + UCS RBAC (permissions to list namespaces required)   |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | Image repositories | Administrator   | All permissions on SWR, such as creating organizations, pushing images, viewing the image list or details about an image, and pulling images                                                     | SWR Administrator                                                         |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | Permissions        | Administrator   | -  Creating and deleting permissions                                                                                                                                                             | UCS FullAccess + IAM ReadOnlyAccess                                       |
   |                    |                 | -  Viewing the permission list or permission details                                                                                                                                             |                                                                           |
   |                    |                 |                                                                                                                                                                                                  |                                                                           |
   |                    |                 | .. note::                                                                                                                                                                                        |                                                                           |
   |                    |                 |                                                                                                                                                                                                  |                                                                           |
   |                    |                 |    When granting permissions, you need to grant the **IAM ReadOnlyAccess** permissions (read-only permissions on IAM) to IAM users to obtain the IAM user list.                                  |                                                                           |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   |                    | Viewer          | Viewing the permission list or permission details                                                                                                                                                | UCS ReadOnlyAccess + IAM ReadOnlyAccess                                   |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+

Custom Policies
---------------

You can create custom policies to supplement the system-defined policies of UCS.

To create a custom policy, choose either visual editor or JSON.

-  Visual editor: Select cloud services, actions, resources, and request conditions. This does not require knowledge of policy grammar.
-  JSON: Create a JSON policy or edit an existing one.

The following lists examples of common UCS custom policies.

**Examples:**

-  Example 1: Grant permission to create a cluster.

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

-  Example 2: Grant permission to deny cluster deletion.

   A policy with only "Deny" permissions must be used together with other policies. If the permissions granted to an IAM user contain both "Allow" and "Deny", the "Deny" permissions take precedence over the "Allow" permissions.

   Assume that you want to grant the permissions of the **UCSFullAccess** policy to a user but want to prevent the user from deleting clusters (**ucs:clusters:delete**). You can create a custom policy for denying cluster deletion, and attach this policy together with the **UCSFullAccess** policy to the user. As an explicit "Deny" policy overrides any "Allow" policy, the user can perform all operations on clusters excepting deleting them. Example policy denying cluster deletion:

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

-  Example 3: Create a custom policy containing multiple actions.

   A custom policy can contain the actions of one or multiple services that are of the same type (global or project-level). Example policy containing multiple actions:

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
