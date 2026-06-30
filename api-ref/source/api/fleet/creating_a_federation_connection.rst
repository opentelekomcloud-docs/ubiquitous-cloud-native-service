:original_name: CreateFederationConnection.html

.. _CreateFederationConnection:

Creating a Federation Connection
================================

Function
--------

This API is used to create a VPC endpoint for connecting to the federation API server after federation is enabled for a fleet.

URI
---

POST /v1/clustergroups/{clustergroupid}/connection

.. table:: **Table 1** Path Parameters

   ============== ========= ====== ===========
   Parameter      Mandatory Type   Description
   ============== ========= ====== ===========
   clustergroupid Yes       String Fleet ID
   ============== ========= ====== ===========

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter    | Mandatory | Type   | Description                                                                                                                                                                                                              |
   +==============+===========+========+==========================================================================================================================================================================================================================+
   | X-Auth-Token | No        | String | Identity authentication information. Requests for calling an API can be authenticated using either a token or AK/SK. If token-based authentication is used, this parameter is mandatory and must be set to a user token. |
   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Content-Type | Yes       | String | Message body type (format). Only **application/json** is supported.                                                                                                                                                      |
   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-----------+-----------+--------+---------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                                                     |
   +===========+===========+========+=================================================================================+
   | projectID | Yes       | String | Project ID                                                                      |
   +-----------+-----------+--------+---------------------------------------------------------------------------------+
   | vpcID     | Yes       | String | VPC ID, which must belong to the project specified by **projectID**.            |
   +-----------+-----------+--------+---------------------------------------------------------------------------------+
   | subnetID  | Yes       | String | Network ID of the subnet. The subnet must be in the VPC specified by **vpcID**. |
   +-----------+-----------+--------+---------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 201**

.. table:: **Table 4** Response body parameters

   ========= ====== ===============
   Parameter Type   Description
   ========= ====== ===============
   id        String VPC endpoint ID
   ========= ====== ===============

Example Requests
----------------

Creating a federation connection

.. code-block:: text

   POST https://ucs.mytcloud.com/v1/clustergroups/{clustergroupid}/connection

   {
     "projectID" : "08d44be1ef00d22e2f6fc0061f54a2f1",
     "vpcID" : "11c9fe72-5a90-4295-bcfe-774726fb9066",
     "subnetID" : "0de91d89-1e06-4e24-b371-35d5d3d3779b"
   }

Example Responses
-----------------

**Status code: 201**

Connecting to the federation API server using a VPC endpoint

.. code-block::

   {
     "id" : "b8c9c1dc-b10f-4644-bc5f-e557efa63782s"
   }

Status Codes
------------

=========== ============================================================
Status Code Description
=========== ============================================================
201         Connecting to the federation API server using a VPC endpoint
=========== ============================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
