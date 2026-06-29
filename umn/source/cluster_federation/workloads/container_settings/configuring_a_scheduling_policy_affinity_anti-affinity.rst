:original_name: ucs_01_0265.html

.. _ucs_01_0265:

Configuring a Scheduling Policy (Affinity/Anti-affinity)
========================================================

Kubernetes supports affinity and anti-affinity scheduling at the node and pod levels. You can configure custom rules to achieve affinity and anti-affinity scheduling. For example, you can deploy frontend pods and backend pods together, deploy the same type of applications on a specific node, or deploy different applications on different nodes.

Configuring Scheduling Policies
-------------------------------

#. Log in to the UCS console and go to the **Federation** page.
#. When creating a workload, click **Scheduling** in the **Advanced Settings** area.

   .. table:: **Table 1** Node affinity settings

      +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter | Description                                                                                                                                                                                                                                                                                  |
      +===========+==============================================================================================================================================================================================================================================================================================+
      | Required  | A hard rule that must be met for scheduling. It corresponds to **requiredDuringSchedulingIgnoredDuringExecution** in Kubernetes. You can add multiple required rules, and scheduling will be performed if any of them is met.                                                                |
      +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Preferred | A soft rule specifying preferences that the scheduler will try to enforce but will not guarantee. It corresponds to **preferredDuringSchedulingIgnoredDuringExecution** in Kubernetes. You can add multiple preferred rules, and scheduling will be performed if any or none of them is met. |
      +-----------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Under **Node affinity**, **Workload affinity**, and **Workload anti-affinity**, click |image1| to add scheduling policies.

   .. table:: **Table 2** Scheduling policy configuration

      +-----------------------------------+------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                |
      +===================================+============================================================================================================+
      | Label Key                         | Node label. You can use the default label or customize a label.                                            |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------+
      | Operator                          | The following relations are supported: **In**, **NotIn**, **Exists**, **DoesNotExist**, **Gt**, and **Lt** |
      |                                   |                                                                                                            |
      |                                   | -  **In**: A label exists in the label list.                                                               |
      |                                   | -  **NotIn**: A label does not exist in the label list.                                                    |
      |                                   | -  **Exists**: A specific label exists.                                                                    |
      |                                   | -  **DoesNotExist**: A specific label does not exist.                                                      |
      |                                   | -  **Gt**: The label value is greater than a specified value (string comparison).                          |
      |                                   | -  **Lt**: The label value is less than a specified value (string comparison).                             |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------+
      | Label Value                       | Label value.                                                                                               |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------+
      | Namespace                         | This parameter is available only in a workload affinity or anti-affinity scheduling policy.                |
      |                                   |                                                                                                            |
      |                                   | Namespace for which the scheduling policy takes effect.                                                    |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------+
      | Topology Key                      | This parameter is available only in a workload affinity or anti-affinity scheduling policy.                |
      |                                   |                                                                                                            |
      |                                   | Select the scope specified by **topologyKey** and then select the content defined by the policy.           |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------+
      | Weight                            | This parameter can be set only in a **Preferred** scheduling policy.                                       |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------+

Node Affinity (nodeAffinity)
----------------------------

In the pod template, you can configure **nodeSelector** to create a pod on a node with a specified label. The following example shows how to use a nodeSelector to deploy pods only on the nodes with the **gpu=true** label.

.. code-block::

   apiVersion: v1
   kind: Pod
   metadata:
     name: nginx
   spec:
     nodeSelector:                 # Node selection. A pod is deployed only on the node with the gpu=true label.
       gpu: true
   ...

You can also use node affinity to do so.

.. code-block::

   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name:  gpu
     labels:
       app:  gpu
   spec:
     selector:
       matchLabels:
         app: gpu
     replicas: 3
     template:
       metadata:
         labels:
           app:  gpu
       spec:
         containers:
         - image:  nginx:alpine
           name:  gpu
           resources:
             requests:
               cpu: 100m
               memory: 200Mi
             limits:
               cpu: 100m
               memory: 200Mi
         imagePullSecrets:
         - name: default-secret
         affinity:
           nodeAffinity:
             requiredDuringSchedulingIgnoredDuringExecution:
               nodeSelectorTerms:
               - matchExpressions:
                 - key: gpu
                   operator: In
                   values:
                   - "true"

A node affinity rule contains more lines, but it is more expressive.

**requiredDuringSchedulingIgnoredDuringExecution** seems to be complex, but it can be easily understood as a combination of two parts.

-  **requiredDuringScheduling** indicates that pods can be scheduled to the node only when all the defined selector rules are met.
-  **IgnoredDuringExecution** means that if the node labels change after Kubernetes schedules the pod, the pod continues to run.

In addition, the operator **In** indicates that the label value must fall in the range specified by **values**. Other available operator values are as follows:

