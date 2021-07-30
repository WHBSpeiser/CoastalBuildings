# CoastalBuildingsFinder

## Description:

### General
CoastalBuildingsFinder is a Jupyter Notebook to aide in the collection of building footprint data for the Eastern United States Coast (more locations to come). The goals of this Notebook are to keep track of various sources of building footprint data, provide an easy interface for extracting that data within 10km of the coast and specified, drawn bounds, and to download such data in a prefereable file format (i.e. GeoJSON, Shapefile, or TIF). The rasterization process is modified from the Mehdi Heris RasterizeBuildingFootprints toolbox: [https://github.com/mehdiheris/RasterizingBuildingFootprints] 



### How CoastalBuildingsFinder works:
The coordinates of a drawn bounding box are extracted and converted into a GeoDataFrame. This GeoDataFrame is used to clip a polyline of the United States Coast, pulled from the UC Berkeley Spatial Library. This clipped polyline is buffered by 10 km. Then, the code ingests the building footprint data from your chosen state of interest. This is done in different ways depending on a chosen datasource. If you chose the Open Street Maps data, for example, the code uses the **osmnx** toolbox to call data from the drawn bounding box; if you choose the MS Footprints building data source, the code pulls the GeoJSON information from  Microsoft's online repository for entire chosen state. After this data is ingested, it is clipped to the coastal polyline 10km buffer, converted to your file choice preference and then downloaded to your chosen directory. 


If you prefer raster information, the code converts your bounding box into a raster with blank values and pixel xy dimensions set to an input resolution with  the projection EPSG:4326. The geometric statistics of your clipped building footprint data are then calculated for each intersecting pixel point. For more information on the calculated statistics check, Heris et al., 2020.




## Installation
### Download Notebook:
All commands are contained within a single notebook which will be continuously updated. Check the repository to make sure you have newest version in order to obtain the maximal entered available building footprint data sources.

### Anaconda Environment:
In order to run the Notebook, multiple Python packages are required. In order to do so, we recomend using **Anaconda** which can be found here: https://www.anaconda.com/. Once in **Anaconda**, install **Jupyter Notebook**. Open Jupyter and find the downloaded notebook. You will be required to download the following packages:
#### GDAL: https://gdal.org/api/python.html
#### ipyleaflet: https://ipyleaflet.readthedocs.io/en/latest/
#### pandas: https://pandas.pydata.org/
#### geopandas: https://geopandas.org/ 
#### Shapely: https://shapely.readthedocs.io/en/stable/
#### pyproj: https://pyproj4.github.io/pyproj/stable/
#### rasterio: https://rasterio.readthedocs.io/en/latest/
#### fiona: https://pypi.org/project/Fiona/
#### osmnx: https://osmnx.readthedocs.io/en/stable/, https://github.com/gboeing/osmnx

## Usage:
### Cell 1: Setting downloads directory
When you run the first cell, a pop-up window will instruct you to choose a directory. The directory folder that you choose will be where any output and incidental data are downloaded.

### Cell 1: State and Source
After choosing your directory, your first cell will display multiple options below the code window. The first will be a dropdown where you choose your available State of interest. In the next dropdown, you will choose an datasource for building footprints within the chosen state. Different sources will take different amounts of time to process and download. This is due their source files varying in sizes or because of the data calling method necessary for the chosen source. Different sources are also of varying accuracy or consist of data collected fromn different years. It is encouraged that you read the information on their data sources in the **Sources** section below.

### Cell 1: Footprint Data Type
Choose your prefered data type for your non-rasterized building footprints from the "File Type" dropdown menu. 
 
### Cell 1: Rasterization
#### Building Footprint Rasters
If you would like footprint data as a TIF, click on the "Check for raster files" checkbox. If checked, 6 TIF raster files will be created in your directory: bldgSum, bldgMin, bldgMax, bldgCount, bldgCentroidCount, and bldgAve. These different rasters will display respective in-pixel statistics for the chosen footprint dataset and region of interest. E.g. bldgCentroidCount will display the number of building centroids in a specified location:


<img src="https://github.com/WHBSpeiser/CoastalBuildings/blob/main/ExampleImages/CentroidCountExample.png" width="400" />


#### Resolution
Enter your desired resolution for the output raster in meters. This will determine the pixelsize in which building footprint statistics are calculated from your chosen location and data source. Coming soon: option to upload a reference raster for pixel size information.

### Cell 2: Region of Interest Extent
After going through the above options, run the second cell. This cell will bring up a ipyleaflet interactive map in which you can draw a bounding box to9 specify your desired coastal region of interest. The information from this bounding box will set maximum extent of the coastline buffered to 10km within the chosen state. **In order for this step to work, choose the rectangle tool**: 


<p align="center">
  <img src="https://github.com/WHBSpeiser/CoastalBuildings/blob/main/ExampleImages/Cell2Example.gif" width="700" />
</p>

(coming soon, polygon drawing compatability)

After you draw your bounds, simply progress to the next cell.

### Cell 3: Download
Finally, to download your data, run the third cell. As mentioned above, processing and downloading time may vary with the size of your bounding box and your chosen data source.

**Please note, if you encounter a 500 Internal Server Error**, you may need to re-enter in the location for the United States Coast polyline. To do this, go to https://geodata.lib.berkeley.edu/catalog/stanford-xv279yj9196 -> Click the **Export** button under GeoJSON -> Right click and copy the url in the hotlink "Your file stanford-xv279yj9196-geojson.json is ready for download", and re-enter this URL in cell 3, line 49:

    coast=gpd.read_file('https://geodata.lib.berkeley.edu/download/file/stanford-xv279yj9196-geojson.json')






## Sources
1. Heris MP, Foks NL, Bagstad KJ, Troy A, Ancona ZH. A rasterized building footprint dataset for the United States. Sci Data. 2020 Jun 29;7(1):207. doi: 10.1038/s41597-020-0542-3. Erratum in: Sci Data. 2020 Jul 16;7(1):245. PMID: 32601298; PMCID: PMC7324622.
2. OSM Street Data: https://www.openstreetmap.org/
3. MS Building Footprints: https://github.com/microsoft/USBuildingFootprints
4. 1:1,000,000-Scale Coastline of the United States, 2014: https://geodata.lib.berkeley.edu/catalog/stanford-xv279yj9196
