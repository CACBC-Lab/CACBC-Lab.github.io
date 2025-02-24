Lab Testing
===========

Multiple test on CACBC-Lab' machines 

Basic Program Testing
---------------------
1. **Open basic programs** and ensure they launch without issues:

   - Click on the :menuselection:`Applications Menu --> Programs`.
   - Search for each of the following programs: :menuselection:`Firefox`, :menuselection:`Terminal`, :menuselection:`Inkscape`, and :menuselection:`RStudio`.
   - Click on each program to open it.
   - Verify that each program starts successfully without errors.
   - Close each program after confirming it works.

User Folder Testing
^^^^^^^^^^^^^^^^^^^
1. **Open Terminal** using:
   :kbd:`Ctrl` + :kbd:`Alt` + :kbd:`T` and navigate to the user ``Home`` folder:

   .. code-block:: console

      $ cd ~  # Shortcut to go Home

2. **Create a new folder:** in the ``Home`` folder

   .. code-block:: console

      $ mkdir test_folder  # Create a new folder
      $ ls                 # Verify the folder was created
      $ cd test_folder     # Enter to this folder

3. **Create and modify files:**

   .. code-block:: console

      $ touch test_file.txt   # Create a test file
      $ ls -lst test_file.txt # Check permissions of this file
    
- Modify this file using ``VSCode``, like this:

    .. code-block:: console

        $ code .  # Open VSCode

- Open the file ``test_file.txt`` at the left panel. Modify the file, then save it.
- Close ``VSCode``.
- Look the content using:
     
     .. code-block:: console

        $ cat test_file.txt

5. **Test file permissions:**

   Each user is a member of a group defined by their research group. This test evaluates the consistency of file permissions across these groups.

   .. code-block:: console

      $ cd /srv/<your_machine_name>/<your_username> # Change to your own folder
      $ touch my_personal_file.txt              # Create a test file
      $ chmod 700 my_personal_file.txt          # Restrict access: for everyone except me
      $ rm /srv/<other_user_machine>/<other_username>/my_personal_file.txt  # Try to delete the file for other user

Conda environment and vienna RNA Testing
---------------------------------------

0. **Check if conda is installed:**

   .. code-block:: console

      $ conda

- If the ``conda`` documentation is printed, it is installed, please continue with step 1.
    
    .. note::
        If you don't have ``conda``, you should install create your own conda installation, where all your environments will be stored, please execute:

        .. code-block:: console

            $ cd /srv/<your_machine_name>/<your_username> # Change to your own folder
            $ mkdir bin # Create a personal bin/ directory for personal software
            $ cd bin # Enter to the folder
            $ wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
            $ bash Miniforge3-Linux-x86_64.sh # Follow the instructions

    - It will start a step-by-step installation. 1) Press :kbd:`Enter`, 2) then accept the license terms typing ``yes``. 
    - Then, the installer will ask about the location of the ``miniforge3/`` installation, please confirm the location in the ``/home/<your_username>/`` directory.
    - Once finished (about 10 minutes), type at the end ``yes``, to automatically activate ``conda`` once you start a terminal session.
    - Close the terminal window and open a new one.

      .. warning::
        - However, we don't want to fill the memory of our common ``home`` directory, we need to move our conda folder to our personal folder. To do so, please type:

        .. code-block:: console

            $ mv /home/<your_username>/miniforge3 /srv/<your_machine_name>/<your_username>/bin/ # Move to your bin folder, it will take about 10 minutes
            $ cd ~/ # Go to your home
            $ ln -s /srv/<your_machine_name>/<your_username>/bin/miniforge3 . # Create a soft link to this folder

        - This trick will enable you to have your ``conda`` environments available in all machines.

1. **Create a test Conda environment:**

   .. code-block:: console

      $ conda env list # Check current environments
      $ conda create --name test_env -c conda-forge # Create the environment
      $ conda activate test_env  # Activate the environment
    
2. **Install viennarna:**

You can search for ``ViennaRNA`` on `Bioconda <https://bioconda.github.io/>`_. Just type in the search box, ``viennarna``, and click on the first `result <https://bioconda.github.io/recipes/viennarna/README.html#package-package%20&#x27;viennarna&#x27;>`_.

   .. code-block:: console

      $ conda install -c bioconda viennarna # Install ViennaRNA
      $ RNAfold --version                   # Confirm the installation

.. important::
   If installation fails, ensure the Bioconda channel is configured:

   .. code-block:: console

      $ conda config --add channels bioconda

3. **Fold an RNA sequence and calculate MFE using Python:**

   .. code-block:: console

      $ python  # Open Python in the terminal

Type this in the ``python`` terminal:

   .. code-block:: python

      import RNA
      sequence = "CUACGGCGCGGCGCCCUUGGCGA"
      mfe_structure, mfe = RNA.fold(sequence)
      print(f"MFE Structure: {mfe_structure}")
      print(f"MFE Value: {mfe} kcal/mol")


