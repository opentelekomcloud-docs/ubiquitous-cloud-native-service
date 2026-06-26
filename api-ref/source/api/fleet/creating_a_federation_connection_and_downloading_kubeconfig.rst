:original_name: CreateFederationCert.html

.. _CreateFederationCert:

Creating a Federation Connection and Downloading kubeconfig
===========================================================

Function
--------

This API is used to create a VPC endpoint for connecting to the federation API server and downloading kubeconfig of the federation API server after federation is enabled for a fleet.

URI
---

POST /v1/clustergroups/{clustergroupid}/cert

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

   +-----------+-----------+---------+----------------------------------------------------------------------+
   | Parameter | Mandatory | Type    | Description                                                          |
   +===========+===========+=========+======================================================================+
   | projectID | Yes       | String  | Project ID                                                           |
   +-----------+-----------+---------+----------------------------------------------------------------------+
   | vpcID     | Yes       | String  | VPC ID, which must belong to the project specified by **projectID**. |
   +-----------+-----------+---------+----------------------------------------------------------------------+
   | subnetID  | Yes       | String  | Subnet ID, which must belong to the VPC specified by **vpcID**.      |
   +-----------+-----------+---------+----------------------------------------------------------------------+
   | duration  | Yes       | Integer | Validity period of the certificate in kubeconfig, in days            |
   +-----------+-----------+---------+----------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 201**

.. table:: **Table 4** Response body parameters

   +-----------------+--------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | Parameter       | Type                                                                                 | Description                                                            |
   +=================+======================================================================================+========================================================================+
   | kind            | String                                                                               | API type. The value is fixed at **Config** and cannot be changed.      |
   +-----------------+--------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | apiVersion      | String                                                                               | API version. The value is fixed at **v1** and cannot be changed.       |
   +-----------------+--------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | clusters        | Array of :ref:`NamedCluster <createfederationcert__response_namedcluster>` objects   | Cluster list                                                           |
   +-----------------+--------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | users           | Array of :ref:`NamedAuthInfo <createfederationcert__response_namedauthinfo>` objects | Certificate information and client key information of a specified user |
   +-----------------+--------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | contexts        | Array of :ref:`NamedContext <createfederationcert__response_namedcontext>` objects   | Context list                                                           |
   +-----------------+--------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | current-context | String                                                                               | Current context                                                        |
   +-----------------+--------------------------------------------------------------------------------------+------------------------------------------------------------------------+

.. _createfederationcert__response_namedcluster:

.. table:: **Table 5** NamedCluster

   +-----------+------------------------------------------------------------------------+---------------------+
   | Parameter | Type                                                                   | Description         |
   +===========+========================================================================+=====================+
   | name      | String                                                                 | Cluster name        |
   +-----------+------------------------------------------------------------------------+---------------------+
   | cluster   | :ref:`ClusterCert <createfederationcert__response_clustercert>` object | Cluster information |
   +-----------+------------------------------------------------------------------------+---------------------+

.. _createfederationcert__response_clustercert:

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

.. _createfederationcert__response_namedauthinfo:

.. table:: **Table 7** NamedAuthInfo

   +-----------+------------------------------------------------------------------+------------------------------------------------------------------------+
   | Parameter | Type                                                             | Description                                                            |
   +===========+==================================================================+========================================================================+
   | name      | String                                                           | User name                                                              |
   +-----------+------------------------------------------------------------------+------------------------------------------------------------------------+
   | user      | :ref:`AuthInfo <createfederationcert__response_authinfo>` object | Certificate information and client key information of a specified user |
   +-----------+------------------------------------------------------------------+------------------------------------------------------------------------+

.. _createfederationcert__response_authinfo:

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

.. _createfederationcert__response_namedcontext:

.. table:: **Table 9** NamedContext

   +-----------+----------------------------------------------------------------+---------------------+
   | Parameter | Type                                                           | Description         |
   +===========+================================================================+=====================+
   | name      | String                                                         | Context name        |
   +-----------+----------------------------------------------------------------+---------------------+
   | context   | :ref:`Context <createfederationcert__response_context>` object | Context information |
   +-----------+----------------------------------------------------------------+---------------------+

.. _createfederationcert__response_context:

.. table:: **Table 10** Context

   ========= ====== ===============
   Parameter Type   Description
   ========= ====== ===============
   cluster   String Cluster context
   user      String User context
   ========= ====== ===============

Example Requests
----------------

Creating a federation connection and downloading kubeconfig

.. code-block:: text

   POST https://ucs.mytcloud.com/v1/clustergroups/{clustergroupid}/cert

   {
     "projectID" : "08d44be1ef00d22e2f6fc0061f54a2f1",
     "vpcID" : "11c9fe72-5a90-4295-bcfe-774726fb9066",
     "subnetID" : "0de91d89-1e06-4e24-b371-35d5d3d3779b",
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
