:original_name: ucs_01_0378.html

.. _ucs_01_0378:

Creating an MCS Object
======================

Constraints
-----------

-  MCS is only available in clusters v1.21 or later.
-  A Service, with both MCI and MCS configured, can only be delivered to the cluster where the Service is deployed, the cluster that accesses the Service, and the cluster where the corresponding workload is deployed in MCS.

.. _ucs_01_0378__section3746123012276:

Preparations
------------

-  Deploying Workloads and Services

   Deploy available workloads (Deployments) and Services on the federation control plane. If no workload or Service is available, create one by referring to :ref:`Deployments <ucs_01_0255>` and :ref:`ClusterIP <ucs_01_0271>`.

-  Configuring the Multi-Cluster Networking

   Check and configure the network connectivity of both inter-cluster nodes and containers by referring to :ref:`Configuring the Cluster Network <ucs_01_0377>`.

.. note::

   If the error message "policy doesn't allow 'get loadbalancer' to be performed." or "because no identity-based policy allows the xxx action." is displayed during MCS instance creation, the agency permissions do not take effect. Wait for a while and try again. If it is displayed in the **Events** window, ignore it.

Creating an MCS Object Using YAML on the Console
------------------------------------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its console.

#. In the navigation pane, choose **Services and Ingresses**. Then, click the **MCS** tab.

#. Click **Create from YAML** in the upper right corner.

#. Select **YAML** for **Current Data** and edit the configuration in the editing area. (Configure the parameters as needed.)

   .. code-block::

      apiVersion: networking.karmada.io/v1alpha1
      kind: MultiClusterService
      metadata:
        name: mcs-24132      # MCS object name
        namespace: default      # Name of the namespace where the MCS object is located
      spec:
        types:
          - CrossCluster     # Inter-cluster service discovery
        providerClusters:
          - name: cluster-25043    # The cluster that this Service will be deployed in
        consumerClusters:
          - name: cluster-29544    # The cluster that will access this Service

#. Click **OK**.

.. _ucs_01_0378__section7746559101919:

Creating an MCS Object Using kubectl
------------------------------------

#. Use kubectl to connect to the federation. For details, see :ref:`Using kubectl to Connect to a Federation <ucs_01_0320>`.

#. Create and edit the **mcs.yaml** file. For details about the parameters in this file, see :ref:`Table 1 <ucs_01_0378__table1673555792620>`.

   **vi mcs.yaml**

   In the example, the defined MCS object is associated with Service **foo**. This Service is deployed in cluster B and can be accessed from cluster A.

   .. code-block::

      apiVersion: networking.karmada.io/v1alpha1
      kind: MultiClusterService
      metadata:
         name: foo                          # MCS object name
         namespace: default                  # Name of the namespace where the MCS object is located
      spec:
         types:
           - CrossCluster                   # Inter-cluster service discovery
         providerClusters:                  # Cluster that the Service is delivered to
           - name: clusterB
         consumerClusters:                  # Cluster that accesses the Service
           - name: clusterA

   .. _ucs_01_0378__table1673555792620:

   .. table:: **Table 1** Key parameters

      +----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                  | Mandatory       | Type            | Description                                                                                                                                                                                                                                                         |
      +============================+=================+=================+=====================================================================================================================================================================================================================================================================+
      | metadata.name              | Yes             | String          | Name of the MCS object, which must be the same as that of the associated Service.                                                                                                                                                                                   |
      +----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | metadata.namespace         | No              | String          | Name of the namespace where the MCS object is located, which must be the same as that of the namespace where the associated Service is located. If this parameter is left blank, **default** is used.                                                               |
      +----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | spec.types                 | Yes             | String          | Traffic direction. To enable service discovery across clusters, set this parameter to **CrossCluster**.                                                                                                                                                             |
      +----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | spec.providerClusters.name | No              | String          | Name of the cluster that the Service is delivered to. Set this parameter to the cluster where the Service is deployed. If this parameter is left blank, the Service is delivered to all clusters in the federation by default.                                      |
      |                            |                 |                 |                                                                                                                                                                                                                                                                     |
      |                            |                 |                 | .. caution::                                                                                                                                                                                                                                                        |
      |                            |                 |                 |                                                                                                                                                                                                                                                                     |
      |                            |                 |                 |    CAUTION:                                                                                                                                                                                                                                                         |
      |                            |                 |                 |    If a Service is deployed in cluster B but cluster A and cluster B are both configured as the delivery targets, the Service is delivered to both clusters. The original Service with the same name in cluster A will be overwritten.                              |
      +----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | spec.consumerClusters.name | No              | String          | Name of the cluster that accesses the Service. Set this parameter to the name of the cluster that is expected to access the Service across clusters through MCS. If this parameter is left blank, all clusters in the federation can access the Service by default. |
      +----------------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Create an MCS object.

   **kubectl apply -f mcs.yaml**

#. Check the status of the MCS object (named **foo**).

   **kubectl describe mcs foo**

   The **status** field in the YAML file records the MCS object status. If the following information is displayed, the endpoint slices are successfully delivered and synchronized, and cross-cluster service discovery is available:

   .. code-block::

      status:
        conditions:
        - lastTransitionTime: "2023-11-20T02:30:49Z"
        message: EndpointSlices are propagated to target clusters.
          reason: EndpointSliceAppliedSuccess
          status: "True"
        type: EndpointSliceApplied

   Run the following commands to operate the MCS object (named **foo**):

   -  **kubectl get mcs foo**: obtains the MCS object.
   -  **kubectl edit mcs foo**: updates the MCS object.
   -  **kubectl delete mcs foo**: deletes the MCS object.

.. _ucs_01_0378__section687594962717:

Cross-Cluster Access
--------------------

After the MCS object is created, you can access the Service from the cluster specified by **consumerClusters.name**.

In the cluster specified by **consumerClusters.name**, create a pod, access the container, and run the **curl http://**\ *Service name*\ **:**\ *Port number* command to access the Service.

If the following information is displayed, the access is successful:

.. code-block::

   / # curl http://Service name:Port number
   ...
   <h1>Welcome to foo!</h1>
   ...
