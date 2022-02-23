Storage Overview & Usage Guidelines 
==========================================
.. _System Specifications: ../system/deepthoughspecifications.html

The HPC is a little different that your desktop at home when it comes to storage, not just computing power. It's a shared resource, so we cant store everybody's data for all time - there just isn't enough space. 
So, before we start putting files onto the HPC, its best you know where to put them in the first place. 

On DeepThought, are two main storage tiers. Firstly our bulk storage is the 'Scratch' area - and is slower, spinning Hard-Disk Drives (HDD's).
The smaller, hyper-fast NVMe Solid-State Drives (SSD's) are located at /local and is much smaller. For the exact specifications and capacities, see the `System Specifications`_.

There is a critical difference between these two locations. The /scratch area is a common storage area. You can access it from all of the login, management and compute nodes on the HPC. This is not the same as /local, which is only available on each compute node.  That is - if you job is running on Node001, the /local only exists on that particular node - you cannot access it anywhere else on the HPC.

.. attention:: The HPC Job & Data Workflow, along with links to the new Data-Workflow Management Portal are under construction and will be linked here when completed.

################################
Storage Accessibility Overview
################################
As general guide, the following table presents the overall storage for the HPC.

+-----------------------+--------------------------+-----------------------------+
| Filesystem Location   | Accessible From          | Capacity                    |
+=======================+==========================+=============================+
| /scratch              |    All Nodes             | ~250TB                      |
+-----------------------+--------------------------+-----------------------------+
| /home                 | All Nodes                |    ~12TB                    |
+-----------------------+--------------------------+-----------------------------+
| /local                | Individual Compute Nodes | ~400GB or ~1.5TB            |
+-----------------------+--------------------------+-----------------------------+
| /RDrive/\<Share Name> |              Head Nodes  | Share Dependant             |
+-----------------------+--------------------------+-----------------------------+

.. warning:: The HPC is classed as **volatile** storage. Your research data and dataset that you wanted backed up MUST be moved to /RDrive.

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
Here is a rough guide as to what should live in your /home/$FAN directory. In general, you want small, little things is here.

* SLURM Scripts
* Results from Jobs.
* 'Small' Data-Sets (<5GB)

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

=========
/Local
=========

Local is the per-node, high speed flash storage that is specific to each node. When running a job, you want to run your data-sets on /local if at all possible - its the quickest storage location on the HPC. You MUST clean-up /local once you are done.

^^^^^^^^^^^^^^^^^^^^^^^^^
What to Store in /local
^^^^^^^^^^^^^^^^^^^^^^^^^

Only *transient files* should live on /local. Anything that your job is currently working on should be on /local. Once your job has finished with these files, they should be copied (or moved) to /scratch. The directory you were working in on /local should then cleaned, removing all files from your job.