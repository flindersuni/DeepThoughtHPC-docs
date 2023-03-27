-------------------------
Gaussian 
-------------------------
=====================
Gaussian  Status
=====================

Gaussian 16 is installed and available for use on the HPC.

.. _Gaussian16 Home: https://gaussian.com/gaussian16/

====================
Gaussian Overview 
====================

From `Gaussian16 Home`_: 

Gaussian 16 is the latest in the Gaussian series of programs. It provides state-of-the-art capabilities for electronic structure modelling. 
Gaussian 16 is licensed for a wide variety of computer systems. All versions of Gaussian 16 contain every scientific/modelling feature, 
and none imposes any artificial limitations on calculations other than your computing resources and patience.


++++++++++++++++++++++++++++++++++++++++++++++++++
Gaussian Program Quick List
++++++++++++++++++++++++++++++++++++++++++++++++++

The main binary for Gaussian is ``g16``.


++++++++++++++++++++++++++++++++++++++
Running Gaussian SLURM Jobs 
++++++++++++++++++++++++++++++++++++++

Gaussian can be somewhat tricky to ensure that it runs in parallel under SLURM. Below are some starting points for you to fine-tune your Guassian runs.  Please remember that 
not all Gaussian algorithms scale well across *multiple nodes*. There are also several variables to you will want to set, or your job will almost certainly crash!

The below options are known to work well as a starting point for general options. These must be before the call to ``g16``: 

- export GAUSS_SCRDIR=$BGFS 
- export GAUSS_RDEF="Maxdisk=-1" 
- export GAUSS_MDEF="$(($SLURM_CPUS_PER_TASK*$SLURM_MEM_PER_CPU-1000))MB"



-------------------------
Single-Node Parallelism 
-------------------------

The ``-c`` CLI Option or the GAUSS_CDEF="" environment variable are what must be set for Gaussian to use >1 CPU Core.

Gaussian expects a list of hardware CPU ID's. You can obtain this within any job launched via SLURM with the following: 

``CPUS_ALLOCATED=`cat /sys/fs/cgroup/cpuset/slurm/uid_$UID/job_$SLURM_JOB_ID/cpuset.cpus``

You can then either: 

- export GAUSS_CDEF=$CPUS_ALLOCATED; # Must be before your call to ``g16``
- g16 -c=$CPUS_ALLOCATED 


--------------------------------------
Multi-Node Parallelism: Linda Workers
--------------------------------------

Linda is the mechanism for Multi-Node parallelism for Gaussian. As **not all algorithms in Gaussian scale well beyond a single node**, 
each job will need testing to identify if MPI-Enabled jobs gain you any significant speedup. 


The following SLURM Snippet is a starting point for Multi-Node execution of Gaussian16::

    ## Guassian16 may benefit from >1 CPU/Task.
    #SBATCH --cpus-per-task=1
    #SBATCH --mem-per-cpu=<Memery needed per CPU>
    #SBATCH --ntasks=<Total Number of Tasks Wanted"
    # 1 Day Runtime, alter as needed 
    #SBATCH --time=1-0 
    # Will write to the $SLURM_SUBMIT_DIR, which is wherever you call sbatch <file>
    #SBATCH --output=%x-%j.out
    #SBATCH --error=%x-%j.err

    module load gaussian
    #SLURM sets this for us, but just in case.
    export OMP_NUM_THREADS=1
    # Make sure LINDA Workers are more talkative
    export GAUSS_LFLAGS="-v"
    # G16 Scratch is in /cluster/jobs/<FAN>/JOBID/
    export GAUSS_SCRDIR=$BGFS
    # Generate the Linda Parallel hosts file
    # If you need >1 CPU/Task, this will need alteration, to append each-nodes CPUSet as well as the node-name
    for n in `scontrol show hostname | sort -u`; do
    echo ${n}
    done | paste -s -d, > g.nodes.$SLURM_JOBID

    # Datestamp Start of G16 run in the SLURM Output file
    date
    g16 -w=`cat g.nodes.$SLURM_JOBID` <INPUT FILE>
    # Datestamp End of G16 run in the SLURM Output file
    date

    # remove the par-nodes file
    rm g.nodes.$SLURM_JOBID
