:original_name: ucs_01_0268.html

.. _ucs_01_0268:

Secrets
=======

A secret is a type of resource that holds sensitive data, such as authentication and key information. Its content is user-defined.

.. note::

   -  After a secret is created on the UCS console, it is in the undeployed state by default. You need to mount the secret when creating or updating a workload. For details, see :ref:`Secret <ucs_01_0278__section10197243134710>`.
   -  After a secret is mounted to a workload, a secret with the same name is created in each cluster to which the workload belongs.

.. _ucs_01_0268__section129181141173214:

Creating a Secret
-----------------

#. Log in to the UCS console. In the navigation pane, choose **Fleets**.

#. On the **Fleets** tab, click the name of the federation-enabled fleet to access its details page.

#. Choose **ConfigMaps and Secrets** in the navigation pane and click the **Secrets** tab.

#. Select the namespace for which you want to create a secret and click **Create Secret** in the upper right corner.

#. Set the parameters listed in :ref:`Table 1 <ucs_01_0268__table16321825732>`.

   .. _ucs_01_0268__table16321825732:

   .. table:: **Table 1** Parameters for creating a secret

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                 |
      +===================================+=============================================================================================================================================================================================================================================================================================+
      | Name                              | Name of a secret, which must be unique in the same namespace.                                                                                                                                                                                                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Namespace                         | Namespace to which the secret belongs. The current namespace is used by default.                                                                                                                                                                                                            |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Description of the secret.                                                                                                                                                                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Type                              | Type of the secret.                                                                                                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                                             |
      |                                   | -  Opaque: common secret. In high-sensitive scenarios, you are advised to encrypt sensitive data using data encryption services and then store the encrypted data in secrets.                                                                                                               |
      |                                   | -  kubernetes.io/dockerconfigjson: a secret that stores the authentication information required for pulling images from a private repository. If you select this secret type, enter the image repository address.                                                                           |
      |                                   | -  IngressTLS: a secret that stores the certificate required by an ingress. If you select this secret type, upload the certificate file and private key file.                                                                                                                               |
      |                                   | -  Other: another type of secret, which is specified manually.                                                                                                                                                                                                                              |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Data                              | Workload secret data can be used in containers.                                                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                             |
      |                                   | -  If the secret type is **Opaque**, enter the key and value. The value must be a Base64-encoded value. You can select **Auto Base64-encoded** to Base64-encode the entered value. For details about manual Base64 encoding, see :ref:`Base64 Encoding <ucs_01_0268__section175000605919>`. |
      |                                   | -  If the secret type is **kubernetes.io/dockerconfigjson**, enter the username and password of the private image repository.                                                                                                                                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Label                             | Labels are attached to objects such as workloads, nodes, and Services in key-value pairs.                                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                                                                                                                             |
      |                                   | Labels define identified attributes of these objects and can be used to manage and select objects.                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                             |
      |                                   | a. Click **Confirm**.                                                                                                                                                                                                                                                                       |
      |                                   | b. Enter the key and value.                                                                                                                                                                                                                                                                 |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

   The new secret is displayed in the secret list.

Using a Secret
--------------

After a secret is created, you can mount the secret to a container for storage during workload creation. Then, you can read the secret data from the mount path of the container. For details, see :ref:`Secret <ucs_01_0278__section10197243134710>`.

.. _ucs_01_0268__section175000605919:

Base64 Encoding
---------------

To Base64-encode a string, run the **echo -n Content to be encoded \| base64** command. The following is an example:

.. code-block::

   echo -n "Content to be encoded" | base64

Related Operations
------------------

You can also perform operations described in :ref:`Table 2 <ucs_01_0268__table555785274319>`.

.. _ucs_01_0268__table555785274319:

.. table:: **Table 2** Related operations

   +------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Operation                          | Description                                                                                         |
   +====================================+=====================================================================================================+
   | Creating a secret from a YAML file | Click **Create from YAML** in the upper right corner to create a secret from an existing YAML file. |
   +------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Viewing details                    | Click the secret name to view its details.                                                          |
   +------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Editing a YAML file                | Click **Edit YAML** in the row where the target secret resides to edit its YAML file.               |
   +------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Updating a secret                  | #. Choose **More** > **Update** in the row where the target secret resides.                         |
   |                                    | #. Modify the secret information according to :ref:`Table 1 <ucs_01_0268__table16321825732>`.       |
   |                                    | #. Click **OK** to submit the modified information.                                                 |
   +------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Deleting a secret                  | Choose **More** > **Delete** in the row where the target secret resides, and click **Yes**.         |
   +------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Deleting secrets in batches        | #. Select the secrets to be deleted.                                                                |
   |                                    | #. Click **Delete** in the upper left corner.                                                       |
   |                                    | #. Click **Yes**.                                                                                   |
   +------------------------------------+-----------------------------------------------------------------------------------------------------+
