:original_name: ucs_01_0411.html

.. _ucs_01_0411:

Overview
========

Constraints
-----------

-  Currently, north-south MCS does not forward the traffic of Services whose network protocol is UDP.
-  North-south MCS is of the LoadBalancer type.

North-South MCS Function
------------------------

North-south MCS can expose the Layer 4 access entry of a Service in a cluster to a load balancer. You can use the listening port on the load balancer to access this Service over the public or private network.

How North-South MCS Works
-------------------------

The North-south MCS function is implemented by MCS Controller. MCS Controller is deployed on the federation control plane to monitor resource object changes in real time, parse rules defined by MCS objects, and forward requests to backend services.

.. _ucs_01_0411__fig34885441251:

.. figure:: /_static/images/en-us_image_0000002053985625.png
   :alt: **Figure 1** Working principle of north-south MCS

   **Figure 1** Working principle of north-south MCS

MCI Controller allows you to configure multiple listener ports for the same load balancer. :ref:`Figure 1 <ucs_01_0411__fig34885441251>` shows the working principle.

#. The deployment personnel create a workload on the federation control plane and configure a Service object for the workload.
#. The deployment personnel create an MCS object on the federation control plane and configure the load balancer and backend service and port.
#. When detecting that the MCS object changes, MCS Controller reconfigures the listener and backend server route on the ELB side according to the traffic access rule defined in MCS.
#. When a user accesses workloads, the traffic is forwarded to the corresponding backend service over the listening port, and then forwarded to each associated workload through the Service.
