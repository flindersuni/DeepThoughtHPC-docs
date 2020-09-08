HPC Etiquette 
==================
The HPC is a shared resource, and to help make sure everybody can 
continue to use the HPC together, the following provides some expected
behavior. 

Head / Login / Management Nodes
--------------------------------

1) The Head / Login / Management Nodes are to be used for light, single-threaded tasks only.

2) If it takes more than 5-10 minutes or > 2-3GB of RAM, do NOT run it on the head node.

3) Some acceptable tasks include:

    * Compiling software for your own use
    * Transferring / Decompressing Files 
    * Light Pre/Post Processing 
    * SLURM Job Management 


General Cluster Rules 
------------------------

1) Use only the resources you need, remembering this is shared resource.

2) Clean up your disk usage in /scratch and /home regularly.

3) Do not attempt to bypass security controls.

4) Do not attempt to bypass job Scheduling.

5) Do not access the compute nodes directly.

6) Utlise /local on the compute nodes for your data sets if possible.


Permissions & Access Levels 
----------------------------
The HPC has the following capabilities. If a capability is NOT listed, 
then you are not permitted to perform the action. Security is approached 
via a list of allowed actions, not a list of denied actions. 

General User 
+++++++++++++++

1) Full read & write permission to your own /scratch/FAN and /home/FAN locations 

2) The ability to compile and run your own software, stored in your /home directory 

3) The ability to run any module present in the module system 

4) Manipulate your own jobs via SLURM


Group Admins 
+++++++++++++
Trusted partners may be appointed 'Group Administrators' at the *sole discretion of the HPC Team* allowing them to: 

1) Perform all actions of a general user

2) Manipulate SLURM actions of users under their remit 


Permissions that are Never Granted
+++++++++++++++++++++++++++++++++++++
The following is a non-exhaustive list of permissions that are never, and will never, be granted to end-users. The HPC is a complicated system 
and, while the Support Team is asked for these permissions quite often, the potential inadvertent damage to systems means these permissions cannot be provided. 

1) Root or Sudo access

2) Global 'Module' Software Installation 

3) Elevated Access to the HPC System 

4) Access to Managerial Systems 


If You Break These Rules 
----------------------------
If you break these rules the HPC Team may take any or all of these actions: 

* Cancellation of Tasks
* Removal problematic files and/or programs
* Warning of expected behavior
* Termination of identified problematic processes
* Revocation of HPC Access
