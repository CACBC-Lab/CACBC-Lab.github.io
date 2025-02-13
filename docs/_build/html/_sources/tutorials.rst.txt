Tutorials
=========

Linux 101
---------

.. important::
    - **Constant width font** (e.g. ``code``) is used for program names, variable names, and other literal text such as input and output in the terminal window.
    - Lines starting with a ``$`` within a literal text block are **commands**. You should type everything after the ``$`` sign into your terminal window, then press the **Enter** key. (The ``$`` indicates the command-line prompt, which may look different on your system.)
    - All other lines within a literal text block are the **output** from the command you just typed.

Terminal, Command Line, and Editor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- **Opening a Terminal**: You can get a terminal by right-clicking on an empty spot on your desktop and choosing "Open Terminal" from the menu.
- **Running Commands**: Type each command next to the command line prompt (usually ``$``), then hit **Enter**.

  Example:

  .. code-block:: console

     $ date
     Tue Jul  7 14:30:25 CEST 2015

- **Manual Pages**: For more information about a command, type ``man`` followed by the command name, then press **Enter**. Exit the manual by pressing **q**.

  Example:

  .. code-block:: console

     $ man date

- **Redirecting Input/Output**:
  - ``|`` (pipe) ties the **standard output** of one command to the **standard input** of another.
  - ``<`` redirects **standard input** from a file.
  - ``>`` redirects **standard output** to a file.

  **Standard output** (often called **stdout**) is what you see in the terminal, while **standard input** (often called **stdin**) is what programs read as input. The pipe symbol ``|`` lets you directly chain multiple programs together.

Below is a list of some useful core commands available in all Linux terminals:

.. list-table:: Common Commands
   :header-rows: 1
   :widths: auto

   * - **Command**
     - **Description**
   * - ``pwd``
     - Displays the path to the current working directory.
   * - ``cd``
     - Changes the working directory (initially your "HOME").
   * - ``ls``
     - Lists files and directories in the current (or specified) directory.
   * - ``mkdir``
     - Creates a directory.
   * - ``rm``
     - Removes a file (add the ``-r`` option to delete a folder).
   * - ``less``
     - Shows file(s) one page at a time.
   * - ``echo``
     - Prints string(s) to standard output.
   * - ``wc``
     - Prints the number of newlines, words, and bytes in a specified file.

For more information about these commands, add ``--help`` to the program name:

.. code-block:: console

   $ rm --help

Examples
^^^^^^^^

Try a few commands on your own:

.. code-block:: console

   $ ls > file_list
   $ less file_list
   $ rm file_list
   $ ls | less

Here, the **stdout** from the ``ls`` command is written to a file called ``file_list``. The next command shows the content of ``file_list``. We quit ``less`` by pressing **q**, then remove the file. Finally, ``ls | less`` **pipes** the output of ``ls`` into ``less`` without saving it to a file.

Next Steps: Creating Directories and Files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now, let's create a working directory, some subfolders, and our first sequence file using the commands we’ve learned. Keep a good structure so you can find your data easily.

1. Find out which directory you’re in:

   .. code-block:: console

      $ pwd

   Your output might look similar to:

   .. code-block:: console

      $ /home/YOURUSER

2. Make sure you’re in your home directory:

   .. code-block:: console

      $ cd ~

3. Create a new folder with subfolders, then add a short DNA sequence:

   .. code-block:: console

      $ mkdir -p ~/Tutorial/Data
      $ cd ~/Tutorial/Data
      $ echo ATGAAGATGA > BAZ.seq

Here, two new folders (``Tutorial`` and the subfolder ``Data``) are created. We move into the ``Data`` folder, then write a short DNA sequence to ``BAZ.seq``.

Replacing DNA Bases with `sed`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For further processing, suppose you need an RNA sequence instead of a DNA sequence. You can replace all occurrences of ``T`` with ``U`` by using the **stream editor** ``sed``:

