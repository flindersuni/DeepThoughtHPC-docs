---------------
Open Data Cube
---------------
The Open Data Cube provides an integrated gridded data analysis environment for decades of analysis ready 
Earth observation satellite and related data from multiple sources.

========================================
Open Data Cube Status
========================================
The Open Data Cube is in Closed Beat Testing with dedicated researchers at this time. Once workflows and integrations are confirmed, the ODC will be generally released. 


========================================
Open Data Cube Current Products
========================================

Will be populated when the ODC reaches General Availability on the HPC. 


========================================
Open Data Cube Installation Guide
========================================

The Open Data Cube is best installed into a Conda Environment, allowing you to update and manipulate it as needed. 

1. Follow the Jupyter Conda Setup, if you wish to use the ODC via the JupyterHub instace
2. ``conda install datacube``. If this step hangs for more that 5 minutes, then follow the 'Advanced Installation Guide' further down this page to get split the install into smaller parts
3. Raise a ServiceOne request for 'Access to the Open Data Cube'
4. Place the provided configuration file in the following location on the HPC /home/<FAN>/.datacube.conf 
5. Activate your Conda environment, and run ``datacube system check`` to verify that your ODC connects correctly


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Open Data Cube Advanced Installation Guide
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
As the Open Data Cube is quite complicated, sometimes Conda can have trouble resolving the dependencies. In this case, we can manually install many of them, before we install the Data Cube itself. 

1. ``conda create --name=odc python=3.9``
2. ``conda install affine pyproj shapely cachetools click``
3. ``conda install cloudpickle dask[array] distributed jsonschema netcdf4``
4. ``conda install numpy psycopg2 lark-parser pandas python-dateutil``
5. ``conda install pyyaml rasterio sqlalchemy toolz xarray\``
6. ``conda install datacube``
7. Raise a ServiceOne request for 'Access to the Open Data Cube'
8. Place the provided configuration file in the following location on the HPC /home/<FAN>/.datacube.conf 
9. Activate your Conda environment, and run ``datacube system check`` to verify that your ODC connects correctly 