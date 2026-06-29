:original_name: ucs_01_0387.html

.. _ucs_01_0387:

Creating a CronFederatedHPA to Scale Pods at Regular Intervals
==============================================================

This section describes how you can create a CronFederatedHPA so that pods in workloads are automatically scaled in or out at regular intervals.

Before creating a CronFederatedHPA, you can learn about the principles and concepts by referring to :ref:`How CronFederatedHPA Works <ucs_01_0386>`. To know the differences between the FederatedHPA and CronFederatedHPA, see :ref:`Overview <ucs_01_0381>`.

Constraints
-----------

CronFederatedHPA can be configured only for clusters 1.19 or later.

Creating a CronFederatedHPA
---------------------------

**Using the console**

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. Click the name of the fleet with federation enabled.

#. Choose **Workload Scaling** in the navigation pane and click the **Scheduled Policies** tab. Then click **Create Scheduled Policy** in the upper right corner.

#. Configure parameters for the CronFederatedHPA by referring to :ref:`Table 1 <ucs_01_0387__table3549115391717>`.

   .. _ucs_01_0387__table3549115391717:

   .. table:: **Table 1** Basic parameters

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                 |
      +===================================+=============================================================================================================================================================================================================================+
      | Policy Name                       | Enter a name for the CronFederatedHPA.                                                                                                                                                                                      |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Namespace                         | Select the namespace for the workload for which you want to configure automatic scaling.                                                                                                                                    |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Object                            | Select **Workloads** or **Metric-based Policy**.                                                                                                                                                                            |
      |                                   |                                                                                                                                                                                                                             |
      |                                   | -  **Workloads**: Select or create a workload you will associate the policy with. For details, see :ref:`Creating a Workload <ucs_01_0254>`.                                                                                |
      |                                   | -  **Metric-based Policy**: Select an existing metric-based policy or click **Create Metric-based Policy** on the right to create one. For details, see :ref:`Creating a FederatedHPA <ucs_01_0404__section1819514962510>`. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Add Rule** in **Policy Settings**. In the displayed dialog box, configure parameters by referring to :ref:`Table 2 <ucs_01_0387__en-us_topic_0000001633034616_table4191443175310>`.

   .. _ucs_01_0387__en-us_topic_0000001633034616_table4191443175310:

   .. table:: **Table 2** Parameters for adding a rule

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                          |
      +===================================+======================================================================================================================================================================+
      | Rule Name                         | Enter a name for the CronFederatedHPA.                                                                                                                               |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Expected Pod Range                | Enter the desired number of pods scaled when the CronFederatedHPA is triggered.                                                                                      |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Triggered                         | Select **Hourly**, **Daily**, **Weekly**, **Monthly**, **Yearly**, or **Cron**.                                                                                      |
      |                                   |                                                                                                                                                                      |
      |                                   | -  **Hourly**: a specific minute in an hour when the policy is executed. For example, if you select **5**, the policy is executed at the fifth minute of every hour. |
      |                                   |                                                                                                                                                                      |
      |                                   | -  **Daily**: a specific minute every day when the policy is executed.                                                                                               |
      |                                   |                                                                                                                                                                      |
      |                                   | -  **Weekly**: a specific minute on a day of each week when the policy is executed.                                                                                  |
      |                                   |                                                                                                                                                                      |
      |                                   | -  **Monthly**: a specific minute on a day of each month when the policy is executed.                                                                                |
      |                                   |                                                                                                                                                                      |
      |                                   | -  **Yearly**: a specific minute on a day of a month in each year when the policy is executed.                                                                       |
      |                                   |                                                                                                                                                                      |
      |                                   | -  **Cron**:                                                                                                                                                         |
      |                                   |                                                                                                                                                                      |
      |                                   |    Cron expression syntax:                                                                                                                                           |
      |                                   |                                                                                                                                                                      |
      |                                   | .. code-block::                                                                                                                                                      |
      |                                   |                                                                                                                                                                      |
      |                                   |     ┌───────────── Minute (0 to 59)                                                                                                                                  |
      |                                   |     │ ┌───────────  Hour (0 to 23)                                                                                                                                   |
      |                                   |     │ │ ┌────────── A day in a month (1 to 31)                                                                                                                       |
      |                                   |     │ │ │ ┌────────  Month (1 to 12)                                                                                                                                 |
      |                                   |     │ │ │ │ ┌─────── A day in a week (0 to 6)                                                                                                                        |
      |                                   |     │ │ │ │ │                                                                                                                                                        |
      |                                   |     │ │ │ │ │                                                                                                                                                        |
      |                                   |     *  *  *  *  *                                                                                                                                                    |
      |                                   |                                                                                                                                                                      |
      |                                   | For example, **0 0 13 \* 5** indicates that a task is started at 00:00 on every Friday and the 13th day of each month.                                               |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Time Zone                         | Select the time zone.                                                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK** and then click **Create**.

   In the displayed policy list, you can view the policy details.

