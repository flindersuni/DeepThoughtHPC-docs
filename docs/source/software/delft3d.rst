-------------------------
Delft3D 
-------------------------
=======
Status
=======
Delft3D 4, Revision 65936 is installed and available for use on the HPC.

.. Delft3D: 

==================
Delft3D Overview 
==================

From `Delft3D`_: 

Delft3D is Open Source Software and facilitates the hydrodynamic (Delft3D-FLOW module), morphodynamic (Delft3D-MOR module), waves (Delft3D-WAVE module), water quality (Delft3D-WAQ module including the DELWAQ kernel) and particle (Delft3D-PART module) modelling


================================
Delft3D Known Issues
================================

Delft3D does **not** currently support Multi-Node Execution.  The binary swan_mpi.exe will *not work and immediately crash with errors*.


+++++++++++++++++++++++++++++
Delft3D Program Quick List
+++++++++++++++++++++++++++++

Below are two main binaries that are used as part of the Delft3D Suite

+--------------+----------------------------------------------+
| Program      | Description                                  |
+==============+==============================================+
| wave         | The WAVE module                              |
+--------------+----------------------------------------------+
| swan_omp.exe | The SWAN Module with Single-Node parallelism |
+--------------+----------------------------------------------+

    Ignore the .exe - ending, it is valid linux binary. Due a transision state between CMake and Make for the Delft3D source-code, 
    the tools and scripts rely on the binary name ending in .exe.
