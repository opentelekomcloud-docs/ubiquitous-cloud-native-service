:original_name: EnableFederation.html

.. _EnableFederation:

Enabling Fleet Federation
=========================

Function
--------

Enabling Fleet Federation

URI
---

POST /v1/clustergroups/{clustergroupid}/federations

.. table:: **Table 1** Path Parameters

   ============== ========= ====== ===========
   Parameter      Mandatory Type   Description
   ============== ========= ====== ===========
   clustergroupid Yes       String Fleet ID
   ============== ========= ====== ===========

.. table:: **Table 2** Query Parameters

   +--------------+-----------+---------+-----------------------------------------------------+
   | Parameter    | Mandatory | Type    | Description                                         |
   +==============+===========+=========+=====================================================+
   | retryjoinall | No        | Boolean | Whether to add the cluster to the federation again. |
   +--------------+-----------+---------+-----------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Request header parameters

   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter    | Mandatory | Type   | Description                                                                                                                                                                                                              |
   +==============+===========+========+==========================================================================================================================================================================================================================+
   | X-Auth-Token | No        | String | Identity authentication information. Requests for calling an API can be authenticated using either a token or AK/SK. If token-based authentication is used, this parameter is mandatory and must be set to a user token. |
   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 201**

Federation has been enabled.

**Status code: 400**

.. table:: **Table 4** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

**Status code: 404**

.. table:: **Table 5** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

**Status code: 500**

.. table:: **Table 6** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

Example Requests
----------------

Enabling fleet federation

.. code-block:: text

   POST https://ucs.mytcloud.com/v1/clustergroups/{clustergroupid}/federations

Example Responses
-----------------

**Status code: 201**

Federation has been enabled.

.. code-block::

   { }

Status Codes
------------

+-------------+-----------------------------------------------------------------+
| Status Code | Description                                                     |
+=============+=================================================================+
| 201         | Federation has been enabled.                                    |
+-------------+-----------------------------------------------------------------+
| 400         | Client request error. The server could not execute the request. |
+-------------+-----------------------------------------------------------------+
| 404         | Resource not found.                                             |
+-------------+-----------------------------------------------------------------+
| 500         | Internal server error.                                          |
+-------------+-----------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
