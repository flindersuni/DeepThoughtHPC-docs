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

APDL, Fluent and the EM Suite / HFSS all have a common requirement. All script, journal or run files **must** have been generated in *TUI* Mode. This means that all commands must been created, and saved via the 
programs' Command Line Interface. An example of this is - in Fluent, you **cannot** use the "Journal Recording" function via the GUI. When running the job, the GUI will not be available and Fluent **will fail**. 


========================================================================
ANSYS APDL Quickstart Command Line Guide
========================================================================

To run a job with ANSYS APDL on the HPC you will need the following: 
    - An ANSYS Script file 
    - Any reference file(s) (eg, a .db file)

Ensure that the paths to anything in the script file reflect where it lives on the HPC, not your local machine. When running with the ``-dis`` option, you must 
use a distributed filesystem like /scratch or /cluster, as all nodes will need to the the files, and /local is *not* visible between individual nodes. 
Below are some example command-line examples to get you started. 

Replace all <OPTIONS> to suit your requirements. You can omit the > PATH_TO_OUTPUT_FILE, and SLURM will capture the ANSYS output and write it to your ``#SBATCH --output=/path/to/file.out``. 

1. Shared-Memory Parallel (Single-Node)


``ansys212 -smp -np $SLURM_NTASKS -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE``

2. Distributed Mode (Multi-Node) 


``ansys212 -dis -mpi openmpi -np $SLURM_NTASKS -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE``

3. Hybrid Distributed Mode (Multi-Node Shared-Memory Parallel)


``ansys212 -dis -mpi openmpi -np $SLURM_NTASKS -nt $SLURM_CPUS_PER_TASK <SLURM Memory Allocation> -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE``

4. GPU Hybrid Distributed Mode (Multi-Node Shared-Memory Parallel with GPU Acceleration)


``ansys212 -dis -mpi openmpi -np $SLURM_NTASKS -nt $SLURM_CPUS_PER_TASK -acc nvidia -na <GPU_COUNT_PER_NODE> -b -s < PATH_TO_SCRIPT_FILE > PATH_TO_OUTPUT_FILE`` 

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

3. You **MUST** use #SBATCH --mem-per-cpu= instead of #SBATCH --mem= to prevent unintended memory allocation layouts
   
``#SBATCH --mem-per-cpu=3G``

4. You **MUST** use the -mpi=openmpi flag when running fluent. The Default IntelMPI *will not work*, and hangs indefinitely 
5. When recording your Journal File, you **MUST** input the commands via the Command-Line or it *will not work*.
6. You **MUST** alter all paths in the TUI Journal File to use ``/`` instead of ``\``, or it *will not work* 
7. You **MUST** alter all paths in the TUI Journal File to be ``/absolute/path/to/your/file``,  or it *will not work*
8. You **MUST** replace the final command of ``/close-fluent`` with ``/exit y`` or your *job will hang until it times out and SLURM kills it*


++++++++++++++++++++++++++++++++++++++++++++++
ANSYS Fluent CLI Solver List 
++++++++++++++++++++++++++++++++++++++++++++++

You must match the solver mode to the mode you created the mesh with.  If you attempt to solve a Double-Precision Mesh with a Single-Precision solver, 
Fluent will crash.

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
| -cnf                            | A MPI Hosts file for Distributed Shared Memory Parallel         |
+---------------------------------+-----------------------------------------------------------------+

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Fluent Shared-Memory Parallel  / Distributed Mode
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Fluent MPI / Distributed Mode needs a 'Hosts' file to tell it what machines to use. Use the below snippet 
generate a file that can be used as the ``-cnf=`` parameter to ensure the Distributed shared-memory parallel
works correctly. 

    # Write Number of Procs/Host to Temp File in /home/<USER>/
    HOST_FILE=~/$SLURM_JOBID.fluent.hosts.txt
    T_HOSTS=~./T_HOSTS
    mpirun hostname | sort | uniq -c > $T_HOSTS

    # reformat to a 'HOSTS' file format that FLUENT likes
    cat ~/T_HOSTS | while read line; do
            echo $line | awk '{print $2":"$1}' >> $HOST_FILE
    done


You can then invoke Fluent like so, assuming you use the snippet: 

``fluent 3ddp -g -nm -cnf=$HOST_FILE -mpi=openmpi -i /path/to/TUI/journal/file``


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


========================================================================
ANSYS EDT (Formerly, HFSS) Quickstart Command Line Guide
========================================================================

To run a job with ANSYS Electronics Desktop (Formerly, HFSS) on the HPC you will need the following: 
    - Your .aedt File

Ensure that the paths to anything in the script file reflect where it lives on the HPC, not your local machine. 
Below are some example command-line examples to get you started. 

1. The general format of a ANSYS EDT Command is: 

``ansysedt <options> <run command> <project name/script name>``

2. Single-Node Execution, No GPU 

``ansysedt -ng -batchsolve -Distributed -machinelist list="$SLURM_NODELIST:$SLURM_NTASKS:$SLURM_CPUS_PER_TASK -monitor /path/to/project.aedt"``

3. Single-Node Execution, GPU Enabled 

``ansysedt -ng -batchsolve -Distributed --machinelist list="$SLURM_NODELIST:$SLURM_NTASKS:$SLURM_CPUS_PER_TASK -monitor -batchoptions "EnbleGPU=1"  /path/to/project.aedt``


