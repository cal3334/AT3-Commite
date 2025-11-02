AT3 – Geospatial Data Analysis Workflow
--------------------------------------
Author: Caleb Campbell
Date: November 2025
Unit: KGG375 – Geospatial Data Analytics
Tools: Python, GeoPandas, Rasterio, Matplotlib, NumPy, Shapely

Overview
--------
This project implements a Python-based geospatial analysis workflow for Assignment 3 (AT3) in KGG375.
It performs full geospatial data processing using GNSS flight path data and a high-resolution DSM of Home Hill, Tasmania.
The workflow integrates vector, raster, and terrain analysis techniques.

Workflow Summary
----------------
1. Flight Path Bounding Box
   - Reads GNSS .pos log file and converts to a GeoDataFrame (EPSG:7855 – MGA2020 Zone 55).
   - Calculates bounding box, convex hull, and total flight path length.
   - Exports results to GeoPackage (uas_flight.gpkg).

2. GNSS Quality & Standard Deviation Visualisation
   - Creates scatter plots for GNSS Q-values and standard deviations.
   - Adds convex hull and bounding box overlays.
   - Colour-coded by GNSS Q value (Fixed, Float, Degraded).
   - Plots exported as PNG images in 'plot_outputs/'.

3. Hillshade Generation
   - Computes slope and aspect from DSM gradients.
   - Generates hillshade raster (azimuth = 340°, altitude = 60°).
   - Exports hillshade GeoTIFF and overlay PNGs.

4. Fledermaus-Simple Slope Analysis
   - Uses 5-cell cross kernel and 9x9 kernel variants.
   - Computes mean, minimum, and maximum slope in degrees.
   - Exports slope rasters and corresponding PNG plots.

5. Surface Area Ratio
   - Calculates surface area, planimetric area, and area ratio (SA/PA).
   - Uses Heron's formula with 8 neighbouring cells.
   - Exports rasters for 3D surface area and ratio maps.

Key Outputs
------------
- uas_flight.gpkg: Flight path, convex hull, and bounding box
- Homehill_2020_Hillshade.tif: Hillshade raster (azimuth 340°, altitude 60°)
- Homehill_DEM_Slope_FM_mean/min/max.tif: Fledermaus slope rasters
- Homehill_DEM_SurfaceArea.tif: Surface area raster
- Homehill_DEM_AreaRatio.tif: Surface-to-planar area ratio raster
- All visualisations exported to 'plot_outputs/' as PNG images

Dependencies
------------
- numpy >= 1.25
- pandas >= 2.0
- geopandas >= 0.14
- shapely >= 2.0
- rasterio >= 1.3
- matplotlib >= 3.8

How to Run
----------
1. Place '20200910_BlakesOpening_site3_flight1z.pos' and 'Homehill_2020_DSM_30cm.tif' in the working directory.
2. Run the Python scripts sequentially:
   - flight_path_analysis.py
   - gnss_visualisation.py
   - hillshade_generation.py
   - slope_fm_simple.py
   - slope_fm_9x9.py
   - surface_area_ratio.py
3. Outputs are saved in the working directory and 'plot_outputs/' folder.

Notes
-----
- All data projected to MGA2020 / Zone 55 (EPSG:7855).
- Scripts are modular, reproducible, and optimised for 0.3 m DSMs.
- Visual outputs are automatically exported as 300 DPI PNGs for inclusion in reports
