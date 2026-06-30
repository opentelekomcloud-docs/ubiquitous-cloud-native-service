:original_name: DownloadFederationKubeconfig.html

.. _DownloadFederationKubeconfig:

Downloading Federation kubeconfig
=================================

Function
--------

This API is used to download the kubeconfig file after the federation is enabled for a fleet and the federation connection is created.

URI
---

POST /v1/clustergroups/{clustergroupid}/kubeconfig

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

   ========= ========= ======= ===========================================
   Parameter Mandatory Type    Description
   ========= ========= ======= ===========================================
   duration  Yes       Integer Validity period of a kubeconfig certificate
   ========= ========= ======= ===========================================

Response Parameters
-------------------

**Status code: 201**

.. table:: **Table 4** Response body parameters

   +-----------------+----------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | Parameter       | Type                                                                                         | Description                                                            |
   +=================+==============================================================================================+========================================================================+
   | kind            | String                                                                                       | API type. The value is fixed at **Config** and cannot be changed.      |
   +-----------------+----------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | apiVersion      | String                                                                                       | API version. The value is fixed at **v1** and cannot be changed.       |
   +-----------------+----------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | clusters        | Array of :ref:`NamedCluster <downloadfederationkubeconfig__response_namedcluster>` objects   | Cluster list                                                           |
   +-----------------+----------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | users           | Array of :ref:`NamedAuthInfo <downloadfederationkubeconfig__response_namedauthinfo>` objects | Certificate information and client key information of a specified user |
   +-----------------+----------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | contexts        | Array of :ref:`NamedContext <downloadfederationkubeconfig__response_namedcontext>` objects   | Context list                                                           |
   +-----------------+----------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | current-context | String                                                                                       | Current context                                                        |
   +-----------------+----------------------------------------------------------------------------------------------+------------------------------------------------------------------------+

.. _downloadfederationkubeconfig__response_namedcluster:

.. table:: **Table 5** NamedCluster

   +-----------+--------------------------------------------------------------------------------+---------------------+
   | Parameter | Type                                                                           | Description         |
   +===========+================================================================================+=====================+
   | name      | String                                                                         | Cluster name        |
   +-----------+--------------------------------------------------------------------------------+---------------------+
   | cluster   | :ref:`ClusterCert <downloadfederationkubeconfig__response_clustercert>` object | Cluster information |
   +-----------+--------------------------------------------------------------------------------+---------------------+

.. _downloadfederationkubeconfig__response_clustercert:

.. table:: **Table 6** ClusterCert

   +----------------------------+---------+-------------------------------------------------+
   | Parameter                  | Type    | Description                                     |
   +============================+=========+=================================================+
   | server                     | String  | Server address                                  |
   +----------------------------+---------+-------------------------------------------------+
   | certificate-authority-data | String  | Certificate authorization data                  |
   +----------------------------+---------+-------------------------------------------------+
   | insecure-skip-tls-verify   | Boolean | Whether to skip server certificate verification |
   +----------------------------+---------+-------------------------------------------------+

.. _downloadfederationkubeconfig__response_namedauthinfo:

.. table:: **Table 7** NamedAuthInfo

   +-----------+--------------------------------------------------------------------------+------------------------------------------------------------------------+
   | Parameter | Type                                                                     | Description                                                            |
   +===========+==========================================================================+========================================================================+
   | name      | String                                                                   | User name                                                              |
   +-----------+--------------------------------------------------------------------------+------------------------------------------------------------------------+
   | user      | :ref:`AuthInfo <downloadfederationkubeconfig__response_authinfo>` object | Certificate information and client key information of a specified user |
   +-----------+--------------------------------------------------------------------------+------------------------------------------------------------------------+

.. _downloadfederationkubeconfig__response_authinfo:

.. table:: **Table 8** AuthInfo

   +-------------------------+--------+------------------------------------------------+
   | Parameter               | Type   | Description                                    |
   +=========================+========+================================================+
   | client-certificate-data | String | Client certificate                             |
   +-------------------------+--------+------------------------------------------------+
   | client-key-data         | String | PEM encoding data from the TLS client key file |
   +-------------------------+--------+------------------------------------------------+
   | token                   | String | Authentication token                           |
   +-------------------------+--------+------------------------------------------------+

.. _downloadfederationkubeconfig__response_namedcontext:

.. table:: **Table 9** NamedContext

   +-----------+------------------------------------------------------------------------+---------------------+
   | Parameter | Type                                                                   | Description         |
   +===========+========================================================================+=====================+
   | name      | String                                                                 | Context name        |
   +-----------+------------------------------------------------------------------------+---------------------+
   | context   | :ref:`Context <downloadfederationkubeconfig__response_context>` object | Context information |
   +-----------+------------------------------------------------------------------------+---------------------+

.. _downloadfederationkubeconfig__response_context:

.. table:: **Table 10** Context

   ========= ====== ===============
   Parameter Type   Description
   ========= ====== ===============
   cluster   String Cluster context
   user      String User context
   ========= ====== ===============

Example Requests
----------------

Downloading federation kubeconfig

.. code-block:: text

   POST https://ucs.mytcloud.com/v1/clustergroups/{clustergroupid}/kubeconfig

   {
     "duration" : 30
   }

Example Responses
-----------------

**Status code: 201**

kubeconfig file

.. code-block::

   {
     "kind" : "Config",
     "apiVersion" : "v1",
     "clusters" : [ {
       "name" : "cluster-demo",
       "cluster" : {
         "server" : "https://ip:port",
         "certificate-authority-data" : ""
       }
     } ],
     "users" : [ {
       "name" : "user",
       "user" : {
         "client-certificate-data" : "",
         "client-key-data" : "",
         "token" : ""
       }
     } ],
     "contexts" : [ {
       "name" : "demo",
       "context" : {
         "cluster" : "cluster-demo",
         "user" : "user"
       }
     } ],
     "current-context" : "demo"
   }

Status Codes
------------

=========== ===============
Status Code Description
=========== ===============
201         kubeconfig file
=========== ===============

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
