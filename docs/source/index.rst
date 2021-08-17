.. DeepThoughtHPC-docs documentation master file, created by
   sphinx-quickstart on Thu Mar 12 09:21:20 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to the DeepThought Documentation
=========================================

The new Flinder HPC is called DeepThought. This new HPC comprises of AMD EPYC based hardware and next-generation management software, allowing for a dynamic and agile HPC service. 

.. _Upgrade Migration Information: migration/upgrademigration.html

.. warning:: 
    DeepThought has recently undergone a series of upgrades that require some user intervention when utlising the upgraded cluster
    Please see `Upgrade Migration Information`_ for actions required.

.. attention::
    This documentation is under active development, meaning that it can
    change over time as we improve it. Please email deepthought@flinders.edu.au if
    you require assistance. We also welcome user contributions  to this documentation 
    - contact the same email above so we can grant you access.


Attribution
----------------------

If you use the HPC to form a part of your research, you should attribute your usage. 
Flinders has minted a DOI that points to this documentation, specific for the HPC Service. It will also allow for tracking the research outputs that the HPC has contributed to.  

Text Citation
++++++++++++++

.. _ARDC Data Citation: https://ardc.edu.au/resources/working-with-data/citation-identifiers/data-citation/

The below text citation follows the standard Australian Research Data Commons (ARDC) format for attributing data and software. For more information on this type of attribution, 
visit the `ARDC Data Citation`_ page. 

``Flinders University (2021). DeepThought (HPC). Retrieved from https://doi.org/10.25957/FLINDERS.HPC.DEEPTHOUGHT``


Reference Managers
+++++++++++++++++++

The following files are provided for integration into your reference manager of choice. To save the file, 'Right Click -> Save Link As..'. 

.. _BibTex: https://raw.githubusercontent.com/flindersuni/DeepThoughtHPC-docs/master/docs/source/flindershpc2021-bibtex.bib
.. _EndNote: https://raw.githubusercontent.com/flindersuni/DeepThoughtHPC-docs/master/docs/source/flindershpc2021-endnote.xml
.. _RIS: https://raw.githubusercontent.com/flindersuni/DeepThoughtHPC-docs/master/docs/source/flindershpc2021-ris.ris

- BibTex_ 
- EndNote_
- RIS_


Table of Contentss
====================

.. toctree::
    :maxdepth: 1
    :caption: User Documentation
 
    Access/accessrequest.rst 
    Access/windows.rst
    Access/unix.rst
    Storage/storageusage.rst
    dataflow/hpcresearchdataflow.rst
    FileTransfers/FileTransfersIntro.md
    LinuxCommands/LinuxIntro.md
    dataflow/hpcjobdataflow.rst
    SLURM/SLURMIntro.md
    ModuleSystem/LMod.md
.. toctree:: 
    :maxdepth: 1 
    :caption: Software Suites

    software/softwaresuitesoverview.rst
    software/ansys.rst
    software/jupyter.rst
    software/singularity.rst
    
 
.. toctree::
    :maxdepth: 1
    :caption: Technical Specifications
 
    system/deepthoughspecifications.md

.. toctree::
    :maxdepth: 1
    :caption: FAQ & Known Issues
 
    FAQ/faq.rst
    FAQ/knownissues.rst
 

.. toctree::
   :maxdepth: 1
   :caption: Software & Support Policies

   policies/fairuse.rst
   policies/accessandpermissions.rst
   migration/upgrademigration.rst
   upgrades/updatelog.rst


Acknowledgements
----------------

We recognise the respect the trademarks of all third-party providers referenced in this documentation. Please see the respective EULAs for software packages used in configuring your own environment based on this knowledgebase.

License
----------

This documentation is released under the `Creative-Commons: Attribution-ShareAlike 4.0 International <http://creativecommons.org/licenses/by-sa/4.0/>`_ license.