R Configuration in Visual Studio Code
-------------------------------------

This part guides you through setting up `R` in Visual Studio Code (`VSCode`).

Prerequisites
^^^^^^^^^^^^^
- **R Installation**: Ensure ``R`` (version 3.4.0 or higher) is installed on your system:

  .. code-block:: console

    $ R # It will open R in the console
- Then, I suggest to use a ``conda`` environment with custom R version and packages, like this:

  .. code-block:: console

      $ conda create -n r_env -c conda-forge r-base # Dowload latests R version


- Then, create a new project and open ``VSCode``:

  .. code-block:: console
    
    $ cd /srv/<your_machine_name>/<your_username> # Change to your own folder
    $ mkdir projects/testR # Create a folder to host your new project
    $ cd projects/testR # Access to the project folder
    $ code . # Open VSCode in the testR folder

1. **To install the R extension in VSCode**:

   - Navigate to the Extensions view by clicking on the square icon in the sidebar or pressing :kbd:`Ctrl` + :kbd:`Shift` + :kbd:`X`.
   - In the search bar, type ``R`` and select the extension it.
   - Click 'Install' to add the extension to VS Code.
   .. - Once it’s installed, you’ll want to set up a few settings to get ``R`` set up for your ``conda`` environment. Click the gear icon in the ``R`` extension pane, and click Extension Settings. Modify the ``Rpath:Linux``.

2. **Install the R Language Server**:

   - Open your R console, in ``VSCode`` go to ::menuselection::``View``, then ::menuselection::``Terminal``
   - Install the `languageserver` package by running:

     .. code-block:: r

        install.packages("languageserver")

4. **Enhance the R experience in VSCode (Optional)**:
   
   - **Radian**: A modern R console that offers features like syntax highlighting and auto-completion. Install Radian by running:

    .. code-block:: r

        install.packages("radian")

   - **httpgd**: An R package that provides a graphics device serving SVG graphics via HTTP and WebSockets, useful for interactive plot viewing in VS Code. Install httpgd by running:

    .. code-block:: r

        install.packages("httpgd")

5. **Running R Code in VS Code**:

   - Create an ``R`` script (`.R` file) in ``VSCode``.
   - Copy and paste the following code:

   .. code-block:: r

        #!/usr/bin/env Rscript

        # Check if ggplot2 is installed; if not, install it.
        if (!require("ggplot2", quietly = TRUE)) {
          install.packages("ggplot2", repos = "https://cloud.r-project.org")
          library(ggplot2)
        }

        # Set seed for reproducibility
        set.seed(123)

        # Create sample data with 100 random points
        data <- data.frame(
          x = rnorm(100),
          y = rnorm(100)
        )

        # Create a ggplot scatter plot
        plot <- ggplot(data, aes(x = x, y = y)) +
          geom_point(color = "blue") +
          labs(
            title = "Sample Scatter Plot",
            x = "X-axis",
            y = "Y-axis"
          ) +
          theme_minimal()

        # Display the plot
        print(plot)

        # Optionally, save the plot to a file (PNG format)
        ggsave("scatter_plot.png", plot, width = 6, height = 4)

   - To run a line of code, place the cursor on the line and press :kbd:`Ctrl` + :kbd:`Enter`. The code will execute in the integrated ``R`` terminal.
   - To run the entire script, press :kbd:`Ctrl` + :kbd:`Shift` + :kbd:`S`.

.. For a comprehensive guide and troubleshooting, refer to the `official VS Code R documentation <https://code.visualstudio.com/docs/languages/r>`_.

Installing ``RStudio`` in a Conda Environment
-----------------------------------------

This guide describes the steps to install R and `RStudio` within a Conda environment using `conda-forge`.

Creating the Conda Environment with ``RStudio``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. **Open a terminal**.
2. **Create a new Conda environment** with ``R``, ``Rstudio`` (now `Posit`), and essential packages:

   .. code-block:: console

      $ conda create --name rstudio_env -c conda-forge r-base r-essentials rstudio-desktop

3. **Activate the environment**:

   .. code-block:: console

      $ conda activate rstudio_env

4. **Verify the installation** by running:

   .. code-block:: console

      $ rstudio

   If `RStudio` opens without errors, the installation was successful!

Installing Additional R Packages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To install additional R packages, use R’s built-in `install.packages()` function. Open R within the Conda environment and run:

.. code-block:: r

   install.packages("ggplot2")
   library(ggplot2)

.. important::
   If package installation fails due to missing system dependencies, try using Conda to install them:

   .. code-block:: console

      $ conda install -c conda-forge r-ggplot2

Launching RStudio from the Conda Environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. **Ensure the Conda environment is active**:

   .. code-block:: console

      $ conda activate rstudio_env

2. **Launch RStudio**:

   .. code-block:: console

      $ rstudio

   The `RStudio` interface should open with the Conda environment’s R version.
