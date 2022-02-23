Fair Usage Guidelines
=======================

The Deepthought HPC provides moderate use at no charge to Flinders University Colleges. 
This is enforced by the Fairshare System and is under constant tweaking and monitoring to ensure 
the best possible outcomes. The current split of resources between colleges is:

* 45 % for CSE 
* 45 % for CMPH 
* 10 % for General

For example, if the HPC had 1000 'shares' that represent its resources, the following would be demonstrative of how they are allocated: 


* 450 'shares' for CSE 
* 450 'shares' for CMPH 
* 100 'shares' for General 


.. _StorageGuidelines: ../storage/storageusage.html
.. _Module System: ../ModuleSystem/LMod.html

Storage Usage Guidelines
============================
See the page at: `StorageGuidelines`_, for details on what storage is present and other details. A general reminder for HPC Storage: 

- All storage is *volatile* and no backup systems are in place
- Cleanup you /home and /scratch regularly 
- Cleanup and /local storage you used at the end of each job


Software Support Guidelines
====================================

HPC Users are encouraged to compile and install their own software when they are comfortable to do so.  
This can be done freely on the head node(s). 

The HPC Support team cannot maintain and provide active support for every piece of software that users of the HPC may need. 
The following guidelines are an excerpt from our HPC Software Support Policy to summarise the key points. 
For more information on how the software can be loaded/unloaded on the HPC, head on over to the `Module System`_.


Supported Software Categories 
-------------------------------
The following categories are how the HPC Team asses and manage the differing types of Software that are present on the HPC. 
For more information, each will have their own section.

* Core 'Most Used' Programs
* Licensed Software 
* Libraries 
* Toolchains 
* Transient Packages 
* Interpreters / Scripting Interfaces 


Core 'Most Used' Programs
++++++++++++++++++++++++++++++++++++
Holds the most used packages on the HPC. The HPC Team monitors the loading and unloading of modules, so we can manage the lifecycle of software on the HPC. 
As an example, some of the most used program on the HPC are: 

* R 
* Python 3.9 
* RGDAL
* CUDA 11.2 Toolkit

While not an exhaustive list of the common software, it does allow the team to focus our efforts and provide more in-depth support for these programs. 
This means they are usually first to be updated and have a wider range of tooling attached to them by default.

Licensed Software 
+++++++++++++++++++++++++++++++++++++++++++
Licensed Software covers the massive packages like ANSYS (which, all installed is about 300 *gigabytes*) which are licensed either to the HPC specifically or 
obtained for usage via the University Site licenses. This covers things like: 

* ANSYS Suite (Structures, Fluids, Electronics, PrepPost & Photonics)


Libraries 
++++++++++++++++++++++++
Generally, these libraries are required as dependencies for other software, however there are some core libraries that are used more than others. 
As an example, the Geometry Engine - Open Source (GEOS) Library is commonly used by other languages (R, Python) to allow for Geo-Spatial calculations. 
Some of the common libraries include: 

* GEOS 
* ZLib
* ImageMagik
* OpenSSL 

Most of these are useful in a direct manner only for software compilation or runtime usage.  

Unless compiling your own software, you can safely ignore this section - the `Module System`_ takes care of this for you.

Toolchains
+++++++++++++++++++++++++
Generally we support the FOSS (Free Open Source Software) Toolchain, comprising of: 

* GNU C, C++ & Fortran Compilers (gcc, g++ and gfortran)
* GNU Bin Utils 
* Open MPI Library 
* Open BLAS, LAPACK & ScaLAPACK 
* FFTW Library 

Transient Packages 
+++++++++++++++++++++
Listed here for completeness, these packages are install-time dependencies or other packages that do not fit within the above schema. 


Scripting Languages
+++++++++++++++++++++
Interpreters like Python & R (Perl, Ruby, Scala, Lua etc.) are complex things and have their own entire ecosystems of packages, versioning and tools. 
These Scripting Interfaces (The technical term is 'Interpreters') are all managed as their own standalone aspect to the HPC. 

Using Python as an example you have: 

* The interpreter 'Python' 
* The package manager 'Pip'
* The Meta-Manager 'Conda'/'Mini-Conda'
* The Virtual Environments Manager 'venv'

Each interacting in slightly different ways and causing other issues. To ensure that the HPC team can support a core set of modules the interpreters are only updated when: 

* Security patches are needed
* A new *Major* Version is available 
* A commonly requested feature requires an upgrade 

Versioning Support 
+++++++++++++++++++++++

Most major packages will be supported in a Latest - 1 fashion. Below show an example when a package would be updated in the quarterly package upgrade cycle.

* Latest Version: 2020a 
* Installed Version: 2019a 
* Supported Version: 2019b 

As not all software follows such clean release patterns, the HPC Team will hold final say on updating a piece of software in the global module lists. 



Upgrade Cycles
=====================================
The HPC Team does their best to adhere to the following cycle for upgrades for software and associated systems. 

======================== ============= =============== ==================================
Software Category        Upgrade Cycle Outage Required Versioning Type  
======================== ============= =============== ==================================
Core Supported Programs   Quarterly        No             N - 1 
Core Licensed Programs    Bi-Yearly        No             N - 1
OS & Managerial Tools     Yearly           Yes            Latest 
Software Images           Bi-Yearly        Partial        Latest 
Scripting Interfaces      Quarterly        No             Major, Security & Feature Minor
Scripting Modules         Quarterly        No             Latest 
======================== ============= =============== ==================================
