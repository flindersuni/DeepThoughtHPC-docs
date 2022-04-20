--------
GROMACS 
--------
===============
GROMACS Status
===============

GROMACS version 2021.5 is installed and available for use on the HPC.  

.. _GROMACS: https://www.gromacs.org/

=================
GROMACS Overview 
=================

From `GROMACS`_: 

GROMACS is a versatile package to perform molecular dynamics, i.e. simulate the Newtonian equations of motion for systems with hundreds to millions of particles.

It is primarily designed for biochemical molecules like proteins, lipids and nucleic acids that have a lot of complicated bonded interactions, but since GROMACS is extremely fast at calculating the nonbonded interactions (that usually dominate simulations) many groups are also using it for research on non-biological systems, e.g. polymers.

GROMACS supports all the usual algorithms you expect from a modern molecular dynamics implementation.


======================================
GROMACS Quickstart Command Line Guide
=======================================

GROMACS uses UCX and will require a custom mpirun invocation. The module system will warn you of this when you load the module. The following is a known good starting point:


``mpirun -mca pml ucx --mca btl ^vader,tcp,uct -x UCX_NET_DEVICES=bond0 <program> <options>``


+++++++++++++++++++++++++++
GROMACS Program Quick List
+++++++++++++++++++++++++++

Below is a quick reference list of the different programs that make up the GROMACS suite.

+------------+-------------------------------------+
| CLI Option | Description                         |
+============+=====================================+
| gmx        | A Wrapper that calls gmx_mpi        |
+------------+-------------------------------------+
| gmx_mpi    | The main MPI Enabled GROMACS binary |
+------------+-------------------------------------+