:original_name: ucs_01_0404.html

.. _ucs_01_0404:

Creating a FederatedHPA to Scale Pods Based on Metric Changes
=============================================================

This section describes how you can create a FederatedHPA so that pods in workloads are automatically scaled in or out based on different metrics.

Before creating a FederatedHPA, you can learn about the principles and concepts by referring to :ref:`How FederatedHPA Works <ucs_01_0383>`. To know the differences between the FederatedHPA and CronFederatedHPA, see :ref:`Overview <ucs_01_0381>`.

Constraints
-----------

FederatedHPA can be configured only for clusters 1.19 or later. To query the cluster version, log in to the UCS console, click the name of the fleet that the cluster is added to, and click **Container Clusters**.

.. _ucs_01_0404__section1819514962510:

Creating a FederatedHPA
-----------------------

**Using the console**

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. Click the name of the fleet with federation enabled.

#. Choose **Workload Scaling** in the navigation pane and click the **Metric-based Policy** tab. Then click **Create Metric-based Policy** in the upper right corner.

#. Configure parameters for the FederatedHPA.

   .. table:: **Table 1** FederatedHPA parameters

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                        |
      +===================================+====================================================================================================================================================================================================================================================================================================================================================================+
      | Policy Name                       | Enter a name containing 4 to 63 characters for the FederatedHPA.                                                                                                                                                                                                                                                                                                   |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Namespace                         | Select the namespace for the workload for which you want to set automatic scaling. You can also create a namespace. For details, see :ref:`Namespaces <ucs_01_0281>`.                                                                                                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Applicable Workload               | Select the name of the workload for which you want to set automatic scaling. You can also create a workload. For details, see :ref:`Workloads <ucs_01_0254>`.                                                                                                                                                                                                      |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Pod Range                         | Enter the minimum and maximum numbers of pods. When the FederatedHPA is triggered, the pods will be scaled within this range.                                                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | -  **Min.**: Enter an integer from **1** to **299**.                                                                                                                                                                                                                                                                                                               |
      |                                   | -  **Max.**: Enter an integer from **1** to **1500**. The value must be greater than the minimum value.                                                                                                                                                                                                                                                            |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Stabilization Window              | The scaling operation is initiated only when the metric continuously reaches the desired value within stabilization window. By default, the stabilization window is 0 seconds for scale-out and 300 seconds for scale-in. For details about stabilization window, see :ref:`How Do I Ensure the Stability of Workload Scaling? <ucs_01_0383__section85588562323>`. |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | -  **Scale-out**: Enter an integer from **0** to **3600**, in seconds.                                                                                                                                                                                                                                                                                             |
      |                                   | -  **Scale-in**: Enter an integer from **0** to **3600**, in seconds.                                                                                                                                                                                                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | System rule                       | If you want to scale pods for a workload based on system metrics, you need to configure this rule.                                                                                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | -  **Metric Name**: Select **CPU utilization** or **Memory utilization**.                                                                                                                                                                                                                                                                                          |
      |                                   | -  **Expected Value**: The scaling operation is triggered when the metric reaches the desired value.                                                                                                                                                                                                                                                               |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Custom rule                       | If you want to scale pods for a workload based on custom metrics, you need to configure this rule.                                                                                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | -  **Metric Name**: Select a name from the drop-down list.                                                                                                                                                                                                                                                                                                         |
      |                                   | -  **Source**: Select the object type described by the custom metric from the drop-down list. Currently, only **Pod** is supported.                                                                                                                                                                                                                                |
      |                                   | -  **Expected Value**: The scaling operation is triggered when the metric reaches the desired value.                                                                                                                                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | .. caution::                                                                                                                                                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   |    CAUTION:                                                                                                                                                                                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   |    -  Custom rules can be created only for clusters 1.19 or later.                                                                                                                                                                                                                                                                                                 |
      |                                   |    -  Before using a custom rule, install the add-on that supports custom metric collection for the cluster. Ensure that the add-on can collect and report the custom metrics of the workloads. For details, see :ref:`Installing a Metric Collection Add-on <ucs_01_0384>`.                                                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Create** in the lower right corner.

   In the displayed policy list, you can view the policy details.

**Using kubectl**

#. Use kubectl to connect to the federation. For details, see :ref:`Using kubectl to Connect to a Federation <ucs_01_0320>`.

