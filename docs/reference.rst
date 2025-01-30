.. _reference:

Reference
=======================

.. _basic-command-line-usage:

Basic Linux Command Line Usage
******************************

Opening a Terminal
------------------
1. **Locate the Terminal**: On most Linux distributions, you can find it in your applications menu or taskbar. Alternatively, use the keyboard shortcut ``Ctrl + Alt + T``.
2. **Check the Prompt**: A typical Linux command line prompt ends with a ``$`` sign for regular users. Once you see this, you’re ready to enter commands.

Essential Commands
------------------
Below are common Linux commands you may frequently use, along with brief explanations and example usages:

- **cat**: Displays the contents of a file on the screen.

  .. code-block:: console

     cat filename.txt

- **cp**: Copies a file or directory from one location to another.

  .. code-block:: console

     cp source_file.txt /path/to/destination/

- **chmod**: Changes the permissions of a file or directory.

  .. code-block:: console

     chmod 755 script.sh

- **cut**: Extracts sections (columns) from each line of input.

  .. code-block:: console

     cut -f 1,3 -d ',' data.csv

- **cd**: Changes the current working directory.

  .. code-block:: console

     cd /path/to/directory

- **head**: Displays the first 10 lines of a file by default.

  .. code-block:: console

     head filename.txt

- **less**: Opens a file or stream in a scrollable interface.

  .. code-block:: console

     less largefile.txt

- **ls**: Lists the contents of a directory.

  .. code-block:: console

     ls -l

- **man**: Shows the manual page for a command.

  .. code-block:: console

     man ls

- **mkdir**: Creates a new directory.

  .. code-block:: console

     mkdir new_folder

- **more**: Displays file contents one screen at a time (similar to ``less``, but older).

  .. code-block:: console

     more filename.txt

- **mv**: Moves or renames a file or directory.

  .. code-block:: console

     mv old_name.txt new_name.txt

- **pwd**: Prints the current working directory.

  .. code-block:: console

     pwd

- **rm**: Removes (deletes) files or directories.

  .. code-block:: console

     rm file_to_remove.txt
     rm -r directory_to_remove

- **touch**: Creates an empty file or updates the timestamp of an existing file.

  .. code-block:: console

     touch newfile.txt

- **wc**: Counts lines, words, and characters in a file.

  .. code-block:: console

     wc filename.txt

- **>** (Redirect operator): Sends standard output to a file (overwrites existing content).

  .. code-block:: console

     echo "Hello" > output.txt

- **<** (Input redirection): Takes standard input from a file.

  .. code-block:: console

     cat < input.txt

- **|** (Pipe): Feeds the output of one command as input to another command.

  .. code-block:: console

     ls -l | grep "txt"

- ***** (Wildcard): Matches one or more characters in filenames.

  .. code-block:: console

     ls *.txt

Conclusion
----------
Learning these basic commands and how to open the terminal will help you navigate a Linux system effectively. Feel free to integrate these commands into your daily workflow, especially when working on bioinformatics projects or managing conda environments.
