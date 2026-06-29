:original_name: ucs_01_0320.html

.. _ucs_01_0320:

Using kubectl to Connect to a Federation
========================================

This section describes how you can use kubectl to connect to a federation.

Permissions
-----------

When you use kubectl to connect to a federation, UCS uses **kubeconfig.json** generated on the federation for authentication. This file contains user information, based on which UCS determines which Kubernetes resources can be accessed by kubectl. The permissions recorded in a **kubeconfig.json** file vary from user to user.

Constraints
-----------

-  For security purposes, the federation API server does not have a public IP address. UCS creates an endpoint in your VPC and subnet and connects the endpoint to the federation API server for the access to the federation. For each federation, only one endpoint is created in the same VPC. If a VPC already has an endpoint for connecting to the federation API server, the endpoint will be reused.

Prerequisites
-------------

-  Before using kubectl to connect to a federation, ensure that the federation has been enabled (:ref:`Enabling Cluster Federation <ucs_01_0018>`) and is running normally.
-  Only the client in a VPC can connect to a federation using kubectl. If there is no client in the VPC, create one.
-  kubectl has been downloaded and uploaded to the client. For details about how to download kubectl, see `Kubernetes releases <https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/README.md>`__.
-  At least the custom policy **iam:clustergroups:get** has been created.


Using kubectl to Connect to a Federation
----------------------------------------

#. Log in to the UCS console and click the fleet name to access the fleet console. Then, click **kubectl** in **Fleet Info**.

#. Select a project, VPC, master node subnet, and validity period as prompted and click **Download** to download the kubectl configuration file.

   The name of the downloaded file is *{Fleet name}*\ **\_kubeconfig.json**.

#. Install and configure kubectl on the executor.

   a. Copy kubectl and its configuration file to the **/home** directory on the executor in the selected VPC and subnet.

   b. Log in to your executor and configure kubectl.

      .. code-block::

         cd /home
         chmod +x kubectl
         mv -f kubectl /usr/local/bin
         mkdir -p $HOME/.kube
         mv -f <fleet-name>_kubeconfig.json $HOME/.kube/config   --Change the fleet name in the command to the actual fleet name.
