:original_name: ucs_01_0013.html

.. _ucs_01_0013:

Kubernetes Resource Objects
===========================

By their application scope, Kubernetes resource objects can be categorized into namespace objects or cluster objects.

Namespace Level
---------------

Namespace is an isolation mechanism of Kubernetes and is used to categorize, filter, and manage any resource object in a cluster.

If different resource objects are placed in different namespaces, they are isolated from each other. For example, run the following command to obtain all pods:

.. code-block::

   kubectl get pod

The pod has a namespace, which defaults to **default**. To specify a namespace, run the following command:

.. code-block::

   kubectl get pod -n default

To obtain pods in all namespaces, run the following command:

.. code-block::

   kubectl get pod --all-namespaces

In this way, you can view all pods in the cluster.

.. code-block::

   $ kubectl get pod --all-namespaces
   NAMESPACE     NAME                                            READY   STATUS    RESTARTS   AGE
   default       nginx-dd9796d66-5chbr                           1/1     Running   0          3d1h
   default       nginx-dd9796d66-xl69p                           1/1     Running   0          15d
   default       sa-example                                      1/1     Running   0          10d
   kube-system   coredns-6fcd88c4c-k8rtf                         1/1     Running   0          48d
   kube-system   coredns-6fcd88c4c-z46p4                         1/1     Running   0          48d
   kube-system   everest-csi-controller-856f8bb679-42rgw         1/1     Running   1          48d
   kube-system   everest-csi-controller-856f8bb679-xs6dz         1/1     Running   0          48d
   kube-system   everest-csi-driver-mkpbv                        2/2     Running   0          48d
   kube-system   everest-csi-driver-v754w                        2/2     Running   0          48d
   kube-system   icagent-5p44q                                   1/1     Running   0          48d
   kube-system   icagent-jrlbl                                   1/1     Running   0          48d
   monitoring    alertmanager-alertmanager-0                     2/2     Running   0          29d
   monitoring    cluster-problem-detector-7788f94f64-thp6s       1/1     Running   0          29d
   monitoring    custom-metrics-apiserver-5f7dcf6d9-n5nrr        1/1     Running   0          19d
   monitoring    event-exporter-6844c5c685-khf5t                 1/1     Running   1          3d1h
   monitoring    kube-state-metrics-8566d5f5c5-7kx7b             1/1     Running   0          29d
   monitoring    node-exporter-7l4ml                             1/1     Running   0          29d
   monitoring    node-exporter-gpxvl                             1/1     Running   0          29d

Pods are namespace objects. Most workload resources, Service resources, and config and storage are also namespace objects.

-  **Workload resources**

   **Pod**: the smallest and simplest unit in the Kubernetes object model that you create or deploy.

   **ReplicaSet**: a backup controller in Kubernetes. It is used to control the managed pods so that the number of pod replicas remains the preset one.

   **Deployment**: declares the pod template and controls the pod running policy. It is applicable to the deployment of stateless applications.

   **StatefulSet**: manages stateful applications. Created pods have persistent identifiers created based on specifications.

   **DaemonSet**: used to deploy background programs in the resident cluster, for example, node log collection.

   **Job**: The job controller creates one or more pods. These pods run according to the running rules until the running is complete.

   **CronJob**: periodically runs a job based on a specified schedule.

-  **Service resources**

   **Service**: Containers deployed in Kubernetes provide Layer-7 network services using HTTP and HTTPS, and Layer-4 network services using TCP and UDP. Services in Kubernetes are used to manage Layer-4 network access in a cluster. Based on the Layer-4 network, Service exposes the container services in a cluster.

   **Ingress**: provides Layer-7 network services using HTTP and HTTPS and common Layer-7 network capabilities. An ingress is a set of rules that allow accessing Services in a cluster. You can configure forwarding rules to enable different URLs to access different Services in a cluster.

-  **Config and storage resources**

   **ConfigMap**: key-value pair, which is used to decouple configurations from running images so that applications more portable.

   **Secret**: key-value pair, which is used to store sensitive information such as passwords, tokens, and keys to reduce the risk of direct exposure.

   **Volume**: A volume is essentially a directory that may contain some data. Containers in a pod can access the directory. A volume will no longer exist if the pod to which it is mounted does not exist. However, files in the volume may outlive the volume, depending on the volume type.

Cluster Level
-------------

A cluster resource has a much larger application scope than a namespace resource. It is visible to the entire cluster and can be invoked. It does not belong to a certain namespace. Therefore, the name of a resource object must be globally unique.

Cluster resources are visible in any namespaces. You do not need to specify a namespace when defining cluster resources.

Cluster resources include Namespace, Node, Role, RoleBinding, ClusterRole, and ClusterRoleBinding.

-  **Namespace**: an isolation mechanism of Kubernetes and is used to categorize, filter, and manage any resource object in a cluster.

   To query all namespaces in a cluster, run the following command:

   .. code-block::

      kubectl get ns

-  **Node**: A node is a basic element of a container cluster and can be a VM or physical machine. The components on a node include kubelet and kube-proxy. A node name must be globally unique.

-  **Role**: defines a set of rules for accessing Kubernetes resources in a namespace.

-  **RoleBinding**: defines the relationship between users and roles.

-  **ClusterRole**: defines a set of rules for accessing Kubernetes resources in a cluster (including all namespaces).

-  **ClusterRoleBinding**: defines the relationship between users and cluster roles.

   .. note::

      Role and ClusterRole specify actions that can be performed on specific resources. RoleBinding and ClusterRoleBinding bind roles to specific users, user groups, or ServiceAccounts.
