:original_name: ucs_01_0317.html

.. _ucs_01_0317:

Managing a Workload
===================

Scenarios
---------

After a workload is created, you can view its details, upgrade it, edit YAML, redeploy it, reschedule it, and delete it.

.. table:: **Table 1** Workload management

   +----------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                                                            | Description                                                                                                                                    |
   +======================================================================+================================================================================================================================================+
   | :ref:`Viewing Workload Details <ucs_01_0317__section15711117135419>` | You can view the basic information, events, and statuses of pods and workloads, and modify workload settings.                                  |
   +----------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Editing a YAML File <ucs_01_0317__section92886245520>`         | You can modify and download the YAML file of a workload online. YAML files of common jobs can only be viewed, copied, and downloaded.          |
   +----------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Upgrading a Workload <ucs_01_0317__section562511118522>`       | You can quickly upgrade a workload by replacing its image or image version without interrupting services.                                      |
   +----------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Redeploying a Workload <ucs_01_0317__section10163140185115>`   | You can redeploy a workload. After the workload is redeployed, all pods in the workload will be restarted. Only Deployments can be redeployed. |
   +----------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Deleting a Workload <ucs_01_0317__section1451814214514>`       | If a workload is no longer used, you can delete it. Deleted workloads or tasks cannot be restored.                                             |
   +----------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ucs_01_0317__section15711117135419:

Viewing Workload Details
------------------------

Click the name of a created workload to go to its details page. On this page, you can view the basic information, events, and statuses of pods and workloads, and modify workload settings.

.. _ucs_01_0317__section92886245520:

Editing a YAML File
-------------------

You can modify and download the YAML files of Deployments, StatefulSets, DaemonSets, CronJobs, and pods. YAML files of jobs can only be viewed, copied, and downloaded. This section uses a Deployment as an example to describe how to edit the YAML file.

#. Log in to the UCS console and access an existing fleet. In the navigation pane, choose **Workloads**.
#. Click the **Deployments** tab, locate your Deployment, and click **Edit YAML** in the **Operation** column. In the dialog box displayed, modify the YAML file.
#. Click **OK**.
#. (Optional) In the **Edit YAML** window, click **Download** to download the YAML file.

.. _ucs_01_0317__section562511118522:

Upgrading a Workload
--------------------

You can quickly upgrade a workload on the UCS console. This section uses a Deployment as an example to describe how to upgrade a workload.

#. Log in to the UCS console and access an existing fleet. In the navigation pane, choose **Workloads**.
#. Click the **Deployments** tab, locate your workload, and click **Upgrade** in the **Operation** column.
#. Upgrade the workload based on service requirements. The method for setting parameters is the same as that for creating a workload.
#. After the update is complete, click **Upgrade Workload**, manually confirm the YAML file, and submit the upgrade.

.. _ucs_01_0317__section10163140185115:

Redeploying a Workload (Available Only for Deployments)
-------------------------------------------------------

After you redeploy a workload, all pods in the workload will be restarted. This section uses a Deployment as an example to describe how to redeploy a workload.

#. Log in to the UCS console and access an existing fleet. In the navigation pane, choose **Workloads**.
#. Click the **Deployments** tab, locate your workload, and choose **More** > **Redeploy** in the **Operation** column.
#. In the displayed dialog box, click **Yes**.

.. _ucs_01_0317__section1451814214514:

Deleting a Workload
-------------------

You can delete a workload or job that is no longer needed. Deleted workloads or jobs cannot be recovered. This section uses a Deployment as an example to describe how to delete a workload.

#. Log in to the UCS console and access an existing fleet. In the navigation pane, choose **Workloads**.
#. Click the **Deployments** tab, locate your workload, and choose **More** > **Delete** in the **Operation** column.
#. In the displayed dialog box, click **Yes**.
