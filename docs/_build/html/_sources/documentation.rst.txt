Documentation
=============

Credentials and access
----------------------

How to change my user password?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Open a terminal and type the command ``passwd``, and follow the instructions. When prompted to enter your current and new password, no characters will appear on the screen while you type (this is normal). Simply type your password and press Enter each time.

  .. code-block:: console

     $ passwd
     Changing password for username.
     Current password:


User's scratch folder
---------------------

How do I access my scratch folder?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Your **scratch** folder is named the same as your username and is located at:

``/srv/<machine_name>/<your_username>/``

To access it, follow these steps:

1. **Use the `cd` command** to navigate to your scratch directory. Replace `<machine_name>` with the machine's name and `<your_username>` with your username:

   .. code-block:: bash

      cd /srv/<machine_name>/<your_username>/

2. If you encounter a ``No such file or directory`` error, double-check that you have entered the correct machine name and username. If the folder does not exist, you are likely in the wrong location.  


How do I create a folder in my scratch folder?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To create a folder inside your **scratch** directory, follow these steps:

1. **Navigate to your scratch folder** using the `cd` command:

   .. code-block:: bash

      cd /srv/<machine_name>/<your_username>/

2. **Create a new folder** using the `mkdir` command. Replace `<folder_name>` with your desired folder name:

   .. code-block:: bash

      mkdir <folder_name>

3. To **verify that the folder was created**, list the contents of the directory:

   .. code-block:: bash

      ls -l

If you see your new folder in the output, the folder was successfully created.

How do I connect remotely to my scratch using an Unix machine:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 Use the Cisco platform using your MEDUni credentials to use a valid ``VPN`` connection. Once you are connected, type:

   .. code-block:: bash

      ssh <user_name>@<ip address>

The ``IP`` address for each machine is specified in this :ref:`table<Computational_Infraestructure_Tab>`.

Conda environment management
----------------------------

This section provides answers to common questions about managing **conda** environments, including creating, deleting, installing packages, and locating environments.

.. _create-delete-conda-env:

How do I create and delete a conda environment?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**To create a conda environment:**

1. Use the following command, replacing `<env_name>` with your desired environment name and `<python_version>` with the required Python version:

   .. code-block:: bash

      $ conda create --name <env_name> python=<python_version>

   Example:

   .. code-block:: bash

      $ conda create --name myenv python=3.9

2. Activate the environment:

   .. code-block:: bash

      $ conda activate <env_name>

---

**To delete a conda environment:**

1. Deactivate the environment if it’s active:

   .. code-block:: bash

      $ conda deactivate

2. Use the following command to delete the environment:

   .. code-block:: bash

      $ conda env remove --name <env_name>

---

.. _install-uninstall-conda-packages:

How do I install and uninstall packages in a conda environment?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**To install a package:**

1. Activate the environment:

   .. code-block:: bash

      $ conda activate <env_name>

2. Install the desired package (replace `<package_name>` with the package name):

   .. code-block:: bash

      $ conda install <package_name>

   Example:

   .. code-block:: bash

      $ conda install samtools

---

**To uninstall a package:**

1. Ensure the environment is activated:

   .. code-block:: bash

      $ conda activate <env_name>

2. Uninstall the package:

   .. code-block:: bash

      $ conda remove <package_name>

   Example:

   .. code-block:: bash

      $ conda remove samtools
 
---

.. _list-conda-envs:

How do I list my conda environments?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To list all available conda environments, use the following command:

.. code-block:: bash

   $ conda env list

Or:

.. code-block:: bash

   $ conda info --envs

The output will show the names of the environments along with their paths, with the currently active environment marked by an asterisk (*).

---

How do I clone a conda environment and create one from a file?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

--
**Clone an environment**

To create an exact copy of an existing conda environment, use the `conda create` command with the `--clone` option:

1. Use the following command, replacing `<existing_env>` with the name of the environment to clone and `<new_env>` with the name of the new environment:

   .. code-block:: bash

      $ conda create --name <new_env> --clone <existing_env>

Example:

.. code-block:: bash

   $ conda create --name myenv_clone --clone myenv

---

**Create a conda environment file**

You can create a conda environment from an **environment file** (typically `environment.yml`) that lists all dependencies and configurations.

1. Ensure you have the `environment.yml` file.
2. Run the following command:

   .. code-block:: bash

      $ conda env create --file environment.yml

This will create the environment with the name specified in the `name:` field of the `environment.yml` file.

---

**Create a conda environment file from existing environment**

To generate an `environment.yml` file from an existing environment (useful for sharing or recreating the environment elsewhere), use:

.. code-block:: bash

   $ conda activate <env_name>
   $ conda env export > environment.yml

This command will save the current environment's configuration to `environment.yml`.

---

**Update a conda environment**

If you need to update an existing environment using an updated `environment.yml` file:

.. code-block:: bash

   $ conda env update --file environment.yml --prune

The `--prune` option removes dependencies no longer required from the environment.
   
.. _locate-conda-env-path:

How do I locate the path of a specific conda environment?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To find the path of a particular conda environment, use the following command:

.. code-block:: bash

   $ conda env list

This will display all environments with their corresponding paths.

Alternatively, if the environment is active, you can use:

.. code-block:: bash

   echo $CONDA_PREFIX

This will return the full path to the active environment.

FAQs
----

.. _where-is-external-device-mounted:

Where is my external device mounted?
------------------------------------

Your external devices (such as memory sticks or hard disks) are mounted in the following directory:

``/run/media/<your_username>/``

To locate your device:

1. **Navigate to the mount directory** using the `cd` command:

   .. code-block:: bash

      cd /run/media/<your_username>/

2. **List the contents** to see the names of the mounted devices:

   .. code-block:: bash

      ls -l

You will recognize your device by its name in the list. If you don’t see your device, ensure it is properly connected and mounted.
