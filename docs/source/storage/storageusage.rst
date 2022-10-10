Storage Overview & Usage Guidelines 
==========================================
.. _System Specifications: ../system/deepthoughspecifications.html

The HPC is a little different that your desktop at home when it comes to storage, not just computing power. It's a shared resource, so we cant store everybody's data for all time - there just isn't enough space. 
So, before we start putting files onto the HPC, its best you know where to put them in the first place. 

On DeepThought, are three main storage tiers. Firstly our bulk storage is the 'Scratch' area - and is slower, spinning Hard-Disk Drives (HDD's). The next storage tier is the 'Cluster' parallel filesystem. 
For distributed jobs, or jobs that required lots of staged files, this filesystem is the standard high-speed and low-latency HPC filesystem. Be aware that it is smaller that /scratch, 
and as such, is a `transient` filesystem. Finally, there are hyper-fast NVMe Solid-State Drives (SSD's) located at /local. For the exact specifications and capacities, see the `System Specifications`_.

We also integrate into R-Drive to allow you access to your Research Data Storage allocations. This is an automatic process for any shares you have access to.  

There is a critical differences between these three locations, so please read this page carefully.

.. attention:: The HPC Job & Data Workflow, along with links to the new Data-Workflow Management Portal are under construction and will be linked here when completed.

################################
Storage Accessibility Overview
################################
As general guide, the following table presents the overall storage for the HPC.

+-----------------------+--------------------------+-------------------------+
| Filesystem Location   | Accessible From          | Capacity                |
+=======================+==========================+=========================+
| /scratch              | All Nodes                | ~250TB                  |
+-----------------------+--------------------------+-------------------------+
| /cluster              | All Nodes                | ~41TB                   |
+-----------------------+--------------------------+-------------------------+
| /home                 | All Nodes                | ~12TB                   |
+-----------------------+--------------------------+-------------------------+
| /local                | Individual Compute Nodes | ~1TB (400GB on Node019) |
+-----------------------+--------------------------+-------------------------+
| /RDrive/\<Share Name> | Head Nodes               | Share Dependant         |
+-----------------------+--------------------------+-------------------------+

.. warning:: The HPC is classed as **volatile** storage. Your research data and datasets that you wanted backed up MUST be moved to /RDrive, or off the HPC.

#########################
Usage Guidelines
#########################

The following sections will go over the individual storage location/mounts along with some general guidelines of what should be stored where.

==========
/Scratch
==========

Scratch is your working space and 'Large Dataset Storage' As you can see from the table above it have far more storage capacity than /home. If you need to store a large data-set, then it should live in here.

^^^^^^^^^^^^^^^^^^^^^^^^^^
What to store in /scratch
^^^^^^^^^^^^^^^^^^^^^^^^^^

Here is a rough guide as to what should live in your /scratch/$FAN directory. In general, anything large, bulky and only needed for a little while should go here.

* Job Working Data-sets
* Large Intermediate Files

===========
/cluster 
===========
.. _SLURM Guide: ../SLURM/SLURMIntro.html

Cluster is the new, high speed parallel filesystem for DeepThought, deployed using BeeGFS. It is highly recommended that you take advantage of high speeds available to reduce the I/O times associated with /scratch - so **please read this section carefully**. 

The directories you can write to in /cluster are controller by SLURM.  When you job starts, SLURM sets multiple environment variables and 
creates directories for you to use on this filesystem. See the environment variables sections of the `SLURM Guide`_ for more information. 

Once you job completes, is cancelled, or errors out, SLURM removes then entire directory of your job. That means, *if you do not move your data from the /cluster 
filesystem, you will lose all of it*. This is by design, and the HPC Team cannot recover any data lost this way. 

Each college is also limited to a **soft limit** on storage that mirrors their HPC SLURM allocation. This is currently

1. 45% CSE, ~18TB 
2. 45% CMPH, ~18TB 
3. 10% Other, ~5TB 

When this quota is exceeded, files can still be written, but the HPC Team is notified of the user and their associated usage.

^^^^^^^^^^^^^^^^^^^^^^^^^^^^
What to store in /cluster? 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Your working data sets
* Temporary job files 
* Results, before you copy them back to /scratch 

=======
/Home
=======
Your 'home' directories. This is a small amount of storage to store your small bits and pieces. This is the analogous to the Windows 'Documents' folder. At a command prompt, your home directory will be shortened to ~/.

^^^^^^^^^^^^^^^^^^^^^^^^
What to store in /home
^^^^^^^^^^^^^^^^^^^^^^^^
Here is a rough guide as to what should live in your /home/$FAN directory. In general, you want small, little things is here.

* SLURM Scripts
* 'Small' Results from Jobs
* 'Small' Data-Sets (<5GB)


=========
/Local
=========

Local is the per-node, high speed flash storage that is specific to each node. When running a job, you want to run your data-sets on /local if at all possible - its the quickest storage location on the HPC. You MUST clean-up /local once you are done.

^^^^^^^^^^^^^^^^^^^^^^^^^
What to Store in /local
^^^^^^^^^^^^^^^^^^^^^^^^^

Only *transient files* should live on /local. Anything that your job is currently working on can be on /local. Once your job has finished with these files, they should be copied (or moved) to /scratch. The directory you were working in on /local should then cleaned, removing all files from your job.