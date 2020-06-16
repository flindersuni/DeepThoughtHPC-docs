# The Module System

In mordern time, almost all HPC systems are multiuser systems and consequently, this brings many challenges. One of such challenges is effectively managing a complex and large volume of software application cohort. 

DeepThought HPC uses the [LMod](https://lmod.readthedocs.io/en/latest/) (Load MODules) system to load/unload applications in the command line. Any modules you use frequently can be loaded on login using your .bash_profile file; modules required for a job should be automated in your SLURM script.

Best way to think of Module is a singular program version + all of its associated dependencies to run correctly.

## Writing Your Own Modules

You can [write your own module files](https://lmod.readthedocs.io/en/latest/015_writing_modules.html#) if you want! This is supported on a best-effort basis by the HPC support team.

## Module Format

As Software requirements for research can be very specific, the modules follow suit as well. Newer modules will have the following syntax:

- Program/Version-Toolchain-Version-Interpreter-Version

To break that down into its individual parts for BioPerl/1.7.2-GCCcore-8.2.0-Perl-5.28.1 in the following sections. 

Manually installed software will always be a shorter format of:

- Program/Version

### Program-Version

This is program that was installed — in this case it's BioPerl, version 1.7.2

### Toolchain-Version

The Compiler Toolchain that was used to compile the program — in this case it's GCCcore, version 8.2.0.

### Interpreter-Version

Some programs have a dependence on another interpreter, like Perl or Python. In this case it's Perl, version 5.28.1. This means, it will also load the module for Perl, Version 5.28.1.

## Useful Commands

Below are some common module commands to load, unload and reset your module system.

### Available Modules

    module avail

Will get you a list of something similar to this - a list of every single available module on the HPC. You can scroll by your 'Up' and 'Down' arrows and 'q' will exit the scroll if you don't want to scroll all the way to then end. The screenshot below is not an exhaustive list of all modules, just an example!

![](../_static/moduleAvailExampleList.png)

### Loaded Modules

    module list

Will get you a list of your current modules.

![](../_static/moduleListExample.png)

### Loading Modules

There are three main ways to load a module. For most of the time, they are functionally equivalent. For more information, head on over to [LMod Loading Types](https://lmod.readthedocs.io/en/latest/010_user.html) and read up on how they differ.

- A good tip! Typing out a partial name and double-tapping 'tab' will attempt to complete the name of what you are typing. This means you don't have to worry about typing the very-long name of a module.

#### Module Load

    module load BioPerl/1.7.2-GCCcore-8.2.0-Perl-5.28.1.

There is also a nice shortcut, that you can use:

    ml BioPerl/1.7.2-GCCcore-8.2.0-Perl-5.28.1.

'ml' is just short for 'module load'. Handy!

## Additional Software & Modules

Generally speaking, we can install almost all Linux/CentOS bounded software/applications on HPC, but we don't always need to go thorough the effort to install things 'globally' for everybody.

1. Are people other than just me going to use this software?
2. If yes, create an ServiceOne Ticket, and Digital Research Services will get it installed on a Best-Effort basis

Otherwise, there is nothing stopping you installing the program locally for yourself! If you run into issues installing software then open an ServiceOne ticket and again, Digital Research Services will help on a best-effort basis.

### An Important Note

The software must in all cases be appropriately licensed.

## Currently Installed Modules

Be warned, that this is a _long_ list. It's updated on best effort basis to help you see what is already present, but the latest list is always available by running the `module list` command on the HPC. Its broken into several segments, as there are several tools used to facilitate the installation and management of software used on the HPC.

### Manually Installed Software / Default Available

This is the list of software that has been 'hand rolled' as it contains either things that at that time, did not have an automated way of installation, or rather esoteric software that required extensive modification to work correctly on the HPC. It is available [here](ManuallyInstalled.md)

### Additional Software

There are additional software collections will be made available in a near future.
