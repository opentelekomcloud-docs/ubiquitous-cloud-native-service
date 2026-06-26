:original_name: ucs_api_0006.html

.. _ucs_api_0006:

Concepts
========

-  Domain

   A domain is created upon successful signing up. The domain has full access permissions for all of its cloud services and resources. It can be used to reset user passwords and grant user permissions. The domain is a payment entity, which should not be used directly to perform routine management. For security purposes, create Identity and Access Management (IAM) users and grant them permissions for routine management.

-  User

   An IAM user is created by an account in IAM to use cloud services. Each IAM user has its own identity credentials (password and access keys).

   You can view the domain name and IAM user ID on the **My Credentials** page. API authentication requires information such as the domain, username, and password.

-  Region

   A region is a geographic area in which cloud resources are deployed. Availability zones (AZs) in the same region can communicate with each other over an intranet, while AZs in different regions are isolated from each other. Deploying cloud resources in different regions can better suit certain user requirements or comply with local laws or regulations.

   For details, see Region and AZ.

-  AZ

   An AZ comprises one or more physical data centers equipped with independent ventilation, fire, water, and electricity facilities. Computing, network, storage, and other resources in an AZ are logically divided into multiple clusters. AZs within a region are interconnected using high-speed optical fibers to allow you to build cross-AZ high-availability systems.

-  Project

   A region corresponds to a project by default. Default projects are defined to group and physically isolate resources (including computing, storage, and network resources) across regions. Users can be granted permissions in a default project to access all resources under theirdomains in the region associated with the project. If you need more refined access control, create subprojects under a default project and create resources in subprojects. Then you can assign users the permissions required to access only the resources in the specific subprojects.


   .. figure:: /_static/images/en-us_image_0000002267758860.png
      :alt: **Figure 1** Project isolation model

      **Figure 1** Project isolation model

-  Enterprise project

   Enterprise projects group and manage resources across regions. Resources in different enterprise projects are logically isolated.

   For details about enterprise projects and about how to obtain enterprise project IDs, see *Enterprise Management User Guide*.
