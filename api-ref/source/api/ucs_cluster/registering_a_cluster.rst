:original_name: RegisterCluster.html

.. _RegisterCluster:

Registering a Cluster
=====================

Function
--------

This API is used to register a cluster. Attached clusters and CCE clusters can be registered.

URI
---

POST /v1/clusters

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

   +------------+-----------+------------------------------------------------------------+-----------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type                                                       | Description                                                                 |
   +============+===========+============================================================+=============================================================================+
   | kind       | Yes       | String                                                     | Resource type. For a registered cluster, set this parameter to **Cluster**. |
   +------------+-----------+------------------------------------------------------------+-----------------------------------------------------------------------------+
   | apiVersion | Yes       | String                                                     | API version. The current version is **v1**.                                 |
   +------------+-----------+------------------------------------------------------------+-----------------------------------------------------------------------------+
   | metadata   | Yes       | :ref:`metadata <registercluster__request_metadata>` object | Cluster metadata information                                                |
   +------------+-----------+------------------------------------------------------------+-----------------------------------------------------------------------------+
   | spec       | Yes       | :ref:`spec <registercluster__request_spec>` object         | Cluster specifications                                                      |
   +------------+-----------+------------------------------------------------------------+-----------------------------------------------------------------------------+

.. _registercluster__request_metadata:

.. table:: **Table 3** metadata

   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type               | Description                                                                                                                                                                         |
   +=================+=================+====================+=====================================================================================================================================================================================+
   | uid             | No              | String             | Cluster ID. This parameter is used only when a CCE cluster is imported for registration. For other types of clusters, you do not need to set this parameter.                        |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | name            | Yes             | String             | CCE cluster name or a custom cluster name (for other types of clusters).                                                                                                            |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | labels          | No              | Map<String,String> | Label information. This parameter can be left empty. If it is not left empty, the value must comply with the Kubernetes label specifications. A maximum of 100 labels can be added. |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | annotations     | No              | Map<String,String> | Cluster annotations information.                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                     |
   |                 |                 |                    | The **kubeconfig** field is mandatory for an attached cluster, and its value is the content of the kubeconfig file.                                                                 |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _registercluster__request_spec:

.. table:: **Table 4** spec

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                                                      |
   +=================+=================+=================+==================================================================================================================================================================================================================================================================+
   | clusterGroupID  | No              | String          | Container fleet ID                                                                                                                                                                                                                                               |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | category        | Yes             | String          | Cluster type. The value must meet the requirements for **provider** and **type**. For details, see :ref:`Cluster Categories and Types <ucs_api_0024>`.                                                                                                           |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | type            | Yes             | String          | Cluster type. The value must meet the requirements for **provider** and **category**. For details, see :ref:`Cluster Categories and Types <ucs_api_0024>`.                                                                                                       |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | provider        | Yes             | String          | Provider. The value must the requirements for **category** and **type**. For details, see :ref:`Cluster Categories and Types <ucs_api_0024>`.                                                                                                                    |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | country         | Yes             | String          | Country code. For details, see :ref:`Country Codes <ucs_api_0022>`.                                                                                                                                                                                              |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | city            | Yes             | String          | City code (consistent with the country)                                                                                                                                                                                                                          |
   |                 |                 |                 |                                                                                                                                                                                                                                                                  |
   |                 |                 |                 | This parameter is optional for a CCE cluster and mandatory for an attached cluster.                                                                                                                                                                              |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | region          | No              | String          | Region information. This parameter is only used when a cluster is imported to CCE for registration. You can obtain the value from the **region** field in the :ref:`API for querying CCE clusters that have not been registered with UCS <listmanagedclusters>`. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | projectID       | No              | String          | Project ID. This parameter is only used when a cluster is imported to CCE for registration. You can obtain the value from the **projectID** field in the :ref:`API for querying CCE clusters that have not been registered with UCS <listmanagedclusters>`.      |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | manageType      | Yes             | String          | Cluster type.                                                                                                                                                                                                                                                    |
   |                 |                 |                 |                                                                                                                                                                                                                                                                  |
   |                 |                 |                 | -  **grouped**: clusters added to a fleet                                                                                                                                                                                                                        |
   |                 |                 |                 |                                                                                                                                                                                                                                                                  |
   |                 |                 |                 | -  **discrete**: clusters not in any fleet                                                                                                                                                                                                                       |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 201**