-  **NotIn**: The label value is not in the specified list.
-  **Exists**: A specific label exists.
-  **DoesNotExist**: A specific label does not exist.
-  **Gt**: The label value is greater than a specified value (string comparison).
-  **Lt**: The label value is less than a specified value (string comparison).

Note that there is no such thing as nodeAntiAffinity because operators **NotIn** and **DoesNotExist** provide the same function.

The following describes how to check whether the rule takes effect. Assume that a cluster has three nodes.

.. code-block::

   $ kubectl get node
   NAME            STATUS   ROLES    AGE   VERSION
   192.168.0.212   Ready    <none>   13m   v1.15.6-r1-20.3.0.2.B001-15.30.2
   192.168.0.94    Ready    <none>   13m   v1.15.6-r1-20.3.0.2.B001-15.30.2
   192.168.0.97    Ready    <none>   13m   v1.15.6-r1-20.3.0.2.B001-15.30.2

Add the **gpu=true** label to the **192.168.0.212** node.

.. code-block::

   $ kubectl label node 192.168.0.212 gpu=true
   node/192.168.0.212 labeled

   $ kubectl get node -L gpu
   NAME            STATUS   ROLES    AGE   VERSION                            GPU
   192.168.0.212   Ready    <none>   13m   v1.15.6-r1-20.3.0.2.B001-15.30.2   true
   192.168.0.94    Ready    <none>   13m   v1.15.6-r1-20.3.0.2.B001-15.30.2
   192.168.0.97    Ready    <none>   13m   v1.15.6-r1-20.3.0.2.B001-15.30.2

Create the Deployment. You can find that all pods are deployed on the **192.168.0.212** node.

.. code-block::

   $ kubectl create -f affinity.yaml
   deployment.apps/gpu created

   $ kubectl get pod -o wide
   NAME                     READY   STATUS    RESTARTS   AGE   IP            NODE
   gpu-6df65c44cf-42xw4     1/1     Running   0          15s   172.16.0.37   192.168.0.212
   gpu-6df65c44cf-jzjvs     1/1     Running   0          15s   172.16.0.36   192.168.0.212
   gpu-6df65c44cf-zv5cl     1/1     Running   0          15s   172.16.0.38   192.168.0.212

Node Preference Rule
--------------------

The preceding **requiredDuringSchedulingIgnoredDuringExecution** rule is a hard rule. The other type, or a soft rule, is **preferredDuringSchedulingIgnoredDuringExecution**, which specifies which nodes are preferred during scheduling.

To achieve this effect, add a node with SSD disks installed to the cluster, add the **DISK=SSD** label to the node, and add the **DISK=SAS** label to another three nodes.

.. code-block::

   $ kubectl get node -L DISK,gpu
   NAME            STATUS   ROLES    AGE     VERSION                            DISK     GPU
   192.168.0.100   Ready    <none>   7h23m   v1.15.6-r1-20.3.0.2.B001-15.30.2   SSD
   192.168.0.212   Ready    <none>   8h      v1.15.6-r1-20.3.0.2.B001-15.30.2   SAS      true
   192.168.0.94    Ready    <none>   8h      v1.15.6-r1-20.3.0.2.B001-15.30.2   SAS
   192.168.0.97    Ready    <none>   8h      v1.15.6-r1-20.3.0.2.B001-15.30.2   SAS

Define a Deployment. Use the **preferredDuringSchedulingIgnoredDuringExecution** rule to set the weight of nodes with the SSD disk installed as **80** and nodes with the **gpu=true** label as **20**. In this way, pods are preferentially deployed on the nodes with the SSD disk installed.

.. code-block::

   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name:  gpu
     labels:
       app:  gpu
   spec:
     selector:
       matchLabels:
         app: gpu
     replicas: 10
     template:
       metadata:
         labels:
           app:  gpu
       spec:
         containers:
         - image:  nginx:alpine
           name:  gpu
           resources:
             requests:
               cpu:  100m
               memory:  200Mi
             limits:
               cpu:  100m
               memory:  200Mi
         imagePullSecrets:
         - name: default-secret
         affinity:
           nodeAffinity:
             preferredDuringSchedulingIgnoredDuringExecution:
             - weight: 80
               preference:
                 matchExpressions:
                 - key: DISK
                   operator: In
                   values:
                   - SSD
             - weight: 20
               preference:
                 matchExpressions:
                 - key: gpu
                   operator: In
                   values:
                   - "true"

After the deployment, you can find that five pods are deployed on the **192.168.0.212** node, and two pods are deployed on the **192.168.0.100** node.

