Fair Usage Guidelines
=======================

The Deepthought HPC provides moderate use at no charge to Flinders University Colleges. 
This is enforced by the Fairshare System and is under constant tweaking and monitoring to ensure 
the best possible outcomes. 

The following can be taken as general guidelines: 

* The current split between colleges is:

  * 45 % CSE 
  * 45 % CMPH 
  * 10 % General


.. GettingAccess: ../Access/GettingAccess.md

Storage Usage Guidelines
============================
As explained in 'Getting Access', /scratch and /home have different targets. Some guidelines to follow : 

* Assume that anything on the HPC is *volatile* storage, and take appropriate backups
* Cleanup /scratch when you are done 
* The HPC Team will either notify users directly, or en-mass if disk-space approaches a cutoff point 



Software Support Guidelines
====================================

HPC Users are encouraged to compile and install their own software when they are comfortable to do so.  
This can be done freely on the head nodes. 

Compiler Toolchains
---------------------
Generally, we support the FOSS (Free Open Source Software) Toolchain, comprising of: 

* GNU C, C++ & Fortran Compilers 
* GNU Bin Utils 
* Open MPI Library 
* Open BLAS, LAPACK & ScaLAPACK 
* FFTW Library 


Software Versioning & Support 
-------------------------------

Not all software is suitable for the HPC, and the HPC team cannot manage every single piece of sftware that exists! 
Below is a list of the core software & libraries that are under active support.  

Versioning Support 
+++++++++++++++++++++++

Most major packages will be supported in a Latest - 1 fashion. Below show an example when a package would be updated in the quarterly package upgrade cycle.

* Latest Version: 2020a 
* Installed Version: 2019a 
* Supported Version: 2019b 

As not all software follows such clean release patterns, the HPC Team will hold final say on updating a piece of software in the global module lists. 

