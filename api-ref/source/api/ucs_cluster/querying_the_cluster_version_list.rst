:original_name: ListRegisteredClusterVersions.html

.. _ListRegisteredClusterVersions:

Querying the Cluster Version List
=================================

Function
--------

This API is used to query the list of cluster versions that are supported by UCS.

URI
---

GET /v1/config/registeredclusterversions

Request Parameters
------------------

.. table:: **Table 1** Request header parameters

   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter    | Mandatory | Type   | Description                                                                                                                                                                                                              |
   +==============+===========+========+==========================================================================================================================================================================================================================+
   | X-Auth-Token | No        | String | Identity authentication information. Requests for calling an API can be authenticated using either a token or AK/SK. If token-based authentication is used, this parameter is mandatory and must be set to a user token. |
   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   ========= ================ ====================
   Parameter Type             Description
   ========= ================ ====================
   versions  Array of strings Cluster version list
   ========= ================ ====================

Example Requests
----------------

None

Example Responses
-----------------

**Status code: 200**

List of supported cluster versions

.. code-block::

   {
     "versions" : [ "v1.19", "v1.20", "v1.21", "v1.22", "v1.23", "v1.24", "v1.25" ]
   }

Status Codes
------------

=========== ==================================
Status Code Description
=========== ==================================
200         List of supported cluster versions
=========== ==================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
