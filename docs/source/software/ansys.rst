-------------------------
ANSYS Engineering Suite 
-------------------------
=======
Status
=======
ANSYS 2021R2 is the current version of the ANSYS Suite installed on the HPC. 

Development on tighter Graphical User Interfaces is currently under investigation. 


==========
Overview 
========== 
The ANSYS Engineering Suite is a comprehensive software suite for engineering simulation.
The new HPC ANSYS integration aims to bring the Remote Solver Manager to DeepThought - allowing 
users to leverage the HPC from their desktops and familiar ANSYS interface. 


=================
Known Issues 
=================
The Intel MPI Library shipped with ANSYS is not 100% compatible with DeepThought. Running with the -smp flag will disable MPI and allow you to run ANSYS as normal on a single node. 


================================
Quickstart Command Line Guide
================================

To run a job with ANSYS on the HPC you will need the following: 
    - A ANSYS Script file 
    - Ay reference file(s) (eg, a .db file)

Ensure that the paths to anything in the script file reflect where it lives on the HPC, not your local machine. 

You can then invoke ANSYS (after loading the ANSYS Module) in 'batch' mode for a single script like so: 

- ansys212 -smp -np <CPUS> -b -s -R PATH_TO_SCRIPT_FILE
- ansys212 -smp -np <CPUS> -bd <DB File Memory Allocation> -m <SLURM Memory Allocation> -b -s < PATH_TO_SCRIPT_FILE


+++++++++++++++++++++++
ANSYS CLI Quick List
+++++++++++++++++++++++
The following is a quick list of some of the common CLI options.


+-------------------+---------------------------------------+
| CLI Option        |       Description                     |
+===================+=======================================+
| -acc nvidia       |  Enable GPU Compute Acceleration      | 
+-------------------+---------------------------------------+
| -np               |  Specify the Number of CPU's          |
+-------------------+---------------------------------------+
| -smp              |  Run ANSYS in Single-Node Mode        |
+-------------------+---------------------------------------+
| -g                | Start the Graphical User interface    |
+-------------------+---------------------------------------+
| -b                | Enable ANSYS Batch mode. Needs -s.    | 
+-------------------+---------------------------------------+
| -i                | Full Input file path                  | 
+-------------------+---------------------------------------+
| -o                | Full Output File Path                 |
+-------------------+---------------------------------------+
| -s                | Read the Ansys Startup Script         |
+-------------------+---------------------------------------+
| -dir /path        | The Working Diretory of ANSYS         |
+-------------------+---------------------------------------+
| -db               | Initial Allocation for the .DB File   |
+-------------------+---------------------------------------+
| -m  <value>       | RAM Allocation for ANSYS.             |
+-------------------+---------------------------------------+
| -R /path/         | Script file Path for batch Mode       |
+-------------------+---------------------------------------+


+++++++++++++++++++++++++
ANSYS Program Quick List
+++++++++++++++++++++++++
The following table lists the ANSYS programs and their associated CLI command


+-------------------+---------------------------------------+
| Program           | Name                                  |
+===================+=======================================+
| Mechanical ADPL   |   ansys212, ansys2021R2               |
+-------------------+---------------------------------------+
| Workbench         |  runwb2                               |
+-------------------+---------------------------------------+
| CFX               |  cfx5                                 |
+-------------------+---------------------------------------+
| FLUENT            |  fluent                               |
+-------------------+---------------------------------------+
| ICEM CFD          | icemcfd                               |
+-------------------+---------------------------------------+
| POLYFLOW          |  polyman                              |
+-------------------+---------------------------------------+
| CFD-Post          |  cfdpost                              |
+-------------------+---------------------------------------+
| Icepak            |  icepak                               |
+-------------------+---------------------------------------+
| TurboGrid         |  cfxtg                                |
+-------------------+---------------------------------------+
| AUTODYN           |   autodyn212                          |
+-------------------+---------------------------------------+


