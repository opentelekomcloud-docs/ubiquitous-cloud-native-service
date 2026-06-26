:original_name: ucs_api_0008.html

.. _ucs_api_0008:

Making an API Request
=====================

This section describes the structure of a REST API request, and uses the IAM API for `obtaining a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__\ obtaining a user token as an example to demonstrate how to call an API. The obtained token can then be used to authenticate the calling of other APIs.

Request URI
-----------

A request URI is in the following format:

**{URI-scheme}://{Endpoint}/{resource-path}?{query-string}**

Although a request URI is included in the request header, most programming languages or frameworks require the request URI to be transmitted separately.

.. table:: **Table 1** URI parameters

   +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter     | Description                                                                                                                                                                                                                                                            |
   +===============+========================================================================================================================================================================================================================================================================+
   | URI-scheme    | Protocol used to transmit requests. All APIs use **HTTPS**.                                                                                                                                                                                                            |
   +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Endpoint      | Domain name or IP address of the server bearing the REST service. The endpoint varies between services in different regions. It can be obtained from `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__"Regions and Endpoints".      |
   +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource-path | Access path of an API for performing a specified operation. Obtain the path from the URI of an API. For example, the **resource-path** of the API used to obtain a user token is **/v3/auth/tokens**.                                                                  |
   +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | query-string  | Query parameter, which is optional. Ensure that a question mark (?) is included before each query parameter that is in the format of *Parameter name*\ =\ *Parameter value*. For example, **?limit=10** indicates that a maximum of 10 data records will be displayed. |
   +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   To simplify the URI display in this document, each API is provided only with a **resource-path** and a request method. The **URI-scheme** of all APIs is **HTTPS**, and the endpoints of all APIs in the same region are identical.

Request Methods
---------------

The HTTP protocol defines the following request methods that can be used to send a request to the server.

.. table:: **Table 2** HTTP methods

   +-----------------------------------+----------------------------------------------------------------------------+
   | Method                            | Description                                                                |
   +===================================+============================================================================+
   | GET                               | Requests the server to return specified resources.                         |
   +-----------------------------------+----------------------------------------------------------------------------+
   | PUT                               | Requests the server to update specified resources.                         |
   +-----------------------------------+----------------------------------------------------------------------------+
   | POST                              | Requests the server to add resources or perform special operations.        |
   +-----------------------------------+----------------------------------------------------------------------------+
   | DELETE                            | Requests the server to delete specified resources, for example, an object. |
   +-----------------------------------+----------------------------------------------------------------------------+
   | HEAD                              | Requests the server to return the response header.                         |
   +-----------------------------------+----------------------------------------------------------------------------+
   | PATCH                             | Requests the server to update partial content of a specified resource.     |
   |                                   |                                                                            |
   |                                   | If the resource does not exist, a new resource will be created.            |
   +-----------------------------------+----------------------------------------------------------------------------+

For example, in the case of the API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__\ obtain a user token, the request method is **POST**. The request is as follows:

.. code-block:: text

   POST https://{{endpoint}}/v3/auth/tokens

Request Header
--------------

You can also add additional header fields to a request, such as the fields required by a specified URI or HTTP method. For example, to request for the authentication information, add **Content-Type**, which specifies the request body type.

:ref:`Table 3 <ucs_api_0008__en-us_topic_0121682347_table1986821153312>` lists common request header fields.

.. _ucs_api_0008__en-us_topic_0121682347_table1986821153312:

.. table:: **Table 3** Common request header fields

   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------+--------------------------------------------+
   | Parameter       | Description                                                                                                                                                                                                                                                                                                          | Mandatory                                         | Example Value                              |
   +=================+======================================================================================================================================================================================================================================================================================================================+===================================================+============================================+
   | Host            | Specifies the server domain name and port number of the resources being requested. The value can be obtained from the URL of the service API. The value is in the format of *Hostname:Port number*. If the port number is not specified, the default port is used. The default port number for **https** is **443**. | No                                                | code.test.com                              |
   |                 |                                                                                                                                                                                                                                                                                                                      |                                                   |                                            |
   |                 |                                                                                                                                                                                                                                                                                                                      | This field is mandatory for AK/SK authentication. | or                                         |
   |                 |                                                                                                                                                                                                                                                                                                                      |                                                   |                                            |
   |                 |                                                                                                                                                                                                                                                                                                                      |                                                   | code.test.com:443                          |
   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------+--------------------------------------------+
   | Content-Type    | Specifies the type (or format) of the message body. The default value **application/json** is recommended. Other values of this field will be provided for specific APIs if any.                                                                                                                                     | Yes                                               | application/json                           |
   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------+--------------------------------------------+
   | Content-Length  | Specifies the length of the request body. The unit is byte.                                                                                                                                                                                                                                                          | No                                                | 3495                                       |
   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------+--------------------------------------------+
   | X-Project-Id    | Specifies the project ID. Obtain the project ID by following the instructions in :ref:`Obtaining a Project ID <ucs_api_0018>`.                                                                                                                                                                                       | No                                                | e9993fc787d94b6c886cbaa340f9c0f4           |
   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------+--------------------------------------------+
   | X-Auth-Token    | Specifies the user token.                                                                                                                                                                                                                                                                                            | No                                                | The following is part of an example token: |
   |                 |                                                                                                                                                                                                                                                                                                                      |                                                   |                                            |
   |                 | It is a response to the API for `obtaining a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__. (This is the only API that does not require authentication.)                                                                                                                  | This field is mandatory for token authentication. | MIIPAgYJKoZIhvcNAQcCo...ggg1BBIINPXsidG9rZ |
   |                 |                                                                                                                                                                                                                                                                                                                      |                                                   |                                            |
   |                 | After the request is processed, the value of **X-Subject-Token** in the response header is the token value.                                                                                                                                                                                                          |                                                   |                                            |
   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------+--------------------------------------------+

.. note::

   In addition to supporting authentication using tokens, APIs support authentication using AK/SK, which uses SDKs to sign a request. During the signature, the **Authorization** (signature authentication) and **X-Sdk-Date** (time when a request is sent) headers are automatically added in the request.

   For more details, see "Authentication Using AK/SK" in :ref:`Authentication <ucs_api_0009>`.

The API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__\ obtain a user token does not require authentication. Only the **Content-Type** field needs to be added to requests for calling the API. An example of such requests is as follows:

.. code-block:: text

   POST https://{{endpoint}}/v3/auth/tokens
   Content-Type: application/json

(Optional) Request Body
-----------------------

This part is optional. The body of a request is often sent in a structured format (for example, JSON or XML) as specified in the **Content-Type** header field. The request body transfers content except the request header.

The request body varies between APIs. Some APIs do not require the request body, such as the APIs requested using the GET and DELETE methods.

In the case of the API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__\ obtain a user token, the request parameters and parameter description can be obtained from the API request. The following provides an example request with a body included. Replace **username**, **domainname** (domain), **\*******\*** (login password), and **xxxxxxxxxxxxxxxxxx** (project name) with the actual values. Obtain the project name from `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__"Regions and Endpoints".

If all data required for the API request is available, you can send the request to call the API through `curl <https://curl.haxx.se/>`__, `Postman <https://www.getpostman.com/>`__, or coding. In the response to the API used to obtain a user token, **x-subject-token** is the desired user token. This token can then be used to authenticate the calling of other APIs.
