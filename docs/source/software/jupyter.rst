------------
Jupyter Hub
------------
====================
Jupyter Hub Status
====================
Released and accessible to all HPC Users at the correct URLs. 

.. _Jupyter Enterprise Gateway: https://jupyter.org/hub
.. _Jupyter URL: https://deepweb.flinders.edu.au/jupyter

====================
Jupyter Hub Overview
====================

The `Jupyter Enterprise Gateway`_ is a multi-user environment for Jupyter Notebooks. DeepThought has integrated 
the Jupyter Gateway to allow users to run jobs on the cluster via the native Web Interface.  

If you have access to the HPC, you automatically have access to the Jupyter Lab. You can the JupyterLab Instance 
via the following `Jupyter URL`_ or manually via https://deepweb.flinders.edu.au/jupyter. Your credentials are the
the same as the HPC, your FAN and password.

If you are a *student* with access to the HPC, the above URLs may work - the URL http://deepteachweb.flinders.edu.au/jupyter is guaranteed to work correctly. 


========================================
Using Conda Environments in Jupyter Hub
========================================

You can use your own custom environment in a Jupyter Kernel. There are some restrictions on python versions that must be adhered to for this integration to work 
correctly. You will also need to install some specific packages. This process of enabling a conda environment to work with the HPC, SLURM and Jupyter Hub is detailed below. 

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Python Version Restrictions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 * Python Version <= 3.9.  

Python 3.10 *will* **not** *work*, due to dependency incompatibility. 

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Conda Environment Preparation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Ensure you have a named conda environment that is loadable by ``conda activate <ENVIRONMENT_NAME>``
2. Ensure that the python version used by the environment is Python 3.9 or less.'
3. Log ont the HPC via SSH and activate your Conda environment ``conda activate <ENVIRONMENT_NAME>`` 
4. Execute the following commands: 
    a. ``python3 -m pip install cm-jupyter-eg-kernel-wlm`` 
    b. ``conda install ipython ipython_genutils``
5. Log into Jupyter Hub with your FAN and password at the `Jupyter URL`_
6. Using the bar on the Left-hand side, select small green symbol
7. Create a new Kernel based on the 'CONDA via SLURM' template. 
    a. Ensure you select any additional modules you need, like GDAL 
    b. Ensure that you select the correct Conda environment to initialise 
8. Use the Kernel in your Jupyter Notebooks

For Reference, the below image shows the Kernel Template Screen. 

.. figure:: ../_static/jupyter-kernel-template.png
    :align: left
    :alt: Jupyter Hub Kernel Template Screen
    
