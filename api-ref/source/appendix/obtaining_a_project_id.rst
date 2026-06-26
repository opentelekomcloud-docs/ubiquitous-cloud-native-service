:original_name: ucs_api_0018.html

.. _ucs_api_0018:

Obtaining a Project ID
======================

Scenarios
---------

A project ID is required for some URLs when an API is called. Therefore, you need to obtain a project ID in advance. Two methods are available:

-  :ref:`Call an API <ucs_api_0018__en-us_topic_0121673684_section86806471133>`.
-  :ref:`Use the console <ucs_api_0018__en-us_topic_0121673684_section32975495318>`.

.. _ucs_api_0018__en-us_topic_0121673684_section86806471133:

Obtaining a Project ID by Calling an API
----------------------------------------

You can obtain the project ID by calling the IAM API used to query project information based on the specified criteria.

The API used to obtain a project ID is **GET https://**\ *{Endpoint}*\ **/v3/projects**. *{Endpoint}* is the IAM endpoint and can be obtained from the administrator\ `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/additional/endpoints.html>`__. For details about API authentication, see :ref:`Authentication <ucs_api_0009>`.

The following is an example response. The value of **id** is the project ID.

.. code-block::

   {
       "projects": [
           {
               "domain_id": "65382450e8f64ac0870cd180d14e684b",
               "is_domain": false,
               "parent_id": "65382450e8f64ac0870cd180d14e684b",
               "name": "project_name",
               "description": "",
               "links": {
                   "next": null,
                   "previous": null,
                   "self": "https://www.example.com/v3/projects/a4a5d4098fb4474fa22cd05f897d6b99"
               },
               "id": "a4a5d4098fb4474fa22cd05f897d6b99",
               "enabled": true
           }
       ],
       "links": {
           "next": null,
           "previous": null,
           "self": "https://www.example.com/v3/projects"
       }
   }

.. _ucs_api_0018__en-us_topic_0121673684_section32975495318:

Obtaining a Project ID on the Console
-------------------------------------

A project ID needs to be specified in the URIs of some APIs. Therefore, you need to obtain the project ID before calling APIs. The following procedure describes how to obtain a project ID:

#. Log in to the management console.

#. Click the username and select **My Credentials** from the drop-down list.

   On the **My Credentials** page, view project IDs in the project list.


   .. figure:: /_static/images/en-us_image_0000002302518757.png
      :alt: **Figure 1** Viewing project IDs

      **Figure 1** Viewing project IDs

   In multi-project scenarios, expand the region, and obtain your sub-project ID from the **Project ID** column.
