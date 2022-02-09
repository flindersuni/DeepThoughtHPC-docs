-------------------------
ANSYS Engineering Suite 
-------------------------
=======
Status
=======
ANSYS 2021R2 is the current version of the ANSYS Suite installed on the HPC. Both Single-Node (-smp) and Multi-Node (-dis) execution is supported.


.. _ANSYS: https://www.ansys.com/

==========
Overview 
========== 
The ANSYS Engineering Suite is a comprehensive software suite for engineering simulation. More information on can be found on the `ANSYS`_ website.


================================
Quickstart Command Line Guide
================================

To run a job with ANSYS on the HPC you will need the following: 
    - An ANSYS Script file 
    - Any reference file(s) (eg, a .db file)

Ensure that the paths to anything in the script file reflect where it lives on the HPC, not your local machine. 

You can then invoke ANSYS (after loading the ANSYS Module) in 'batch' mode for a single script like so: 

1. Single-Node (Single-Node)


- ansys212 -smp -np <CPUS> -bd <DB File Memory Allocation> -m <SLURM Memory Allocation> -b -s < PATH_TO_SCRIPT_FILE
2. Distributed Mode (Multi-Node)


- ansys212 -dis -np <CPUS> -bd <DB FILE Memory Allocation> -m <SLURM Memory Allocation> -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE

+++++++++++++++++++++++
ANSYS CLI Quick List
+++++++++++++++++++++++
The following is a quick list of some of the common CLI options.


+-------------------+--------------------------------------------+
| CLI Option        | Description                                |
+===================+============================================+
| -acc nvidia       | Enable GPU Compute Acceleration            |
+-------------------+--------------------------------------------+
| -dis              | Run ANSYS in Distributed (Multi-Node) Mode |
+-------------------+--------------------------------------------+
| \-np value        | Specify the Number of CPU's: -np 12        |
+-------------------+--------------------------------------------+
| -smp              | Run ANSYS in Single-Node Mode              |
+-------------------+--------------------------------------------+
| -g                | Start the Graphical User interface         |
+-------------------+--------------------------------------------+
| -b                | Enable ANSYS Batch mode. Needs -s.         |
+-------------------+--------------------------------------------+
| -i                | Full Input file path                       |
+-------------------+--------------------------------------------+
| -o                | Full Output File Path                      |
+-------------------+--------------------------------------------+
| -s                | Read the Ansys Startup Script              |
+-------------------+--------------------------------------------+
| -dir /path        | The Working Diretory of ANSYS              |
+-------------------+--------------------------------------------+
| -db               | Initial Allocation for the .DB File        |
+-------------------+--------------------------------------------+
| \-m value         | RAM Allocation for ANSYS. -m 40000         |
+-------------------+--------------------------------------------+
| \< /path/         | Script file Path for batch Mode            |
+-------------------+--------------------------------------------+
| \> /path/file.out | Path to store ANSYS Output to file         |
+-------------------+--------------------------------------------+


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


