.. _lab-testing:

Lab Testing
===========

This section outlines the independent testing procedures for lab functions. Two independent testers will perform the following tests step by step.

Basic Program Testing
---------------------
1. **Open basic programs** and ensure they launch without issues:
   - Click on the application menu or press the shortcut keys.
   - Search for each of the following programs: Firefox, Terminal, Inkscape, and R.
   - Click on each program to open it.
   - Verify that each program starts successfully without errors.
   - Close each program after confirming it works.

.. important::
   If any program fails to start, install it using the following command:

   .. code-block:: console

      sudo apt install firefox inkscape r-base

User Folder Testing
-------------------
1. **Open Terminal and navigate to the user folder:**
   - Press `Ctrl + Alt + T` to open the terminal.
   - Type `cd ~` and press `Enter` to move to the home directory.

2. **Create a new folder:**
   - Type `mkdir test_folder` and press `Enter`.
   - Verify the folder was created by running `ls`.

3. **Delete files:**
   - Create a test file using `touch test_file.txt`.
   - Remove the file using `rm test_file.txt`.
   - Confirm it has been deleted by running `ls`.

.. important::
   If `rm` does not work due to permission issues, try using:

   .. code-block:: console

      sudo rm test_file.txt

4. **Modify files using VSCode:**
   - Open VSCode by typing `code .` in the terminal.
   - Create a new file and write some text.
   - Save the file and close VSCode.

.. important::
   If VSCode is not installed, install it using:

   .. code-block:: console

      sudo snap install code --classic

5. **Test file permissions:**
   - Create a test file using `touch restricted_file.txt`.
   - Change file permissions to restrict access: `chmod 600 restricted_file.txt`.
   - Switch to another user and try to modify or delete the file.
   - Verify that the file is protected.

Conda Environment and ViennaRNA Testing
---------------------------------------
1. **Create a test Conda environment:**
   - Open the terminal.
   - Run `conda create --name test_env -c conda-forge -y` to create the environment.
   - Activate it using `conda activate test_env`.

.. important::
   If Conda is not installed, install Miniconda with:

   .. code-block:: console

      wget https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh
      bash Mambaforge-Linux-x86_64.sh

2. **Install ViennaRNA:**
   - Run `conda install -c conda-forge -c bioconda viennarna -y`.
   - Confirm the installation by running `RNAfold --version`.

.. important::
   If installation fails, ensure the Bioconda channel is configured:

   .. code-block:: console

      conda config --add channels bioconda

3. **Fold an RNA sequence and calculate MFE using Python:**
   - Open Python in the terminal by typing `python`.
   - Run the following script:

   .. code-block:: python

      import RNA
      sequence = "CUACGGCGCGGCGCCCUUGGCGA"
      mfe_structure, mfe = RNA.fold(sequence)
      print(f"MFE Structure: {mfe_structure}")
      print(f"MFE Value: {mfe} kcal/mol")

R Package Installation and Analysis in VSCode
---------------------------------------------
1. **Open VSCode:**
   - Press `Ctrl + Alt + T` to open the terminal.
   - Type `code .` and press `Enter` to launch VSCode.

2. **Install necessary R packages:**
   - Open the R terminal inside VSCode.
   - Run the following commands:

   .. code-block:: r

      install.packages("ggplot2")
      library(ggplot2)

.. important::
   If R is not installed, install it using:

   .. code-block:: console

      sudo apt install r-base

3. **Execute a basic data visualization using ggplot2:**
   - Run the following R script:

   .. code-block:: r

      data <- data.frame(x = 1:10, y = rnorm(10))
      ggplot(data, aes(x, y)) + geom_point() + geom_smooth()

   - Ensure the graph is displayed correctly.

RStudio Testing
---------------
1. **Open RStudio:**
   - Click on RStudio from the application menu.
   - Open a new R script file.

2. **Install R packages and run an analysis:**
   - Run the same installation and visualization script from the VSCode section.
   - Confirm that the plot appears without errors.

.. important::
   If RStudio is not installed, install it using:

   .. code-block:: console

      sudo apt install rstudio

This structured testing ensures that core lab functions work as expected across different users and software environments.


