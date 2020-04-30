
# SLURM: Example Script

    #!/bin/bash
    # Please note that you need to adapt this script to your job
    # Submitting as is will fail cause the job to fail 
    # The keyword command for SLURM is #SBATCH --option
    # Anything starting with a # is a comment and will be ignored
    # ##SBATCH is a commented-out #SBATCH command
    ##################################################################
    # Change FAN to your fan account name
    # Change JOBNAME to what you want to call the job
    # This is what is shows when attmepting to Monitor / interrogate the job,
    # So make sure it is something pertinent!
    #
    #SBATCH --job-name=FAN_JOBNAME
    #
    ##################################################################
    # If you want email updates form SLURM for your job.
    # Change MYEMAIL to your email address
    #SBATCH --mail-user=MYEMAIL@flinders.edu.au
    #SBATCH --mail-type=ALL
    # 
    # Valid 'points of notification are': 
    # BEGIN, END, FAIL, REQUEUE. 
    # ALL means all of these
    ##################################################################
    # Tell SLURM where to put the Job 'Output Log' text file. 
    # This will aid you in debugging crashed or stalled jobs.
    #SBATCH --output=/home/$FAN/JOBNAME-log.txt
    ##################################################################
    # For now, you must select a partition for jobs to run on. 
    #  Valid partitions 's are hpc_cmph, hpc_cse, hpc_other and hpc_melfeu
    #SBATCH --partition=PARTITIONNAME
    ##################################################################
    # Tell SLURM how long your job should run for, at most. 
    # SLURM will kill/stop the job if it goes over this amount of time. 
    # Currently, this is unlimited - however, due to the upcoming 
    # implementation of Fairshare Score, you do not want to run a job
    # for too long.
    # The command format is as follows: #SBATCH --time=DAYS-HOURS
    #SBATCH --time=14=0
    #
    ##################################################################
    # How many tasks is your job going to run? 
    # Unless you are running something that is Parallel / Modular or
    # pipelined, leave this as 1.
    #
    #SBATCH --ntasks=1
    # If each task will need more that a single CPU, then alter this 
    # value. Remeber, this is multiplicative, so if you sk for 
    # 4 TASK and 4 CPUS per Task, you will be allocated 16 CPU;s 
    #SBATCH --cpus-per-task=1
    ##################################################################
    # Set the memory requirements for the job in MB. Your job will be
    # allocated exclusive access to that amount of RAM. In the case it
    # overuses that amount, Slurm will kill it. The default value is 
    # around 2GB per core.
    # Note that the lower the requested memory, the higher the
    # chances to get scheduled to 'fill in the gaps' between other
    # jobs. 
    #SBATCH --mem-per-cpu=4080MB
    ##################################################################
    # Change the number of GPU's required and the most GPU's that can be 
    # requested is 2. As there are limited GPU slots, they are heavily 
    # weighted against for Fairshare Score calculations. 
    # This line reqeuests 0 GPU's by default.
    #
    #SBATCH --gres="gpu:0"
    ##################################################################
    # Load any modules that are required. This is exactly the same as 
    # loading them manually, with a space-seperated list, or you can 
    # write multiple lines.
    # You will need to uncomment these.
    #module add miniconda/3.0 cuda10.0/toolkit/10.0.130 
    #module add miniconda/3.0 
    #module add cuda10.0/toolkit/10.0.130 
    ##################################################################
    # If you have not already transferred you data-sets to your /scratch 
    # directory, then you can do so as a part of you job.
    # Change the FAN and JOBNAME as needed.
    # REMOVE the data from /home when you do not need it, as /home space is
    # limited.
    
    # Copy Data to /scratch
    cp -r /home/$FAN/??DataDirectory?? /scratch/user/FAN/JOBNAME

    # Remove from /home
    rm -rf /home/$FAN/??DataDirectory??

    ##################################################################
    # Enter the command-line arguments that you job needs to run. 

    python36 Generator.py
    
    ##################################################################
    # Once you job has finished its processing, copy back your results 
    # and ONLY the results from /scratch. 

    cp /scratch/user/FAN/JOBNAME/??ResultsOutput.txt?? ~/JOBNAME/

    # Now, cleanup your /scratch directoryu of the extra data you have. 
    # If you need to keep the data-set for later usage, then utilise
    # your preffered method to get it OFF the HPC, and into your
    # local storage.
    rm -rf /scrach/user/FAN/JOBNAME
    ##################################################################
    # Print out the 'Job Efficency' - this is how well your job used the
    # resources you asked for. The higher the better!
    seff $SLURM_JOBID
