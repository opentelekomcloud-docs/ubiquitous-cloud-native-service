:original_name: ucs_01_0377.html

.. _ucs_01_0377:

Configuring the Cluster Network
===============================

Before creating an MCS object, ensure connectivity of both inter-cluster nodes and containers.

Check the connectivity by referring to :ref:`Table 1 <ucs_01_0377__table3713445915>`. If the network between nodes or containers is not connected, connect them. If they still cannot be connected, rectify the fault by referring to :ref:`FAQ <ucs_01_0377__section94811833195412>`.

.. _ucs_01_0377__table3713445915:

.. table:: **Table 1** Connectivity of both inter-cluster nodes and containers

   +------------------------+---------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Inter-Cluster Network  | How to Check                                                                                                                          | How to Connect                                                                                                                                             |
   +========================+=======================================================================================================================================+============================================================================================================================================================+
   | Node connectivity      | Ping the IP address of a node in cluster B from cluster A. If the ping succeeds, the node connectivity is normal.                     | #. Configure the network type.                                                                                                                             |
   |                        |                                                                                                                                       |                                                                                                                                                            |
   |                        |                                                                                                                                       |    Set the network type to underlay for inter-cluster pod communication. For details, see :ref:`Cluster Network Types <ucs_01_0377__section191095498203>`. |
   |                        |                                                                                                                                       |                                                                                                                                                            |
   |                        |                                                                                                                                       | #. Connect the network between clusters.                                                                                                                   |
   |                        |                                                                                                                                       |                                                                                                                                                            |
   |                        |                                                                                                                                       |    -  Network connectivity between CCE clusters:                                                                                                           |
   |                        |                                                                                                                                       |                                                                                                                                                            |
   |                        |                                                                                                                                       |       CCE clusters in the same VPC can communicate with each other by default.                                                                             |
   |                        |                                                                                                                                       |                                                                                                                                                            |
   |                        |                                                                                                                                       |       Use a VPC peering connection to connect CCE clusters across VPCs.                                                                                    |
   |                        |                                                                                                                                       |                                                                                                                                                            |
   |                        |                                                                                                                                       |    -  Network connectivity between clusters of other types:                                                                                                |
   |                        |                                                                                                                                       |                                                                                                                                                            |
   |                        |                                                                                                                                       |       Enable the network between clusters of other types as required.                                                                                      |
   +------------------------+---------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Container connectivity | Use curl to access the IP address of a pod in cluster B from cluster A. If the access succeeds, the container connectivity is normal. |                                                                                                                                                            |
   +------------------------+---------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ucs_01_0377__section191095498203:

Cluster Network Types
---------------------

Ensure that underlay networks are supported for inter-cluster pod communication. The following table lists the types of clusters that support underlay networks.

.. _ucs_01_0377__table17109949192016:

.. table:: **Table 2** Types of clusters that support underlay networks

   +----------------------+----------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | Cluster Type         | Cluster Subtype      | Network Type                                                                              | Support Underlay Network |
   +======================+======================+===========================================================================================+==========================+
   | T Cloud clusters     | CCE clusters         | Container tunnel network                                                                  | No                       |
   +----------------------+----------------------+-------------------------------------------------------------------------------------------+--------------------------+
   |                      |                      | VPC network                                                                               | Yes                      |
   +----------------------+----------------------+-------------------------------------------------------------------------------------------+--------------------------+
   |                      | CCE Turbo clusters   | Cloud native network 2.0                                                                  | Yes                      |
   +----------------------+----------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | On-premises clusters | On-premises clusters | Overlay and underlay networks                                                             | Yes                      |
   |                      |                      |                                                                                           |                          |
   |                      |                      | The overlay network is used by default. You need to manually enable the underlay network. |                          |
   +----------------------+----------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | Attached clusters    | Attached clusters    | Underlay network                                                                          | Network type-based       |
   +----------------------+----------------------+-------------------------------------------------------------------------------------------+--------------------------+

.. _ucs_01_0377__section94811833195412:

FAQ
---

If nodes or containers in different clusters cannot access each other, check the items listed in the following table.

.. table:: **Table 3**

   +-------------------------------------------------------------------------+------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | Check Item                                                              | Fault Locating                                                                     | Solution                                                                                      |
   +=========================================================================+====================================================================================+===============================================================================================+
   | Whether the cluster version is v1.21 or later                           | Access the cluster details page.                                                   | Upgrade the cluster.                                                                          |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | Whether clusters can be accessed over an underlay network               | Check this item by referring to :ref:`Table 2 <ucs_01_0377__table17109949192016>`. | Configure the network type by referring to :ref:`Table 2 <ucs_01_0377__table17109949192016>`. |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | Whether CIDR blocks overlap in the routes of the VPC peering connection | Go to the VPC peering connection details page.                                     | Modify the overlapped CIDR blocks.                                                            |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
