# Aspen-x-Firelines
JFSP Project investigating the effect of aspen on adjacent fire suppression operations in the southern Rocky Mountains 

## Description of the project

This repository contains all code and data for *Fire lines adjacent to aspen are unlikely to hold 
during extreme burning conditions in southern Rocky Mountain forests*.

## Organization of the project

The project has the following structure:

-   *.gitignore*: a plain text file that specifies intentionally
    untracked files and directories that Git should ignore

-   Scripts: This subdirectory contains all code written for this project.
    In order for the code to work, files should be run sequentially
    (i.e., *1-Predictor Generation and Projection.R* then *2-Main Script Aspen Fire Lines.R*).

    -   *1-Predictor Generation and Projection.R*: This code compiles, reprojects, and crops environmental
        data.

    -   *2-Main Script Aspen Fire Lines.R*: The code for reproducing the main
        results presented therein.

-   Aspen Firelines Data: This subdirectory contains publicly available data used in this project and serves as the root directory for inputs and outputs of scripts.

    -   *./data/Boundary*: subdirectory containing study area boundary 
        -   SouthernRockyBoundary_10kmBuff.shp: polygon of US EPA III ecoregion for the southern Rocky Mountains buffered to 10 km. 

    -   *./data/NIFC Lines*: subdirectory containing NIFC fire line data
        -   EventLine____.shp: .shp files for unprocessed NIFC event lines for years 2018-2023 that span fire events in CONUS.
        -   SR_FLs.shp: .shp file containing the processed NIFC event line data for the Southern Rockies.
    
    -   *./data/NIFC Polygons*: subdirectory containing NIFC fire polygon data
        -   EventPolygon____.shp: .shp files for unprocessed NIFC event polygons for years 2018-2023 that span fire events in CONUS.
        -   SR_FLs.shp: .shp file containing the processed NIFC event polygon data for the Southern Rockies.
    
    -   *./data/Predictor Rasters*: subdirectory containing processed model inputs
        -   ./data/Predictor Rasters/Climate: subdirectory containing processed climate data.
            - SR_MM_YYYY_diffs.tif: .tif files with the difference in 30 year normal VPD for a given month (MM) and year (YYYY) for the study region data from WorldClim (1 x 1 km resolution)
        -   ./data/Predictor Rasters/ICS-209 csv: subdirectory with ICS-209+ data.
            - ics209-plus-wf_sitreps_1999to2023.csv: datasheet containing ICS-209+ data from 1999-2023 to get information on fire growth
        -   ./data/Predictor Rasters/Land Cover: subdirectory with land cover data.
            - Aspen_Binary: .tif file from Cook et al. 2024 containing P/A of aspen in southern Rocky Mountains (10 x 10 m)
            - DougFir_Binary: .tif file from TreeMap (Riley et al. 2021) containing P/A of Douglas-Fir in southern Rocky Mountains (30 x 30 m)
            - Gambel_Binary: .tif file from TreeMap (Riley et al. 2021) containing P/A of Gambel oak in southern Rocky Mountains (30 x 30 m)
            - Grass_Binary: .tif file from NLCD 2019 containing P/A of grasslands in southern Rocky Mountains (30 x 30 m)
            - Lodgepole_Binary: .tif file from TreeMap (Riley et al. 2021) containing P/A of lodgepole pine in southern Rocky Mountains (30 x 30 m)
            - Other_Binary: .tif file from NLCD 2019 containing P/A of other landcover types (e.g., development, agriculture, etc.) in southern Rocky Mountains (30 x 30 m)
            - PJ_Binary: .tif file from TreeMap (Riley et al. 2021) containing P/A of pinyon-juniper woodlands in southern Rocky Mountains (30 x 30 m)
            - Ponderosa_Binary: .tif file from TreeMap (Riley et al. 2021) containing P/A of ponderosa pine in southern Rocky Mountains (30 x 30 m)
            - SF_Binary: .tif file from TreeMap (Riley et al. 2021) containing P/A of spruce/fir in southern Rocky Mountains (30 x 30 m)
            - Shrub_Binary: .tif file from NLCD 2019 containing P/A of shrublands in southern Rocky Mountains (30 x 30 m)
        -   ./data/Predictor Rasters/Topographic: subdirectory containing processed topographic data.
            - elev.tif: .tif file of elevation (m) from USGS national map (30 x 30 m resolution)
            - slope.tif: .tif file of slope from USGS national map (30 x 30 m resolution)
            - tpi.tif: .tif file of topographic position index from USGS national map (30 x 30 m resolution)
        -   ./data/Predictor Rasters/Wind csv: subdirectory containing wind data from various sources.
            - RAWS_data_SRockies.csv: gust and average daily wind speed (mph) data from RAWS across the Southern Rockies
            - WindData.csv: gust and average daily wind speed (mph) data from airports across the Southern Rockies
            - WindData_CSUmtnCampus.csv: gust and average daily wind speed (mph) data from CSU mountain campus
            - WindData_SNOTEL.csv: gust and average daily wind speed (mph) data from SNOTEL sites across the Southern Rockies

    -   *./data/Preprocessed Rasters*: subdirectory containing unprocessed raster (raw data)
        -   ./data/Predictor Rasters/Climate: subdirectory containing raw climate data.
            - SR_MM_YYYY_diffs.tif: .tif files with the difference in 30 year normal VPD for a given month (MM) and year (YYYY) for the study region data from WorldClim (1 x 1 km resolution)
        -   ./data/Predictor Rasters/Land Cover: subdirectory with raw land cover data.
            - NLCD_2019_SR.tif: .tif file from NLCD 2019 containing landcover for southern Rocky Mountains (30 x 30 m)
            - s2aspen_prob_10m_binOpt.tif: .tif file from Cook et al. 2024 containing probability of aspen in southern Rocky Mountains (10 x 10 m)
            - TreeMap2016.tif: .tif file from TreeMap (Riley et al. 2021) containing forest composition across USA (30 x 30 m)
            - TreeMap2016_tree_table.csv: .csv from Riley et al. 2021 to match raster values with species codes
        -   ./data/Predictor Rasters/Topographic: subdirectory containing processed topographic data.
            - SRockies_DEM_10kmBuff.tif: .tif file of elevation (m) from USGS national map (30 x 30 m resolution)
            - SRockies_slope_10kmBuff.tif: .tif file of slope from USGS national map (30 x 30 m resolution)
            - SRockies_TPI_10kmBuff.tif: .tif file of topographic position index from USGS national map (30 x 30 m resolution)

    -   *./data/Results*: subdirectory to output results of main script
        - cellcounts.csv: number of cells within the study area (tot), within fire perimeters (burn), and touching fire lines (Fls), for each land cover category
        - CleanedFireLines.csv: cleaned data for input into models post spatial extractions (main product of data cleaning)
        - LinesForMapping.shp: .shp file of CleanedFireLines.csv for mapping in ArcGIS Pro for figure 1.
        - NonParametricResults.csv: .csv of results from fischer tests corresponding to Figure 2
        - Table1.csv: raw data that corresponds to table 1
        - TableS3.csv: raw data that corresponds to table s3
    
    -   *./VPd_Addon*: subdirectory with raw VPd data from worldclim (1 x 1 km). Data were processed in ArcGIS pro to calculate difference in 30 year normal of each month for a given year.
                       Prior to calculating the 30 year differences, each raster needed to be resampled (bilinear) to 10 x 10 m and units changed to kPa
        - ./VPd_Addon/Means: subdirectory with 30 year normal VPd for a given month
            - SR_MM_mean.tif: .tif file for the 30 year normal VPd for a given month (MM) (march - november when fires occurred during study time period)
        - ./VPd_Addon/YrYYYY_avgs: series of subdirectories for years (YYYY) 2019-2023 of the study
            - SR_MM_YYYY.tif: the VPd for a given month (MM) and year (YYYY) of the study.
            - SR_MM_YYYY_resamp.tif: VPd layer resampled to appropriate resolution
            - SR_MM_YYYY_resamp_div.tif: resampled VPd layer divided by 10 to get the correct units for VPd
        - ./VPd_Addon/YrYYYY_diffs: series of subdirectors for differences between years (YYYY) and 30 year normal for each given month
            - SR_MM_YYYY_diffs.tif: differences between years (YYYY) and 30 year normal for each given month (MM)
    
-   Documents

-   *README.md:* this file
