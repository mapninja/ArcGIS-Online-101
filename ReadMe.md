# ArcGIS Online 101

## Overview

This workshop aims to accomplish two things: Introduce participants to basic vocabulary, concepts and techniques for working with spatial data in research and introduce the interface and tools in ArcGIS Online, a web-based alternative to desktop GIS software. This introductory session will focus upon the fundamental concepts and skills needed to begin using ArcGIS Online for the exploration and analysis of spatial data.  

Topics will include:  

* Spatial Data Models and Formats
* Projections and Coordinate Systems
* Basic Data Management
* The ArcGIS Online User Interface
* Simple Analysis using Visualization

GIS Resources:
Stanford Geospatial Center website - http://gis.stanford.edu/

Stanford GIS Listserv - https://mailman.stanford.edu/mailman/listinfo/stanfordgis

## Setup

Users should prepare for this workshop by ensuring that they have an updated browser (preferably Chrome or Firefox) downloading the data to their local hard drive.

**Stanford Affiliates** should be able to access the Stanford University Library's enterprise supbscription to ArcGIS Online, using Stanford Single-SignOn with their SUNetID at: 

[https://stanford.maps.arcgis.com](https://stanford.maps.arcgis.com/sharing/rest/oauth2/authorize?client_id=arcgisonline&display=default&response_type=token&state=%7B"returnUrl"%3A"https%3A%2F%2Fstanford.maps.arcgis.com%2Fhome%2Findex.html"%2C"useLandingPage"%3Atrue%7D&expiration=20160&locale=en&redirect_uri=https%3A%2F%2Fstanford.maps.arcgis.com%2Fhome%2Faccountswitcher-callback.html&force_login=true&hideCancel=true&showSignupOption=true&signuptype=esri)

### Data

The data package for the workshop can be downloaded from []()

The project data folder contains the following datasets:

* **deathAddresses.csv**  - this is a table latitude and longitude coordinates for addresses affected by the cholera outbreak. This table also contains the number of deaths at each address.  
* **snow_map.png.tif** - this is a non-georeferenced image of the map from John Snow's original report on the cholera outbreak of 1854. 
* **Study_Area.shp** - This file is simply a rectangular feature that describes our area of interest.  


#### Additional Files
There is an extra backup data folder that contains versions of files that we will create during the workshop. These files are provided in case any of the steps can't be completed due to software errors or other problems. Welcome to working with open source.  
* **Snow-cholera-map-1_modified** - this is a geo-referenced image of the map from John Snow's original report on the cholera outbreak of 1854.  
* **Water_Pumps.geojson** - this is a spatial data file containing the locations of all of the water pumps recorded in John Snow's original map of the cholera outbreak.  Who woo hoo 

## Getting started on a project  

In this section we will cover starting a new ArcGIS Online project. We will create a new Web Map and go over the basic ArcGIS Online interface.

### Logging in

SSO stuff

### Interface overview

Overview

#### The Basic Components of the ArcGIS Online Interface

The QGIS interface is made up of three basic components:

**Tabs:**
**The Map**
**The Toolbar:**
**Details Panel**


### Basemap layers

Change to Light Grey Canvas

Hack Stamen tiles as your basemap

http://tile.stamen.com/toner-lite/{level}/{col}/{row}@2x.png

### Searching and adding content from ArcGIS Online

No Georeferencing

Can't upload a geotiff anymore?

Add the John Snow Map, published by yalemaps

Save your map

### Uploading a shapefile

*Talk about the shapefile format*

*Zipping a shapefile for upload*

Upload Study Area shapefile

Adjust Symbology

Rename

### Explore navigation in webmaps
(Be sure to test for MacOS and Win)
The Scale Widget

Panning

Shift-Dragging - Zooms in

Command/Control-Shift Dragging - Zooms out

Shift/Scrolling - Zooms in and out

### Scale in Webmaps

How map tiling  works in a web map

### Spatial Bookmarks

Creat a bookmark for the Broad Street Pump

### Coordinate Reference Systems in ArcGIS Online

How CRS works in Web Maps in general, and ArcGIS Online, in particular.

### Create a data layer from an XY table?

Often the data sets that you want to work with will not come as spatial data sets. In this step we will add a table of data that contains fields with the latitude and longitude coordinates of the deaths addresses we want to analyze.

Drag & Drop

Geocode using coordinate field

### Layer symbology

Proportional symbols on Death Addresses

### Viewing the Attributes 

Popups for individual features

Attribute Tables
Sorting
Pan to Selection

Save your map

### Statistics on a field  

**Holy shit, you can't do statistics on a field in AGO? WTF?**

*you have to add a csv in the Add Items interface of Content, to have control over column types. SUmmary only shows for numeric. SHould show for everything, so you can do freq anaysis, too, though*
## Creating spatial data

### Digitize features from a georeferenced map

Save your map

Go to Content

Create an empty point layer for the Water Pumps

Rename it

Add a 'Label' field

Open in Map Viewer

Adjust symbology

### Add points to your shapefile

Start an edit session

Digitize all pumps (13)

### (Reverse) Geocoding

Holy shit, you can't reverse geocode in AGO, either?

### Labels

Label Water Pumps with nearest address.

## Basic spatial data analysis

### Spatial Join (Point Aggregation)

Use spatial join to tag each death address with the name of the pump, nearest.

Nope, can't to a K Nearest Neighbor, either. 

### Summary Statistics

Finally, we would like to summarize the deaths in the outbreak, grouping our summary by the name of the Water Pump that each Death Address is nearest. We will do this using the **Group Stats Tool** which allows us to do a statistical summary similar to the one we did earlier on the entire data set, but this time grouped by nearest water pump.


1.  On the pull-down menu go to **Plugins\> Manage and install plugins.**

2.  On the Plugins window search, type **Group Stats** and select it.

3.  Click on **Install plugin.**

4.  Close the **Plugin Window.**  
![](media/image007-drop-shadow.png)


After the installation a **GroupStats Tool** ![](media/image008.png) appears on the Vector Toolbar.

1. **Click** the **Group Stats tool**

2. **Select Deaths_Allocated** as Layer.  
![](media/image009-drop-shadow.png)

Drag from **Fields** to **Column**: average, count and sum. 

On **Rows,** drag Name (originally from the Water_Pump data layer), and 

on **Value** drag **Num_Cases.**

1.  **Click** on **Calculate** to visualize the summary table.

2.  **Click** the Sum field header on the resulting table to **Sort descending** on the **SUM\_Num\_Cases** field.

Note that the **Broadwick Pump** has the highest value for two of three
significant attributes: **Count** (No. of households), **Sum** (Total Deaths),
and **Average** (Mean Deaths per Household).

1.  On the **Group Stats Window,** go the **Data\> Save all to CSV file. Save** the **Ouput Table** to your **Data** Folder and name it **Deaths\_Summary\_by\_Pumps**.

2.  **Close** the Group Stats Window

## Basic Measures of Spatial Central Tendency

### Spatial Mean (Mean Center)

The Mean Center is the average x- and y-coordinate of all the features in the study area. It's useful for tracking changes in the distribution or for comparing the distributions of different types of features. Here, we will use the Mean Center to highlight the distribution of deaths around the Broad Street Pump.  

First, we will calculate a simple spatial mean. This is simply the mean center of the **distribution of locations** 

1. On the pull-down menu go to menu go to **Vector \> Analysis \> Mean
coordinate(s)**  
![](media/image010-drop-shadow.png)  

1. Select **Deaths_Allocated** as the Input vector layer.
2. Leave the **Weight field** and **Unique ID field** as **Optional.**
3. **Click Browse** to **save** the Output Shapefile as:
    **Deaths\_Spatial\_Mean** to the **Data** Folder**.**
4. **Click OK** to calculate the **Mean Center** and **Close**.
5. Change the **Symbology** for the **Deaths\_Spatial\_Mean layer** to something that contrasts with the other symbologies.

### Weighted Spatial Mean

1. **Run** the **Mean Center tool** again, this time assigning the
   **Num_Cases** field as the **Weight Field**.
2. **Save** the **Output Shapefile** to the **Data** folder and name it **Deaths_Weighted_Spatial_Mean**.
3. **Apply a symbology** to the **Deaths_Weighted_Spatial_Mean layer**.

#### Bonus:  
Set the "Unique ID" option to the "label" field and observe the results. This has the effect of "casing" the spatial mean, based upon the spatial allocation that we did earlier.

### Standard Distance

The Standrad Distance is the spatial statistics equivalent of the standard deviation. It describes the radius around the spatial mean (or weighted spatial mean), which contains 68% of locations in your dataset. It can be very useful for working with GPS data.

![](media/image011-drop-shadow.png)

On the pull-down menu go to menu go to **Processing \> Toolbox** to open the
**Processing Toolbox Window.**

![](media/image012-drop-shadow.png)

On the **Processing Toolbox Window type** to **search**: **Spatial point pattern
analysis** and **double click** to open the tool window.

1.  Select **Death Addresses** as the **Point** layer.

2.  Click the 3 dots and **Select** Save to a file.

3.  **Give** an appropriate name and **Save** the **3 Output Files** on your
    **Data** folder.

![](media/image013-drop-shadow.png)

**Click Run** to calculate the **Standard Distance, Mean Centre and Bounding
Box.**

>   The red dot is the mean center (no weight field; the large circle is the
>   standard distance, which gives an indication of how closely the points are
>   distributed around the mean center; and the rectangle is the bounding box,
>   describing the smallest possible rectangle which will still enclose all the
>   points.

### Creating a surface from Point Data to Highlight “Hotspots”

![media/image14.png](media/image014-drop-shadow.png)

#### Kernel Density

The Kernel Density Tool calculates a magnitude per unit area from the point features using a kernel function to fit a smoothly tapered surface to each point. The result is a raster dataset which can reveal “hotspots” in the array of point data.

1.  Go to the **Processing Toolbox Window** and **type** to search **Kernel Density Estimation (SAGA)** and **double click** to open the tool window.
2.  **Select** the **Deaths_Allocated** layer as the **Points** features.
3.  Select **Num_Cases** as the **Weight Field.**
4.  Set the **Radius** option to **50** (this is in meters).
5.  On the **Output Extent** option, click the 3 dots and select **Use
    layer/canvas extent.**
6.  On the resulting window search for **Study Area** and **Click OK.**
![](media/image015-drop-shadow.png)

Set the **Cellsize** to 10 (this is also in meters)

1.  On the **Kernel Option click** the 3 dots and select **Save to File.**

2.  **Save** the **Output Raster** to the **Data Folder** as **Kernel_Density.**

3.  **Click Run** to run the Kernel Density tool.

4.  **Right Click** the **Kernel_Density layer** and **open** its
    **properties**.

![](media/image016-drop-shadow.png)

**Go** to the **Style Tab** and select

1.  **Render Type:** Singleband gray

    1.  **Color Gradient:** White to black

    2.  **Contrast enhancement:** Stretch to MinMax.

    3.  **Load min/max values:** Select min/max and click load.

    4.  **Hue:** Check Colorize and select a color of your choice

    5.  **Resampling:** Zoomed in **Bilinear.**

    6.  **Click OK**

![](media/image017-drop-shadow.png)

## Creating a Basic Map Layout (in process)

Toggle off uneeded layers & Arrange layers in order of visibility

Change Project CRS to Basemap CRS

Make Symbology & Label adjustments

Rename Layers

Switch to Layout Mode

Add Map

Add Legend

Add Scale

Add Neatline

Add Text

Print to PNG







