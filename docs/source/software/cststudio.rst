-----------------------------------------
CST Studio Suite 
-----------------------------------------

.. _CST Studio 2022: https://www.ansys.com/

========================================
CST Studio Suite Status
========================================

`CST Studio 2022`_ is the current version of the CST Studio Suite installed on the HPC. Currently, Single-Node Module and GPU acceleration are tested and confirmed to be working via a manual CLI call. 

The ``cst_`` job-submission scripts will work, however they *do not* allocate resources in an effective manner for DeepThought. Use at your own risk, as a manually created SLURM job will 
give you much better results. 

Below are the modes of operation and their status.

+----------------------+--------------------+
| Run Mode             | Status             |
+======================+====================+
| GPU Accelerated      | Working/Released   |
+----------------------+--------------------+
| Single-Node Parallel | Working/Released   |
+----------------------+--------------------+
| Multi-Node Parallel  | Testing/Unreleased |
+----------------------+--------------------+


========================================================================
CST Studio Suite Quickstart Command Line Guide
========================================================================

To run a CST Studio job on the HPC you will need your ``.cst`` file, and the associated SLURM script. Modify any <OPTIONS> to your requirements.  

1.  Single-Node, GPU Accelerated

    ``cst_design_environment -defaultacc -with-gpu=<NUMBER_OF_GPUS_REQUESTED> -m -r -num-threads=$SLURM_CPUS_PER_TASK -project-file /path/to/projet.cst``

2. Single-Node, CPU Only 

   ``cst_design_environment -m -r -num-threads=$SLURM_CPUS_PER_TASK -project-file /path/to/project.cst``


3. Multi-Node GPU Accelerated 
    
   ``Coming Soon, when MPI is released``


4. Multi-Node, CPU Only 
    
   ``Coming Soon, when MPI is released``




++++++++++++++++++++++++++++++++++++++++++++++
CST Studio Suite CLI Quick List
++++++++++++++++++++++++++++++++++++++++++++++

+---------------------------------+--------------------------------------------------------------+
| CLI Option                      | Description                                                  |
+=================================+==============================================================+
| -defaultacc                     | Enable Compute Acceleration Detection.                       |
+---------------------------------+--------------------------------------------------------------+
| -with-gpu=<NUM_GPU>             | Per Node, the number of GPU's (Max 2). Requires -defaultacc. |
+---------------------------------+--------------------------------------------------------------+
| -m -r                           | Enable 'Batch' Mode                                          |
+---------------------------------+--------------------------------------------------------------+
| -num-threads=<COUNT>            | Number of threads (CPU's) to use                             |
+---------------------------------+--------------------------------------------------------------+
| -num-cpudevices=<COUNT>         | MPI Only. Use only if you know what NUMA is                  |
+---------------------------------+--------------------------------------------------------------+
| -withmpi                        | Enable MPI                                                   |
+---------------------------------+--------------------------------------------------------------+
| -machinefile=/path/to/file      | Path to the CST Machine File. Required for MPI.              |
+---------------------------------+--------------------------------------------------------------+
| -autompi                        | Automatically detect the MPI Type. Required for MPI.         |
+---------------------------------+--------------------------------------------------------------+
| -shared-dir                     | A shared space for CST. Defaults to $TMPDIR                  |
+---------------------------------+--------------------------------------------------------------+
| -project-file /path/to/file.cst | Path to .CST Project FIle                                    |
+---------------------------------+--------------------------------------------------------------+