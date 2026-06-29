:original_name: ucs_01_0944.html

.. _ucs_01_0944:

Creating an HPA Policy with Custom Metrics
==========================================

Kubernetes' default HPA policy only allows for auto scaling based on CPU and memory usage. However, in more complex service scenarios, this may not be sufficient to meet routine O&M requirements. To resolve this issue, you can configure HPA policies with custom metrics, allowing for flexible workload scaling.


.. figure:: /_static/images/en-us_image_0000002527868302.png
   :alt: **Figure 1** Using an HPA policy with custom metrics

   **Figure 1** Using an HPA policy with custom metrics

This section uses an example to describe how to deploy an Nginx application, which uses the **container_cpu_usage_core_per_second** metric exposed by Prometheus to identify the number of CPU cores used by a container on a per-second basis. For more information about Prometheus metrics, see `METRIC TYPES <https://prometheus.io/docs/concepts/metric_types/>`__.

Step 1: Install Cloud Native Cluster Monitoring
-----------------------------------------------

#. Log in to the CCE console and click the cluster name to access the cluster console.

#. In the navigation pane, choose **Add-ons**. Locate **Cloud Native Cluster Monitoring** on the right and click **Install**.

   Prioritize the configurations listed below and adjust any other configurations as needed.

   -  **Data Storage Configuration**: Select **Local Data Storage** and enable **Report Monitoring Data to AOM**.
   -  Auto Service Discovery: If you `use annotations to monitor custom metrics <https://docs.otc.t-systems.com/cloud-container-engine/umn/o_and_m/o_and_m_best_practices/monitoring_custom_metrics_using_cloud_native_cluster_monitoring.html#cce-10-0373>`__, you also need to enable Auto Service Discovery for the add-on. Otherwise, metrics cannot be automatically discovered and collected.

#. Click **Install**.

Step 2: Register the Metrics API
--------------------------------

Register Prometheus as the service that provides the Metrics API.

.. note::

   -  If **Local Data Storage** is enabled for the Cloud Native Cluster Monitoring add-on, basic resource metrics can only be provided through the Metrics API.
   -  If the Kubernetes Metrics Server add-on has been installed in the cluster, uninstall it.

Resource metrics of containers and nodes, such as CPU and memory usage, can be obtained through the Kubernetes Metrics API. Resource metrics can be directly accessed, for example, by using the **kubectl top** command, or used by HPA or CustomedHPA policies for auto scaling.

The add-on can provide the Kubernetes Metrics API that is disabled by default. To enable the API, create the following APIService object:

.. code-block::

   apiVersion: apiregistration.k8s.io/v1
   kind: APIService
   metadata:
     labels:
       app: custom-metrics-apiserver
       release: cceaddon-prometheus
     name: v1beta1.metrics.k8s.io
   spec:
     group: metrics.k8s.io
     groupPriorityMinimum: 100
     insecureSkipTLSVerify: true
     service:
       name: custom-metrics-apiserver
       namespace: monitoring
       port: 443
     version: v1beta1
     versionPriority: 100

You can save the object as a file, name it **metrics-apiservice.yaml**, and run the following command:

.. code-block::

   kubectl create -f metrics-apiservice.yaml

Run the **kubectl top pod -n monitoring** command. If information similar to the following is displayed, the Metrics API can be accessed:

.. code-block::

   NAME                                                      CPU(cores)   MEMORY(bytes)
   ......
   custom-metrics-apiserver-d4f556ff9-l2j2m                  38m          44Mi
   ......

.. important::

   To uninstall the add-on, run the following kubectl command and delete the APIService object. Otherwise, residual APIService resources may prevent the installation of the Kubernetes Metrics Server add-on.

   .. code-block::

      kubectl delete APIService v1beta1.metrics.k8s.io

Step 3: Modify the Configuration File
-------------------------------------

#. In the navigation pane of the cluster console, choose **ConfigMaps and Secrets** and switch to the **monitoring** namespace.

#. Update **user-adapter-config**. You can modify the **rules** field in **user-adapter-config** to convert the metrics exposed by Prometheus to metrics that can be associated with HPA.

   Add the following example rule:

   .. code-block::

      rules:
          - seriesQuery: 'container_cpu_usage_seconds_total{namespace!="",pod!=""}'
            seriesFilters: []
            resources:
              overrides:
                namespace:
                  resource: namespace
                pod:
                  resource: pod
            name:
              matches: "^(.*)_seconds_total"
              as: "${1}_core_per_second"
            metricsQuery: 'sum(rate(<<.Series>>{<<.LabelMatchers>>}[1m])) by (<<.GroupBy>>)'

   In this example, the existing **container_cpu_usage_seconds_total** metrics are aggregated into the **container_cpu_usage_core_per_second** metric, which is then used for HPA policies. For details, see `Metrics Discovery and Presentation Configuration <https://github.com/kubernetes-sigs/prometheus-adapter/blob/master/docs/config.md>`__.

   -  **seriesQuery**: PromQL request data, which specifies the metrics to be obtained by users. You can configure this parameter as needed.
   -  **metricsQuery**: aggregates the PromQL query data in **seriesQuery**.
   -  **resources**: data labels in PromQL, which are used to match resources. The resources here refer to api-resource such as pods, namespaces, and nodes in a cluster. You can run **kubectl api-resources -o wide** to check the resources. The key corresponds to **LabelName** in the Prometheus data. Ensure that the Prometheus metric data contains **LabelName**.
   -  **name**: indicates that Prometheus metric names are converted to readable metric names based on regular expression matching. In this example, **container_cpu_usage_seconds_total** is converted to **container_cpu_usage_core_per_second**.

#. Redeploy the **custom-metrics-apiserver** workload in the **monitoring** namespace.

#. Wait for about 15 seconds and run the following command to check whether the metric has been added:

   .. code-block::

      kubectl get --raw  "/apis/custom.metrics.k8s.io/v1beta1/namespaces/default/pods/*/container_cpu_usage_core_per_second"

   |image1|

Step 4: Create a Workload
-------------------------

Create a workload on the federation console. For details, see :ref:`Deployments <ucs_01_0255>`.

Step 5: Create an HPA Policy
----------------------------

Create an HPA policy on the federation console and select the workload created in the previous step as the scaling target. For details, see :ref:`Creating a FederatedHPA to Scale Pods Based on Metric Changes <ucs_01_0404>`.

.. |image1| image:: /_static/images/en-us_image_0000002558988139.png
