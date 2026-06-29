:original_name: ucs_01_0006.html

.. _ucs_01_0006:

Registering an Attached Cluster (Private Network Access)
========================================================

Connecting attached clusters located in on-premises data centers or third-party clouds to UCS over public networks may cause security risks. To ensure stability and security, you can use private networks to connect the clusters to UCS for management.

The private network features high speed, low latency, and security. After you connect the on-premises network or the private network of a third-party cloud to the cloud network over Direct Connect or VPN, you can use a VPC endpoint to access UCS over the private network.

Constraints
-----------

-  The **T Cloud** **account** must have the **UCS FullAccess** and **VPCEndpoint Administrator** permissions.

-  If you are connecting a foreign cluster to UCS, ensure that this connection and the subsequent actions you will take comply with the local laws and regulations.

-  Ensure that your Kubernetes cluster has passed the CNCF Certified Kubernetes Conformance Program and the cluster version is 1.19 or later.

-  For attached clusters connected to UCS over private networks, the image repository may be restricted due to network restrictions.

   For clusters that are connected to UCS over a private network, images cannot be downloaded from SWR. Ensure that your nodes where your workloads run can access the public network.

Prerequisites
-------------

-  A cluster has been created and is running normally.
-  A VPC has been created in the region where UCS is available. For details, see `Creating a VPC <https://docs.otc.t-systems.com/virtual-private-cloud/umn/vpc_and_subnet/vpc/creating_a_vpc.html>`__.

   .. note::

      The subnet CIDR block of the VPC cannot overlap with the subnet CIDR block of the on-premises data center or third-party cloud. If the CIDR blocks overlap, the cluster cannot be connected to UCS. For example, if the subnet CIDR block of an on-premises data center is 192.168.1.0/24, the subnet CIDR block of the T Cloud VPC cannot be 192.168.1.0/24.

-  You have obtained the kubeconfig file of the cluster to be added. The procedure varies depending on the vendor. For details about the kubeconfig file, see `Organizing Cluster Access Using kubeconfig Files <https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/>`__.

.. _ucs_01_0006__section18529126141714:

Step 1: Prepare the Network Environment
---------------------------------------

.. important::

   After the on-premises network or the private network of the third-party cloud and the cloud network are connected, you are advised to ping the private IP address of a T Cloud server in the target VPC from an on-premises server or a server of the third-party cloud to check network connectivity.

Connect the on-premises data center or the third-party cloud to the T Cloud VPC.

-  VPN: See `Connecting to a VPC Through a VPN <https://docs.otc.t-systems.com/virtual-private-network/umn/getting_started/enterprise_edition_vpn/index.html>`__.

Step 2: Register a Cluster
--------------------------

#. Log in to the UCS console.

#. In the navigation pane, choose **Fleets**. In the **Attached clusters** card, click **Register Cluster**.

#. Configure the cluster parameters listed in :ref:`Table 1 <ucs_01_0006__ucs_01_0005_table147663516508>`. The parameters marked with an asterisk (*) are mandatory.

   .. _ucs_01_0006__ucs_01_0005_table147663516508:

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

.. _ucs_01_0006__section19895151719408:

Step 3: Buy a VPC Endpoint
--------------------------

#. Log in to the UCS console, click **Click to connect** in the card of the target cluster, and select **Private access**.

#. .. _ucs_01_0006__li1851615272529:

   In **Create a VPC endpoint**, click |image3| to record the service name.

#. Log in to the VPC Endpoint console and click **VPC Endpoint** to create a VPC endpoint for each service.

#. Select the region that the VPC endpoint belongs to.

#. Select **Find a service by name**, enter the service name recorded in :ref:`2 <ucs_01_0006__li1851615272529>`, and click **Verify**.

#. Select the VPC and subnet connected to the cluster network in :ref:`Step 1: Prepare the Network Environment <ucs_01_0006__section18529126141714>`.

#. Select **Automatically assign IP address** or **Manually specify IP address** for assigning the private IP address of the VPC endpoint.

#. Configure other parameters, click **Create Now**, and confirm the specifications.

   -  If the configuration is correct, click **Submit**.
   -  If any of the configurations is incorrect, click **Previous** to modify the parameters as needed, and click **Next** > **Submit**.

Step 4: Connect the Cluster to UCS
----------------------------------

#. Log in to the UCS console. In the card of the cluster in the **Pending connection** status, click **Private access**.

#. .. _ucs_01_0006__li8588162217405:

   Select the VPC endpoint created in :ref:`Step 3: Buy a VPC Endpoint <ucs_01_0006__section19895151719408>`.

#. Upload the agent configuration file in :ref:`2 <ucs_01_0006__li8588162217405>` to the node.

#. Click **Configure Cluster Access** and run commands in the cluster. You can click |image4| on the right to copy each command.

   .. important::

      -  For clusters that are connected to UCS over a private network, images cannot be downloaded from SWR. Ensure that your nodes where your workloads run can access the public network.
      -  To pull the proxy-agent container image, the cluster must be able to access the public network, or the image can be uploaded to an image repository that can be accessed by the cluster. Otherwise, the image will fail to be deployed.

#. Go to the UCS console and refresh the cluster status. The cluster is in the **Running** state.

.. |image1| image:: /_static/images/en-us_image_0000001293009114.png
.. |image2| image:: /_static/images/en-us_image_0000001345751013.png
.. |image3| image:: /_static/images/en-us_image_0000001853742645.png
.. |image4| image:: /_static/images/en-us_image_0000001645555145.png
