:original_name: UpdateCluster.html

.. _UpdateCluster:

Updating a Cluster
==================

Function
--------

This API is used to update a cluster. Currently, only the country/city of attached clusters can be updated.

URI
---

PUT /v1/clusters/{clusterid}

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
   | Content-Type | Yes       | String | Message body type (format). Only **application/json** is supported.                                                                                                                                                      |
   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +------------+-----------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type                                                                       | Description                                                                                     |
   +============+===========+============================================================================+=================================================================================================+
   | kind       | Yes       | String                                                                     | API type. The value is fixed at **Cluster** and cannot be changed.                              |
   +------------+-----------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | apiVersion | Yes       | String                                                                     | API version. The value is fixed at **v1** and cannot be changed.                                |
   +------------+-----------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | metadata   | No        | :ref:`UpdateObjectMeta <updatecluster__request_updateobjectmeta>` object   | Basic information about a cluster. Metadata is a collection of attributes.                      |
   +------------+-----------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | spec       | No        | :ref:`UpdateClusterSpec <updatecluster__request_updateclusterspec>` object | Detailed description of a cluster. UCS creates or updates objects by defining or updating spec. |
   +------------+-----------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+

.. _updatecluster__request_updateobjectmeta:

.. table:: **Table 4** UpdateObjectMeta

   =========== ========= ====== ==================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ==================
   annotations No        Object Cluster annotation
   =========== ========= ====== ==================

.. _updatecluster__request_updateclusterspec:

.. table:: **Table 5** UpdateClusterSpec

   ========= ========= ====== ====================================
   Parameter Mandatory Type   Description
   ========= ========= ====== ====================================
   country   No        String Country where the cluster is located
   city      No        String City where the cluster is located
   ========= ========= ====== ====================================

Response Parameters
-------------------

**Status code: 200**

The cluster has been updated.

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

Updating a cluster

.. code-block:: text

   PUT https://ucs.mytcloud.com/v1/clusters/{clusterid}

   {
     "kind" : "Cluster",
     "apiVersion" : "v1",
     "metadata" : {
       "annotations" : {
         "kubeconfig" : "{\"kind\":\"Config\",\"apiVersion\":\"v1\",\"preferences\":{},\"clusters\":[{\"name\":\"internalCluster\",\"cluster\":{\"server\":\"https://ip:5443\",\"insecure-skip-tls-verify\":true}}],\"users\":[{\"name\":\"user\",\"user\":{\"client-certificate-data\":\"\",\"client-key-data\":\"\"}}],\"contexts\":[{\"name\":\"internal\",\"context\":{\"cluster\":\"internalCluster\",\"user\":\"user\"}}],\"current-context\":\"internal\"}"
       }
     },
     "spec" : {
       "country" : "AL",
       "city" : "AL"
     }
   }

Example Responses
-----------------

**Status code: 200**

The cluster has been updated.

.. code-block::

   { }

Status Codes
------------

+-------------+-----------------------------------------------------------------+
| Status Code | Description                                                     |
+=============+=================================================================+
| 200         | The cluster has been updated.                                   |
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
