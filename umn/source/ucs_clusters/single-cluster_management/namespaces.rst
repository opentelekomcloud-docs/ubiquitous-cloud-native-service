:original_name: ucs_01_0117.html

.. _ucs_01_0117:

Namespaces
==========

Namespaces that you create on the cluster console apply only to the current cluster. You can create Kubernetes objects and manage resource quotas in such namespaces, or delete these namespaces.

-  The **default** namespace created by the system supports quota management but cannot be deleted.
-  Namespaces created by a cluster, such as **kube-public** and **kube-system**, do not support quota management and cannot be deleted.

.. _ucs_01_0117__en-us_topic_0167389656_section31143617514:

Creating a Namespace
--------------------

#. Access the cluster details page.
#. Choose **Namespaces** in the navigation pane, click **Create Namespace** in the upper right corner, and configure parameters.

   -  **Namespace Name**: Name of the namespace, which must be unique in a cluster.

   -  **Description**: Description of the namespace.

   -  **Quota Management**: If this function is enabled, you can configure resource quotas. Resource quotas can limit the amount of resources available in namespaces, achieving resource allocation by namespace.

      If you do not enable this function, you can click **Manage Quota** in the namespace list to configure resource quotas after the namespace is created. For details, see :ref:`Configuring Resource Quotas in a Namespace <ucs_01_0117__en-us_topic_0167389656_section1883212914267>`.

#. Click **OK**.

Deleting a Namespace
--------------------

.. important::

   Deleting a namespace will delete all data resources related to the namespace. Exercise caution when performing this operation.

#. Access the cluster details page.
#. In the navigation pane, choose **Namespaces**, select the target namespace, and choose **More** > **Delete**.

.. _ucs_01_0117__en-us_topic_0167389656_section1883212914267:

Configuring Resource Quotas in a Namespace
------------------------------------------

Resource quotas can limit the amount of resources available in namespaces, achieving resource allocation by namespace.

Namespace-level resource quotas limit the amount of resources available to teams or users when these teams or users use the same cluster. The quotas include the total number of a type of objects and the total amount of compute resources (CPU and memory) consumed by the objects.

.. important::

   The **kube-public** and **kube-system** namespaces do not support resource quota settings.

#. Access the cluster details page.
#. In the navigation pane, choose **Namespaces**, locate the target namespace, and click **Manage Quota** in the **Operation** column.
#. Configure resource quotas.

   .. important::

      -  There is no limit on quotas by default. To specify a resource quota, enter an integer greater than or equal to 1. If you want to limit the CPU or memory quota, you must specify the CPU or memory request when creating a workload.
      -  Accumulated quota usage includes the default resources created by the system, such as the Kubernetes Service (view this Service using the kubectl tool) created in the **default** namespace. Therefore, you are advised to set a resource quota greater than what you expect.

   -  **CPU (cores)**: maximum number of CPU cores that can be allocated to workload pods in the namespace.
   -  **Memory (MiB)**: maximum amount of memory that can be allocated to workload pods in the namespace.
   -  **StatefulSet**: Maximum number of StatefulSets that can be created in the namespace.
   -  **Deployment**: Maximum number of Deployments that can be created in the namespace.
   -  **Job**: Maximum number of jobs that can be created in the namespace.
   -  **Cron Job**: Maximum number of cron jobs that can be created in the namespace.
   -  **Pods**: maximum number of pods, including those in terminated state, that can be created in the namespace.
   -  **Pods** (excluding terminated pods): maximum number of pods in a non-terminated state that can be created in the namespace.
   -  **Services**: maximum number of Services, including those in terminated state, that can be created in the namespace.
   -  **Services** (excluding terminated Services): maximum number of Services in a non-terminated state that can be created in the namespace.
   -  **PersistentVolumeClaims (PVCs)**: maximum number of PVCs that can be created in the namespace.
   -  **ConfigMaps**: maximum number of ConfigMaps that can be created in the namespace.
   -  **Secrets**: maximum number of secrets that can be created in the namespace.

#. Click **OK**.
