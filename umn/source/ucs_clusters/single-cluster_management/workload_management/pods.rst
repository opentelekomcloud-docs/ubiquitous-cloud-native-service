:original_name: ucs_01_0108.html

.. _ucs_01_0108:

Pods
====

A pod is the smallest and simplest unit in the Kubernetes object model that you create or deploy. A pod encapsulates an application's container (or, in some cases, multiple containers), storage resources, a unique network identity (IP address), as well as options that govern how the container(s) should run. A pod represents a single instance of an application in Kubernetes, which might consist of either a single container or a small number of containers that are tightly coupled and that share resources.

Creating a Pod from a YAML File
-------------------------------

#. Log in to the UCS console and access the cluster console. Choose **Workloads** > **Pods** and click **Create from YAML**.
#. On the displayed **Create from YAML** page, edit the YAML file.
#. Click **OK**.

Related Operations
------------------

-  **View Events**: You can set search criteria, such as the time segment during which an event is generated or the event name, to view related events.
-  **View Containers**: You can view the container name, status, image, and restarts of the pod.
-  **View YAML**: You can view the YAML file of the pod.
