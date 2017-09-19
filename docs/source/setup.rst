Setup instructions
==================

Requirements
------------

This toolset is written for use in Linux.

You will need access to a PC or server with at least:

* 8 GB of RAM to run sen2cor.
* 32 - 128 GB of RAM to run sen2three (depending on how many images you aim to combine).

Installing Anaconda Python
--------------------------

The ESA tools sen2cor and sen2three are at present reliant upon use of a particular version of the Anaconda Python distribution (v 4.2.0). At the time of writing, newer versions of Anaconda Python are incompatable with sen2cor and sen2three, though this may well change in future.

To install Anaconda Python, open a terminal window, change directory to the location you'd like to install Anaconda Python, and run the following commands:

.. code-block:: console
    
    wget https://repo.continuum.io/archive/Anaconda2-4.2.0-Linux-x86_64.sh
    bash Anaconda2-4.2.0-Linux-x86_64.sh


Once complete, you'll need to add this version of Python to your .bashrc file as follows:

.. code-block:: console
    
    # Substitute root for the path to your system's installation and .bashrc file.
    echo 'export PATH="/root/anaconda2/bin:$PATH"' >> /root/.bashrc
    exec -l $SHELL


If this has functioned, on executing `python`_ in a terminal window, you should ssee the following:

.. code-block:: console

    Python 2.7.12 |Anaconda custom (64-bit)| (default, Jul  2 2016, 17:42:40) 
    [GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    Anaconda is brought to you by Continuum Analytics.
    Please check out: http://continuum.io/thanks and https://anaconda.org
    >>> 


Installing sen2cor
------------------

sen2cor is an ESA program to perform atmospheric correction and cloud masking of Sentinel-2 level 1C images. It generates a new file containing bottom of atmosphere reflectance values and a cloud mask.

For further details and up-to-date installation instructions, see the `sen2cor website <http://step.esa.int/main/third-party-plugins-2/sen2cor/>`_.

At the time of writing, sen2cor can be installed using the following commands. sen2cor must be installed after Anaconda Python. Open a terminal window, change directory to the location you'd like sen2cor to be installed, and run the following commands:

.. code-block:: console

    wget http://step.esa.int/thirdparties/sen2cor/2.3.1/sen2cor-2.3.1.tar.gz
    tar -xvzf sen2cor-2.3.1.tar.gz
    rm sen2cor-2.3.1.tar.gz
    cd sen2cor-2.3.1
    python setup.py install

Once complete, you need to reference this software in your .bashrc file as follows:

.. code-block:: console

    # Substitute /home/user for the path to your system's installation and .bashrc file.
    echo "source /home/user/sen2cor/L2A_Bashrc" >> /home/user/.bashrc
    exec -l $SHELL


To test the installation, type ``L2A_Process --help`` in a terminal window to show running instructions. You should see something that looks like the following:

.. code-block:: console

    usage: L2A_Process [-h] [--resolution {10,20,60}] [--sc_only] [--cr_only]
                       [--refresh] [--GIP_L2A GIP_L2A] [--GIP_L2A_SC GIP_L2A_SC]
                       [--GIP_L2A_AC GIP_L2A_AC]
                       directory
    
    Sentinel-2 Level 2A Processor (Sen2Cor). Version: 2.4.0, created: 2017.02.03,
    supporting Level-1C product version: 14.
    
    positional arguments:
      directory             Directory where the Level-1C input files are located

    optional arguments:
      -h, --help            show this help message and exit
      --resolution {10,20,60}
                            Target resolution, can be 10, 20 or 60m. If omitted,
                            all resolutions will be processed
      --sc_only             Performs only the scene classification at 60 or 20m
                            resolution
      --cr_only             Performs only the creation of the L2A product tree, no
                            processing
      --refresh             Performs a refresh of the persistent configuration
                            before start
      --GIP_L2A GIP_L2A     Select the user GIPP
      --GIP_L2A_SC GIP_L2A_SC
                            Select the scene classification GIPP
      --GIP_L2A_AC GIP_L2A_AC
                            Select the atmospheric correction GIPP


Installing sen2three
--------------------

sen2three is an ESA program to combine multiple level 2A images from Sentinel-2 into cloud-free composite images. It generates a new file containing the best quality cloud-free image that it can construct from available imagery.

For further details and up-to-date installation instructions, see the `sen2three website <http://step.esa.int/main/third-party-plugins-2/sen2three/>`_.

.. note: This processing chain requires sen2three version 1.1.0 or later. At the time of writing this has not been formally released, but can be downloaded from GitHub.

At the time of writing, sen2three can be installed as follows. sen2three must be installed after Anaconda Python. The first step is to download the the file `sen2three-1.1.0.tar.gz`_ from GitHub using an internet browser window from the URL https://github.com/senbox-org/sen2proc/blob/master/SEN2THREE/distributions/v1.1.0/sen2three-1.1.0.tar.gz. Save the file to the location that you'd like it to be installed.

Open a terminal window, change directory to the location you saved `sen2three-1.0.0.tar.gz`_, and run the following commands:

.. code-block:: console

    tar -xvzf sen2three-1.1.0.tar.gz
    rm sen2three-1.1.0.tar.gz
    cd sen2three-1.1.0
    python setup.py install

Once complete, you need to reference this software in your `.bashrc`_ file as follows:

.. code-block:: console

    # Substitute /home/user for the path to your system's installation and .bashrc file.
    echo "source /home/user/sen2three/L3_Bashrc" >> /home/user/.bashrc
    exec -l $SHELL

To test the installation, type `L3_Process --help`_ in a terminal window. You should see the following:

.. code-block:: console

    usage: L3_Process [-h] [--resolution {10,20,60}] [--clean] directory

    Sentinel-2 Level 3 Processor (Sen2Three), 1.0.1, created: 2017.02.13,
    supporting Level-1C product version: 13.

    positional arguments:
    directory             Directory where the Level-2A input files are located

    optional arguments:
    -h, --help            show this help message and exit
    --resolution {10,20,60}
                            Target resolution, can be 10, 20 or 60m. If omitted,
                            all resolutions will be processed
    --clean               Removes the L3 product in the target directory before
                            processing. Be careful!


.. note:: Installation of sen2three v1.1.0 has been known to cause issues with the glymur library in Anaconda Python. If you encounter error messages relating to glymur, they can be fixed by re-installing glymur using the command: `pip install 'glymur==0.8.6'`.


Installing sentinelsat
----------------------

Sentinelsat is the toolset used to access data from the Sentinel-2 archive at the [Copernicus Open Access Data Hub](https://scihub.copernicus.eu/).

Up-to-date installation instructions can be found `here <https://pypi.python.org/pypi/sentinelsat>`_.

At the time of writing, the installation process is as follows:

.. code-block:: console

    pip install sentinelsat


Installing sen2mosaic
---------------------

sen2mosaic can be downloaded to a machine from its repository. To do this, open a terminal window and input:

.. code-block:: console

    git clone git@bitbucket.org:sambowers/sen2mosaic.git


Where do I get help?
--------------------

For help installing sen2cor and sen2three, it's best to refer to the `ESA STEP forum <http://forum.step.esa.int/>`_. For assistance in setting up and using sen2mosaic, email `sam.bowers@ed.ac.uk <mailto:sam.bowers@ed.ac.uk>`_.
