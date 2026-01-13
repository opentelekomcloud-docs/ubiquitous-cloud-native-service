:original_name: ucs_01_0262.html

.. _ucs_01_0262:

Setting Health Check for a Container
====================================

Scenarios
---------

Health check regularly checks the health status of containers during container running. If the health check function is not configured, a pod cannot detect application exceptions or automatically restart the application to restore it. This will result in a situation where the pod status is normal but the application in the pod is abnormal.

Kubernetes provides the following health check probes:

-  **Liveness probe** (livenessProbe): checks whether a container is still alive. It is similar to the **ps** command that checks whether a process exists. If the liveness check of a container fails, the cluster restarts the container. If the liveness check is successful, no operation is executed.
-  **Readiness probe** (readinessProbe): checks whether a container is ready to process user requests. Upon that the container is detected unready, service traffic will not be directed to the container. It may take a long time for some applications to start up before they can provide services. This is because that they need to load disk data or rely on startup of an external module. In this case, the application process is running, but the application cannot provide services. To address this issue, this health check probe is used. If the container readiness check fails, the cluster masks all requests sent to the container. If the container readiness check is successful, the container can be accessed.

Check Methods
-------------

-  **HTTP request**

   This health check mode can be used for containers that provide HTTP/HTTPS services. The cluster periodically initiates an HTTP/HTTPS GET request to such containers. If the return code of the HTTP/HTTPS response is within 200-399, the probe is successful. Otherwise, the probe fails. In this health check mode, you must specify a container listening port and an HTTP/HTTPS request path.

-  **TCP**

   For a container that provides TCP communication services, the cluster periodically establishes a TCP connection to the container. If the connection is successful, the probe is successful. Otherwise, the probe fails. In this health check mode, you must specify a container listening port.

   For example, if you have a Nginx container with service port 80, after you specify TCP port 80 for container listening, the cluster will periodically initiate a TCP connection to port 80 of the container. If the connection is successful, the probe is successful. Otherwise, the probe fails.

-  **Command**

   CLI is an efficient tool for health check. When using the CLI, you must specify an executable command in a container. The cluster periodically runs the command in the container. If the command output is 0, the health check is successful. Otherwise, the health check fails.

   The CLI mode can be used to replace the HTTP request-based and TCP port-based health check.

   -  For a TCP port, you can use a script to connect to a container port. If the connection is successful, the script returns **0**. Otherwise, the script returns **-1**.

   -  For an HTTP request, you can use a script to run the **wget** command for a container.

      **wget http://127.0.0.1:80/health-check**

      Check the return code of the response. If the return code is within 200-399, the script returns **0**. Otherwise, the script returns **-1**.

      .. important::

         -  Put the program to be executed in the container image so that the program can be executed.
         -  If the command to be executed is a shell script, do not directly specify the script as the command, but add a script parser. For example, if the script is **/data/scripts/health_check.sh**, the program is **sh/data/scripts/health_check.sh**. The reason is that the cluster is not in the terminal environment when executing programs in a container.

Common Parameters
-----------------

.. table:: **Table 1** Common parameters

   +------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                                | Description                                                                                                                                                                                                                                                       |
   +==========================================+===================================================================================================================================================================================================================================================================+
   | **Period** (periodSeconds)               | Probe detection period, in seconds.                                                                                                                                                                                                                               |
   |                                          |                                                                                                                                                                                                                                                                   |
   |                                          | For example, if this parameter is set to **30**, the detection is performed every 30 seconds.                                                                                                                                                                     |
   +------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Delay** (initialDelaySeconds)          | Check delay time in seconds. Set this parameter according to the normal startup time of services.                                                                                                                                                                 |
   |                                          |                                                                                                                                                                                                                                                                   |
   |                                          | For example, if this parameter is set to 30, the health check will be started 30 seconds after the container is started. The time is reserved for containerized services to start.                                                                                |
   +------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Timeout** (timeoutSeconds)             | Timeout duration. Unit: second.                                                                                                                                                                                                                                   |
   |                                          |                                                                                                                                                                                                                                                                   |
   |                                          | For example, if this parameter is set to **10**, the timeout wait time for performing a health check is 10s. If the wait time elapses, the health check is regarded as a failure. If the parameter is left blank or set to **0**, the default timeout time is 1s. |
   +------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Success Threshold** (successThreshold) | Minimum consecutive successes for the probe to be considered successful after having failed.                                                                                                                                                                      |
   |                                          |                                                                                                                                                                                                                                                                   |
   |                                          | The default value is **1**, which is also the minimum value.                                                                                                                                                                                                      |
   |                                          |                                                                                                                                                                                                                                                                   |
   |                                          | The value of this parameter is fixed to **1** in **Liveness Probe**.                                                                                                                                                                                              |
   +------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Failure Threshold** (failureThreshold) | Number of retry times when the detection fails.                                                                                                                                                                                                                   |
   |                                          |                                                                                                                                                                                                                                                                   |
   |                                          | Giving up in case of liveness probe means to restart the container. In case of readiness probe the pod will be marked **Unready**.                                                                                                                                |
   |                                          |                                                                                                                                                                                                                                                                   |
   |                                          | The default value is **3**, and the minimum value is **1**.                                                                                                                                                                                                       |
   +------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

YAML Example
------------

.. code-block::

   apiVersion: v1
   kind: Pod
   metadata:
     labels:
       test: liveness
     name: liveness-http
   spec:
     containers:
     - name: liveness
       image: nginx:alpine
       args:
       - /server
       livenessProbe:
         httpGet:
           path: /healthz
           port: 80
           httpHeaders:
           - name: Custom-Header
             value: Awesome
         initialDelaySeconds: 3
         periodSeconds: 3
       readinessProbe:
         exec:
           command:
             - cat
             - /tmp/healthy
         initialDelaySeconds: 5
         periodSeconds: 5
