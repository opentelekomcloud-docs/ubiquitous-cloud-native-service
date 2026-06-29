:original_name: ucs_01_0157.html

.. _ucs_01_0157:

Identity Policy-based Authorization (New IAM Version)
=====================================================

System-defined permissions in identity policy-based authorization provided by `Identity and Access Management (IAM) <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0026.html>`__ let you control access to UCS. With IAM, you can:

-  Create IAM users for personnel based on your enterprise's organizational structure. Each IAM user has their own identity credentials for accessing UCS resources.
-  Grant users only the permissions required to perform a given task based on their job responsibilities.
-  Entrust an account or a cloud service to perform efficient O&M on your UCS resources.

If your account meets your permissions requirements, you can skip this section.

:ref:`Figure 1 <ucs_01_0157__fig798020119436>` shows the process flow of identity policy-based authorization.

Prerequisites
-------------

-  A user with the **Security Administrator** role (for example, your account) has all IAM permissions except role switching. Only these users can view user groups and their permissions on the **Permissions** page on the UCS console.

Configuration Description
-------------------------

On the UCS console, when you choose **Permissions** > **Add Permission** to create a user or user group, you will be directed to the IAM console to complete the process. After the user or user group is created and the permissions are configured, you can view the information on the **Permissions** page of the cluster or fleet. This section describes the operations in IAM.

Process Flow
------------

.. _ucs_01_0157__fig798020119436:

.. figure:: /_static/images/en-us_image_0000002524559447.png
   :alt: **Figure 1** Process of granting UCS permissions

   **Figure 1** Process of granting UCS permissions

#. Create a user or user group.

   On the IAM console, create a user or user group.

   .. note::

      UCS is a global service deployed for all regions. When granting permissions, set the authorization scope to **All resources**.

#. Attach a system-defined identity policy to the user or user group.

   Grant the permissions defined in the system-defined identity policy **UCSReadOnlyPolicy** to the user or user group, or attach the system-defined identity policy to it.

#. `Log in as the IAM user <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0032.html>`__ and verify permissions.

   In the authorized region, perform the following operations:

   -  Choose **Service List** > **Ubiquitous Cloud Native Service**. In the navigation pane, choose **Infrastructure** > **Fleets**. Create a fleet or register a cluster. If a message appears indicating that you have insufficient permissions to perform the operation, the **UCSReadOnlyPolicy** policy is in effect.
   -  Choose another service from **Service List**. If a message appears indicating that you have insufficient permissions to access the service, the **UCSReadOnlyPolicy** policy is in effect.

.. _ucs_01_0157__section853330222:

Identity Policies
-----------------

The system-defined identity policies preset for UCS in IAM are **UCSFullAccessPolicy**, **UCSCommonOperationsPolicy**, and **UCSReadOnlyPolicy**.

-  **UCSFullAccessPolicy**: administrator permissions for UCS. Users with these permissions can perform all operations on UCS, including creating permission policies and security policies.
-  **UCSCommonOperationsPolicy**: common operation permissions for UCS. Users with these permissions can create workloads, distribute traffic, and perform other operations.
-  **UCSReadOnlyPolicy**: read-only permissions for UCS.

Least-Privilege Permissions for UCS Functions
---------------------------------------------

Services on T Cloud are interdependent, so UCS depends on other cloud services to implement some functions (such as image repositories and domain name resolution). The three system-defined identity policies in :ref:`Identity Policies <ucs_01_0157__section853330222>` are often used together with the roles or policies of other cloud services for refined authorization. When granting permissions to IAM users, the administrator must comply with the principle of least privilege. :ref:`Table 1 <ucs_01_0157__table7597629178>` lists the least-privilege permissions required by the Administrator, Operator, and Viewer roles to use UCS functions.

.. important::

   -  If your T Cloud account logs in to the UCS console for the first time, you need to grant permissions to the account. UCS will create an agency named **ucs_admin_trust** for you in IAM. Do not delete or modify the agency.
   -  If no permissions are granted to the user group that an IAM user belongs to, access to the UCS console will be denied. Grant permissions by referring to :ref:`Table 1 <ucs_01_0157__table7597629178>`.
   -  **UCSFullAccessPolicy** does not have the RBAC permissions of CCE clusters. You need to go to the **Permissions** page to grant permissions for CCE clusters as described in the following table.

.. _ucs_01_0157__table7597629178:

