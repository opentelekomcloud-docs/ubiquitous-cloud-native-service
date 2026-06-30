:original_name: UpdateClusterGroupAssociatedClusters.html

.. _UpdateClusterGroupAssociatedClusters:

Adding Clusters to a Fleet
==========================

Function
--------

This API is used to add clusters to a fleet. One or more clusters can be added at the same time. This API cannot be used to remove clusters from a fleet.

URI
---

PUT /v1/clustergroups/{clustergroupid}/associatedclusters

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

   +------------+-----------+------------------+-----------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type             | Description                                                                 |
   +============+===========+==================+=============================================================================+
   | clusterIds | No        | Array of strings | Cluster IDs for updating information about clusters associated with a fleet |
   +------------+-----------+------------------+-----------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

Clusters have been added to the fleet.

**Status code: 400**

.. table:: **Table 4** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

**Status code: 500**

.. table:: **Table 5** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

Example Requests
----------------

Updating clusters in a fleet

.. code-block:: text

   PUT https://ucs.mytcloud.com/v1/clustergroups/{clustergroupid}/associatedclusters

   {
     "clusterIds" : [ "xxxx-xxxx-xxxx" ]
   }

Example Responses
-----------------

**Status code: 200**

Clusters have been added to the fleet.

.. code-block::

   { }

Status Codes
------------

+-------------+-----------------------------------------------------------------+
| Status Code | Description                                                     |
+=============+=================================================================+
| 200         | Clusters have been added to the fleet.                          |
+-------------+-----------------------------------------------------------------+
| 400         | Client request error. The server could not execute the request. |
+-------------+-----------------------------------------------------------------+
| 500         | Internal server error.                                          |
+-------------+-----------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
