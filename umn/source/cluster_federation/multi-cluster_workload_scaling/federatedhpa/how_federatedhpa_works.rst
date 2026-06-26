:original_name: ucs_01_0383.html

.. _ucs_01_0383:

How FederatedHPA Works
======================

FederatedHPA can automatically scale in or out pods for workloads in response to system metrics (CPU usage and memory usage) or custom metrics.

FederatedHPAs and :ref:`scheduling policies <ucs_01_0265>` can be used together to implement various functions. For example, after a FederatedHPA scales out pods in your workload, you can configure a scheduling policy to schedule the pods to clusters with more resources. This solves the resource limitation of a single cluster and improves the fault recovery capability.


How FederatedHPA Works
----------------------

:ref:`Figure 1 <ucs_01_0383__fig6282757162219>` shows the working principle of FederatedHPA. The details are as follows:

#. The HPA controller periodically requests metrics data of a workload from either the system metrics API or the custom metrics API.
#. After receiving the metric query request, karmada-apiserver routes the request to karmada-metrics-adapter that was registered through its API.
#. After receiving the request, karmada-metrics-adapter collects the metrics data of the workload.
#. karmada-metrics-adapter returns :ref:`calculated metrics data <ucs_01_0383__section1182118361051>` to the HPA controller.
#. The HPA controller :ref:`calculates the desired number of pods <ucs_01_0383__section10814102132619>` based on the returned metrics data and maintains the :ref:`stability of workload scaling <ucs_01_0383__section85588562323>`.

.. _ucs_01_0383__fig6282757162219:

.. figure:: /_static/images/en-us_image_0000001770983106.png
   :alt: **Figure 1** Working principle of FederatedHPA

   **Figure 1** Working principle of FederatedHPA

.. _ucs_01_0383__section1182118361051:

How Do I Calculate Metrics Data?
--------------------------------

There are system metrics and custom metrics. Their calculation methods are as follows:

-  System metrics

   There are two types of system metrics: CPU usage and memory usage. The system metrics can be queried and monitored through metrics API. For example, if you want to control the CPU usage of a workload at a reasonable level, you can create a FederatedHPA for the workload based on the CPU usage metric.

   .. note::

      Usage = CPUs or memory used by pods in a workload/Requested CPUs or memory

-  Custom metrics

   You can create a FederatedHPA for a workload based on custom metrics such as requests per second and writes per second. The HPA controller then queries for these custom metrics from a series of APIs.

If you set multiple desired metric values when creating a FederatedHPA, the HPA controller evaluates each metric separately and uses the scaling algorithm to determine the new workload scale based on each one. The largest scale is selected for the autoscale operation.

.. _ucs_01_0383__section10814102132619:

How Do I Calculate the Desired Number of Pods?
----------------------------------------------

The HPA controller operates on the scaling ratio between the desired metric value and current metric value and then uses that ratio to calculate the desired number of pods based on the current number of pods.

-  Current number of pods = Number of pods in the **Ready** state in all clusters

When calculating the desired number of pods, the HPA controller chooses the largest recommendation based on the last five minutes to prevent subsequent autoscaling operations before the workload finishes responding to prior autoscaling operations.

-  Desired number of pods = Current number of pods x (Current metric value/Desired metric value)

For example, if the current CPU usage is 100% and the desired CPU usage is 50%, the desired number of pods is twice the current number of pods.

.. _ucs_01_0383__section85588562323:

How Do I Ensure the Stability of Workload Scaling?
--------------------------------------------------

To ensure the stability of workload scaling, the HPA controller is designed to provide the following functions:

-  Stabilization window

   When detecting that the metric data reaches the desired value (the scaling standard is met), the HPA controller continuously checks the metric data within stabilization window. If the result shows that the metric data continuously reaches the desired value, the HPA controller performs scaling. By default, the stabilization window is 0 seconds for a scale-out and 300 seconds for a scale-in. The values can be changed. In actual configuration, to avoid service jitter, a scale-out needs to be fast, and a scale-in needs to be slow.

-  Tolerance

   Tolerance = abs (Current metric value/Desired metric value - 1)

   abs indicates an absolute value. If the metric value change is within the specified tolerance range, the scaling operation will not be triggered. The default value is 0.1 and cannot be changed.

For example, if you select the default settings when creating a FederatedHPA, a scale-in will be triggered when the metric value is more than 1.1 times the desired value and lasts for more than 300 seconds, and a scale-out will be triggered when the metric value is less than 0.9 times the desired value and lasts for more than 0 seconds.