.. table:: **Table 1** Least-privilege permissions for UCS functions

   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   | Function           | Permission Type | Permissions                                                                                                                                                                                      | Least-Privilege Permissions                                                    |
   +====================+=================+==================================================================================================================================================================================================+================================================================================+
   | Fleets             | Administrator   | -  Creating and deleting a fleet                                                                                                                                                                 | UCSFullAccessPolicy                                                            |
   |                    |                 | -  Registering a T Cloud cluster (CCE standard cluster or CCE Turbo cluster) or an attached cluster                                                                                              |                                                                                |
   |                    |                 | -  Unregistering a cluster                                                                                                                                                                       |                                                                                |
   |                    |                 | -  Adding a cluster to or removing a cluster from a fleet                                                                                                                                        |                                                                                |
   |                    |                 | -  Adding permissions for a cluster or fleet                                                                                                                                                     |                                                                                |
   |                    |                 | -  Enabling cluster federation and managing the federation (such as creating a workload and creating a domain name access policy)                                                                |                                                                                |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   |                    | Viewer          | Querying the list of clusters or fleets, or details about a cluster or fleet                                                                                                                     | UCSReadOnlyPolicy                                                              |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   | T Cloud clusters   | Administrator   | Read-write permissions on T Cloud clusters and all Kubernetes resource objects (such as nodes, workloads, jobs, and Services) in the clusters                                                    | UCSFullAccessPolicy + CCEFullPolicy                                            |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   |                    | Developer       | Read-write permissions on T Cloud clusters and most Kubernetes resource objects in the clusters and read-only permissions on Kubernetes resource objects such as namespaces and resource quotas  | UCSCommonOperationsPolicy + CCEFullPolicy                                      |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   |                    | Viewer          | Read-only permissions on T Cloud clusters and all Kubernetes resource objects (such as nodes, workloads, jobs, and Services) in the clusters                                                     | UCSReadOnlyPolicy + CCEFullPolicy                                              |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   | Attached clusters  | Administrator   | Read-write permissions on attached clusters and all Kubernetes resource objects (such as nodes, workloads, jobs, and Services) in the clusters                                                   | UCSFullAccessPolicy                                                            |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   |                    | Developer       | Read-write permissions on attached clusters and most Kubernetes resource objects in the clusters and read-only permissions on Kubernetes resource objects such as namespaces and resource quotas | UCSCommonOperationsPolicy + UCS RBAC (permissions to list namespaces required) |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   |                    | Viewer          | Read-only permissions on attached clusters and all Kubernetes resource objects (such as nodes, workloads, jobs, and Services) in the clusters                                                    | UCSReadOnlyPolicy + UCS RBAC (permission to list namespaces required)          |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   | Image repositories | Administrator   | All permissions on SWR, such as creating organizations, pushing images, viewing the image list or details about an image, and pulling images                                                     | SWRFullAccessPolicy                                                            |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   | Permissions        | Administrator   | -  Creating and deleting permissions                                                                                                                                                             | UCSFullAccessPolicy + IAMReadOnlyPolicy                                        |
   |                    |                 | -  Viewing the permission list or permission details                                                                                                                                             |                                                                                |
   |                    |                 |                                                                                                                                                                                                  |                                                                                |
   |                    |                 | .. note::                                                                                                                                                                                        |                                                                                |
   |                    |                 |                                                                                                                                                                                                  |                                                                                |
   |                    |                 |    When granting permissions, you need to grant the **IAMReadOnlyPolicy** permissions (read-only permissions on IAM) to IAM users to obtain the IAM user list.                                   |                                                                                |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+
   |                    | Viewer          | Viewing the permission list or permission details                                                                                                                                                | UCSReadOnlyPolicy + IAMReadOnlyPolicy                                          |
   +--------------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------+

Example Custom Identity Policies
--------------------------------

You can create custom identity policies to supplement the system-defined identity policies of UCS.

To create a custom identity policy, choose either visual editor or JSON.

-  Visual editor: Select cloud services, actions, resources, and request conditions. This does not require knowledge of policy grammar.
-  JSON: Create a JSON policy or edit an existing one.

When creating a custom identity policy, use the Resource element to specify the resources the identity policy applies to and use the Condition element (service-specific condition keys) to control when the identity policy is in effect. The following provides examples of custom UCS identity policies.

-  Example 1: Grant permission to create a cluster.

   .. code-block::

      {
        "Version": "5.0",
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ucs:clusters:createCluster"
            ]
          }
        ]
      }

-  Example 2: Create a custom identity policy containing multiple actions.

   A custom identity policy can contain the actions of one or more services. Example identity policy containing multiple actions:

   .. code-block::

      {
        "Version": "5.0",
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ucs:clustergroups:createFleet",
              "ucs:clustergroups:deleteFleet"
            ]
          },
          {
            "Effect": "Deny",
            "Action": [
              "ucs:addons:delete"
            ]
          }
        ]
      }
