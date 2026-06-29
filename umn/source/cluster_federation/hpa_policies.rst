:original_name: ucs_01_0170.html

.. _ucs_01_0170:

HPA Policies
============

Horizontal Pod Autoscaling (HPA) is a Kubernetes function that implements horizontal auto scaling of pods. It dynamically adjusts the number of workload pods based on the usage of workload resources. HPA supports system metrics (CPU and memory, depending on the metrics API) or custom metrics (depending on the custom metrics API).

For details about HPA working principles, see `CCE User Guide <https://docs.otc.t-systems.com/cloud-container-engine/umn/auto_scaling/scaling_a_workload/index.html#cce-10-0293>`__.

Constraints
-----------

-  At least one pod is available in the cluster for which an auto scaling policy is to be created. If no pod is available, the system automatically performs pod scale-out.
-  A maximum of min(max(4, 2 x Number of current replicas), MaxReplicas) pods can be added to a cluster at a time.
-  To use HPA, add-ons such as metrics-server or prometheus that can provide metrics APIs must be installed in the cluster. If Prometheus is used, you need to register Prometheus as the service that provides the metrics API. For details, see `Providing Resource Metrics <https://docs.otc.t-systems.com/cloud-container-engine/umn/add-ons/cloud_native_observability_add-ons/index.html#cce-10-0908>`__.

Procedure
---------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. Click the name of the fleet with federation enabled.

#. Choose **HPA Policies** in the navigation pane, select the namespace to which the HPA policy belongs, and click **Create HPA Policy** in the upper right corner.

#. .. _ucs_01_0170__li5221385815:

   Configure the parameters.

   |image1|

   .. table:: **Table 1** HPA policy parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                               |
      +===================================+===========================================================================================================================================================================================================================+
      | Pod Range                         | Enter the minimum and maximum numbers of pods. When the policy is triggered, the pods will be scaled within this range.                                                                                                   |
      |                                   |                                                                                                                                                                                                                           |
      |                                   | -  **Min.**: Enter an integer from **1** to **299**.                                                                                                                                                                      |
      |                                   | -  **Max.**: Enter an integer from **1** to **1500**. The value must be greater than the minimum value.                                                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Stabilization Window              | The scaling operation is initiated only when the metric continuously reaches the desired value within stabilization window. By default, the stabilization window is 0 seconds for scale-out and 300 seconds for scale-in. |
      |                                   |                                                                                                                                                                                                                           |
      |                                   | -  **Scale-out**: Enter an integer from **0** to **3600**, in seconds.                                                                                                                                                    |
      |                                   | -  **Scale-in**: Enter an integer from **0** to **3600**, in seconds.                                                                                                                                                     |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | System rule                       | If you want to scale pods for a workload based on system metrics, you need to configure this rule.                                                                                                                        |
      |                                   |                                                                                                                                                                                                                           |
      |                                   | -  **Metric Name**: Select **CPU usage** or **Memory usage**.                                                                                                                                                             |
      |                                   | -  **Expected Value**: The scaling operation is triggered when the metric reaches the desired value.                                                                                                                      |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Custom rule                       | If you want to scale pods for a workload based on custom metrics, you need to configure this rule.                                                                                                                        |
      |                                   |                                                                                                                                                                                                                           |
      |                                   | -  **Metric Name**: Select a name from the drop-down list.                                                                                                                                                                |
      |                                   | -  **Source**: Select the object type described by the custom metric from the drop-down list. Currently, only **Pod** is supported.                                                                                       |
      |                                   | -  **Expected Value**: The scaling operation is triggered when the metric reaches the desired value.                                                                                                                      |
      |                                   |                                                                                                                                                                                                                           |
      |                                   | .. caution::                                                                                                                                                                                                              |
      |                                   |                                                                                                                                                                                                                           |
      |                                   |    CAUTION:                                                                                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                           |
      |                                   |    -  Custom rules can be created only for clusters 1.19 or later.                                                                                                                                                        |
      |                                   |    -  Before using a custom rule, install the add-on that supports custom metric collection for the cluster. Ensure that the add-on can collect and report the custom metrics of the workloads.                           |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. important::

      If the message **Metric server not installed** is displayed, install the metrics-server add-on in the target cluster. For details, see :ref:`Installing metrics-server <ucs_01_0170__section397645215489>`.

#. Click **OK**. After the policy is created, you can view it in the HPA policy list.

Related Operations
------------------

You can also perform operations described in :ref:`Table 2 <ucs_01_0170__table1619535674020>`.

.. _ucs_01_0170__table1619535674020:

.. table:: **Table 2** Related operations

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                         | Description                                                                                                                                                                                       |
   +===================================+===================================================================================================================================================================================================+
   | Viewing details                   | #. Select the namespace to which the HPA policy belongs.                                                                                                                                          |
   |                                   | #. (Optional) Search for an HPA policy by its name.                                                                                                                                               |
   |                                   | #. Click the name of an HPA policy to view its details, including basic information and policy information of each cluster.                                                                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Viewing the YAML file             | Click **View YAML** in the row where the target HPA policy resides to view the YAML file of the HPA policy.                                                                                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Viewing events                    | You can click **View Event** in the row where the target HPA policy resides to view the current Kubernetes events of the policy. Events are retained for one hour and then automatically deleted. |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Updating an HPA policy            | #. Choose **More** > **Update** in the row where the target HPA policy resides.                                                                                                                   |
   |                                   | #. Modify information based on :ref:`HPA policy parameters <ucs_01_0170__li5221385815>`.                                                                                                          |
   |                                   | #. Click **OK** to submit the modified information.                                                                                                                                               |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting an HPA policy            | Choose **More** > **Delete** in the row where the target HPA policy resides, and click **Yes**.                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting HPA policies in batches  | #. Select the HPA policies to be deleted.                                                                                                                                                         |
   |                                   | #. Click **Delete** in the upper left corner.                                                                                                                                                     |
   |                                   | #. Click **Yes**.                                                                                                                                                                                 |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ucs_01_0170__section397645215489:

Installing metrics-server
-------------------------

The metrics-server add-on is an aggregator for monitoring data of core cluster resources. It can be easily installed in your clusters.

#. Run the following command to install metrics-server:

   **kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml**

#. Run the following command to check whether metrics-server is successfully installed:

   **kubectl get deployment metrics-server -n kube-system**

   If information similar to the following is displayed, the installation is successful:

   .. code-block::

      NAME             READY   UP-TO-DATE   AVAILABLE   AGE
      metrics-server   1/1     1            1           6m

.. |image1| image:: /_static/images/en-us_image_0000002471229772.png