#. Create and edit the **fhpa.yaml** file. For details about the key parameters, see :ref:`Table 2 <ucs_01_0404__table1673555792620>`.

   **vi fhpa.yaml**

   In this example, the FederatedHPA is named **hpa-example-hpa** and associated with the workload named **hpa-example**. The stabilization window is 0 seconds for scale-out and 300 seconds for scale-in. The maximum number of pods is 100 and the minimum number of pods is 2. There are two system metric rules: **memory** and **cpu**. The desired memory usage in **memory** is 50%, and the desired CPU usage in **cpu** is 60%.

   .. code-block::

      apiVersion: autoscaling.karmada.io/v1alpha1
      kind: FederatedHPA
      metadata:
        name: hpa-example-hpa                               # FederatedHPA name
        namespace: default                                  # Namespace where the workload resides
      spec:
        scaleTargetRef:
          apiVersion: apps/v1
          kind: Deployment
          name: hpa-example                                 # Workload name
        behavior:
          scaleDown:
            stabilizationWindowSeconds: 300                 # The stabilization window is 300 seconds for scale-in.
          scaleUp:
            stabilizationWindowSeconds: 0                   # The stabilization window is 0 seconds for scale-out.
        minReplicas: 2                                      # The minimum number of pods is 2.
        maxReplicas: 100                                    # The maximum number of pods is 100.
        metrics:
          - type: Resource
             resource:
              name: memory                                  # Name of the first rule
              target:
                 type: Utilization                          # The metric type is resource usage.
                 averageUtilization: 50                     # Desired average resource usage
          - type: Resource
             resource:
              name: cpu                                     # Name of the second rule
              target:
                 type: Utilization                          # The metric type is resource usage.
                 averageUtilization: 60                     # Desired average resource usage

   .. _ucs_01_0404__table1673555792620:

   .. table:: **Table 2** Key parameters

      +----------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                  | Mandatory       | Type            | Description                                                                                                                                                                                                                                                             |
      +============================+=================+=================+=========================================================================================================================================================================================================================================================================+
      | stabilizationWindowSeconds | No              | String          | Stabilization window for scale-in. Enter an integer from **0** to **3600**, in seconds. If this parameter is not specified, the default value is **300**.                                                                                                               |
      |                            |                 |                 |                                                                                                                                                                                                                                                                         |
      |                            |                 |                 | .. note::                                                                                                                                                                                                                                                               |
      |                            |                 |                 |                                                                                                                                                                                                                                                                         |
      |                            |                 |                 |    The scaling operation is initiated only when the metric continuously reaches the desired value within stabilization window. For details about stabilization window, see :ref:`How Do I Ensure the Stability of Workload Scaling? <ucs_01_0383__section85588562323>`. |
      +----------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | stabilizationWindowSeconds | No              | String          | Stabilization window for scale-out. Enter an integer from **0** to **3600**, in seconds. If this parameter is not specified, the default value is **0**.                                                                                                                |
      +----------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | minReplicas                | Yes             | String          | Minimum number of pods that can be scaled in for a workload when the scaling policy is triggered. Enter an integer from **1** to **299**.                                                                                                                               |
      +----------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | maxReplicas                | Yes             | String          | Maximum number of pods that can be scaled out for a workload when the scaling policy is triggered. Enter an integer from **1** to **1500** and ensure that the value is greater than the minimum value.                                                                 |
      +----------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | name                       | Yes             | String          | Rule name. For scaling operations based on system metrics, **memory** is used as the rule name of the memory usage, and **cpu** is used as the rule name of the CPU usage.                                                                                              |
      +----------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | type                       | Yes             | String          | Metric type.                                                                                                                                                                                                                                                            |
      |                            |                 |                 |                                                                                                                                                                                                                                                                         |
      |                            |                 |                 | -  **Value**: total number of pods                                                                                                                                                                                                                                      |
      |                            |                 |                 | -  **AverageValue**: Total number of pods/Number of current pods                                                                                                                                                                                                        |
      |                            |                 |                 | -  **Utilization**: vCPUs or memory used by pods in a workload/Requested vCPUs or memory                                                                                                                                                                                |
      +----------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | averageUtilization         | Yes             | String          | The scaling operation is triggered when the metric reaches the desired value.                                                                                                                                                                                           |
      +----------------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Create a FederatedHPA.

   **kubectl apply -f fhpa.yaml**

   If information similar to the following is displayed, the policy has been created:

   .. code-block::

      FederatedHPA.autoscaling.karmada.io/hpa-example-hpa created

   You can run the following commands to check the workload scaling:

   -  **kubectl get deployments**: checks the current number of pods in a workload.
   -  **kubectl describe federatedhpa hpa-example-hpa**: views scaling events (latest three records) of the FederatedHPA.

   You can run the following commands to manage FederatedHPA **hpa-example-hpa** (replaced with the actual name):

   -  **kubectl get federatedhpa hpa-example-hpa**: obtains the FederatedHPA.
   -  **kubectl edit federatedhpa hpa-example-hpa**: updates the FederatedHPA.
   -  **kubectl delete federatedhpa hpa-example-hpa**: deletes the FederatedHPA.
