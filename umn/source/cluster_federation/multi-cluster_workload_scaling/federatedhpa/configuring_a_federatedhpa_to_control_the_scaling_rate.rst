:original_name: ucs_01_0395.html

.. _ucs_01_0395:

Configuring a FederatedHPA to Control the Scaling Rate
======================================================

Why Do I Need to Control the Scaling Rate?
------------------------------------------

To limit the rate at which pods are scaled by the HPA controller, scale-out needs to be fast, and scale-in needs to be slow. However, if only the stabilization window is configured, the scaling rate cannot be limited after the stabilization window expires. To accurately and flexibly limit the scaling rate, you can configure the behavior section of the spec in the YAML file. In the behavior section, the scaling rate can be unique for each FederatedHPA, and different rates can be configured for scale-out and scale-in operations.

Procedure
---------

The following describes behavior structures in common service scenarios. In other service scenarios, for example, if you want to perform slow scale-out or fast scale-in, you can set **scaleUp** and **scaleDown** under the **behavior** field by referring to the following description of each behavior structure.

-  Scenario 1: Fast scale-out

   If you want to perform a fast scale-out at peak hours, you can set **Percent** to a large value.

   .. code-block::

      behavior:
        scaleUp:
          policies:
          - type: Percent
            value: 900
            periodSeconds: 60

   In this example, the value of **Percent** is **900**. This means the scaling rate increases tenfold (1 + 900%) in each scaling period. For example, if the number of pods in a workload starts from 1, the number of pods added every 60 seconds changes as follows: 1 > 10 > 100 > ... . Note that the number of pods after scale-out cannot exceed the maximum number of pods configured in the FederatedHPA.

   Resource consumption of the Percent type fluctuates greatly. If you want the resource consumption to be controllable, use the Pods type with the absolute value.

   .. code-block::

      behavior:
        scaleDown:
          policies:
          - type: Pods
            value: 10
            periodSeconds: 60

   In this example, the value of **Pods** is **10**. This means 10 pods are added in each scaling period. For example, if the number of pods in a workload starts from 1, the number of pods added every 60 seconds changes as follows: 1 > 11 > 21 > ... . Note that the number of pods after scale-out cannot exceed the maximum number of pods configured in the FederatedHPA.

-  Scenario 2: Slow scale-in

   If you want to scale in pods in a workload more slowly after peak hours to improve application reliability, you can set **Pods** to a small value and **periodSeconds** to a large value.

   .. code-block::

      behavior:
        scaleDown:
          policies:
          - type: Pods
            value: 1
            periodSeconds: 600

   In this example, the value of **Pods** is **1**, and the value of **periodSeconds** is **600**. This means the scale-in period is 600 seconds, and one pod is reduced for each scale-in. If the initial number of pods is 100, the number of pods to be scaled in every 600 seconds changes as follows: 100 > 99 > 98 > … . In extreme cases, if you do not want the pods in a workload to be automatically scaled in, you can set **Percent** or **Pods** to **0**.

-  Scenario 3: Default scaling rate

   If **behavior** is not configured, the default settings of the FederatedHPA are as follows:

   .. code-block::

      behavior:
        scaleDown:
          stabilizationWindowSeconds: 300
          policies:
          - type: Percent
            value: 100
            periodSeconds: 15
        scaleUp:
          stabilizationWindowSeconds: 0
          policies:
          - type: Percent
            value: 100
            periodSeconds: 15
          - type: Pods
            value: 4
            periodSeconds: 15

   In the default configuration, the scaling period is 15 seconds. In each scaling period, scale-out or scale-in is performed at a rate of twice (1 + 100%). 4 pods to be scaled each time.
