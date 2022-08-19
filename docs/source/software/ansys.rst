-------------------------
ANSYS Engineering Suite 
-------------------------

=============
ANSYS Status
=============

ANSYS 2021R2 is the current version of the ANSYS Suite installed on the HPC. Both Single-Node (-smp) and Multi-Node (-dis) execution is supported as well as GPU acceleration. 

.. _ANSYS: https://www.ansys.com/

==============================
Before You Start
==============================

APDL, Fluent and the EM Suite / HFSS all have a common requirement. All script, journal or run files **must** have been generated in *TUI* Mode. This means that all command must been created, and saved via the 
programs' Command Line Interface. An example of this is - in Fluent, you **cannot** use the "Journal Recording" function via the GUI. When running the job, the GUI will not be available and Fluent **will fail**. 


========================================================================
ANSYS APDL Quickstart Command Line Guide
========================================================================

To run a job with ANSYS APDL on the HPC you will need the following: 
    - An ANSYS Script file 
    - Any reference file(s) (eg, a .db file)

Ensure that the paths to anything in the script file reflect where it lives on the HPC, not your local machine. When running with the ``-dis`` option, you must 
use a distributed filesystem like /scratch (or /cluster, when available) as all nodes will need to the the files, and /local is *not* visible between individual nodes. 
Below are some example command-line examples to get you started. 

Replace all <OPTIONS> to suit your requirements. You can omit the > PATH_TO_OUTPUT_FILE, and SLURM will capture the ANSYS output and write it to your ``#SBATCH --output=/path/to/file.out``. 

1. Shared-Memory Parallel (Single-Node)


``ansys212 -smp -np $SLURM_NTASKS -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE``

2. Distributed Mode (Multi-Node) 


``ansys212 -dis -np $SLURM_NTASKS -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE``

3. Hybrid Distributed Mode (Multi-Node Shared-Memory Parallel)


``ansys212 -dis -np $SLURM_NTASKS -nt $SLURM_CPUS_PER_TASK <SLURM Memory Allocation> -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE``

4. GPU Hybrid Distributed Mode (Multi-Node Shared-Memory Parallel with GPU Acceleration)


``ansys212 -dis -np $SLURM_NTASKS -nt $SLURM_CPUS_PER_TASK -acc nvidia -na <GPU_COUNT_PER_NODE> -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE`` 

++++++++++++++++++++++++++++++++++++++++++++++
ANSYS APDL CLI Quick List
++++++++++++++++++++++++++++++++++++++++++++++

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

========================================================================
ANSYS Fluent Quickstart Command Line Guide
========================================================================

To run a job using ANSYS Fluent you will need: 
    - Journal File(s) (TUI Mode *only*)
    - Shape Files 
    - Mesh Files 

As with APDL, ensure that the paths to anything in the script file reflect where it lives on the HPC, 
not your local machine. When running with the -dis option, you must use a distributed filesystem like 
/scratch (or $BGFS) as all nodes will need to the the files, and /local is not visible between individual nodes. 
Below are some example command-line examples to get you started.

There are less modes of operation than ANSYS APDL. You must specify the solver type along with any options. 

1. Single-Node Parallel, 3-Dimensional, Double-Precision Solver, No GUI or Graphics, Hidden Mesh, 64 Processes, CPU Only

``fluent 3ddp -g -nm -t 64 -mpi=openmpi -i /path/to/TUI/journal/file``

2. Single-Node Parallel, 3-Dimensional, Single-Precision Solver, No GUI or Graphics, Hidden Mesh, 64 Processes, 2 GPU's per Compute Node

``fluent 3d -g -nm -t 64 -mpi=openmpi -gpgpu=2 -i /path/to/TUI/journal/file``

        Important Note: **gpugpu=X** must be divisible evenly with **-t <X>**, or GPU Acceleration will be **disabled**. 

========================================================================
SLURM Task Layout and CLI Requirements 
========================================================================

When designing your SLURM scripts, you must follow the these guidelines, due to how ANSYS Fluent structures its MPI Calls. If you do no, your Fluent 
run will not run with the expected core-count! 

1. Do **NOT** force a node constraint on SLURM via #SBATCH -N 1 or #SBATCH --nodes=1, unless you know *exactly* what you are doing

    ``GPU Acceleration may require this, contact the HPC Team for assitance if you are unsure``


2. You **MUST** use #SBATCH --ntasks=X and #SBATCH --cpus-per-task=1 to allocate CPUS, *not* #SBATCH --ntasks=1 --cpus-per-task=X 

    ``#SBATCH --ntasks=64 and #SBATCH --cpus-per-task=1 will get you 64 CPUS, in 64 Tasks``

