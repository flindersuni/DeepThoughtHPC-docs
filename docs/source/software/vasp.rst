-------------------------
VASP
-------------------------
=======================================
VASP Status
=======================================
VASP: The Vienna Ab initio Simulation Package version 6.2.0 is operational with OpenACC GPU support on the HPC for the Standard, Gamma Ponit and Non-Collinear versions of the program. 

.. _VASP: https://www.vasp.at/

==========================================
VASP Overview 
==========================================
From `VASP`_:

The Vienna Ab initio Simulation Package (VASP) is a computer program for atomic scale materials modelling, e.g. electronic structure calculations and quantum-mechanical molecular dynamics, from first principles.

VASP computes an approximate solution to the many-body Schrödinger equation, either within density functional theory (DFT), solving the Kohn-Sham equations, or within the Hartree-Fock (HF) approximation, solving the Roothaan equations. Hybrid functionals that mix the Hartree-Fock approach with density functional theory are implemented as well. Furthermore, Green’s functions methods (GW quasiparticles, and ACFDT-RPA) and many-body perturbation theory (2nd-order Møller-Plesset) are available in VASP.


================================================================
VASP Quickstart Command Line Guide
================================================================
VASP must be started via the MPI wrapper script. If your SLURM Script has requested a GPU, VASP will autodetect and use the GPU for all supported operations. Substitute the VASP binary of your requirements.

``mpirun <MPI OPTIONS> vasp_std <OPTIONS>`` 

+++++++++++++++++++++++++
VASP Program Quick List
+++++++++++++++++++++++++

Below is a quick reference list of the different programs that make up the VASP suite.

+----------------+----------------------------------------------------------------------------------------------------------------+
| CLI Option     | Description                                                                                                    |
+================+================================================================================================================+
| vasp_std       | Standard version of VASP                                                                                       |
+----------------+----------------------------------------------------------------------------------------------------------------+
| vasp_std_debug | Debug, and slower version of the standard VASP binary. Unless specifically asked, you should use vasp_std      |
+----------------+----------------------------------------------------------------------------------------------------------------+
| vasp_gam       | Gamma Ponit version of VASP                                                                                    |
+----------------+----------------------------------------------------------------------------------------------------------------+
| vasp_gam_debug | Debug, and slower version of the Gamma Ponit VASP binary. Unless specifically asked, you should use vasp_gam   |
+----------------+----------------------------------------------------------------------------------------------------------------+
| vasp_nlc       | Non Collinear version of VASP                                                                                  |
+----------------+----------------------------------------------------------------------------------------------------------------+
| vasp_ncl_debug | Debug, and slower version of the Non Collinear VASP binary. Unless specifically asked, you should use vasp_ncl |
+----------------+----------------------------------------------------------------------------------------------------------------+

