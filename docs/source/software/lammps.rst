------------------
LAMMPS
------------------
==============
LAMMPS Status
==============

LAMMPS was installed from the Development Branch on 7th Jan, 2022. 

There are two versions of LAMMPS installed on DeepThought, each with their own modules:

1. A CPU only version, with the program called called lmp 
2. A GPU only version, with the program called lmp_gpu 

*You cannot run the GPU enabled version without access to a GPU, as it will cause errors.*

.. _LAMMPS: https://lammps.org


=================
LAMMPS Overview 
=================
From LAMMPS_:

LAMMPS is a classical molecular dynamics code with a focus on materials modelling. It's an acronym for Large-scale Atomic/Molecular Massively Parallel Simulator. LAMMPS has 
potentials for solid-state materials (metals, semiconductors) and soft matter (biomolecules, polymers) and coarse-grained or mesoscopic systems. It can be used to model 
atoms or, more generically, as a parallel particle simulator at the atomic, meso, or continuum scale.

LAMMPS runs on single processors or in parallel using message-passing techniques and a spatial-decomposition of the simulation domain. Many of its models have versions that 
provide accelerated performance on CPUs, GPUs, and Intel Xeon Phis. The code is designed to be easy to modify or extend with new functionality. LAMMPS is distributed as an 
open source code under the terms of the GPLv2. The current version can be downloaded here. Links are also included to older versions. All LAMMPS development is done via 
GitHub, so all versions can also be accessed there. Periodic releases are also posted to SourceForge.

==========================
LAMMPS Installed Packages
==========================

The following is an extract from the ``lmp -h`` option, showing the enabled packages and capabilities of the LAMMPS installation.

        ASPHERE ATC AWPMD BOCS BODY BROWNIAN CG-DNA CG-SDK CLASS2 COLLOID COLVARS 
        COMPRESS CORESHELL DIELECTRIC DIFFRACTION DIPOLE DPD-BASIC DPD-MESO DPD-REACT 
        DPD-SMOOTH DRUDE EFF EXTRA-COMPUTE EXTRA-DUMP EXTRA-FIX EXTRA-MOLECULE 
        EXTRA-PAIR FEP GPU GRANULAR H5MD INTERLAYER KIM KSPACE LATBOLTZ LATTE MACHDYN 
        MANIFOLD MANYBODY MC MDI MEAM MESONT MESSAGE MGPT MISC ML-HDNNP ML-IAP ML-PACE 
        ML-QUIP ML-RANN ML-SNAP MOFFF MOLECULE MOLFILE MPIIO MSCG NETCDF OPENMP OPT 
        ORIENT PERI PHONON PLUGIN PLUMED POEMS PTM PYTHON QEQ QMMM QTB REACTION REAXFF 
        REPLICA RIGID SCAFACOS SHOCK SMTBQ SPH SPIN SRD TALLY UEF VORONOI VTK YAFF

======================================
LAMMPS Quickstart Command Line Guide
======================================

LAMMPS uses UCX and will require a custom mpirun invocation. The module system will warn you of this when you load the module. The following is a known good starting point:


``mpirun -mca pml ucx --mca btl ^vader,tcp,uct -x UCX_NET_DEVICES=bond0 <program> <options>``