.. code-block::

   $ kubectl create -f affinity2.yaml
   deployment.apps/gpu created

   $ kubectl get po -o wide
   NAME                   READY   STATUS    RESTARTS   AGE     IP            NODE
   gpu-585455d466-5bmcz   1/1     Running   0          2m29s   172.16.0.44   192.168.0.212
   gpu-585455d466-cg2l6   1/1     Running   0          2m29s   172.16.0.63   192.168.0.97
   gpu-585455d466-f2bt2   1/1     Running   0          2m29s   172.16.0.79   192.168.0.100
   gpu-585455d466-hdb5n   1/1     Running   0          2m29s   172.16.0.42   192.168.0.212
   gpu-585455d466-hkgvz   1/1     Running   0          2m29s   172.16.0.43   192.168.0.212
   gpu-585455d466-mngvn   1/1     Running   0          2m29s   172.16.0.48   192.168.0.97
   gpu-585455d466-s26qs   1/1     Running   0          2m29s   172.16.0.62   192.168.0.97
   gpu-585455d466-sxtzm   1/1     Running   0          2m29s   172.16.0.45   192.168.0.212
   gpu-585455d466-t56cm   1/1     Running   0          2m29s   172.16.0.64   192.168.0.100
   gpu-585455d466-t5w5x   1/1     Running   0          2m29s   172.16.0.41   192.168.0.212

In the preceding example, the node scheduling priority is as follows. Nodes with both **SSD** and **gpu=true** labels have the highest priority. Nodes with the **SSD** label but no **gpu=true** label have the second priority (weight: 80). Nodes with the **gpu=true** label but no **SSD** label have the third priority. Nodes without any of these two labels have the lowest priority.


.. figure:: /_static/images/en-us_image_0000001503659388.png
   :alt: **Figure 1** Scheduling priority

   **Figure 1** Scheduling priority

From the preceding output, you can find that no pods of the Deployment are scheduled to node **192.168.0.94**. This is because the node already has many pods on it and its resource usage is high. This also indicates that the **preferredDuringSchedulingIgnoredDuringExecution** rule defines a preference rather than a hard requirement.

Workload Affinity (podAffinity)
-------------------------------

Node affinity rules affect only the affinity between pods and nodes. Kubernetes also supports configuring inter-pod affinity rules. For example, the frontend and backend of an application can be deployed together on one node to reduce access latency. There are also two types of inter-pod affinity rules: **requiredDuringSchedulingIgnoredDuringExecution** and **preferredDuringSchedulingIgnoredDuringExecution**.

Assume that the backend of an application has been created and has the **app=backend** label.

.. code-block::

   $ kubectl get po -o wide
   NAME                       READY   STATUS    RESTARTS   AGE     IP            NODE
   backend-658f6cb858-dlrz8   1/1     Running   0          2m36s   172.16.0.67   192.168.0.100

You can configure the following pod affinity rule to deploy the frontend pods of the application to the same node as the backend pods.

.. code-block::

   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name:   frontend
     labels:
       app:  frontend
   spec:
     selector:
       matchLabels:
         app: frontend
     replicas: 3
     template:
       metadata:
         labels:
           app:  frontend
       spec:
         containers:
         - image:  nginx:alpine
           name:  frontend
           resources:
             requests:
               cpu:  100m
               memory:  200Mi
             limits:
               cpu:  100m
               memory:  200Mi
         imagePullSecrets:
         - name: default-secret
         affinity:
           podAffinity:
             requiredDuringSchedulingIgnoredDuringExecution:
             - topologyKey: kubernetes.io/hostname
               labelSelector:
                 matchExpressions:
                 - key: app
                   operator: In
                   values:
                   - backend

Deploy the frontend and you can find that the frontend is deployed on the same node as the backend.

.. code-block::

   $ kubectl create -f affinity3.yaml
   deployment.apps/frontend created

   $ kubectl get po -o wide
   NAME                        READY   STATUS    RESTARTS   AGE     IP            NODE
   backend-658f6cb858-dlrz8    1/1     Running   0          5m38s   172.16.0.67   192.168.0.100
   frontend-67ff9b7b97-dsqzn   1/1     Running   0          6s      172.16.0.70   192.168.0.100
   frontend-67ff9b7b97-hxm5t   1/1     Running   0          6s      172.16.0.71   192.168.0.100
   frontend-67ff9b7b97-z8pdb   1/1     Running   0          6s      172.16.0.72   192.168.0.100

The **topologyKey** field specifies the selection range. The scheduler selects nodes within the range based on the affinity rule defined. The effect of **topologyKey** is not fully demonstrated in the preceding example because all the nodes have the **kubernetes.io/hostname** label, that is, all the nodes are within the range.

To see how **topologyKey** works, assume that the backend of the application has two pods, which are running on different nodes.

.. code-block::

   $ kubectl get po -o wide
   NAME                       READY   STATUS    RESTARTS   AGE     IP            NODE
   backend-658f6cb858-5bpd6   1/1     Running   0          23m     172.16.0.40   192.168.0.97
   backend-658f6cb858-dlrz8   1/1     Running   0          2m36s   172.16.0.67   192.168.0.100

