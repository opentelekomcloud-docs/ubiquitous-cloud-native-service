:original_name: ucs_01_0107.html

.. _ucs_01_0107:

Jobs and Cron Jobs
==================

Overview
--------

In Kubernetes, there are two types of jobs: one-off jobs and cron jobs.

A job (one-off job) is a resource object that Kubernetes uses to control batch tasks. Jobs are different from long-term servo tasks (such as Deployments and StatefulSets). The former are started and terminated at specific times, while the latter run unceasingly unless being terminated. The pods managed by a job automatically exit after successfully completing the job based on user configurations. The success flag varies depending on the **spec.completions** policy. A single-pod job is considered successful if one pod completes successfully. A job with a fixed success count is considered successful if N pods complete successfully. A queue job is considered successful based on the global success confirmed by the application.

Similar to a crontab in Linux OS, a cron job can:

-  Run a scheduled job once at the specified time.
-  Run a scheduled job periodically at the specified time.

The typical usage of a cron job is as follows:

-  Schedules jobs at the specified time.
-  Creates jobs to run periodically, for example, database backup and email sending.

Creating a Job
--------------

A job runs pods that perform a completable task. The pods automatically exit after successfully completing the task. Before creating a workload, you can run a job to upload an image to the image repository.

#. (Optional) If you use a private container image to create your job, upload the container image to the image repository.

#. Access the cluster console. In the navigation pane, choose **Workloads**. On the displayed page, click the **Jobs** tab. In the upper right corner, click **Create from Image**.

#. Set basic workload parameters.

   **Basic Info**

   -  **Workload Type**: Select **Job**.
   -  **Workload Name**: Enter a workload name.
   -  **Namespace**: Select the namespace of the workload. The default value is **default**. You can also click **Create Namespace** to create one. For details, see :ref:`Creating a Namespace <ucs_01_0117__en-us_topic_0167389656_section31143617514>`.
   -  **Pods**: Enter the number of pods.

   **Container Settings**

   -  **Container Information**: Multiple containers can be configured in a pod. You can click **Add Container** on the right to configure multiple containers for the pod.

      -  **Basic Info**: See :ref:`Table 1 <ucs_01_0107__en-us_topic_0150272097_en-us_topic_0000001236922598_table6496632151617>`.

         .. _ucs_01_0107__en-us_topic_0150272097_en-us_topic_0000001236922598_table6496632151617:

         .. table:: **Table 1** Basic information parameters

            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Parameter                         | Description                                                                                                                                                                                                                                                                              |
            +===================================+==========================================================================================================================================================================================================================================================================================+
            | Container Name                    | Name the container.                                                                                                                                                                                                                                                                      |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Image Name                        | Click **Select Image** and select the image used by the container.                                                                                                                                                                                                                       |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | -  **My Images**: images in the image repository of the current region. If no image is available, click **Upload Image** to upload an image.                                                                                                                                             |
            |                                   | -  **Open Source Images**: official images in the open source image repository.                                                                                                                                                                                                          |
            |                                   | -  **Shared Images**: private images shared by another account.                                                                                                                                                                                                                          |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Image Tag                         | Select the image tag to be deployed.                                                                                                                                                                                                                                                     |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Pull Policy                       | Image update or pull policy. If you select **Always**, the image is pulled from the image repository each time. If you do not select **Always**, the existing image of the node is preferentially used. If the image does not exist in the node, it is pulled from the image repository. |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | CPU Quota                         | -  **Request**: minimum number of CPU cores required by a container. The default value is 0.25 cores.                                                                                                                                                                                    |
            |                                   | -  **Limit**: maximum number of CPU cores available for a container. Do not leave **Limit** unspecified. Otherwise, intensive use of container resources will occur and your workload may exhibit unexpected behavior.                                                                   |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Memory Quota                      | -  **Request**: minimum amount of memory required by a container. The default value is 512 MiB.                                                                                                                                                                                          |
            |                                   | -  **Limit**: maximum amount of memory available for a container. When memory usage exceeds the specified memory limit, the container will be terminated.                                                                                                                                |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | For details about **Request** and **Limit** of CPU or memory, see :ref:`Setting Container Specifications <ucs_01_0147>`.                                                                                                                                                                 |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Init Container                    | Select whether to use the container as an init container.                                                                                                                                                                                                                                |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | An init container is a special container that runs before app containers in a pod. For details, see `Init Containers <https://kubernetes.io/docs/concepts/workloads/pods/init-containers/>`__.                                                                                           |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Privileged Container              | Programs in a privileged container have certain privileges.                                                                                                                                                                                                                              |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | If **Privileged Container** is enabled, the container is assigned privileges. For example, privileged containers can manipulate network devices on the host machine and modify kernel parameters.                                                                                        |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

      -  **Lifecycle**: The lifecycle callback functions can be called in specific phases of the container. For example, if you want the container to perform a certain operation before stopping, set the corresponding function. Currently, lifecycle callback functions, such as startup, post-start, and pre-stop are provided. For details, see :ref:`Setting Container Lifecycle Parameters <ucs_01_0148>`.

      -  **Environment Variable**: Environment variables affect the way a running container will behave. Configuration items set by environment variables will not change if the pod lifecycle ends. For details, see :ref:`Setting Environment Variables <ucs_01_0150>`.

      -  **Data Storage**: Store container data using **Local Volumes** and **PersistentVolumeClaims (PVCs)**. You are advised to use PVCs to store workload pod data on a cloud volume. If you store pod data on a local volume and a fault occurs on the node, the data cannot be restored. For details about container storage, see :ref:`Container Storage <ucs_01_0112>`.

   -  **Image Access Credential**: Select the credential for accessing the image repository. This credential is used only for accessing a private image repository. If the selected image is a public image, you do not need to select a secret. For details on how to create a secret, see :ref:`Creating a Secret <ucs_01_0115>`.

   **Advanced Settings**

   -  **Labels and Annotations**: You can click **Confirm** to add a label or annotation for the pod. The key of the new label or annotation cannot be the same as that of an existing one.
   -  **Job Settings**

      -  **Parallel Pods**: Maximum number of pods that can run in parallel during job execution. The value cannot be greater than the total number of pods in the job.
      -  **Timeout (s)**: Once a job reaches this time, the job status becomes failed and all pods in this job will be deleted. If you leave this parameter blank, the job will never time out.

