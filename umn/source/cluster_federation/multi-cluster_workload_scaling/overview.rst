:original_name: ucs_01_0381.html

.. _ucs_01_0381:

Overview
========

Why Workload Scaling?
---------------------

The ever-changing application traffic brings changing resource requirements to container workloads. During workload deployment and management, if resources are reserved for a workload based on the service requirements at peak hours, a large number of resources will be wasted. If a resource threshold is set for a workload, applications may be abnormal when the resource usage exceeds the threshold. In Kubernetes, a `Horizontal Pod Autoscaler (HPA) <https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/>`__ can automatically scale in or out pods for workloads in a single cluster in response to metric changes. However, the HPA does not apply to multi-cluster scenarios.

UCS provides you with automatic workload scaling in multi-cluster scenarios. The automatic workload scaling is based on metric changes or at regular intervals, which raises scaling flexibility and stability.

Advantages
----------

UCS workload scaling has the following advantages:

-  Multi-cluster: You can configure the same scaling policy for multiple clusters in the federation.
-  High availability: Pods in your workload can be quickly scaled out at peak hours to ensure workload availability, or scaled in at off-peak hours to save resources.
-  Multi-function: Pods in your workload can be scaled in or out based on metric changes or at regular intervals in complex scenarios.

-  Multi-scenario: You can configure scaling policies for online services, large-scale computing and training, and training and inference on deep learning GPUs or shared GPUs.

Working Principles
------------------

UCS workload scaling is implemented by FederatedHPA and CronFederatedHPA, as shown in :ref:`Figure 1 <ucs_01_0381__fig517010412307>`.

-  FederatedHPA can automatically scale in or out pods for workloads in response to system metrics or custom metrics. When the metric reaches the desired value, workload scaling is triggered.
-  CronFederatedHPA can automatically scale in or out pods for workloads at regular intervals. When the triggering time arrives, workload scaling is triggered.

.. _ucs_01_0381__fig517010412307:

.. figure:: /_static/images/en-us_image_0000001810853161.png
   :alt: **Figure 1** Working principles of workload scaling

   **Figure 1** Working principles of workload scaling

Constraints
-----------

-  UCS scaling policies apply only to Deployments. For details about the comparisons among different types of workloads, see :ref:`Workloads <ucs_01_0254>`.
-  UCS scaling policies are used to scale in or out pods for workloads. To schedule the pods to specific clusters, you need to configure :ref:`scheduling policies <ucs_01_0265>`.