Add the **prefer=true** label to nodes **192.168.0.97** and **192.168.0.94**.

.. code-block::

   $ kubectl label node 192.168.0.97 prefer=true
   node/192.168.0.97 labeled
   $ kubectl label node 192.168.0.94 prefer=true
   node/192.168.0.94 labeled

   $ kubectl get node -L prefer
   NAME            STATUS   ROLES    AGE   VERSION                            PREFER
   192.168.0.100   Ready    <none>   44m   v1.15.6-r1-20.3.0.2.B001-15.30.2
   192.168.0.212   Ready    <none>   91m   v1.15.6-r1-20.3.0.2.B001-15.30.2
   192.168.0.94    Ready    <none>   91m   v1.15.6-r1-20.3.0.2.B001-15.30.2   true
   192.168.0.97    Ready    <none>   91m   v1.15.6-r1-20.3.0.2.B001-15.30.2   true

Define **topologyKey** in the **podAffinity** section as **prefer**.

.. code-block::

         affinity:
           podAffinity:
             requiredDuringSchedulingIgnoredDuringExecution:
             - topologyKey: prefer
               labelSelector:
                 matchExpressions:
                 - key: app
                   operator: In
                   values:
                   - backend

The scheduler recognizes the nodes with the **prefer** label, that is, **192.168.0.97** and **192.168.0.94**, and then finds the pods with the **app=backend** label. In this way, all frontend pods are deployed onto **192.168.0.97**.

.. code-block::

   $ kubectl create -f affinity3.yaml
   deployment.apps/frontend created

   $ kubectl get po -o wide
   NAME                        READY   STATUS    RESTARTS   AGE     IP            NODE
   backend-658f6cb858-5bpd6    1/1     Running   0          26m     172.16.0.40   192.168.0.97
   backend-658f6cb858-dlrz8    1/1     Running   0          5m38s   172.16.0.67   192.168.0.100
   frontend-67ff9b7b97-dsqzn   1/1     Running   0          6s      172.16.0.70   192.168.0.97
   frontend-67ff9b7b97-hxm5t   1/1     Running   0          6s      172.16.0.71   192.168.0.97
   frontend-67ff9b7b97-z8pdb   1/1     Running   0          6s      172.16.0.72   192.168.0.97

Workload Anti-Affinity (podAntiAffinity)
----------------------------------------

Unlike the scenarios in which pods are preferred to be scheduled onto the same node, sometimes, it could be the exact opposite. For example, if certain pods are deployed together, they will affect the performance.

The following example defines an inter-pod anti-affinity rule, which specifies that pods must not be scheduled to nodes that already have pods with the **app=frontend** label, that is, to deploy the pods of the frontend to different nodes with each node has only one replica.

.. code-block::

   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name:   frontend
     labels:
       app:  frontend
   spec:
     selector:
       matchLabels:
         app: frontend
     replicas: 5
     template:
       metadata:
         labels:
           app:  frontend
       spec:
         containers:
         - image:  nginx:alpine
           name:  frontend
           resources:
             requests:
               cpu:  100m
               memory:  200Mi
             limits:
               cpu:  100m
               memory:  200Mi
         imagePullSecrets:
         - name: default-secret
         affinity:
           podAntiAffinity:
             requiredDuringSchedulingIgnoredDuringExecution:
             - topologyKey: kubernetes.io/hostname
               labelSelector:
                 matchExpressions:
                 - key: app
                   operator: In
                   values:
                   - frontend

Deploy the frontend and query the deployment results. You can find that each node has only one frontend pod and one pod of the Deployment is **Pending**. This is because when the scheduler is deploying the fifth pod, all nodes already have one pod with the **app=frontend** label on them. There is no available node. Therefore, the fifth pod will remain in the **Pending** status.

.. code-block::

   $ kubectl create -f affinity4.yaml
   deployment.apps/frontend created

   $ kubectl get po -o wide
   NAME                        READY   STATUS    RESTARTS   AGE   IP            NODE
   frontend-6f686d8d87-8dlsc   1/1     Running   0          18s   172.16.0.76   192.168.0.100
   frontend-6f686d8d87-d6l8p   0/1     Pending   0          18s   <none>        <none>
   frontend-6f686d8d87-hgcq2   1/1     Running   0          18s   172.16.0.54   192.168.0.97
   frontend-6f686d8d87-q7cfq   1/1     Running   0          18s   172.16.0.47   192.168.0.212
   frontend-6f686d8d87-xl8hx   1/1     Running   0          18s   172.16.0.23   192.168.0.94

.. |image1| image:: /_static/images/en-us_image_0000001554898973.png
