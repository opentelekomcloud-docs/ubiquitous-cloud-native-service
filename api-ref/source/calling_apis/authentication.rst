:original_name: ucs_api_0009.html

.. _ucs_api_0009:

Authentication
==============

Requests for calling an API can be authenticated using an AK/SK pair.

AK/SK Authentication
--------------------

An AK/SK is used to verify the identity of a request sender. In AK/SK authentication, a signature needs to be obtained and then added to requests.

.. note::

   AK: access key ID, which is a unique identifier used together with an SK to sign requests cryptographically.

   SK: secret access key, which is used together with an AK to sign requests cryptographically. It identifies a request sender and prevents the request from being modified.

The following demo shows how to sign a request and use an HTTP client to send an HTTPS request.

Download the demo at https://github.com/api-gate-way/SdkDemo.

If you do not need the demo project, visit the following URL to download the API Gateway signing SDK:

Request an API Gateway signing SDK from the enterprise administrator.

Decompress the downloaded package to obtain a JAR file. Add the decompressed JAR file to the dependency path, as shown below.


.. figure:: /_static/images/en-us_image_0000002302431869.png
   :alt: **Figure 1** Adding the API Gateway signing SDK

   **Figure 1** Adding the API Gateway signing SDK

#. Generate an AK/SK. (If you already have an AK/SK file, skip this step and find it. Generally, the file name is **credentials.csv**.)

   a. Log in to the console.
   b. Click the username and select **My Credentials** from the drop-down list.

   c. In the navigation tree on the left, click **Access Keys**.
   d. Click **Create Access Key**. The **Create Access Key** dialog box is displayed.
   e. Click **OK** to download the AK/SK.

      .. note::

         Keep the AK/SK secure.

#. Download and decompress the demo code.

#. .. _ucs_api_0009__en-us_topic_0121671869_li19564155663214:

   Import the demo project into Eclipse.


   .. figure:: /_static/images/en-us_image_0000002302431877.png
      :alt: **Figure 2** Selecting an existing project

      **Figure 2** Selecting an existing project


   .. figure:: /_static/images/en-us_image_0000002302518741.png
      :alt: **Figure 3** Selecting the decompressed demo code

      **Figure 3** Selecting the decompressed demo code


   .. figure:: /_static/images/en-us_image_0000002267861934.png
      :alt: **Figure 4** Example structure

      **Figure 4** Example structure

#. Sign the request.

   The request signing method is integrated in the JAR files imported in :ref:`3 <ucs_api_0009__en-us_topic_0121671869_li19564155663214>`. The request needs to be signed before it is sent. The signature will then be added as part of the HTTP header to the request.

   The demo code is classified into three classes:

   -  **AccessService**: an abstract class that merges the GET, POST, PUT, and DELETE methods into the **access** method
   -  **Demo**: an execution entry used to simulate the sending of GET, POST, PUT, and DELETE requests
   -  **AccessServiceImpl**: **access** method implementation, which contains the code required for communication with API Gateway

   a. Edit the main method in the **Demo.java** file and replace the bold text with actual values.

      If you use other methods such as POST, PUT, and DELETE, see the corresponding comment.

      Specify *region*, *serviceName*, *AK/SK*, and *URL* with actual values. In this demo, the URLs for accessing VPC resources are used.

      To obtain the project ID in the URLs, see :ref:`Obtaining a Project ID <ucs_api_0018>`.

      To obtain the endpoint, see "Regions and Endpoints".

      ::

         //TODO: Replace region with the name of the region in which the service to be accessed is located.
         private static final String region = "";

         //TODO: Replace vpc with the name of the service you want to access. For example, ecs, vpc, iam, and elb.
         private static final String serviceName = "";

         public static void main(String[] args) throws UnsupportedEncodingException
         {
         //TODO: Replace the AK and SK with those obtained on the My Credentials page.
         String ak = "ZIRRKMTWP******1WKNKB";
         String sk = "Us0mdMNHk******YrRCnW0ecfzl";

         //TODO: To specify a project ID (multi-project scenarios), add the X-Project-Id header.
         //TODO: To access a global service, such as IAM, DNS, CDN, and TMS, add the X-Domain-Id header to specify an account ID.
         //TODO: To add a header, find "Add special headers" in the AccessServiceImple.java file.

         //TODO: Test the API
         String url = "https://{Endpoint}/v1/{project_id}/vpcs";
         get(ak, sk, url);

         //TODO: When creating a VPC, replace {project_id} in postUrl with the actual value.
         //String postUrl = "https://serviceEndpoint/v1/{project_id}/cloudservers";
         //String postbody ="{\"vpc\": {\"name\": \"vpc\",\"cidr\": \"192.168.0.0/16\"}}";
         //post(ak, sk, postUrl, postbody);

         //TODO: When querying a VPC, replace {project_id} in url with the actual value.
         //String url = "https://serviceEndpoint/v1/{project_id}/vpcs/{vpc_id}";
         //get(ak, sk, url);

         //TODO: When updating a VPC, replace {project_id} and {vpc_id} in putUrl with the actual values.
         //String putUrl = "https://serviceEndpoint/v1/{project_id}/vpcs/{vpc_id}";
         //String putbody ="{\"vpc\":{\"name\": \"vpc1\",\"cidr\": \"192.168.0.0/16\"}}";
         //put(ak, sk, putUrl, putbody);

         //TODO: When deleting a VPC, replace {project_id} and {vpc_id} in deleteUrl with the actual values.
         //String deleteUrl = "https://serviceEndpoint/v1/{project_id}/vpcs/{vpc_id}";
         //delete(ak, sk, deleteUrl);
         }

   b. Compile and run the code to call an API.

      In the **Package Explorer** area on the left, right-click **Demo.java** and choose **Run AS** > **Java Application** from the shortcut menu to run the demo code.

      You can view the API calling logs on the console.
