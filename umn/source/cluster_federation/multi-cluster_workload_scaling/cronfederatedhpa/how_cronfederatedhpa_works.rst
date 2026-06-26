:original_name: ucs_01_0386.html

.. _ucs_01_0386:

How CronFederatedHPA Works
==========================

CronFederatedHPA is needed because FederatedHPA can only scale in or out pods for workloads based on metrics data. However, metric-based scaling brings in latency. CronFederatedHPA can automatically scale in or out pods for workloads at regular intervals.

You can configure a CronFederatedHPA for workloads whose resource usage changes periodically, so that pods can be added before predicated peak hours and reclaimed at off-peak hours.


How CronFederatedHPA Works
--------------------------

:ref:`Figure 1 <ucs_01_0386__fig6282757162219>` shows the working principle of CronFederatedHPA. When creating a CronFederatedHPA, you can specify a time to adjust the maximum and minimum numbers of pods in a FederatedHPA or directly specify the number of pods desired.

.. _ucs_01_0386__fig6282757162219:

.. figure:: /_static/images/en-us_image_0000001796643017.png
   :alt: **Figure 1** Working principle of CronFederatedHPA

   **Figure 1** Working principle of CronFederatedHPA

Using CronFederatedHPA Separately
---------------------------------

If CronFederatedHPA is separately used, it periodically adjusts the number of pods for workloads. After you set the effective time and desired number of pods in a CronFederatedHPA, pods will be periodically scaled after the CronFederatedHPA is in effect.


.. figure:: /_static/images/en-us_image_0000001749724282.png
   :alt: **Figure 2** Using CronFederatedHPA separately

   **Figure 2** Using CronFederatedHPA separately

The detailed procedure is as follows:

#. .. _ucs_01_0386__li417075217585:

   Create a CronFederatedHPA and set the effective time and desired number of pods.

   -  Effective time: the time when the CronFederatedHPA takes effect.
   -  Desired number of pods: the desired number of pods when the CronFederatedHPA takes effect.

#. When the CronFederatedHPA takes effect, the **number of existing pods** in the workload will be compared with the **desired number of pods** set in :ref:`1 <ucs_01_0386__li417075217585>`. If the desired number is greater, pods are scaled out for the workload. If the desired number is smaller, pods are scaled in.

   Number of existing pods: the number of pods in the workload before the CronFederatedHPA takes effect.

Using Both CronFederatedHPA and FederatedHPA
--------------------------------------------

If both FederatedHPA and CronFederatedHPA are used, CronFederatedHPA runs based on FederatedHPA and periodically adjusts the maximum and minimum numbers of pods in the FederatedHPA for scheduled scaling.


.. figure:: /_static/images/en-us_image_0000001796723973.png
   :alt: **Figure 3** Using both FederatedHPA and CronFederatedHPA

   **Figure 3** Using both FederatedHPA and CronFederatedHPA

The detailed procedure is as follows:

#. .. _ucs_01_0386__li95414719312:

   Create a CronFederatedHPA and set the effective time and desired number of pods.

   -  Effective time: the time when the CronFederatedHPA takes effect.
   -  Desired number of pods: the number of pods set in the CronFederatedHPA. When CronFederatedHPA takes effect, this number will be used as a reference for adjusting the maximum and minimum numbers of pods in the FederatedHPA. The maximum and minimum numbers can be used as starting points for adjusting the number of pods for a workload.

#. When the CronFederatedHPA takes effect, the **number of existing pods** of the workload, **maximum number of pods** and **minimum number of pods** in the FederatedHPA, and **desired number of pods** set in :ref:`1 <ucs_01_0386__li95414719312>` will be compared to determine how much the maximum and minimum numbers of pods in the FederatedHPA will be adjusted. Then, the FederatedHPA scales in or out pods for the workload based on the adjusted maximum and minimum numbers of pods.

   -  Number of existing pods: the number of pods in the workload before the CronFederatedHPA takes effect.
   -  Maximum number of pods in the FederatedHPA: the maximum number of pods for a workload.
   -  Minimum number of pods in the FederatedHPA: the minimum number of pods for a workload.

:ref:`Figure 4 <ucs_01_0386__fig589603120167>` and :ref:`Table 1 <ucs_01_0386__table95895442176>` show the possible scaling scenarios when both FederatedHPA and CronFederatedHPA are used. You can learn about how CronFederatedHPA takes effect on the FederatedHPA and workload based on the number of existing pods, maximum number of pods, minimum number of pods, and desired number of pods.

