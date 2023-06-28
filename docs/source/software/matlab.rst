------------------
Mathworks MATLAB 
------------------
==============
MATLAB Status
==============

Matlab 2020b is the currently installed version on the HPC. 

Flinders has also licenced MATLAB for usage at NCI on Gadi. You will need to join the **matlab_flinders** group via 'My NCI'. Once membership is approved by the HPC Team, then you will be able to run MATLAB at GADI. Please see the NCI Wiki for any help running MATLAB on NCI computing resources. 

The HPC Team has updated the licencing and capabilities of MATLAB on DeepThought. You can now use Parallel Server via SLURM and the Parallel Computing Toolbox to run MATLAB in a distributed manner on DeepThought.

.. _MATLAB Running Code on Clusters and Clouds: https://au.mathworks.com/help/matlab-parallel-server/running-at-scale.html

Please see the MATLAB help as a starting point to use MATLAB Parallel Server via SLURM or the Parallel Computing Toolkit `MATLAB Running Code on Clusters and Clouds`_ is a good starting point. 

.. _MathWorks MATLAB: https://au.mathworks.com/


=================
MATLAB Overview 
=================

`Mathworks MATLAB`_ is a leading mathematical analysis suite.  Coupled with their 
Parallel Server, the new MATLAB Integration will enable the full power of DeepThought 
and a greatly enhanced user experience. 


======================================
MATLAB Quickstart Command Line Guide
======================================

To run a job with MATLAB on the HPC you will need the following: 
    - A MATLAB Script file 
    - Any Datasets (eg, a .csv)

Ensure that the paths to anything in the script file reflect where it lives on the HPC, not your local machine. 

You can then invoke MATLAB (after loading the MATLAB Module) like so: 
    
    - matlab  -r _PATH_TO_SCRIPT_FILE 
