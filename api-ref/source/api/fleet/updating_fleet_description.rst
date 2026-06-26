:original_name: UpdateClusterGroup.html

.. _UpdateClusterGroup:

Updating Fleet Description
==========================

Function
--------

This API is used to update the description of a fleet. You must have the permission to update the fleet.

URI
---

PUT /v1/clustergroups/{clustergroupid}/description

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

   =========== ========= ====== =================
   Parameter   Mandatory Type   Description
   =========== ========= ====== =================
   description Yes       String Fleet description
   =========== ========= ====== =================

Response Parameters
-------------------

**Status code: 200**

Update succeeded.

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

Updating fleet description

.. code-block:: text

   PUT https://ucs.mytcloud.com/v1/clustergroups/{clustergroupid}/description

   {
     "description" : "aaaaaaaaa"
   }

Example Responses
-----------------

**Status code: 200**

Update succeeded.

.. code-block::

   { }

Status Codes
------------

+-------------+-----------------------------------------------------------------+
| Status Code | Description                                                     |
+=============+=================================================================+
| 200         | Update succeeded.                                               |
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
