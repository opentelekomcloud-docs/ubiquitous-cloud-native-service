:original_name: ucs_01_0115.html

.. _ucs_01_0115:

Creating a Secret
=================

A secret is a type of resource that holds sensitive data, such as authentication and key information, required by a workload. Its content is user-defined. After creating secrets, you can use them as files or environment variables in a containerized workload.


Creating a Secret
-----------------

#. Log in to the UCS console and access the cluster console.

#. In the navigation pane, choose **ConfigMaps and Secrets**. Click the **Secrets** tab. You can create a secret directly or using YAML. If you want to create a secret using YAML, go to :ref:`5 <ucs_01_0115__en-us_topic_0160121211_li69121840101813>`.

#. Select the namespace that the secret will belong to.

#. Click **Create Secret**.

   Configure the parameters as described in :ref:`Table 1 <ucs_01_0115__en-us_topic_0160121211_table16321825732>`.

   .. _ucs_01_0115__en-us_topic_0160121211_table16321825732:

   .. table:: **Table 1** Parameters for creating a secret

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                         |
      +===================================+=====================================================================================================================================================================================================================================================================================================================+
      | Name                              | Name of the secret you create, which must be unique in a namespace.                                                                                                                                                                                                                                                 |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Namespace                         | Namespace that the secret belongs to. The current namespace is used by default.                                                                                                                                                                                                                                     |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Description of the secret.                                                                                                                                                                                                                                                                                          |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Secret Type                       | Type of the secret.                                                                                                                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                                     |
      |                                   | -  **Opaque**: a general-purpose secret. In high-sensitive scenarios, you are advised to encrypt sensitive data using Data Encryption Workshop (DEW) and then store the encrypted data in secrets.                                                                                                                  |
      |                                   | -  **kubernetes.io/dockerconfigjson**: a secret that stores the authentication information required for pulling images from a private repository. If you select this secret type, enter the image repository address.                                                                                               |
      |                                   | -  **IngressTLS**: a secret that stores the certificate required for Layer 7 load balancing. If you select this secret type, upload the certificate file and private key file.                                                                                                                                      |
      |                                   | -  **Other**: another type of secret, which is specified manually.                                                                                                                                                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Data                              | Workload secret data can be used in containers.                                                                                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                                     |
      |                                   | -  If the secret type is **Opaque**, enter the key and value. The value must be a Base64-encoded value. You can select **Auto Base64 Encoding** to Base64-encode the entered value. For details about manual Base64 encoding, see :ref:`Base64 Encoding <ucs_01_0115__en-us_topic_0160121211_section175000605919>`. |
      |                                   | -  If the secret type is **kubernetes.io/dockerconfigjson**, enter the username and password of the private image repository.                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                                     |
      |                                   |    .. note::                                                                                                                                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                                     |
      |                                   |       Secrets can be used to create workload storage volumes and configure workload environment variables. When configuring workload environment variables, ensure that the secret data is not empty.                                                                                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Labels                            | Labels are attached to objects such as workloads, nodes, and Services in key-value pairs.                                                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                                     |
      |                                   | Labels define the identifiable attributes of these objects and are used to manage and select the objects.                                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                                     |
      |                                   | a. Enter the key and value.                                                                                                                                                                                                                                                                                         |
      |                                   | b. Click **Confirm**.                                                                                                                                                                                                                                                                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. .. _ucs_01_0115__en-us_topic_0160121211_li69121840101813:

   Create a secret from a YAML file by clicking **Create from YAML**.

   .. note::

      To create a resource by uploading a file, ensure that the resource description file has been created. UCS supports files in JSON or YAML format. For details, see :ref:`Secret Resource File Configuration <ucs_01_0115__en-us_topic_0160121211_section187197531454>`.

   You can import or directly write the file content in YAML or JSON format.

   -  Method 1: Import an orchestration file.

      Click **Import** to import a YAML or JSON file. The content of the YAML or JSON file is displayed in the orchestration content area.

   -  Method 2: Directly orchestrate the content.

      In the orchestration content area, enter the content of the YAML or JSON file.

#. When the configuration is complete, click **OK**.

   The new secret is displayed in the secret list.

.. _ucs_01_0115__en-us_topic_0160121211_section187197531454:

Secret Resource File Configuration
----------------------------------

This section provides a configuration example of a secret resource file.

For example, you can retrieve the username and password for a workload through a secret.

-  YAML format

   The content in the secret file **secret.yaml** is as follows. The value must be encoded using Base64. For details, see :ref:`Base64 Encoding <ucs_01_0115__en-us_topic_0160121211_section175000605919>`.

   .. code-block::

      apiVersion: v1
      kind: Secret
      metadata:
        name: mysecret           #Secret name
        namespace: default       #Namespace. The default value is default.
      data:
        username: bXktdXNlcm5hbWUK  #Username, which must be encoded using Base64.
        password: ******  #The value must be encoded using Base64.
      type: Opaque     #You are advised not to change this parameter value.

-  JSON format

   The content in the secret file **secret.json** is as follows:

   .. code-block::

      {
        "apiVersion": "v1",
        "kind": "Secret",
        "metadata": {
          "name": "mysecret",
          "namespace": "default"
        },
        "data": {
          "username": "bXktdXNlcm5hbWUK",
          "password": "******"
        },
        "type": "Opaque"
      }

Related Operations
------------------

After a secret is created, you can perform the operations described in :ref:`Table 2 <ucs_01_0115__en-us_topic_0160121211_table555785274319>`.

.. note::

   The secrets in the **kube-system** namespace can only be viewed.

.. _ucs_01_0115__en-us_topic_0160121211_table555785274319:

.. table:: **Table 2** Other operations

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
   | Operation                         | Description                                                                                                   |
   +===================================+===============================================================================================================+
   | Editing a YAML file               | Click **Edit YAML** in the row where the target secret resides to edit its YAML file.                         |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
   | Updating a secret                 | #. Click **Update** in the row where the target secret resides.                                               |
   |                                   | #. Modify the secret data according to :ref:`Table 1 <ucs_01_0115__en-us_topic_0160121211_table16321825732>`. |
   |                                   | #. Click **OK**.                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
   | Deleting a secret                 | Click **Delete** in the row where the target secret resides.                                                  |
   |                                   |                                                                                                               |
   |                                   | Delete the secret as prompted.                                                                                |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
   | Deleting secrets in batches       | #. Select the secrets to be deleted.                                                                          |
   |                                   | #. Click **Delete** in the upper left corner.                                                                 |
   |                                   | #. Delete the secret as prompted.                                                                             |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------+

.. _ucs_01_0115__en-us_topic_0160121211_section175000605919:

Base64 Encoding
---------------

To encode a character string using Base64, run the **echo -n Content to be encoded \| base64** command. The following is an example:

.. code-block::

   root@ubuntu:~# echo -n "Content to be encoded" | base64
   ******
