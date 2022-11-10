-------------------------
Delft3D 
-------------------------
=====================
Delft3D Status
=====================

Delft3D 4, Revision 65936 is installed and available for use on the HPC.

.. _Delft3D Home: https://oss.deltares.nl/web/delft3d

====================
Delft3D Overview 
====================

From `Delft3D Home`_: 

Delft3D is Open Source Software and facilitates the hydrodynamic (Delft3D-FLOW module), morphodynamic (Delft3D-MOR module), waves (Delft3D-WAVE module), water quality (Delft3D-WAQ module including the DELWAQ kernel) and particle (Delft3D-PART module) modelling


================================
Delft3D Known Issues
================================

1. Delft3D does **not** currently support Multi-Node Execution.  The binary swan_mpi.exe will *not* work and immediately crash with errors.

2. The ``.mdw`` file **CANNOT** start with a capital letter, or ``wave`` will crash with the error below: 

.. code-block:: sh


    terminate called after throwing an instance of 'char const*'

    Program received signal SIGABRT: Process abort signal.

    Backtrace for this error:
    #0  0x15555344cb1f in ???
    #1  0x15555344ca9f in ???
    #2  0x15555341fe04 in ???
    #3  0x155553d8edb4 in _ZN9__gnu_cxx27__verbose_terminate_handlerEv
        at ../../../../libstdc++-v3/libsupc++/vterminate.cc:95
    #4  0x155553d8cb85 in _ZN10__cxxabiv111__terminateEPFvvE
        at ../../../../libstdc++-v3/libsupc++/eh_terminate.cc:47
    #5  0x155553d8cbd0 in _ZSt9terminatev
        at ../../../../libstdc++-v3/libsupc++/eh_terminate.cc:57
    #6  0x155553d8ce13 in __cxa_throw
        at ../../../../libstdc++-v3/libsupc++/eh_throw.cc:93
    #7  0x4ee0b8 in throwexception_
        at /local/delf3d/delft3d4_65936/src/utils_lgpl/deltares_common/packages/deltares_common_c/src/throwexception.cpp:35
    #8  0x411889 in wave_init_
        at /local/delf3d/delft3d4_65936/src/engines_gpl/wave/packages/kernel/src/wave_init.f90:66
    #9  0x404f6d in waves_main
        at /local/delf3d/delft3d4_65936/src/engines_gpl/wave/packages/wave/src/wave_exe.f90:130
    #10  0x404a7c in main
        at /local/delf3d/delft3d4_65936/src/engines_gpl/wave/packages/wave/src/wave_exe.f90:35
    /cm/local/apps/slurm/var/spool/job1447072/slurm_script: line 104: 811018 Aborted                 (core dumped) wave S3.mdw




++++++++++++++++++++++++++++++++++++++++++++++++++
Delft3D Program Quick List
++++++++++++++++++++++++++++++++++++++++++++++++++

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
