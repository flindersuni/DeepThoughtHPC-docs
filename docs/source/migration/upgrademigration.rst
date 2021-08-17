===============================
DeepThought Upgrade Migration 
===============================

DeepThought has undergone major upgrades. To make it as seamless for our users as possible, we made sure to keep 
your /home and /scratch directories and import them across to the Upgraded Cluster. 

The following steps are required for a user to undertake when they migrate across to the new 
cluster. 


Module System
+++++++++++++++
The old module system was partially configured, and while it worked just fine, has quite a few legacy options 
and multiple enhancements 'under the hood' so to speak. Modules now use a global, system-wide cache to speed up 
all operations dealing with modules.  

Action Needed 
**************

1. If your /home director has a folder called ``.lmod.d/``
2. Remove this directory

The old module system would generate a per-user cache, stored locally. Due to changes in the module layout and system 
configuration, the old cache is now invalid. 

If you do not delete this directory, invalid entires will cause cause module load errors when using the new cluster. 


New Software Suites 
+++++++++++++++++++++

There are new enterprise integrations on the HPC. For details, please see the new 
'Software Suites' section in the left navigation bar. 