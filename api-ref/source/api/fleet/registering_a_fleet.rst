:original_name: RegisterClusterGroup.html

.. _RegisterClusterGroup:

Registering a Fleet
===================

Function
--------

This API is used to create a fleet. You can select clusters during fleet creation.

URI
---

POST /v1/clustergroups

Request Parameters
------------------

.. table:: **Table 1** Request header parameters

   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter    | Mandatory | Type   | Description                                                                                                                                                                                                              |
   +==============+===========+========+==========================================================================================================================================================================================================================+
   | X-Auth-Token | No        | String | Identity authentication information. Requests for calling an API can be authenticated using either a token or AK/SK. If token-based authentication is used, this parameter is mandatory and must be set to a user token. |
   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Content-Type | Yes       | String | Message body type (format). Only **application/json** is supported.                                                                                                                                                      |
   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Request body parameters

   +-----------+-----------+-------------------------------------------------------------------------------------------------------------+----------------------------+
   | Parameter | Mandatory | Type                                                                                                        | Description                |
   +===========+===========+=============================================================================================================+============================+
   | metadata  | Yes       | :ref:`RegisterClusterGroupObjectMeta <registerclustergroup__request_registerclustergroupobjectmeta>` object | Fleet metadata information |
   +-----------+-----------+-------------------------------------------------------------------------------------------------------------+----------------------------+
   | spec      | No        | :ref:`RegisterClusterGroupSpec <registerclustergroup__request_registerclustergroupspec>` object             | Attribute                  |
   +-----------+-----------+-------------------------------------------------------------------------------------------------------------+----------------------------+

.. _registerclustergroup__request_registerclustergroupobjectmeta:

.. table:: **Table 3** RegisterClusterGroupObjectMeta

   ========= ========= ====== ===========
   Parameter Mandatory Type   Description
   ========= ========= ====== ===========
   name      Yes       String Fleet name
   ========= ========= ====== ===========

.. _registerclustergroup__request_registerclustergroupspec:

.. table:: **Table 4** RegisterClusterGroupSpec

   =========== ========= ================ ============================
   Parameter   Mandatory Type             Description
   =========== ========= ================ ============================
   clusterIds  No        Array of strings ID of the associated cluster
   description No        String           Fleet description
   =========== ========= ================ ============================

Response Parameters
-------------------

**Status code: 201**

.. table:: **Table 5** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   uid       String Fleet UID
   ========= ====== ===========

**Status code: 400**

.. table:: **Table 6** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

**Status code: 403**

.. table:: **Table 7** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

**Status code: 500**

.. table:: **Table 8** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

Example Requests
----------------

Creating a fleet and (optional) adding clusters to the fleet

.. code-block::

   https://ucs.mytcloud.com/v1/clustergroups

   {
     "metadata" : {
       "name" : "group02281605"
     },
     "spec" : {
       "clusterIds" : [ "514c1a3c-8ec7-11ec-b384-0255ac100189", "d4804da3-8f03-11ec-b384-0255ac100189" ],
       "description" : "aaaaaaaaa"
     }
   }

Example Responses
-----------------

**Status code: 201**

The fleet has been created (the UID of the fleet is returned).

.. code-block::

   {
     "uid" : "6efb4a18-2fa4-11ee-ad1d-0255ac1001c4"
   }

Status Codes
------------

+-------------+-----------------------------------------------------------------+
| Status Code | Description                                                     |
+=============+=================================================================+
| 201         | The fleet has been created (the UID of the fleet is returned).  |
+-------------+-----------------------------------------------------------------+
| 400         | Client request error. The server could not execute the request. |
+-------------+-----------------------------------------------------------------+
| 403         | The server refused the request.                                 |
+-------------+-----------------------------------------------------------------+
| 500         | Internal server error.                                          |
+-------------+-----------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
