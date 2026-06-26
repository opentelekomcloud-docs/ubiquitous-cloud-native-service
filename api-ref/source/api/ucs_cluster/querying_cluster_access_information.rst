:original_name: ShowClusterAccessInfo.html

.. _ShowClusterAccessInfo:

Querying Cluster Access Information
===================================

Function
--------

This API is used to query the cluster access information. The cluster ID must comply with the Kubernetes UUID format rules. You must have permission to query the corresponding cluster. Otherwise, the authentication fails. The agent certificate can be downloaded only once. This API is only used to query the access information of attached clusters. If a CCE cluster ID is transferred, 400 will be returned.

URI
---

GET /v1/clusters/{clusterid}/accessinfo

.. table:: **Table 1** Path Parameters

   ========= ========= ====== ===========
   Parameter Mandatory Type   Description
   ========= ========= ====== ===========
   clusterid Yes       String Cluster ID
   ========= ========= ====== ===========

.. table:: **Table 2** Query Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                                                         |
   +=============+===========+========+=====================================================================================================================================+
   | vpcendpoint | No        | String | IP address of the VPC endpoint for accessing on-premises clusters. This parameter is mandatory for clusters on the private network. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------+
   | region      | No        | String | Access region. This parameter is mandatory for clusters accessed over a private network.                                            |
   +-------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------+

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

**Status code: 200**

.. table:: **Table 4** Response body parameters

   ========= ================ ===========
   Parameter Type             Description
   ========= ================ ===========
   [items]   Array of objects   
   ========= ================ ===========

**Status code: 400**

.. table:: **Table 5** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

**Status code: 403**

.. table:: **Table 6** Response body parameters

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   ``-``     String   
   ========= ====== ===========

**Status code: 410**

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

None

Example Responses
-----------------

**Status code: 200**

Cluster access information returned.

.. code-block::

   [ {
     "apiVersion" : "apps/v1",
     "kind" : "Deployment",
     "metadata" : {
       "labels" : {
         "app" : "proxy-agent"
       },
       "name" : "proxy-agent",
       "namespace" : "kube-system"
     },
     "spec" : {
       "replicas" : 2,
       "template" : {
         "metadata" : {
           "labels" : {
             "app" : "proxy-agent"
           }
         },
         "spec" : {
           "tolerations" : [ {
             "key" : "role",
             "operator" : "Equal",
             "value" : "manage"
           } ],
           "containers" : [ {
             "command" : [ "/proxy-agent" ],
             "args" : [ "--logtostderr=true", "--ca-cert=/var/certs/agent/ca.crt", "--agent-cert=/var/certs/agent/proxy-agent.crt", "--agent-key=/var/certs/agent/proxy-agent.key", "--proxy-server-host=proxyurl.ucs.mytcloud.com", "--proxy-server-port=30123", "--agent-id={uuid}", "--agent-identifiers=host={ip_addr}" ],
             "image" : "{image_addr}",
             "imagePullPolicy" : "IfNotPresent",
             "name" : "proxy-agent"
           } ],
           "priorityClassName" : "system-cluster-critical",
           "hostAliases" : [ {
             "ip" : "{ip_addr}",
             "hostnames" : [ "proxyurl.ucs.mytcloud.com" ]
           } ]
         }
       }
     }
   }, {
     "apiVersion" : "v1",
     "kind" : "Secret",
     "metadata" : {
       "name" : "proxy-agent-cert",
       "namespace" : "kube-system"
     },
     "type" : "Opaque",
     "data" : {
       "ca.crt" : "{ca crt}",
       "proxy-agent.crt" : "{proxy-agent crt}",
       "proxy-agent.key" : "{proxy-agent key}",
       "common_shared.key" : "{common_shared key}",
       "root.key" : "{root key}"
     }
   } ]

Status Codes
------------

+-------------+-----------------------------------------------------------------+
| Status Code | Description                                                     |
+=============+=================================================================+
| 200         | Cluster access information returned.                            |
+-------------+-----------------------------------------------------------------+
| 400         | Client request error. The server could not execute the request. |
+-------------+-----------------------------------------------------------------+
| 403         | The server refused the request.                                 |
+-------------+-----------------------------------------------------------------+
| 410         | The certificate has been downloaded.                            |
+-------------+-----------------------------------------------------------------+
| 500         | Internal server error.                                          |
+-------------+-----------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
