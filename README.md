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

The tutorials will use several different datasets from the PRF, these are listed below and described in more detail in the following sections.

- Invidual Tree Measurements
- Plot locations

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
| DBH              | Dbh (cm)                                                                     |
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

Field plots in the PRF containing the trees in `trees.csv` are georeferenced, and their locations are provided in the `plots.gpkg` file. This is a spatial point dataset stored in a GeoPackage (.gpkg) file. The data is projected in the **WGS 84 / UTM zone 18N** coordinate reference system (CRS).

Each field plot is circular, with a radius of 14.1m (625m^2). Note that this dataset is in a **point** format (i.e., only XY coordinates of plot centers).

| **Column** | **Definition**                                                                 |
|------------|-------------------------------------------------------------------------------|
| Plot       | Unique identifier for plot, equivalent to "PlotName" column in `trees.csv`|
| Date       | String representating the date when plot was visited. |
| Northing   | Y coordinate in the CRS (see description above) |
| Easting    | X coordinate in the CRS (see description above) |
| Source     | Device used to collect the coordinates of the plot center. Note that the spatial accuracy of coordinates vary between devices. |


**File: plots.gpkg**

# Suggested Use of AI

Artificial intelligence (AI), specifically, large language model (LLMs) are no doubt useful tools for programming and data analysis with python. However, we must be cautious when implementing these tools, as we would with any new tool. To maximize the learning outcomes of this tutorial series, we enourage users to always think critically about code you are using, especially if it has been generated by AI. 

Using AI for basic tasks (e.g., removing columns from a data frame) is an effective way to save time. However, we recommend you try to perform higher level planning and program design yourself without relying too heavily on AI.

It is also worth noting that information available to AI is in many cases out of date. Since python packages are updated regularly (sometime weekly), it is likely that code provided to you by AI may be out of date. We strongly recommend always consulting python documentation as the primary source of information when trying to solve a problem.

# Useful References

**You can learn more about the PRF in the following publications:**

* [White, Joanne C., et al. "The Petawawa Research Forest: Establishment of a remote sensing supersite." The Forestry Chronicle 95.3 (2019): 149-156.](https://doi.org/10.5558/tfc2019-024).

* [Hoepting, Michael, Trevor Jones, and Jeff Fera. "Collaborating on climate change at the Petawawa Research Forest." The Forestry Chronicle 95.2 (2019): 62-65.](https://pubs.cif-ifc.org/doi/abs/10.5558/tfc2019-012)

* [Bolton, Douglas K., et al. "Optimizing Landsat time series length for regional mapping of lidar-derived forest structure." Remote sensing of Environment 239 (2020): 111645.](https://doi.org/10.1016/j.rse.2020.111645)



