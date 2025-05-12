# Data Analytics Tutorials in Forestry

![prf_image](https://opendata.nfis.org/mapserver/PRF_Layout.jpg)

## Table of Contents

- [Background](#background)
- [Using Tutorials](#using-tutorials)
- [Data Description](#data-description)
- [Useful References](#useful-references)

# [Background]((#background))

These tutorials make use of the publicly available Petawawa Research Forest (PRF)  dataset provided by the Canadian Forest Service (CFS).  The PRF is the oldest research forest in Canada, dating back to 1918. As such, the area has a rich historical record of remote sensing and forest inventory data, and has recently become a remote sensing "supersite".

**You can view the full PRF dataset at the following link:**

[https://opendata.nfis.org/mapserver/PRF.html](https://opendata.nfis.org/mapserver/PRF.html)


# [Using Tutorials](#using-tutorials)

These tutorials are designed to be run on **[Google Collab](https://colab.research.google.com/)**. All collab scripts are designed to run independently


# [Data Description](#data-description)

The tutorials will use several different datasets from the PRF, these are listed below and described in more detail in the following sections.

- Invidual Tree Measurements
- Plot locations

**[All data used in the tutorials is available on Google Drive at this link](https://drive.google.com/file/d/1UDKAdXW0h6JSf7k31PZ-srrQ3487l9e2/view?usp=sharing)**


## Individual Tree Measurements

**File: trees.csv**

Individual tree measurements were taken at permanent sample plots (PSPs) across the PRF in 2018. A data dictionary is provided below summarizing the `trees.csv`. In this data, each tree is a row and each column is an attribute (e.g., height).

| **Column**       | **Definition**                                                                 |
|------------------|-------------------------------------------------------------------------------|
| PlotName         | Plot name                                                                    |
| TreeID           | Tree ID                                                                      |
| TreeSpec         | Tree species                                                                 |
| Origin           | Origin. N = natural (includes coppice), P = planted                          |
| Status           | Status. L = Live, D = Dead (only includes decayclass 1 & 2)                  |
| DBH              | Dbh (cm)                                                                     |
| CrownClass       | Crown class                                                                  |
| QualityClass     | Quality class                                                                |
| DecayClass       | Decay class                                                                  |
| Ht               | Height (m), includes estimated heights                                       |
| HLF              | HLF                                                                          |
| HtFlag           | HtFlag                                                                       |
| baha             | Basal area/ha = Dbh * Dbh * 0.00007854 * stems                               |
| ht_meas          | Height (m), if measured in the field                                         |
| stems            | Stems per hectare (number of trees/ha each tree represents)                  |
| mvol             | Gross merchantable volume (m³/ha)                                            |
| tvol             | Gross total volume (m³/ha)                                                  |
| biomass          | Aboveground biomass (kg/ha)                                                 |
| size             | Sawlog size                                                                  |

## Plot Locations

Field plots in the PRF containing the trees in `trees.csv` are georeferenced, and their locations are provided in the `plots.gpkg` file. This is a spatial dataset stored in a GeoPackage (.gpkg) file. The data is projected in the **WGS 84 / UTM zone 18N** coordinate reference system (CRS).

| **Column** | **Definition**                                                                 |
|------------|-------------------------------------------------------------------------------|
| Plot       | Unique identifier for plot, equivalent to "PlotName" column in `trees.csv`|
| Date       | String representating the date when plot was visited. |
| Northing   | Y coordinate in the CRS (see description above) |
| Easting    | X coordinate in the CRS (see description above) |
| Source     | Device used to collect the coordinates of the plot center. Note that the spatial accuracy of coordinates vary between devices. |


**File: plots.gpkg**

# [Useful References](#useful-references)

**You can learn more about the PRF in the following publications:**

* [White, Joanne C., et al. "The Petawawa Research Forest: Establishment of a remote sensing supersite." The Forestry Chronicle 95.3 (2019): 149-156.](https://doi.org/10.5558/tfc2019-024).

* [Hoepting, Michael, Trevor Jones, and Jeff Fera. "Collaborating on climate change at the Petawawa Research Forest." The Forestry Chronicle 95.2 (2019): 62-65.](https://pubs.cif-ifc.org/doi/abs/10.5558/tfc2019-012)

* [Bolton, Douglas K., et al. "Optimizing Landsat time series length for regional mapping of lidar-derived forest structure." Remote sensing of Environment 239 (2020): 111645.](https://doi.org/10.1016/j.rse.2020.111645)



