:original_name: RetryClusterActivation.html

.. _RetryClusterActivation:

Activating a Cluster
====================

Function
--------

This API is used to activate a cluster. The cluster ID must comply with the Kubernetes UUID format rules, and you must have the required permission on the corresponding cluster. Otherwise, the authentication fails.

URI
---

PUT /v1/clusters/{clusterid}/activation

.. table:: **Table 1** Path Parameters

   ========= ========= ====== ===========
   Parameter Mandatory Type   Description
   ========= ========= ====== ===========
   clusterid Yes       String Cluster ID
   ========= ========= ====== ===========

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

The cluster has been activated.

**Status code: 400**

.. table:: **Table 3** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

**Status code: 500**

.. table:: **Table 4** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

Example Requests
----------------

Activating a cluster

.. code-block:: text

   POST https://ucs.mytcloud.com/v1/clusters/{clusterid}/activation

Example Responses
-----------------

**Status code: 200**

The cluster has been activated.

.. code-block::

   { }

Status Codes
------------

+-------------+-----------------------------------------------------------------+
| Status Code | Description                                                     |
+=============+=================================================================+
| 200         | The cluster has been activated.                                 |
+-------------+-----------------------------------------------------------------+
| 400         | Client request error. The server could not execute the request. |
+-------------+-----------------------------------------------------------------+
| 500         | Internal server error.                                          |
+-------------+-----------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
