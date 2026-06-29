:original_name: ucs_01_0017.html

.. _ucs_01_0017:

Overview
========

Introduction
------------

Cluster federation is a multi-cloud container orchestration capability provided by Karmada. Cluster federation aims to manage multi-cluster applications in cross-cloud and cross-region scenarios, with features such as unified multi-cluster management, application deployment, service discovery, and auto scaling.

Constraints
-----------

Only **OTC accounts** or users with the **UCS FullAccess** permissions can enable or disable cluster federation.

Usage
-----

:ref:`Figure 1 <ucs_01_0017__fig168485961715>` shows how to use cluster federation.

.. _ucs_01_0017__fig168485961715:

.. figure:: /_static/images/en-us_image_0000001682205542.png
   :alt: **Figure 1** Process of using cluster federation

   **Figure 1** Process of using cluster federation

Cluster federation is bound to fleets. To use cluster federation for multi-cluster management, perform the following operations:

-  :ref:`Connect the cluster to be managed to UCS <ucs_01_0200>` and :ref:`add it to a fleet <ucs_01_0004>`.
-  :ref:`Enable cluster federation <ucs_01_0018>` for the fleet and :ref:`use kubectl to connect the cluster to the federation <ucs_01_0320>`.
