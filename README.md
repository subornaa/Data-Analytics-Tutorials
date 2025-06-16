# Data Analytics Tutorials in Forestry

![prf_image](https://opendata.nfis.org/mapserver/PRF_Layout.jpg)

## Table of Contents

- [Background](#background)
- [Using Tutorials](#using-tutorials)
- [Data Description](#data-description)
- [Suggested Use of AI](#suggested-use-of-ai)
- [Useful References](#useful-references)

# Background

These tutorials make use of the publicly available Petawawa Research Forest (PRF)  dataset provided by the Canadian Forest Service (CFS).  The PRF is the oldest research forest in Canada, dating back to 1918. As such, the area has a rich historical record of remote sensing and forest inventory data, and has recently become a remote sensing "supersite".

**You can view the full PRF dataset at the following link:**

[https://opendata.nfis.org/mapserver/PRF.html](https://opendata.nfis.org/mapserver/PRF.html)


# Using Tutorials

These tutorials are designed to be run on **[Google Collab](https://colab.research.google.com/)**. All collab scripts are designed to run independently


# Data Description

The tutorials will use several different datasets from the PRF, these are described in more detail in the following sections.



**[All data used in the tutorials is available on Google Drive at this link](https://drive.google.com/file/d/1UDKAdXW0h6JSf7k31PZ-srrQ3487l9e2/view?usp=sharing)**


## Individual Tree Measurements

**File: trees.csv**

Individual tree measurements were taken at permanent sample plots (PSPs) across the PRF in 2018. A data dictionary is provided below summarizing the `trees.csv`. In this data, each tree is a row and each column is an attribute (e.g., height).

| **Column**       | **Definition**                                                               |
|------------------|------------------------------------------------------------------------------|
| PlotName         | Unique plot identifier                                                       |
| TreeID           | Unique tree identifier                                                       |
| species          | Tree common species name                                                     |
| Origin           | Origin. N = natural (includes coppice), P = planted                          |
| Status           | Status. L = Live, D = Dead (only includes decayclass 1 & 2)                  |
| DBH              | Diameter at breast height (cm)                                               |
| CrownClass       | Crown class (D = Dominant; C = Codominant; I = Intermediate; OS = Overtopped/suppressed; A = Anomaly; E = Emergent)                                                                                         |
| DecayClass       | Decay class (1 = recently dead, top is intact; 2 = greater than 50 % coarse; >3 = dead for several years)                                                                                            |
| height           | Tree top height in meters                                                    |
| baha             | Basal area/ha = Dbh * Dbh * 0.00007854 * stems                               |
| codom            | Whether a tree is codominant or not (either Y or N)                          |
| mvol             | Gross merchantable volume (m³/ha)                                            |
| tvol             | Gross total volume (m³/ha)                                                   |
| biomass          | Aboveground biomass (kg/ha)                                                  |
| size             | Sawlog size category (Poles, Under, Small, Medium, Large)                    |


## Plot Locations

**File: plots.gpkg**

Field plots in the PRF containing the trees in `trees.csv` are georeferenced, and their locations are provided in the `plots.gpkg` file. This is a spatial point dataset stored in a GeoPackage (.gpkg) file.

Each field plot is circular, with a radius of 14.1m (625m^2). Note that this dataset is in a **point** format (i.e., only XY coordinates of plot centers).

| **Column** | **Definition**                                                                 |
|------------|-------------------------------------------------------------------------------|
| Plot       | Unique identifier for plot, equivalent to "PlotName" column in `trees.csv`|
| Date       | String representating the date when plot was visited. |
| Northing   | Y coordinate in the CRS (see description above) |
| Easting    | X coordinate in the CRS (see description above) |
| Source     | Device used to collect the coordinates of the plot center. Note that the spatial accuracy of coordinates vary between devices. |


## PRF Boundary

**File: boundary.gpkg**

Polygon dataset including the boundary of the Petawawa Research Forest (PRF). The data is projected in the **WGS 84 / UTM zone 18N** coordinate reference system (CRS). All other spatial datasets are projected in this CRS unless otherwise specified.

## PRF Water

**File: water.gpkg**

Polygons delineating water bodies in the PRF including lakes, wetlands, rivers, and creeks.

## Airborne Laser Scanning (ALS) LiDAR derived metrics

**File: als_metrics.tif**

LiDAR (airborne laser scanning, ALS) derived metrics (i.e., statistical summaries) in raster raster format spanning the PRF. This raster can be used as a proxy for the forest canopy height.

The raster contains 67 bands (each band is one metric) which are descibed below. Some descriptions are for a range of bands due to redundancy.

| Band(s)  | Metric Name(s)             | Description                |
|----------|----------------------------|----------------------------|
| B1       | avg_95                     |  Average height trimmed at 95% of max height |
| B2       | avg                        |  Average height      |
| B3 - B11 | b10, b20, b30, ... , b90   |  Decile % of points between 0 and 99% height       |
| B12 - B24| dns_2m, dns_4m, dns_5m, ... , dns_25m | Density percentage of all returns Xm - 49m divided by all returns |
| B25      | kur_95                     |  Kurtosis height trimmed at 95% of max height |
| B26 - 38 | p01, p05, p10, ... , p99   |  Height percentiles                  |
| B39      | qav                        |  Average square height |
| B40      | skew_95                    |  Skewness height trimmed at 95% of max height |
| B41 - B64| d0_2, d2_4, d4_6, ..., d46_48 | Number of returns from X-Y meters divided by all returns         |
| B65      | std_95                     | Standard deviation of height trimmed at 95% of max height |
| B66      | vci_1mbin                  | Vertical Complexity Index (VCI) with a 1 m bin        |
| B67      | vci_0.5bin                 | Vertical Complexity Index (VCI) with a 0.5 m bin        |


## Sentinel-2 Imagery

**Files:**
- **petawawa_s2_2018.tif**
- **petawawa_s2_2024.tif**

Sentinel-2 (S2) is a European Space Agency multispectral satellite constellation including 3 sensors. S2 imagery contains 12 bands spanning the visible, near infrared, and shortwave infrared portions of the electromagnetic spectrum, with a spatial resolution ranging from 10m - 60m depending on the band. The table below summarized all the S2 bands. For the purpose of this analyis, all S2 imagery was resampled to a 10m resolution, but understand that this does not account for the fact that some bands are inherently lower resolution.

| Band  | Wavelength (S2A / S2B)                | Description     |
|-------|---------------------------------------|-----------------|
| B1    | 443.9nm / 442.3nm                     | Aerosols        |
| B2    | 496.6nm / 492.1nm                     | Blue            |
| B3    | 560nm / 559nm                         | Green           |
| B4    | 664.5nm / 665nm                       | Red             |
| B5    | 703.9nm / 703.8nm                     | Red Edge 1      |
| B6    | 740.2nm / 739.1nm                     | Red Edge 2      |
| B7    | 782.5nm / 779.7nm                     | Red Edge 3      |
| B8    | 835.1nm / 833nm                       | NIR             |
| B8A   | 864.8nm / 864nm                       | Red Edge 4      |
| B9    | 945nm / 943.2nm                       | Water vapor     |
| B11   | 1613.7nm / 1610.4nm                   | SWIR 1          |
| B12   | 2202.4nm / 2185.7nm                   | SWIR 2          |

We include two time steps of S2 imagery to support temporal anlysis, including imagery of the PRF from 2018 and 2024.

S2 imagery was processed in Google Earth Engine (GEE) using the following script:

https://code.earthengine.google.com/e0a63220c15068398d6d432be5e3ccb8

The dataset is described in more detail at the link below:

https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_SR_HARMONIZED

## LiDAR Point Cloud Subset

**File: forest_point_cloud.las**

**Files:**
- **forest_point_cloud.las**
- **forest_point_cloud_footprint.gpkg**

LiDAR (airborne laser scanning) point cloud of a forested subset area in the PRF. Data is provided in the LAS file format, and includes XYZ coordinates of LiDAR returns. 

The spatial coverage (i.e., footprint) of the LAS file is provided in the associated `forest_point_cloud_footprint.gpkg` file.

# Suggested Use of AI

Artificial intelligence (AI), specifically, large language model (LLMs) are no doubt useful tools for programming and data analysis with python. However, we must be cautious when implementing these tools, as we would with any new tool. To maximize the learning outcomes of this tutorial series, we enourage users to always think critically about code you are using, especially if it has been generated by AI. 

Using AI for basic tasks (e.g., removing columns from a data frame) is an effective way to save time. However, we recommend you try to perform higher level planning and program design yourself without relying too heavily on AI.

It is also worth noting that information available to AI is in many cases out of date. Since python packages are updated regularly (sometime weekly), it is likely that code provided to you by AI may be out of date. We strongly recommend always consulting python documentation as the primary source of information when trying to solve a problem.

# Useful References

**You can learn more about the PRF in the following publications:**

* [Riofrío, José, et al. "Modelling height growth of temperate mixedwood forests using an age-independent approach and multi-temporal airborne laser scanning data." Forest Ecology and Management 543 (2023): 121137.](https://doi.org/10.1016/j.foreco.2023.121137)

* [Bolton, Douglas K., et al. "Optimizing Landsat time series length for regional mapping of lidar-derived forest structure." Remote sensing of Environment 239 (2020): 111645.](https://doi.org/10.1016/j.rse.2020.111645)

* [White, Joanne C., et al. "The Petawawa Research Forest: Establishment of a remote sensing supersite." The Forestry Chronicle 95.3 (2019): 149-156.](https://doi.org/10.5558/tfc2019-024).

* [Hoepting, Michael, Trevor Jones, and Jeff Fera. "Collaborating on climate change at the Petawawa Research Forest." The Forestry Chronicle 95.2 (2019): 62-65.](https://pubs.cif-ifc.org/doi/abs/10.5558/tfc2019-012)