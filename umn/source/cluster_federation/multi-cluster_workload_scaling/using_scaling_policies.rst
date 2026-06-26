:original_name: ucs_01_0382.html

.. _ucs_01_0382:

Using Scaling Policies
======================

This section describes how to use FederatedHPA and CronFederatedHPA.

Using FederatedHPA
------------------

:ref:`Figure 1 <ucs_01_0382__fig846419314614>` shows how to use FederatedHPA.

.. _ucs_01_0382__fig846419314614:

.. figure:: /_static/images/en-us_image_0000001770812128.png
   :alt: **Figure 1** Using FederatedHPA

   **Figure 1** Using FederatedHPA

#. Add clusters to a fleet, enable cluster federation for the fleet, and create Deployments. (Workload scaling is based on workloads deployed in multiple clusters.) For details, see :ref:`Registering a Cluster <ucs_01_0200>`, :ref:`Enabling Cluster Federation <ucs_01_0018>`, and :ref:`Creating a Workload <ucs_01_0255>`.
#. Install the metrics data collection add-on for clusters. For details, see :ref:`Installing a Metric Collection Add-on <ucs_01_0384>`.
#. Create a FederatedHPA. For details, see :ref:`Creating a FederatedHPA to Scale Pods Based on Metric Changes <ucs_01_0404>`.
#. Configure a scaling rate. For details, see :ref:`Configuring a FederatedHPA to Control the Scaling Rate <ucs_01_0395>`.
#. Modify or delete the FederatedHPA. For details, see :ref:`Managing a FederatedHPA <ucs_01_0385>`.

Using CronFederatedHPA
----------------------

**Using CronFederatedHPA Separately**

:ref:`Figure 2 <ucs_01_0382__fig18205194418194>` shows how to use CronFederatedHPA separately.

.. _ucs_01_0382__fig18205194418194:

.. figure:: /_static/images/en-us_image_0000001770629424.png
   :alt: **Figure 2** Process of using CronFederatedHPA separately

   **Figure 2** Process of using CronFederatedHPA separately

#. Add clusters to a fleet, enable cluster federation for the fleet, and create Deployments. (Workload scaling is based on workloads deployed in multiple clusters.) For details, see :ref:`Registering a Cluster <ucs_01_0200>`, :ref:`Enabling Cluster Federation <ucs_01_0018>`, and :ref:`Creating a Workload <ucs_01_0255>`.
#. Create a CronFederatedHPA. For details, see :ref:`Creating a CronFederatedHPA to Scale Pods at Regular Intervals <ucs_01_0387>`.
#. Modify or delete the CronFederatedHPA. For details, see :ref:`Managing a CronFederatedHPA <ucs_01_0388>`.

**Using CronFederatedHPA and FederatedHPA Together**

:ref:`Figure 3 <ucs_01_0382__fig457816211594>` shows how to use CronFederatedHPA and FederatedHPA together.

.. _ucs_01_0382__fig457816211594:

.. figure:: /_static/images/en-us_image_0000001770644580.png
   :alt: **Figure 3** Process of using CronFederatedHPA and FederatedHPA together

   **Figure 3** Process of using CronFederatedHPA and FederatedHPA together

#. Add clusters to a fleet, enable cluster federation for the fleet, and create Deployments. (Workload scaling is based on workloads deployed in multiple clusters.) For details, see :ref:`Registering a Cluster <ucs_01_0200>`, :ref:`Enabling Cluster Federation <ucs_01_0018>`, and :ref:`Creating a Workload <ucs_01_0255>`.
#. Install the metrics data collection add-on for clusters. For details, see :ref:`Installing a Metric Collection Add-on <ucs_01_0384>`.
#. Create a FederatedHPA. For details, see :ref:`Creating a FederatedHPA to Scale Pods Based on Metric Changes <ucs_01_0404>`.
#. Create a CronFederatedHPA. For details, see :ref:`Creating a CronFederatedHPA to Scale Pods at Regular Intervals <ucs_01_0387>`.
#. Modify or delete the two scaling policies. For details, see :ref:`Managing a FederatedHPA <ucs_01_0385>` and :ref:`Managing a CronFederatedHPA <ucs_01_0388>`.
