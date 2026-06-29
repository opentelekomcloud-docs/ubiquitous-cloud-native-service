:original_name: ucs_01_0384.html

.. _ucs_01_0384:

Installing a Metric Collection Add-on
=====================================

Before creating a FederatedHPA, you need to install the add-on that supports metrics APIs for a cluster to collect workload metrics. If you have installed the add-on, skip this step.

Selecting an Add-on
-------------------

UCS provides two types of add-ons: Kubernetes Metrics Server and kube-prometheus-stack. The add-ons apply to different cluster and metric types. For details about how to select an add-on, see :ref:`Table 1 <ucs_01_0384__table7143458202220>`.

.. _ucs_01_0384__table7143458202220:

.. table:: **Table 1** Add-ons that provide metrics APIs

   +-------------------------+-----------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Applicable Cluster Type | Supported Metric Type | Add-on                                                      | Precautions                                                                                                                                                                                                                                   |
   +=========================+=======================+=============================================================+===============================================================================================================================================================================================================================================+
   | T Cloud clusters        | System metrics        | Install Kubernetes Metrics Server or kube-prometheus-stack. | After installing kube-prometheus-stack, you need to register it as a service that provides the metrics API.                                                                                                                                   |
   +-------------------------+-----------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                         | Custom metrics        | Install kube-prometheus-stack.                              | -  Before installing this add-on, check your cluster version. If the version is earlier than v1.19, upgrade the cluster version first.                                                                                                        |
   |                         |                       |                                                             | -  When installing this add-on, you must select the server mode. In this mode, you can customize metrics.                                                                                                                                     |
   |                         |                       |                                                             | -  After installing this add-on, aggregate custom metrics to the Kubernetes API server.                                                                                                                                                       |
   +-------------------------+-----------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Non-T Cloud clusters    | System metrics        | Install Kubernetes Metrics Server.                          | For details, see :ref:`Installing an Add-on <ucs_01_0384__section17533159174117>`.                                                                                                                                                            |
   +-------------------------+-----------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                         | Custom metrics        | No add-on available.                                        | To collect the custom metrics of a non-T Cloud cluster, you need to install `Prometheus Adapter <https://github.com/kubernetes-sigs/prometheus-adapter>`__, configure a custom metric collection rule, and then create a FederatedHPA policy. |
   +-------------------------+-----------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ucs_01_0384__section17533159174117:

Installing an Add-on
--------------------

After selecting an applicable add-on, install it for the cluster by referring to the precautions in :ref:`Table 1 <ucs_01_0384__table7143458202220>` and related documents.

.. caution::

   Install the metric collection add-on for all clusters in a federation for which a scaling policy needs to be created. Otherwise, metric collection will be abnormal and the scaling policy will become invalid.

-  For details about how to install Kubernetes Metrics Server, see `Kubernetes Metrics Server <https://docs.otc.t-systems.com/cloud-container-engine/umn/add-ons/cloud_native_observability_add-ons/kubernetes_metrics_server.html>`__.
-  For details about how to install kube-prometheus-stack, see `kube-prometheus-stack <https://docs.otc.t-systems.com/cloud-container-engine/umn/add-ons/cloud_native_observability_add-ons/cloud_native_cluster_monitoring.html>`__.
