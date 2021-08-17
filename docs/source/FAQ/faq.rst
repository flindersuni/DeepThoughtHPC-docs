*****
FAQ 
*****

Below are some of the common steps that the team has been asked to resolve more than once, so we put them here to (hopefully) answer your questions before you have to wait in the Ticket Queue! 

What are the SLURM Partitions? 
===============================
There are three at this point: 

* general 
* gpu
* melfeu 

You can omit the 

* #SBATCH partition=<name> directive
    

as the sane-default for you is the hpc_general partition. If you need access to the GPU's you **must** user the hpc_gpu queue.

SLURM - Tasks & OpenMPI/MPI
===========================
When running jobs enabled with OpenMPI/MPI, there is some confusion around how it all works and what the correct settings for SLURM are. The biggest confusion is around what a 'Task' is, and when to use them.

Tasks
-----
Think of a task as a 'Bucket of Resources' you ask for. It cannot talk to another bucket without some way to communicate - this is what OpenMPI/MPI does for you. It lets any number of buckets talk to each other.

When asking SLURM for resources, when you ask for N Tasks, you will get N tasks of X size that you asked for, and all are counted against your usage. For example

* -N12 --cpus-per-task=10 --mem-per-cpu=2G

Will get you a combined *total* of 120 CPUs and 240GB of RAM *spread across 12 individual little instances*.

Running the Job
----------------
There are several ways to correctly start OpenMPI/MPI based programs. SLURM does an excellent job of integrating with OpenMPI/MPI, so usually it will 'Just Work'.  Its highly dependant upon how the program is structured and written.  Here are some options that can help you boot things when they do not go to plan.

* mpirun - bootstraps a program under MPI.  Best tested under a manual allocation via salloc.
* srun - Acts nearly the same as 'sbatch' but runs immediacy via SLURM, instead of submitting the job for later execution.

OOM Killer
-----------
Remember, that each 'task' is its own little bucket - which means that SLURM tracks it individually! If a single task goes over its resource allocation, SLURM will kill it, and usually that causes a cascade failure with the rest of your program, as you suddenly have a process missing.


IsoSeq3: Installation
=====================

IsoSeq3, from Pacific Bio Sciences has install instructions that won't get you all the way on DeepThought.  There are some missing packages and some commands that must be altered to get you up and running.
This guide will assume that you are starting from scratch, so feel free to skip any steps you have already performed. 

The steps below will:

* Create a new Virtual Environment
* Install the dependencies for IsoSeq
* Install IsoSeq3
* Alter a SLURM script to play nice with Conda

Conda/Python Environment
--------------------------
Only thing you will need to decide is 'where you want to store my environment' you can store it in your /home directory if you like or in /scratch. Just put it someplace that is easy to remember.
To get you up and running (anywhere it says FAN, please substitute yours):

* module load miniconda/3.0
* conda create -p /home/FAN/isoseq3 python=3.7
* source activate /home/FAN/isoseq3
* You may get a warning saying 'your shell is not setup to use conda/anaconda correctly' - let it do its auto-configuration. Then Issue

  * source ~/.bashrc
    
When all goes well, your prompt should read something similar to

.. image::  ../_static/conda_active_env.png
    
Notice the (/home/ande0548/isoseq3)? Thats a marker to tell you which Python/Conda Environment you have active at this point. 

BX Python 
----------
The given bx-python version in the wiki doesn't install correctly, and if it *does* work, then it will fail on run. To get a working version, run the following.

* conda install -c conda-forge -c bioconda bx-python

Which will get you a working version.

IsoSeq3 
---------

Finally, we can install IsoSeq3 and its dependencies. 

* conda install -c bioconda isoseq3 pbccs pbcoretools bamtools pysam lima


Will get you all the tools installed into your virtual environment. To test this, you should be able to call the individual commands, like so. 

.. image:: ../_static/conda_isoseq3_installed.png


SLURM Modifications
-------------------- 

You may get an issue when you ask SLURM to run your job about CONDA not being initialised correctly. This is a very-brute-force hammer approach, but it will cover everything for you. 

Right at the start of your script, add the following lines: 

* module load miniconda/3.0
* conda init --all
* source /home/FAN/.bashrc
* conda activate /path/to/conda/environment

This will load conda, initialises (all of your) conda environment(s), force a shell refresh and load that new configuration, then finally load up your environment. Your job can now run without strange conda-based initialisation errors.


BX-Python 
=========
The given bx-python is a problematic module that appears in many of the BioScience packages in Conda, below will get you a working, Python 3 version.
These steps are the same as the installation for IsoSeq3, but given how often this particular python package gives the support team issues, it gets its own section!

* conda install -c conda-forge -c bioconda bx-python
