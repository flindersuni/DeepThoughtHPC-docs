---------------
Open Data Cube
---------------
The Open Data Cube provides an integrated gridded data analysis environment for decades of analysis ready 
Earth observation satellite and related data from multiple sources.

========================================
Open Data Cube Status
========================================
Released for General Usage. You will need to raise a ServiceOne Request asking for 'Access to the Open Data Cube'. 


========================================
Open Data Cube Current Products
========================================
The following products have a known index in the Open Data Cube. If the product or date-range you wish to analyse is not currently present in the Data Cube, please raise a ServiceOne request for 'Add of Modify open Data Cube Datasets'.

+----------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ODC Product Name           | Description                                                                                                           |
+============================+=======================================================================================================================+
| ga_lst5_ard_3              | Geoscience Australia Landsat 5 Thematic Mapper Analysis Ready Data Collection 3                                       |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ga_ls7e_ard_3              | Geoscience Australia Landsat 7 Enhanced Thematic Mapper Plus Analysis Ready Data Collection 3                         |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ga_ls8c_ard_3              | Geoscience Australia Landsat 8 Operational Land Imager and Thermal Infra-Red Scanner Analysis Ready Data Collection 3 |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ga_s2am_ard_provisional_3  | Geoscience Australia Sentinel 2a MSI Analysis Ready Data Collection 3 (provisional)                                   |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ga_s2bm_ard_provisional_3  | Geoscience Australia Sentinel 2b MSI Analysis Ready Data Collection 3 (provisional)                                   |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ls5_nbart_geomedial_annual | Surface Reflectance Geometric Median 25 metre, 100km tile, Australian Albers Equal Area projection (EPSG:3577)        |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ls7_nbart_geomedial_annual | Surface Reflectance Geometric Median 25 metre, 100km tile, Australian Albers Equal Area projection (EPSG:3577)        |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ls8_nbart_geomedian_annual | Surface Reflectance Geometric Median 25 metre, 100km tile, Australian Albers Equal Area projection (EPSG:3577)        |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------+
| s2a_ard_granule            | Sentinel-2A MSI Definitive ARD - NBART and Pixel Quality                                                              |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------+
| s2b_ard_granule            | Sentinel-2B MSI Definitive ARD - NBART and Pixel Quality                                                              |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------+



========================================
Open Data Cube Installation Guide
========================================

The Open Data Cube is best installed into a Conda Environment, allowing you to update and manipulate it as needed. 

1. Follow the Jupyter Conda Setup, if you wish to use the ODC via the JupyterHub instance
2. ``conda install datacube``. If this step hangs for more that 5 minutes, then follow the 'Advanced Installation Guide' further down this page to get split the install into smaller parts
3. Raise a ServiceOne request for 'Access to the Open Data Cube'
4. Place the provided configuration file in the following location on the HPC: ``/home/<FAN>/.datacube.conf``
5. Activate your Conda environment, and run ``datacube system check`` to verify that your ODC connects correctly


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Open Data Cube Advanced Installation Guide
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
As the Open Data Cube is quite complicated, sometimes Conda can have trouble resolving the dependencies. In this case, we can manually install many of them, before we install the Data Cube itself. 

1. 1. If you have not performed an initial ``conda init bash``, issue ``module load Miniconda3`` followed by ``conda init bash``, then log-out and log back in to the HPC.
2. ``conda create --name=odc python=3.9``
3. ``conda activate odc``
4. ``conda config --add channels conda-forge``
5. ``conda install affine pyproj shapely cachetools click``
6. ``conda install cloudpickle dask[array] distributed jsonschema netcdf4``
7. ``conda install numpy psycopg2 lark-parser pandas python-dateutil``
8. ``conda install pyyaml rasterio sqlalchemy toolz xarray``
9. ``conda install datacube``
10. Raise a ServiceOne request for 'Access to the Open Data Cube'
11. Place the provided configuration file in the following location on the HPC /home/<FAN>/.datacube.conf 
12. Activate your Conda environment, and run ``datacube system check`` to verify that your ODC connects correctly 
