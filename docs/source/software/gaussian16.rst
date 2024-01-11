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

The below bash function will setup G16 to run correctly, no matter if you asked for GPU or CPU on a single node. There are several ways you can use this script: 

#. Copy and past the method body (everything between { and } ) ``inline`` *before* you start ``g16``. 
#. Copy the entire snippet, then call the setup method as ``setup_g16_env`` *before* you start ``g16``
#. Store it somewhere, and call it as either ``. /path/to/env/setup/script.sh`` or ``source /path/to/env/setup/script``, again, *before* you start ``g16``. 

The script is as follows::

    #!/bin/bash
    # Author: Scott Anderson
    # Version: 1.0
    # Reason: Gaussian16 just... doesn't do auto-detection. This script sets up the CDEF, GDEF, MDEF, MDisk and SCRDir correctly to allow for gaussian to function in parallel without stomping all over SLURM.
    # Notes: Abuses the fact that SLURM will quite nicely set affinity for us, so we can do a limited amount of parsing
    #        We do split out the working CPU set, just for 'verification', but G16 still needs the 'GPU Controller' CPU's in its main 'CPU' List
    #        Or it will complain about 'CPUID not bound to thread' and then die in a fire. Hence, the stange dance of lazy awk sub() calls, but not actually
    #        using the list that gets created as the CDEF= option.
    #        
    #        A known limitation: Only up to 2 GPUs. Thats the max we have per node on DeepThought, so thats what we can deal with. 
            
    setup_g16_env() {
            # Do the memory first.
            ALLOWED_MEM=`cat /sys/fs/cgroup/memory/slurm/uid_$UID/job_$SLURM_JOB_ID/memory.limit_in_bytes | numfmt --to-unit=M`
            BUFFER_MEM=`echo $(( $ALLOWED_MEM - 512 ))`
            export GAUSS_MDEF=`echo $BUFFER_MEM"MB"`
            echo "GAUSS_MDEF set to $GAUSS_MDEF, from a SLURM Maximum of $ALLOWED_MEM"
            # Scratch Disk & Max Disk Read/Write 
            export GAUSS_SCRDIR=$BGFS 
            export GAUSS_RDEF="Maxdisk=-1"
            export CPUS_ALLOCATED=`cat /sys/fs/cgroup/cpuset/slurm/uid_$UID/job_$SLURM_JOB_ID/cpuset.cpus`
            # Check to see if we got a list or a run of cpus, e.g., 12,13,15,61 vs. 64-72.
            # FYI needs further testing to handle the possibility of 1,2,3,5-22 in the list.
            if [[ "$CPUS_ALLOCATED" == *"-"* ]]; then
                    echo "Found Sequential CPU list of $CPUS_ALLOCATED, converting to individual core ID's...."
                    START_SEQ=`echo $CPUS_ALLOCATED | awk '{split($0,a,"-");print a[1]}'`
                    END_SEQ=`echo $CPUS_ALLOCATED | awk '{split($0,a,"-");print a[2]}'`
                    echo "Start: $START_SEQ End: $END_SEQ"
                    if [[ $START_SEQ && $END_SEQ ]]; then
                            export CPUS_ALLOCATED=`seq -s ',' $START_SEQ $END_SEQ`
                            echo "CPUs set to $CPUS_ALLOCATED..."
                    else
                            echo "FOUND SEQUENCE, BUT UNABLE TO FIGURE OUT START AND END OF LISTS. CANNOT SETUP GAUSSIAN, JOB EXITING!"
                            exit 99
                    fi
            fi
            if [[ -z $CUDA_VISIBLE_DEVICES ]]; then
                    echo "No Allocated or visible GPU devices. Not exporting GAUS_GDEF="
                    export GAUSS_CDEF=$CPUS_ALLOCATED
                    echo "GAUSS_CDEF set to $CPUS_ALLOCATED"
                    return
            else
                    echo "Found CUDA Visible Devices: $CUDA_VISIBLE_DEVICES"
                    # Are we >1 GPU?
                    IFS="," read -r -a array <<< $CUDA_VISIBLE_DEVICES;
                    if [[ ${#array[@]} -eq 2 ]]; then
                            echo "Found 2 GPUs..."
                            export C_CPU_1=`echo $CPUS_ALLOCATED | awk '{split($0,a,","); print a[1]}'`
                            export C_CPU_2=`echo $CPUS_ALLOCATED | awk '{split($0,a,","); print a[2]}'`
                            echo "GPU Control CPUs: $C_CPU_1 $C_CPU_2"
                            export WORK_CPUS=`echo $CPUS_ALLOCATED | awk '{split($0,a,","); sub(a[1]",", "", $0); sub(a[2]",","",$0); print $0}'`
                            echo "Work CPUS: $WORK_CPUS"
                            export GAUSS_GDEF="$CUDA_VISIBLE_DEVICES=$C_CPU_1,$C_CPU_2"
                            echo "GAUSS_GDEF set to: $GAUSS_GDEF"
                            export GAUSS_CDEF=$CPUS_ALLOCATED
                            echo "GAUSS_CDEF set to: $CPUS_ALLOCATED"
                            return
                    elif [[ ${#array[@]} -eq 1 ]]; then
                            echo "Found a Single GPU..."
                            export C_CPU_1=`echo $CPUS_ALLOCATED | awk '{split($0,a,","); print a[1]}'`
                            export WORK_CPUS=`echo $CPUS_ALLOCATED | awk '{split($0,a,","); sub(a[1]",", "", $0);  print $0}'`
                            echo "Work CPUS: $WORK_CPUS"
                            export GAUSS_GDEF="$CUDA_VISIBLE_DEVICES=$C_CPU_1"
                            echo "GAUSS_GDEF set to: $GAUSS_GDEF"
                            export GAUSS_CDEF=$CPUS_ALLOCTED
                            echo "GAUSS_CDEF set to: $CPUS_ALLOCATED"
                            return

                    else
                            echo "CRITICAL ERROR! WE CAN SEE $CUDA_VISIBLE_DEVICES as NOT EMPTY, BUT UNABLE TO EXTRA GPU ID's NEEDED"
                            echo "SETTING GAUSSING TO CPU ONLY MODE!"
                            export GAUSS_CDEF=$CPUS_ALLOCATED
                            echo "GAUSS_CDEF set to $CPUS_ALLOCATED"
                            return
                    fi
            fi
        }
    # Call method as named
    setup_g16_env 


+++++++++++++++++++++++++++++++++++++++
Multi-Node Parallelism: Linda Workers
+++++++++++++++++++++++++++++++++++++++

Linda is the mechanism for Multi-Node parallelism for Gaussian. As **not all algorithms in Gaussian scale well beyond a single node**, 
each job will need testing to identify if MPI-Enabled jobs gain you any significant speedup. 

Do not attempt to mix this with the above script for single-node setup, as it WILL almost certainly fail.


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