3. You **MUST** use #SBATCH --mem-per-cpu instead of#SBATCH  --mem= to prevent unintended memory allocation layouts
   
    ``#SBATCH --mem-per-cpu=3G``

4. You **MUST** use the -mpi=openmpi flag when running fluent. The Default IntelMPI *will not work*, and hangs indefinitely 

5. You **MUST** Create your Journal File in TUI Mode, via the Command-Line or it *will not work*.
6. You **MUST** alter all paths in the TUI Journal File to use ``/`` instead of ``\``, or it *will not work* 
7. You **MUST** alter all paths in the TUI Journal File to be ``/absolute/path/to/your/file``,  or it *will not work*
8. You **MUST** replace the final command of ``/close-fluent`` with ``exit Y`` or your *job will hand until it times out and SLURM kills it*


++++++++++++++++++++++++++++++++++++++++++++++
ANSYS Fluent CLI Solver List 
++++++++++++++++++++++++++++++++++++++++++++++

+------------+----------------------------------------+
| CLI Option | Description                            |
+============+========================================+
| 3ddp       | 3-Dimensional, Double Precision Solver |
+------------+----------------------------------------+
| 3d         | 3-Dimensional, Single Precision Solver |
+------------+----------------------------------------+
| 2ddp       | 2-Dimensional, Double Precision Solver |
+------------+----------------------------------------+
| 2d         | 2-Dimensional, Single Precision Solver |
+------------+----------------------------------------+


++++++++++++++++++++++++++++++++++++++++++++++
ANSYS Fluent CLI Quick List 
++++++++++++++++++++++++++++++++++++++++++++++

+---------------------------------+-----------------------------------------------------------------+
| CLI Option                      | Description                                                     |
+=================================+=================================================================+
| -aas                            | Start Fluent in 'Server' Mode                                   |
+---------------------------------+-----------------------------------------------------------------+
| -affinity=<core or sock or off> | Override the automatic process affinity settings                |
+---------------------------------+-----------------------------------------------------------------+
| -app=                           | Load the specified app                                          |
+---------------------------------+-----------------------------------------------------------------+
| -cflush                         | Clear the System RAM by asking the OS to flush the File-Buffers |
+---------------------------------+-----------------------------------------------------------------+
| -driver=<opengl or x11 or null> | Override the automatic driver detection for Graphics            |
+---------------------------------+-----------------------------------------------------------------+
| -g                              | Run without GUI or Graphics                                     |
+---------------------------------+-----------------------------------------------------------------+
| -gpgpu=<X>                      | Specify the Number of GPU's per Node (Max 2)                    |
+---------------------------------+-----------------------------------------------------------------+
| -gr                             | Run without Graphics                                            |
+---------------------------------+-----------------------------------------------------------------+
| -gu                             | Run without the GUI                                             |
+---------------------------------+-----------------------------------------------------------------+
| -i /path/to/journal/file        | Read and Execute the specified Journal File                     |
+---------------------------------+-----------------------------------------------------------------+
| -mpi=openmpi                    | Must be set to OpenMPI. IntelMPI will not work                  |
+---------------------------------+-----------------------------------------------------------------+
| -nm                             | Do not display mesh after reading                               |
+---------------------------------+-----------------------------------------------------------------+
| -post                           | Run post-processing only                                        |
+---------------------------------+-----------------------------------------------------------------+
| -prepost                        | Run pre-post only                                               |
+---------------------------------+-----------------------------------------------------------------+
| -r                              | List all releases/program                                       |
+---------------------------------+-----------------------------------------------------------------+
| -r<V>                           | Use the specified version                                       |
+---------------------------------+-----------------------------------------------------------------+
| -t <X>                          | Specify the number of Processors                                |
+---------------------------------+-----------------------------------------------------------------+
| -tm                             | Specify the number of Processes for Meshing                     |
+---------------------------------+-----------------------------------------------------------------+




++++++++++++++++++++++++++++++++++++++++++++++++++
ANSYS CLI Program Quick List
++++++++++++++++++++++++++++++++++++++++++++++++++
The following table lists the Global ANSYS programs and their associated CLI command.


+-----------------+-----------------------+
| Program         | Name                  |
+=================+=======================+
| Mechanical ADPL | ansys212, ansys2021R2 |
+-----------------+-----------------------+
| ANSYS Workbench | runwb2                |
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


