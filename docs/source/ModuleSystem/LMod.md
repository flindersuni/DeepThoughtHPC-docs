# The Module System

The system uses the [lmod](https://lmod.readthedocs.io/en/latest/) (Load MODules) system to load/unload applications in the command line. Any modules you use frequently can be loaded on login using your .bash_profile file; modules required for a job should be automated in your SLURM script.

Best way to think of Module is a Singular Program Version + all of its associated dependencies to run correctly.

## Module Format

As Software requirements for research can be very specific, the modules follow suit as well. Newer modules will have the following syntax:

- Program/Version-Toolchain-Version-Interpreter-Version

To break that down into its individual parts for BioPerl/1.7.2-GCCcore-8.2.0-Perl-5.28.1.

### Program-Version

This is program that was installed — in this case it's BioPerl, version 1.7.2

### Toolchains-Version

The Compiler Toolchain that was used to compiler the program — in this case it's GCCcore, version 8.2.0.

### Interpreter-Version

Some programs have a dependence on another interpreter, like Perl or Python. In this case it's Perl, version 5.28.1.

## Useful Commands

Below are some common module commands to load, unload and reset your module system.

### Available Modules

    module avail

### Loaded Modules

    module list

### Loading Modueles

There are three main ways to load a module. For most of the time, they are functionally equivalent. For more information, head on over to [LMod Loading Types]() and read up on how they differ.

- A good tip! Typing out a partial name and double-tapping 'tab' will attempt to complete the name of what you are typing. This means you don't have to worry about typing the very-long name of a module.

#### Module Load

    module load BioPerl/1.7.2-GCCcore-8.2.0-Perl-5.28.1.

There is also a nice shortcut, that you can use:

    ml BioPerl/1.7.2-GCCcore-8.2.0-Perl-5.28.1.

'ml' is just short for 'module load'. Handy!

## Additional Software

We can install nearly anything onto the HPC, but we don't always need to go thorough the effort to install things 'globally' for everybody.

1. Are people other than just me going to use this software?
2. If yes, create an Assyst Ticket, and Digital Research Services will get it installed on a Best-Effort basis

Otherwise, there is nothing stopping you installing the program locally for yourself! If you run into issues installing software then open an Assysts ticket and again, Digital Research Services will help on a best-effort basis.

### An Important Note

The software must in all cases be appropriately licensed.