**Using kubectl**

#. Use kubectl to connect to the federation. For details, see :ref:`Using kubectl to Connect to a Federation <ucs_01_0320>`.

#. Create and edit a **cfhpa.yaml** file.

   **vi cfhpa.yaml**

   For details about the parameters in this file, see :ref:`Table 3 <ucs_01_0387__table1673555792620>`. In this example, the CronFederatedHPA named **cron-federated-hpa** is used for the **test** workload and contains two rules (**Scale-Up** and **Scale-Down**) for scheduled scaling. **Scale-Up** specifies that 10 pods are scaled out at 8:30 daily, and **Scale-Down** specifies that 5 pods are scaled in at 21:00 daily.

   .. code-block::

      apiVersion: autoscaling.karmada.io/v1alpha1
      kind: CronFederatedHPA
      metadata:
        name: cron-federated-hpa           # CronFederatedHPA name
      spec:
        scaleTargetRef:
          apiVersion: apps/v1
          kind: Deployment                 # Select Deployment or FederatedHPA.
          name: test                       # Name of the workload or FederatedHPA
        rules:
        - name: "Scale-Up"                 # Rule name
          schedule: 30 08 * * *            # Time when the policy is triggered
          targetReplicas: 10               # Desired number of pods, which is a non-negative integer
          timeZone: ******                 # Time zone
        - name: "Scale-Down"               # Rule name
          schedule: 0 21 * * *             # Time when the policy is triggered
          targetReplicas: 5                # Desired number of pods, which is a non-negative integer
          timeZone: ******                 # Time zone

   .. _ucs_01_0387__table1673555792620:

   .. table:: **Table 3** Key parameters

      +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------+
      | Parameter       | Mandatory       | Type            | Description                                                                                                            |
      +=================+=================+=================+========================================================================================================================+
      | kind            | Yes             | String          | Select **Deployment** or **FederatedHPA**.                                                                             |
      |                 |                 |                 |                                                                                                                        |
      |                 |                 |                 | -  **Deployment**: The CronFederatedHPA is used separately.                                                            |
      |                 |                 |                 | -  **FederatedHPA**: Both FederatedHPA and CronFederatedHPA are used.                                                  |
      +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------+
      | name            | Yes             | String          | Enter the rule name of 1 to 32 characters in the CronFederatedHPA.                                                     |
      +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------+
      | schedule        | Yes             | String          | Time when the policy is triggered. Cron expression syntax:                                                             |
      |                 |                 |                 |                                                                                                                        |
      |                 |                 |                 | .. code-block::                                                                                                        |
      |                 |                 |                 |                                                                                                                        |
      |                 |                 |                 |     ┌───────────── Minute (0 to 59)                                                                                    |
      |                 |                 |                 |     │ ┌───────────  Hour (0 to 23)                                                                                     |
      |                 |                 |                 |     │ │ ┌────────── A day in a month (1 to 31)                                                                         |
      |                 |                 |                 |     │ │ │ ┌────────  Month (1 to 12)                                                                                   |
      |                 |                 |                 |     │ │ │ │ ┌─────── A day in a week (0 to 6)                                                                          |
      |                 |                 |                 |     │ │ │ │ │                                                                                                          |
      |                 |                 |                 |     │ │ │ │ │                                                                                                          |
      |                 |                 |                 |      *  *  *  *  *                                                                                                     |
      |                 |                 |                 |                                                                                                                        |
      |                 |                 |                 | For example, **0 0 13 \* 5** indicates that a task is started at 00:00 on every Friday and the 13th day of each month. |
      +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------+
      | targetReplicas  | Yes             | String          | Enter the desired number of pods scaled when the CronFederatedHPA is triggered.                                        |
      +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------+
      | timeZone        | Yes             | String          | Select the time zone.                                                                                                  |
      +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------+

#. Create a CronFederatedHPA.

   **kubectl apply -f cfhpa.yaml**

   If information similar to the following is displayed, the policy has been created:

   .. code-block::

      CronFederatedHPA.autoscaling.karmada.io/cron-federated-hpa created

   You can run the following commands to check the workload scaling:

   -  **kubectl get deployments**: checks the current number of pods in a workload.
   -  **kubectl describe cronfederatedhpa cron-federated-hpa**: views scaling events (latest three records) of the CronFederatedHPA.

   You can run the following commands to manage CronFederatedHPA **cron-federated-hpa** (replaced with the actual name):

   -  **kubectl get cronfederatedhpa cron-federated-hpa**: obtains the CronFederatedHPA.
   -  **kubectl edit cronfederatedhpa cron-federated-hpa**: updates the CronFederatedHPA.
   -  **kubectl delete cronfederatedhpa cron-federated-hpa**: deletes the CronFederatedHPA.
