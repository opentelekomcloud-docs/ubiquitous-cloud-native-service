:original_name: DeleteClusterGroup.html

.. _DeleteClusterGroup:

Deleting a Fleet
================

Function
--------

This API is used to delete a fleet. A fleet can only be deleted when there are no clusters in it. To delete a fleet, remove the clusters from the fleet first. The cluster IDs must comply with the Kubernetes UUID format rules, and you must have the operation permission on the clusters. Otherwise, the authentication fails.

URI
---

DELETE /v1/clustergroups/{clustergroupid}

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

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String
   ========= ====== ===========

**Status code: 400**

.. table:: **Table 4** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String
   ========= ====== ===========

**Status code: 403**

.. table:: **Table 5** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String
   ========= ====== ===========

**Status code: 404**

.. table:: **Table 6** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String
   ========= ====== ===========

**Status code: 500**

.. table:: **Table 7** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String
   ========= ====== ===========

Example Requests
----------------

None

Example Responses
-----------------

None

Status Codes
------------

+-------------+-----------------------------------------------------------------+
| Status Code | Description                                                     |
+=============+=================================================================+
| 200         | The fleet has been deleted.                                     |
+-------------+-----------------------------------------------------------------+
| 400         | Client request error. The server could not execute the request. |
+-------------+-----------------------------------------------------------------+
| 403         | The server refused the request.                                 |
+-------------+-----------------------------------------------------------------+
| 404         | Resource not found.                                             |
+-------------+-----------------------------------------------------------------+
| 500         | Internal server error.                                          |
+-------------+-----------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