.. table:: **Table 5** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   uid       String Cluster ID
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

**Status code: 404**

.. table:: **Table 8** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

**Status code: 409**

.. table:: **Table 9** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

**Status code: 500**

.. table:: **Table 10** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

Example Requests
----------------

-  Registering a CCE cluster

   .. code-block:: text

      POST https://ucs.mytcloud.com/v1/clusters

      {
        "kind" : "Cluster",
        "apiVersion" : "v1",
        "metadata" : {
          "name" : "cce-cluster",
          "uid" : "44052cdd-8cd2-11ee-abd1-0255ac1001bd"
        },
        "spec" : {
          "region" : "******",
          "category" : "self",
          "type" : "turbo",
          "projectID" : "05495693df80d3c92fa1c01795c2be02",
          "clusterGroupID" : "",
          "manageType" : "discrete",
          "city" : "110000",
          "country" : "*****",
          "provider" : {
            "CCE" : "cce"
          }
        }
      }

-  Registering an attached cluster

   .. code-block:: text

      POST https://ucs.mytcloud.com/v1/clusters

      {
        "kind" : "Cluster",
        "apiVersion" : "v1",
        "metadata" : {
          "name" : "ack-cluster",
          "annotations" : {
            "kubeconfig" : "{\"kind\":\"Config\",\"apiVersion\":\"v1\",\"preferences\":{},\"clusters\":[{\"name\":\"internalCluster\",\"cluster\":{\"server\":\"https://kubernetes.default.svc.cluster.local:443\",\"insecure-skip-tls-verify\":true}}],\"users\":[{\"name\":\"ucs-user\",\"user\":{\"token\":\"token-string\"}}],\"contexts\":[{\"name\":\"internal\",\"context\":{\"cluster\":\"internalCluster\",\"user\":\"ucs-user\"}}],\"current-context\":\"internal\"}"
          },
          "labels" : { }
        },
        "spec" : {
          "category" : "attachedcluster",
          "clusterGroupID" : "",
          "manageType" : "discrete",
          "city" : "110000",
          "country" : "**",
          "provider" : {,
            "AWS" : "aws",
            "AZURE" : "azure",
            "OPENSHIFT" : "openshift",
            "TCloudSTACK" : "tcloudstack",
            "TCloud" : "tcloud",
            "PRIVATEK8S" : "privatek8s",
            "OTHER" : "other",
            "FLEXIBLEENGINE" : "FlexibleEngine",
            "FLEXIBLEENGINESTACK" : "FlexibleEngineStack",
          },
          "type" : "ack"
        }
      }

Example Responses
-----------------

**Status code: 201**

The cluster has been registered (the ID of the registered cluster is returned).

.. code-block::

   {
     "uid" : "b0d1ecb5-7947-11ee-9467-0255ac1001bf"
   }

Status Codes
------------

+-------------+---------------------------------------------------------------------------------+
| Status Code | Description                                                                     |
+=============+=================================================================================+
| 201         | The cluster has been registered (the ID of the registered cluster is returned). |
+-------------+---------------------------------------------------------------------------------+
| 400         | Client request error. The server could not execute the request.                 |
+-------------+---------------------------------------------------------------------------------+
| 403         | The server refused the request.                                                 |
+-------------+---------------------------------------------------------------------------------+
| 404         | Resource not found.                                                             |
+-------------+---------------------------------------------------------------------------------+
| 409         | There was a request conflict.                                                   |
+-------------+---------------------------------------------------------------------------------+
| 500         | Internal server error.                                                          |
+-------------+---------------------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