#. After the job is created, you can view the job in the job list.

   If the status of the job is **Processing**, the job has been created successfully.

Creating a Cron Job
-------------------

A cron job can run a scheduled job once or periodically at the specified time. The job automatically exits after successfully completing the task. For example, you can perform time synchronization for all active nodes at the specified time.

#. (Optional) If you use a private container image to create your cron job, upload the container image to the image repository.

#. Access the cluster console. In the navigation pane, choose **Workloads**. On the displayed page, click the **Cron Jobs** tab. In the upper right corner, click **Create Workload**.

#. Configure workload parameters.

   **Basic Info**

   -  **Workload Type**: Select **Cron Job**.
   -  **Workload Name**: Enter a workload name.
   -  **Namespace**: Select the namespace of the workload. The default value is **default**. You can also click **Create Namespace** to create one. For details, see :ref:`Creating a Namespace <ucs_01_0117__en-us_topic_0167389656_section31143617514>`.

   **Container Settings**

   -  **Container Information**: Multiple containers can be configured in a pod. You can click **Add Container** on the right to configure multiple containers for the pod.

      -  **Basic Info**: See :ref:`Table 2 <ucs_01_0107__table16352162517819>`.

         .. _ucs_01_0107__table16352162517819:

         .. table:: **Table 2** Basic information parameters

            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Parameter                         | Description                                                                                                                                                                                                                                                                              |
            +===================================+==========================================================================================================================================================================================================================================================================================+
            | Container Name                    | Name the container.                                                                                                                                                                                                                                                                      |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Image Name                        | Click **Select Image** and select the image used by the container.                                                                                                                                                                                                                       |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | -  **My Images**: images in the image repository of the current region. If no image is available, click **Upload Image** to upload an image.                                                                                                                                             |
            |                                   | -  **Open Source Images**: official images in the open source image repository.                                                                                                                                                                                                          |
            |                                   | -  **Shared Images**: private images shared by another account.                                                                                                                                                                                                                          |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Image Tag                         | Select the image tag to be deployed.                                                                                                                                                                                                                                                     |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Pull Policy                       | Image update or pull policy. If you select **Always**, the image is pulled from the image repository each time. If you do not select **Always**, the existing image of the node is preferentially used. If the image does not exist in the node, it is pulled from the image repository. |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | CPU Quota                         | -  **Request**: minimum number of CPU cores required by a container. The default value is 0.25 cores.                                                                                                                                                                                    |
            |                                   | -  **Limit**: maximum number of CPU cores available for a container. Do not leave **Limit** unspecified. Otherwise, intensive use of container resources will occur and your workload may exhibit unexpected behavior.                                                                   |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Memory Quota                      | -  **Request**: minimum amount of memory required by a container. The default value is 512 MiB.                                                                                                                                                                                          |
            |                                   | -  **Limit**: maximum amount of memory available for a container. When memory usage exceeds the specified memory limit, the container will be terminated.                                                                                                                                |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | For details about **Request** and **Limit** of CPU or memory, see :ref:`Setting Container Specifications <ucs_01_0147>`.                                                                                                                                                                 |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Init Container                    | Select whether to use the container as an init container.                                                                                                                                                                                                                                |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | An init container is a special container that runs before app containers in a pod. For details, see `Init Containers <https://kubernetes.io/docs/concepts/workloads/pods/init-containers/>`__.                                                                                           |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Privileged Container              | Programs in a privileged container have certain privileges.                                                                                                                                                                                                                              |
            |                                   |                                                                                                                                                                                                                                                                                          |
            |                                   | If **Privileged Container** is enabled, the container is assigned privileges. For example, privileged containers can manipulate network devices on the host machine and modify kernel parameters.                                                                                        |
            +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

      -  **Lifecycle**: The lifecycle callback functions can be called in specific phases of the container. For example, if you want the container to perform a certain operation before stopping, set the corresponding function. Currently, lifecycle callback functions, such as startup, post-start, and pre-stop are provided. For details, see :ref:`Setting Container Lifecycle Parameters <ucs_01_0148>`.

      -  **Environment Variable**: Environment variables affect the way a running container will behave. Configuration items set by environment variables will not change if the pod lifecycle ends. For details, see :ref:`Setting Environment Variables <ucs_01_0150>`.

   -  **Image Access Credential**: Select the credential for accessing the image repository. This credential is used only for accessing a private image repository. If the selected image is a public image, you do not need to select a secret. For details on how to create a secret, see :ref:`Creating a Secret <ucs_01_0115>`.

   **Execution Settings**

   -  **Concurrency Policy**: The following three modes are supported:

      -  **Forbid**: A new job cannot be created before the previous job is completed.
      -  **Allow**: The cron job allows concurrently running jobs, which preempt cluster resources.
      -  **Replace**: If it is time for a new job run and the previous job run has not finished yet, the cron job replaces the currently running job run with a new job run.

   -  **Policy Settings**: Time when a new cron job is executed. Scheduled rules in YAML are implemented using the cron expression.

      -  A cron job is executed at a fixed interval. The unit can be minute, hour, day, or month. For example, if a cron job is executed every 30 minutes and the corresponding cron expression is **\*/30 \* \* \* \***, the execution time starts from 0 in the unit range, for example, **00:00:00**, **00:30:00**, **01:00:00**, and **...**.
      -  The cron job is executed by month. For example, if a cron job is executed at 00:00 on the first day of each month, the corresponding cron expression is **0 0 1 \*/1 \***, and the execution time is **\****-01-01 00:00:00**, **\****-02-01 00:00:00**, and **...**.
      -  The cron job is executed by week. For example, if a cron job is executed at 00:00 every Monday, the corresponding cron expression is **0 0 \* \* 1**, and the execution time is **\****-**-01 00:00:00 on Monday**, **\****-**-08 00:00:00 on Monday**, and **...**.
      -  **Custom Cron Expression**: For details about how to use cron expressions, see `cron <https://en.wikipedia.org/wiki/Cron>`__.

      .. note::

         -  If a cron job is executed at a fixed time (by month) and the number of days in a month does not exist, the job will not be executed that month. For example, if a cron job is set to run on the 30th day of every month, but a month like February only has 28 or 29 days, the cron job will not run during that month and will instead resume on the 30th day of the following month.

         -  The cron expression defines a fixed period, but it is not always strict. The time unit range starts at 0 and is divided by the period. For example, if the unit is minute, the range is from 0 to 59. If the value cannot be evenly divided, the last period is reset. This means that an accurate period can only be represented when it can evenly divide its time unit range.

            Take a cron job that is executed by hour as an example. As **/2, /3, /4, /6, /8, and /12** can exactly divide 24 hours, an accurate period can be represented. If another period is used, the last period will be reset at the beginning of a new day. For example, if the cron expression is **\* \*/12 \* \* \***, the execution time is **00:00:00** and **12:00:00** every day. If the cron expression is **\* \*/13 \* \* \***, the execution time is **00:00:00** and **13:00:00** every day. At 00:00 on the next day, the execution time is updated even if the period does not reach 13 hours.

   -  **Job Records**: You can set the number of jobs that are successfully executed or fail. Setting a limit to **0** corresponds to keeping none of the jobs after they are completed.

   **Advanced Settings**

   -  **Labels and Annotations**: You can click **Confirm** to add a label or annotation for the pod. The key of the new label or annotation cannot be the same as that of an existing one.

#. After the cron job is created, you can view the cron job in the cron job list.

   If the status is **Started**, the cron job has been created successfully.

Related Operations
------------------

-  **View Events**: You can set search criteria, such as the time segment during which an event is generated or the event name, to view related events.
-  **Pods/Jobs**: View the information about the target pod/job.

   -  **View Events**: Event information generated by the pod, which is stored for one hour.
   -  **Pods**: View the pod name, status, and restart times.
   -  **View YAML**: View the YAML file of the pod.
   -  **Delete**: Delete the pod.

-  **View/Edit YAML**: View or edit the YAML file of the workload.
-  **Delete**: Delete the workload.
-  **Stop** (for cron jobs only): Stop a cron job.
