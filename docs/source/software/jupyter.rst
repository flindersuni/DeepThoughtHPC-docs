------------
Jupyter Hub
------------
=======
Status
=======
Released and accessible to all HPC USers at the correct URLs. 

.. _Jupyter Enterprise Gateway: https://jupyter.org/hub
.. _Jupyter URL: https://deepweb.flinders.edu.au/jupyter

=========
Overview
=========
The `Jupyter Enterprise Gateway`_ is a multi-user environment for Jupyter Notebooks. DeepThought has integrated 
the Jupyter Gateway to allow users to run jobs on the cluster via the native Web Interface.  

If you have access to the HPC, you automatically have access to the Jupyter Lab. You can the JupyterLab Instance 
via the following `Jupyter URL`_ or manually via https://deepweb.flinders.edu.au/jupyter. Your credentials are the
the same as the HPC, your FAN and password.

If you are a student with access to the HPC, the above URLs may work - the URL http://deepteachweb.flinders.edu.au/jupyter is guaranteed to work correctly. 


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Using Conda Environments in Jupyter Hub
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can use your own custom environment in a Jupyter Kernel. To do so on the HPC via SLURM requires a few simple, extra steps. 


1. Ensure you have a named conda environment that is loadable by ``conda activate <ENVIRONMENT_NAME>`` 
2. Execute ``pip install cm-jupyter-eg-kernel-wlm``. You must use pip, as the package is not available via conda.
3. Log into the HPC Jupyter instace at the `Jupyter URL`_.  
4. Create a new Kernel, using the 'Conda via SLURM' Template. Ensure you change the environemnt from 'base' to the environment you wish to use. 
5. Use this Kernel with your Jupyter Notebook