------------------
Mathworks MATLAB 
------------------
=======
Status
=======
Matlab 2020b is the currently installed version on the HPC. 

investigation is under way to enable tighter GUI integration and better workload management. 


.. MathWorks MATLAB: https://au.mathworks.com/


=================
Overview 
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
