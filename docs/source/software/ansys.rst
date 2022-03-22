-------------------------
ANSYS Engineering Suite 
-------------------------
=============
ANSYS Status
=============
ANSYS 2021R2 is the current version of the ANSYS Suite installed on the HPC. Both Single-Node (-smp) and Multi-Node (-dis) execution is supported as well as GPU acceleration.


.. _ANSYS: https://www.ansys.com/

===============
ANSYS Overview 
=============== 
The ANSYS Engineering Suite is a comprehensive software suite for engineering simulation. More information on can be found on the `ANSYS`_ website.


====================================
ANSYS Quickstart Command Line Guide
====================================

To run a job with ANSYS on the HPC you will need the following: 
    - An ANSYS Script file 
    - Any reference file(s) (eg, a .db file)

Ensure that the paths to anything in the script file reflect where it lives on the HPC, not your local machine. Below are some exmaple command-line examples to get you started. 

Replace all <OPTIONS> to suit your requirements. 

1. Shared-Memory Parallel (Single-Node)


``ansys212 -smp -np $SLURM_NTASKS -db <DB File Memory Allocation> -m <SLURM Memory Allocation> -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE``

2. Distributed Mode (Multi-Node) 


``ansys212 -dis -np $SLURM_NTASKS -db <DB FILE Memory Allocation> -m <SLURM Memory Allocation> -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE``

3. Hybrid Distributed Mode (Multi-Node Shared-Memory Parallel)


``ansys212 -dis -np $SLURM_NTASKS -nt $SLURM_CPUS_PER_TASK -db <DB FILE Memory Allocation> -m <SLURM Memory Allocation> -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE``

4. GPU Hybrid Distributed Mode (Multi-Node Shared-Memory Parallel with GPU Acceleration)


``ansys212 -dis -np $SLURM_NTASKS -nt $SLURM_CPUS_PER_TASK -acc nvidia -na <GPU_COUNT> -db <DB FILE Memory Allocation> -m <SLURM Memory Allocation> -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE`` 

+++++++++++++++++++++++
ANSYS CLI Quick List
+++++++++++++++++++++++
The following is a quick list of some of the common CLI options.


+-------------------+--------------------------------------------------------------------------------------------------------------------+
| CLI Option        | Description                                                                                                        |
+===================+====================================================================================================================+
| -acc nvidia       | Enable GPU Compute Acceleration                                                                                    |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| \-na value        | The number GPU per Compute Node ANSYS should use. Current Max: 2                                                   |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| -dis              | Run ANSYS in Distributed (Multi-Node) Mode                                                                         |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| \-np value        | In SMP mode, specify the number of CPU's to use. In Distributed/Hybrid mode, specify the number of Tasks/Processes |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| \-nt value        | Specify the number of threads per process in Hybrid mode                                                           |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| -smp              | Run ANSYS in Single-Node Mode                                                                                      |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| -g                | Start the Graphical User interface                                                                                 |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| -b                | Enable ANSYS Batch mode. Needs -s.                                                                                 |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| -i                | Full Input file path                                                                                               |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| -o                | Full Output File Path                                                                                              |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| -s                | Read the Ansys Start-up Script                                                                                     |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| -dir /path        | The Working Directory of ANSYS                                                                                     |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| -db               | Initial Allocation for the ANSYS .db file. Can be omitted.                                                         |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| \-m value         | RAM Allocation for ANSYS, in MB. Can be omitted.                                                                   |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| \< /path/         | Script file Path for batch Mode                                                                                    |
+-------------------+--------------------------------------------------------------------------------------------------------------------+
| \> /path/file.out | Path to store ANSYS Output to file                                                                                 |
+-------------------+--------------------------------------------------------------------------------------------------------------------+


+++++++++++++++++++++++++
ANSYS Program Quick List
+++++++++++++++++++++++++
The following table lists the ANSYS programs and their associated CLI command.


+-----------------+-----------------------+
| Program         | Name                  |
+=================+=======================+
| Mechanical ADPL | ansys212, ansys2021R2 |
+-----------------+-----------------------+
| Workbench       | runwb2                |
+-----------------+-----------------------+
| CFX             | cfx5                  |
+-----------------+-----------------------+
| FLUENT          | fluent                |
+-----------------+-----------------------+
| ICEM CFD        | icemcfd               |
+-----------------+-----------------------+
| POLYFLOW        | polyman               |
+-----------------+-----------------------+
| CFD-Post        | cfdpost               |
+-----------------+-----------------------+
| Icepak          | icepak                |
+-----------------+-----------------------+
| TurboGrid       | cfxtg                 |
+-----------------+-----------------------+
| AUTODYN         | autodyn212            |
+-----------------+-----------------------+


