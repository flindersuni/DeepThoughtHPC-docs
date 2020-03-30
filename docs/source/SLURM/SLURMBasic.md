# SLURM: The Basics

These are some of the basic commands. The Slurm quick start guide is also very helpful to acquaint yourself with the most used commands.

Slurm has also produced the [Rosetta Stone](../../_static/SLURMRosettaStone.pdf) - a document that shows equivalents between several workload managers.

## Job submission

Once the slurm script is modified and ready to run, go to the location you have saved it and run the command:

    sbatch <name of script>.sh

To test your job use:

    sbatch --test-only <name of script>.sh

This does not actually submit anything. Useful for testing new scripts for errors.

## Job information

List all current jobs for a user:

    squeue -u <username>

List all running jobs for a user:

    squeue -u <username> -t RUNNING

List all pending jobs for a user:

    squeue -u <username> -t PENDING

List all current jobs in the shared partition for a user:

    squeue -u <username> -p shared

List detailed information for a job (useful for troubleshooting):

    scontrol show jobid -dd <jobid>

## Cancelling a job

To cancel a job based on the jobid, run the command:

    scancel <jobid of the job to cancel>

To cancel a job based on the user, run the command: 

    scancel -u <username of job to cancel>

To cancel all the pending jobs for a user:

    scancel -t PENDING -u <username>

To cancel one or more jobs by name:

    scancel --name myJobName

To hold a particular job from being scheduled:

    scontrol hold <jobid>

To release a particular job to be scheduled:

    scontrol release <jobid>

To requeue (cancel and rerun) a particular job:

    scontrol requeue <jobid>