.. _ucs_01_0386__fig589603120167:

.. figure:: /_static/images/en-us_image_0000001749883158.png
   :alt: **Figure 4** Scaling scenarios when both policies are used

   **Figure 4** Scaling scenarios when both policies are used

.. _ucs_01_0386__table95895442176:

.. table:: **Table 1** Scaling scenarios when both policies are used

   +--------------+----------------------------------------------------------------------------------------------------------+-------------------------+-------------------------+--------------------------------+----------------------------------------------------------------------------------------+
   | Scenario No. | Description                                                                                              | Desired Number of Pods  | Number of Existing Pods | Minimum/Maximum Number of Pods | Result                                                                                 |
   |              |                                                                                                          |                         |                         |                                |                                                                                        |
   |              |                                                                                                          | (in a CronFederatedHPA) | (in a Workload)         | (in a FederatedHPA)            |                                                                                        |
   +==============+==========================================================================================================+=========================+=========================+================================+========================================================================================+
   | 1            | **Desired number of pods** < Minimum number of pods <= Number of existing pods <= Maximum number of pods | 3                       | 5                       | 4/10                           | -  The minimum number of pods in the FederatedHPA is changed to 3.                     |
   |              |                                                                                                          |                         |                         |                                | -  The number of existing pods of the workload is not changed.                         |
   +--------------+----------------------------------------------------------------------------------------------------------+-------------------------+-------------------------+--------------------------------+----------------------------------------------------------------------------------------+
   | 2            | **Desired number of pods** = Minimum number of pods <= Number of existing pods <= Maximum number of pods | 4                       | 5                       | 4/10                           | -  The minimum number of pods in the FederatedHPA is not changed.                      |
   |              |                                                                                                          |                         |                         |                                | -  The number of existing pods of the workload is not changed.                         |
   +--------------+----------------------------------------------------------------------------------------------------------+-------------------------+-------------------------+--------------------------------+----------------------------------------------------------------------------------------+
   | 3            | Minimum number of pods < **Desired number of pods** < Number of existing pods <= Maximum number of pods  | 5                       | 6                       | 4/10                           | -  The minimum number of pods in the FederatedHPA is changed to 5.                     |
   |              |                                                                                                          |                         |                         |                                | -  The number of existing pods of the workload is not changed.                         |
   +--------------+----------------------------------------------------------------------------------------------------------+-------------------------+-------------------------+--------------------------------+----------------------------------------------------------------------------------------+
   | 4            | Minimum number of pods < **Desired number of pods** = Number of existing pods <= Maximum number of pods  | 5                       | 5                       | 4/10                           | -  The minimum number of pods in the FederatedHPA is changed to 5.                     |
   |              |                                                                                                          |                         |                         |                                | -  The number of existing pods of the workload is not changed.                         |
   +--------------+----------------------------------------------------------------------------------------------------------+-------------------------+-------------------------+--------------------------------+----------------------------------------------------------------------------------------+
   | 5            | Minimum number of pods <= Number of existing pods < **Desired number of pods** < Maximum number of pods  | 6                       | 5                       | 4/10                           | -  The minimum number of pods in the FederatedHPA is changed to 6.                     |
   |              |                                                                                                          |                         |                         |                                | -  The number of existing pods of the workload is changed to 6.                        |
   +--------------+----------------------------------------------------------------------------------------------------------+-------------------------+-------------------------+--------------------------------+----------------------------------------------------------------------------------------+
   | 6            | Minimum number of pods <= Number of existing pods < **Desired number of pods** = Maximum number of pods  | 10                      | 4                       | 4/10                           | -  The minimum number of pods in the FederatedHPA is changed to 10.                    |
   |              |                                                                                                          |                         |                         |                                | -  The number of existing pods of the workload is changed to 10.                       |
   +--------------+----------------------------------------------------------------------------------------------------------+-------------------------+-------------------------+--------------------------------+----------------------------------------------------------------------------------------+
   | 7            | Minimum number of pods <= Number of existing pods <= Maximum number of pods < **Desired number of pods** | 11                      | 4                       | 4/10                           | -  The minimum and maximum numbers of pods in the FederatedHPA are both changed to 11. |
   |              |                                                                                                          |                         |                         |                                | -  The number of existing pods of the workload is changed to 11.                       |
   +--------------+----------------------------------------------------------------------------------------------------------+-------------------------+-------------------------+--------------------------------+----------------------------------------------------------------------------------------+
