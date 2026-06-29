:original_name: ucs_01_0275.html

.. _ucs_01_0275:

DNS Policies
============

Applications deployed in different clusters can be accessed using a unified public domain name. After you configure a public domain name, UCS can use it as a root domain name to generate a complete domain name for applications. You can configure a DNS policy to interconnect a Service and ingress with DNS so that applications deployed across clusters can be accessed through the unified public domain name. In addition, you can create custom traffic distribution ratio to suit your needs.

Configuring a Domain Name
-------------------------

Before configuring domain name access for an application, ensure that the domain name has been registered with the domain name service provider and licensed. Otherwise, the domain name cannot be accessed.

If you have a registered and licensed domain name, go to :ref:`3 <ucs_01_0275__li184348548298>` to add record sets.

If you do not register a domain name, `create a public zone <https://docs.otc.t-systems.com/domain-name-service/umn/public_zones/creating_a_public_zone.html>`__ and complete the ICP filing, resolution, and configuration of the domain name as prompted. The procedure for domain name registration and licensing is as follows:

#. Create a public zone. for example, **ucsclub.cn**.

   -  If you do not create a public zone, `create one <https://docs.otc.t-systems.com/domain-name-service/umn/public_zones/creating_a_public_zone.html>`__.
   -  If you have created a public zone, go to :ref:`2 <ucs_01_0275__li126612364299>`.

#. .. _ucs_01_0275__li126612364299:

   Complete the ICP filing.

   -  If your domain name does not been licensed, apply for ICP filing using ICP License Service.
   -  If your domain name has been licensed, go to :ref:`3 <ucs_01_0275__li184348548298>`.

#. .. _ucs_01_0275__li184348548298:

   Add record sets.

   -  If you do not add record sets, `add ones <https://docs.otc.t-systems.com/domain-name-service/umn/record_sets/record_set_overview.html>`__.
   -  If you have added record sets, go to :ref:`4 <ucs_01_0275__li627472211317>`.

#. .. _ucs_01_0275__li627472211317:

   Configure the domain name.

   Select the domain name and configure it.

Creating a DNS Policy
---------------------

After a Deployment is created, you can click **Create Service** to create a Service of the LoadBalancer type so that the Deployment can provide services for external systems. On the page indicating that the LoadBalancer Service is created, click **Create DNS Policy**.

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.
#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its details page.
#. Choose **DNS Policies** in the navigation pane, and click **Create DNS Policy**.
#. Set parameters of the associated Service.

   -  **Namespace**: Select a namespace.
   -  **Target Service**: Select a target Service. If no LoadBalancer Service is available, create one first. For details about how to create a Service, see :ref:`LoadBalancer <ucs_01_0273>`.

#. Click **Next** and set the access mode.

   -  **Active/Standby**: The traffic will be distributed only to the selected active cluster. You can change the traffic ratio to change the role of active and standby clusters.
   -  **Adaptive**: The traffic is automatically distributed based on the number of pods in each cluster. In addition, you can enable region affinity to allow users in a specific region to access a specific cluster.
   -  **Custom**: You can create custom traffic distribution ratio for each cluster. In addition, you can enable region affinity to allow users in a specific region to access a specific cluster.

#. Click **Create DNS Policy**. The creation task will take a period of time. You can click **Back to DNS Policies** or **View DNS Policy Details** to view the created DNS policy.

Modifying an Alias
------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.
#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its details page.
#. Choose **DNS Policies** in the navigation pane and click the name of a policy to access its details page.
#. Click |image1|, enter an alias, and click |image2|.

Modifying the Traffic Distribution Ratio
----------------------------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.
#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its details page.
#. Choose **DNS Policies** in the navigation pane and click the name of a policy to access its details page.
#. On the topology tab, click **Edit**.
#. Modify parameters and click **OK**.

Viewing the DNS Policy Address
------------------------------

After a DNS policy is created, you can view its address in the DNS policy list.

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.
#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its details page.
#. Choose **DNS Policies** in the navigation pane. In the DNS policy list, view the value in the **Domain Name** column.

Deleting a DNS Policy
---------------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.
#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its details page.
#. Click **Delete** in the **Operation** column of the target DNS policy.
#. In the **Delete DNS Policy** dialog box, click **Yes**.

.. |image1| image:: /_static/images/en-us_image_0000001503680580.png
.. |image2| image:: /_static/images/en-us_image_0000001554800229.png
