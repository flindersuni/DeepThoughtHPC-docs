# The Module System

The system uses the [lmod](https://lmod.readthedocs.io/en/latest/) (Load MODules) system to load/unload applications in the command line. Any modules you use frequently can be loaded on login using your .bash_profile file; modules required for a job should be automated in your slurm script.
Checking what modules are available

## Module Format

As Software requirements for reserach can be very specific, the modules follow suit as well. Newer modules will have the following syntax: 

- 

This uses the 'avail' option of the module command.

In the command line type: module avail
Checking what modules are loaded

This uses the 'list' option of the module command.

In the command line type: module list
Loading modules

This uses the 'add' option of the module command, followed by the software package you wish to load.

In the command line type: module add python2
Unloading modules

This uses the 'load' option of the module command, followed by the software package you wish to unload.

In the command line type: module unload python2
Installing additional modules & applications

If you do not see a module listed for the application that you wish to run, (and  it will be used by other people besides you), please contact Digital Research Services to have it installed for all users via an Assyst request.

If the application is just for you, you can install applications to your home directory following the install instructions of that application.

Please note, the software must in all cases be appropriately licensed.  

If there are issues installing software then an Assyst request can be assigned to DRS, who will assist on a best effort basis.