.. code-block:: console

   $ sed 's/T/U/g' BAZ.seq > BAZ_RNA.seq

This command reads ``BAZ.seq`` and writes the modified sequence (with ``T`` replaced by ``U``) to a new file called ``BAZ_RNA.seq``.

Conclusion
^^^^^^^^^^

You now know how to open a terminal, run basic Linux commands, and structure your own directories and files. By combining these commands with additional tools like ``sed``, you can effectively manage and transform your data. Continue exploring and practicing to gain confidence in the command line environment!


.. _conda-environment-setup:

Setting up a Conda Environment
------------------------------

In this guide, we explain how to create and manage a new bioinformatic project using **conda** environments on Linux. This approach ensures a stable, reproducible setup for your tools and dependencies.

What is Conda?
^^^^^^^^^^^^^^
Conda is a cross-platform package manager that allows you to create self-contained environments. It helps you keep different versions of software, libraries, and dependencies organized and prevents conflicts.

Prerequisites
^^^^^^^^^^^^^
1. **Conda Installed**: Make sure you have Anaconda or Miniconda installed on your Linux system. If not, follow the official installation instructions:
   - Anaconda: https://www.anaconda.com/products/distribution
   - Miniconda: https://docs.conda.io/en/latest/miniconda.html

   These guides show you how to run the necessary installation commands on Linux.

2. **Terminal Access**: We will be typing commands into a terminal window on Linux.

Creating a New Project Folder
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
1. Create a new folder (directory) for your bioinformatic project. This folder will hold all the relevant data, scripts, and results.

   .. code-block:: console

      mkdir my_bioinformatics_project
      cd my_bioinformatics_project

2. Keep your project folder organized by creating subdirectories for data, scripts, and results:

   .. code-block:: console

      mkdir data scripts results

Creating and Activating a Conda Environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
1. **Open a terminal** on Linux.
2. **Create** a new conda environment, specifying a name and any key package(s) you want installed:

   .. code-block:: console

      conda create --name my_bioenv python=3.9

   - ``--name my_bioenv`` sets the name of the environment (change it to something meaningful).
   - ``python=3.9`` chooses the specific Python version you need.

3. **Activate** the environment:

   .. code-block:: console

      conda activate my_bioenv

   Your prompt should change to show ``(my_bioenv)`` at the beginning, indicating you’re working inside the environment.

Installing Packages
^^^^^^^^^^^^^^^^^^^
Within the activated environment, install the bioinformatic or data science packages you need. For example:

.. code-block:: console

   conda install numpy pandas biopython

These packages will be installed **only in the current environment**, keeping your system clean and other environments unaffected.

Using the Environment
^^^^^^^^^^^^^^^^^^^^^
1. **Run Python or other tools** within the environment:

   .. code-block:: console

      python

2. **Install additional packages** at any time:

   .. code-block:: console

      conda install <package-name>

3. **Use specialized channels** like ``bioconda`` if needed:

   .. code-block:: console

      conda install -c bioconda <bioinformatics-package>

Deactivating and Managing Environments
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- **Deactivate** the environment:

  .. code-block:: console

     conda deactivate

- **List** all environments to see what you have:

  .. code-block:: console

     conda env list

- **Remove** an environment when you no longer need it:

  .. code-block:: console

     conda remove --name my_bioenv --all

Best Practices
^^^^^^^^^^^^^^
1. Keep a record of the packages and their versions. You can export the environment to a file:

   .. code-block:: console

      conda env export > my_bioenv.yml

2. Share this file with collaborators or use it to recreate the environment on another machine:

   .. code-block:: console

      conda env create -f my_bioenv.yml

Summary
^^^^^^^
In this guide, we covered the basics of setting up and working within a conda environment for a new bioinformatic project in Linux. This approach helps ensure reproducible research, facilitates collaboration, and prevents conflicts among different dependencies. With these steps, you are ready to begin your projects in a structured, well-organized manner!
