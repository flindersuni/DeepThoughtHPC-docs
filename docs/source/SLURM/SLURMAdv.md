

Using job arrays allows a user to deal with large numbers of jobs. For more information, see SLURM job arrays.

To cancel an indexed job in a job array:

scancel <jobid>_<index>

To find the original submit time for your job array:

sacct -j 32532756 -o submit -X --noheader | uniq

 

The following are good for both jobs and job arrays. Commands can be combined to allow efficiency and flexibility.

Suspend all running jobs for a user (takes into account job arrays):

squeue -ho %A -t R | xargs -n 1 scontrol suspend

Resume all suspended jobs for a user:

squeue -o "%.18A %.18t" -u <username> | awk '{if ($2 =="S"){print $1}}' | xargs -n 1 scontrol resume

After resuming, check if any are still suspended:

squeue -ho %A -u $USER -t S | wc -l

The following is useful if your group has its own queue and you want to quickly see usage:

lsload |grep 'Hostname\|<partition>'
