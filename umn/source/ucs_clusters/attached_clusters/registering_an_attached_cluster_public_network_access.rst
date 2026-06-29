:original_name: ucs_01_0005.html

.. _ucs_01_0005:

Registering an Attached Cluster (Public Network Access)
=======================================================

This section describes how to register an attached cluster and connect it to UCS over a public network.

Constraints
-----------

-  The **T Cloud** **account** must have the **UCS FullAccess** and **VPCEndpoint Administrator** permissions.

-  If you are connecting a foreign cluster to UCS, ensure that this connection and the subsequent actions you will take comply with the local laws and regulations.
-  Ensure that your Kubernetes cluster has passed the CNCF Certified Kubernetes Conformance Program and the cluster version is 1.19 or later.

Prerequisites
-------------

-  A cluster has been created and is running normally.
-  The node where the proxy-agent component is deployed must be accessible from the public network through an EIP or a NAT gateway.
-  You have obtained the kubeconfig file of the cluster to be added. The procedure varies depending on the vendor. For details about the kubeconfig file, see `Organizing Cluster Access Using kubeconfig Files <https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/>`__.

Step 1: Register a Cluster
--------------------------

#. Log in to the UCS console.

#. In the navigation pane, choose **Fleets**. In the **Attached clusters** card, click **Register Cluster**.

#. Configure the cluster parameters listed in :ref:`Table 1 <ucs_01_0005__table147663516508>`. The parameters marked with an asterisk (*) are mandatory.

   .. _ucs_01_0005__table147663516508:

   .. table:: **Table 1** Basic information for registering a cluster

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                          |
      +===================================+======================================================================================================================================================================================================================================================================+
      | \* Cluster Name                   | Enter a name, starting with a lowercase letter and not ending with a hyphen (-). Only lowercase letters, digits, and hyphens (-) are allowed.                                                                                                                        |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | \* Service Provider               | Select a cluster service provider.                                                                                                                                                                                                                                   |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | \* Region                         | Select a region where the cluster is deployed.                                                                                                                                                                                                                       |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Cluster Label                     | Optional. You can add labels in the form of key-value pairs to classify clusters. A key or value can contain a maximum of 63 characters starting and ending with a letter or digit. Only letters, digits, hyphens (-), underscores (_), and periods (.) are allowed. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | \* kubeconfig                     | Upload the kubectl configuration file to complete cluster authentication. The file can be in JSON or YAML format. The procedure for obtaining the kubeconfig file varies depending on the vendor.                                                                    |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | \* Context                        | Select the corresponding context. After the kubeconfig file is uploaded, the option list automatically obtains the **contexts** field from the file.                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                      |
      |                                   | The default value is the context specified by the **current-context** field in the kubeconfig file. If the file does not contain this field, you need to manually select a context from the list.                                                                    |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Fleet                             | Select the fleet that the cluster belongs to.                                                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                      |
      |                                   | A cluster can be added to only one fleet. Fleets are used for fine-grained access management. If you do not select a fleet, the cluster will be displayed on the **Clusters Not in Fleet** tab upon registration. You can add it to a fleet later.                   |
      |                                   |                                                                                                                                                                                                                                                                      |
      |                                   | You cannot select a fleet with federation enabled when registering a cluster. To add a cluster to a fleet with federation enabled, register the cluster with UCS first. For details about federation, see :ref:`Enabling Cluster Federation <ucs_01_0018>`.          |
      |                                   |                                                                                                                                                                                                                                                                      |
      |                                   | For details about how to create a fleet, see :ref:`Managing Fleets <ucs_01_0004>`.                                                                                                                                                                                   |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**. Connect the cluster to the network within 30 minutes. You can choose either the public or the private network access mode. For details about the network connection process, click |image1| in the upper right corner.

   If the cluster is not connected to UCS within 30 minutes, it will fail to be registered. In this case, click |image2| in the upper right corner to register it again. If the cluster has been connected to UCS but no data is displayed, wait for 2 minutes and refresh the cluster.

Step 2: Access the Network
--------------------------

After the cluster is registered with UCS, its status is **Pending connection**. In this case, the network connection between UCS and the cluster is not established. You need to configure a network agent in the cluster.

#. Log in to the UCS console.

#. .. _ucs_01_0005__li174014195511:

   Click **Public access** in the row of the target cluster to download the configuration file of the cluster agent.

   .. note::

      The configuration file contains private keys and can be downloaded only once. Keep the file secure.

#. Use kubectl to connect to the cluster, run the following command to create a YAML file named **agent.yaml** (which can be changed as needed) in the cluster, and copy the agent configuration in :ref:`2 <ucs_01_0005__li174014195511>` and paste it to the YAML file:

   **vim agent.yaml**

#. Run the following command in the cluster to deploy the agent:

   .. code-block::

      kubectl apply -f agent.yaml

#. Check the deployment of the cluster agent.

   .. code-block::

      kubectl -n kube-system get pod | grep proxy-agent

   If the deployment is successful, the expected output is:

   .. code-block::

      proxy-agent-5f7d568f6-6fc4k 1/1 Running 0 9s

#. Check the status of the cluster agent.

   .. code-block::

      kubectl -n kube-system logs <Agent Pod Name> | grep "Start serving"

   If the cluster agent is running normally, the expected log output is:

   .. code-block::

      Start serving

#. Go to the UCS console and refresh the cluster status. The cluster is in the **Running** state.

.. |image1| image:: /_static/images/en-us_image_0000001293009114.png
.. |image2| image:: /_static/images/en-us_image_0000001345751013.png
