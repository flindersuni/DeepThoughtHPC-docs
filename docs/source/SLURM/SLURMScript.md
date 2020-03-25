
# SLURM: Example Script

    #!/bin/bash

    ##################################################################

    # Please note that you need to adapt this script to your job

    # Submitting as is will fail cause the job to fail 

    ##################################################################

    # Change FAN to your fan account name

    # Change JOBNAME to what you want to call the job

    #

    #SBATCH --job-name=FAN_JOBNAME

    #

    ##################################################################

    # This section is optional delete if not required

    #

    # Change MYEMAIL to your email address

    #SBATCH --mail-user=MYEMAIL@flinders.edu.au

    #SBATCH --mail-type=ALL

    #     (ALL = BEGIN, END, FAIL, REQUEUE)

    #

    ##################################################################

    # Change JOBNAME to the name of the job, this will put the job log

    # in your home directory

    #SBATCH --output=~/JOBNAME-log.txt

    #

    # Change PARTITIONNAME to the partition you have been granted 

    # access too run the job on. 

    # Valid partitions 's are hpc_cmph, hpc_cse, hpc_other, and 

    # hpc_melfeu

    #

    #SBATCH --partition=PARTITIONNAME

    #

    ##################################################################

    # This section is optional delete if not required

    #

    # Change DAYS and HOURS to how long you want the job to run for

    #

    #SBATCH --time=DAYS-HOURS

    #

    ##################################################################

    # Change ntasks to the number of tasks the script will run

    #SBATCH --ntasks=1

    #

    # Change the cpus-per-task to the number of CPU's to be used

    #SBATCH --cpus-per-task=1

    #

    ##################################################################

    # This section is optional delete if not required

    #

    # Set the memory requirements for the job in MB. Your job will be

    # allocated exclusive access to that amount of RAM. In the case it

    # overuses that amount, Slurm will kill it. The default value is 

    # around 2GB per core.

    #

    # Note that the lower the requested memory, the higher the

    # chances to get scheduled to 'fill in the gaps' between other

    # jobs. 

    #

    #SBATCH --mem-per-cpu=128

    #

    ##################################################################

    # This section is optional delete if not required

    #

    # Change the number of GPU's required

    # If no GPU's are required leave at 0

    # The most GPU's that can be requested is 2

    #

    #SBATCH --gres="gpu:0"

    #

    ##################################################################

    # This section is optional delete if not required

    #

    # Load any modules that are required

    module add python36

    #

    ##################################################################

    # This section is optional delete if not required

    #

    # If required copy your data to the scratch location for 

    # processing, change FAN and JOBNAME

    cp /???/???? /scratch/user/FAN/JOBNAME

    #

    ##################################################################

    # Enter required steps below the job will run

    #

    python36 Generator.py

    #

    ##################################################################

    # This section is optional delete if not required

    #

    # If required copy your data from the scratch location,  

    # change FAN and JOBNAME

    #

    cp -avr /scratch/user/FAN/JOBNAME/ ~/JOBNAME/

    #

    ##################################################################
