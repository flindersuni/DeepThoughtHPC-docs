===============================
DeepThought Upgrade Migration 
===============================

The DeepThought HPC has undergone major upgrades. To make it as seamless for our users as possible, we made sure to keep 
your /home and /scratch directories the same in the new cluster. 

This means that all your files and folders are untouched when you migrate to the new, rebuilt cluster.

The following steps are required for a user to undertake when they migrate across to the new 
cluster. 


Installed Software 
++++++++++++++++++++++
The HPC Support Team has removed all software not loaded via the module system in the last 6 months. Every effort was made 
to ensure we did not remove an actively used piece of software. 


Action Needed
****************
If your software package is no longer visible in the ``module avail`` list, then please either submit a ServiceOne request 
for HPC Software, or notify the HPC Support Team via email. 

Module System
+++++++++++++++
The old module system was partially configured, and while it worked just fine, has quite a few legacy options 
and multiple enhancements 'under the hood' so to speak. Modules now use a global, system-wide cache to speed up 
all operations dealing with modules.  

Action Needed 
**************

1. If your /home directory has a folder called ``.lmod.d/``
2. Remove this directory

The old module system would generate a per-user cache, stored locally. Due to changes in the module layout and system 
configuration, the old cache is now invalid. 

If you do not delete this directory, invalid entires will cause cause module load errors when using the new cluster. 


New Software Suites 
+++++++++++++++++++++

There are new enterprise integrations on the HPC. For details, please see the new 
'Software Suites' section in the left navigation bar. 