1. Multi-Node

``Under Testing``

++++++++++++++++++++++++++++++++++++++++++++++
ANSYS EDT CLI Quick List 
++++++++++++++++++++++++++++++++++++++++++++++

All of these options have expanded options for specific use cases. If you need the options, please contact the HPC Team. 

+---------------------------------------+------------------------------------------------------------------------------------+
| CLI Option                            | Description                                                                        |
+=======================================+====================================================================================+
| -batchsolve                           | Enable Batch Solving                                                               |
+---------------------------------------+------------------------------------------------------------------------------------+
| -ng                                   | Disable GUI, Required for SLURM Jobs                                               |
+---------------------------------------+------------------------------------------------------------------------------------+
| -Local / -Remote / -Distributed       | Solver distribution Type, prefer -Distributed                                      |
+---------------------------------------+------------------------------------------------------------------------------------+
| -machinelist list="host:tasks:cpus"   | Define the Machine List for Distributed tasks. Required for -Distributed           |
+---------------------------------------+------------------------------------------------------------------------------------+
| -machinelist file="/path/to/file"     | Instead of a CLI option, define a file to use as the Machine list for -Distributed |
+---------------------------------------+------------------------------------------------------------------------------------+
| -batchoptions="option1=value,options" | Specific batch options. A useful one: EnableGPU=1                                  |
+---------------------------------------+------------------------------------------------------------------------------------+
| -monitor                              | Print progress to STDOUT                                                           |
+---------------------------------------+------------------------------------------------------------------------------------+

====================================
ANSYS RSM: Remote Solve Manager
====================================

Last, but certainly not least - the GUI based, fire-and-forget Remote Solve Manger. 

There are a few hoops that you must jump through to get it all setup to work with DeepThought. RSM is hard-locked per version of the application. 

Currently, only 2021R2 is supported. 

You will need to the following installed: 

1. ANSYS RSM Configuration 2021R2 
2. ANSYS Workbench
3. Fluent / Mechanical / Electrical App 

All of the above assumes that already have access to DeepThought. If not, then you will need to ask for access to the HPC.

++++++++++++++++++++++++++++++++++++++++++++++++
Setting Up ANSYS RSM 2021R2 for DeepThought
++++++++++++++++++++++++++++++++++++++++++++++++

Below is a checklist for getting ANSYS RSM online. 99% of this checklist is initial setup, and after its all set, you `do not` need to do it again!

1. Open ANSY RSM Configuration

2. Add a 'New HPC Resource'

3. Set the 'Name' field to a name you want to refer to this configuration as 

4. Set the 'HPC Type' to to 'SLURM'

5. Set the 'Submit Host' to hpc-head01.deept.flinders.edu.au 

6. Remember the SLURM 'Job Submission Arguments'. Take a stab at how much RAM per CPU you want, and add --mem-per-cpu=3G etc, to this line. If submitting to the `high-capacity` queue, you will also need to add --qos=hc-concurrent-jobs to this field as well!

7. Ensure that 'User SSH protocol for Inter and intra-node communications is Ticked'

8. 'How Does the Client communicate with SLURM is 'Able to Directly Submit Jobs'

9. Click to the 'File Management' Tab 

10. 'Client to HPC File Management' is 'RSM Internal File Transfer Mechanism'

11. 'Staging Directory on the HPC Cluster', is a directory of your choice on /scratch. For example ``/scratch/user/<FAN>/ANSYS_STAGE_IN/``

12. 'HPC Side File-Management' is set to 'Scratch directory local to the execution node(s)'

13. 'HPC Scratch directory' is set to ``$TEMPDIR``. This is a HPC Admin team managed variable, so it will `just work`. 

14. Click to the 'Queues' Tab

15. Use the Autodiscover Options to get RSM to fill out the Queues for you. 

16. Use your FAN + Password to allow RSM to log into the HPC on your behalf

17. Close the RSM Configuration for now. Open your Project in your ANSYS App (Mechanical/Fluent etc.)

18. Find the 'Solve Process Settings', and open it. 

19. Create a new entry, and point it at the RSM Queue you want to use. RSM Queues are the same as the HPC Queues.

20. Set this new RSM as the 'Default' for your program if you `always` want to use RSM via the HPC to solve things.

21. Open Workbench. For each project that you want to use RSM for, select the 'Solution Properties'

22. Set the 'Solution Process' to 'Submit to Remote Solve Manager'

23. Set the 'Solve Process Setting' to the new setting you just made in Mechanical/Fluent etc. 

24. Leave Workbench open for now, SSH into the HPC. 

25. Edit your ~/.bashrc file. Right at the end, add the following ``module load intel-compilers``. ANSYS has a nice hidden call to ``ifort`` for user-added functions, so you MUST auto-load the intel-compilers for your user account, or it will fail. 

26. Back to Workbench, and now we can hit 'Solve'.

27. Watch the HPC queue, you should see job appearing 

28. You can also open the RSM Job Monitor program, and watch your jobs there.

29. DONE! The only alterations would be to the 'Job Submission Arguments' to tweak your --mem-per-cpu= parameter, or if submitting to the high-capacity queue, adding --qos=hc-concurrent-jobs
