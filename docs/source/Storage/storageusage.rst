Storage Overview & Usage Guidelines 
==========================================
.. _System Specifications: ../system/deepthoughspecifications.html

The HPC is a little different that your desktop at home when it comes to storage, not just computing power. It's a shared resource, so we cant store everybody's data for all time - there just isn't enough space. 
So, before we start putting files onto the HPC, its best you know where to put them in the first place. 

On DeepThought, are two main storage tiers. Firstly our bulk storage is the 'Scratch' area - and is slower, spinning Hard-Disk Drives (HDD's).
The hyper-fast NVMe Solid-State Drives (SSD's) are located at /local and are much smaller. For the exact specifications and capacities, see the `System Specifications`_.

There is a critical difference between these two locations. The /scratch area is a common storage area. You can access it from all of the login, management and compute nodes on the HPC. This is not the same as /local, which is only available on each compute node.  That is - if your job is running on Node001, the /local only exists on that particular node - you cannot access it anywhere else on the HPC.

################################
Storage Accessibility Overview
################################
As general guide, the following table presents the overall storage for the HPC.

+---------------------+--------------------------+-------------------------------------+
| Filesystem Location | Accessible From          | Capacity                            |
+=====================+==========================+=====================================+
| /scratch            |    All Nodes             | ~250TB                              |
+---------------------+--------------------------+-------------------------------------+
| /home               | All Nodes                |    ~12TB                            |
+---------------------+--------------------------+-------------------------------------+
| /local              | Individual Compute Nodes | ~400GB or ~1.5TB                    |
+---------------------+--------------------------+-------------------------------------+
| /r_drive/\<folder>  |               Head Nodes | N/A                                 |
+---------------------+--------------------------+-------------------------------------+
| /RDrive             |  Head Nodes              | Variable, Size of R-Drive Allocation|
+---------------------+--------------------------+-------------------------------------+             

.. attention:: /The r_drive/ location is NOT the University R:\\ Drive. It is a remnant from eRSA that is being phased out to the University R:\\ Drive. 

The /r_drive/ locations are data mount points from the now defunct eRSA Project and are slowly being phased out. Any point under /r_drive/ will *auto mount on access*. Just attempt to touch or change to the correct directory under the /r_drive/ path and the HPC will handle this automatically for you. Until you do this, the directory **will be invisible**.

#########################
Usage Guidelines
#########################

The following sections will go over the individual storage location/mounts along with some general guidelines of what should be stored where.

=======
/Home
=======
Your 'home' directories. This is a small amount of storage to store your small bits and pieces. This is the analogous to the Windows 'Documents' folder. At a command promp, your home directory will be shortened to ~/.

^^^^^^^^^^^^^^^^^^^^^^^^
What to store in /home
^^^^^^^^^^^^^^^^^^^^^^^^
Here is a rough guide as to what should live in your /home/$FAN directory. In general, you want to store small miscellaneous files here. 

1. SLURM Scripts
2. Results from Jobs.
3. 'Small' Data-Sets (<5GB)
4. Self-Installed Programs or Libraries

==========
/Scratch
==========

Scratch is your working space and 'Large Dataset Storage' As you can see from the table above it have far more storage capacity than /home. If you need to store a large data-set, then it should live in here.

^^^^^^^^^^^^^^^^^^^^^^^^^^
What to store in /scratch
^^^^^^^^^^^^^^^^^^^^^^^^^^

Here is a rough guide as to what should live in your /scratch/$FAN directory. In general, anything large, bulky and only needed for a little while should go here.
  
1. Job Working Data-sets
2. Large Intermediate Files

=========
/Local
=========

.. _SLURM Temporary Directories: ../SLURM/SLURMIntro.html#tmpdir-and-slurm-job-arrays
Local is the per-node, high speed flash storage that is specific to each node. When running a job, you want to run your data-sets on /local if at all possible - its the quickest storage location on the HPC. You MUST cleanup /local once you are done.

^^^^^^^^^^^^^^^^^^^^^^^^^
What to Store in /local
^^^^^^^^^^^^^^^^^^^^^^^^^

Only *transient files* should live on /local. Anything that your job is currently working on should be on /local. Once your job has finished with these files, they should be copied (or moved) to /scratch. The directory you were working in on /local should then cleaned, removing all files. 

The HPC creates a /local directory for you per job that can be used in your SLURM scripts. This is covered in more detail in `SLURM Temporary Directories`_.

===========
/RDrive
===========

/RDrive is the location for all RDrive allocations.  The HPC will discover and automatically display any RDrive Folders you have access to.

All /RDrive mount points are only surfaced on the Head-Node. The /RDrive is not present on the compute nodes and you cannot use it as a part of your SLURM scripts. 

The /RDrive is not a location to perform any computation on, and is limited in access speed. All data that forms part of dataset for calculations
must be copied to a HPC local mount before you commence work. 