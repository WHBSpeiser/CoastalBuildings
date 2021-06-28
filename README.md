# BuildingRasters

So far, committed are three different tools for turning polygons of desired ROI's into building footprint rasters. 




OSM_Footprints:
  -This is a working code to extract and download OSM footprint data to an input region of choice. The code is written for Hatteras Island, but can be refocused by following incode instruction.
  
  
Footprint_Clipper:
  -This tool helps take your OSM or MS data and clip it to an input region of interest shapefile.
  
  
  
 Heris Rasterize:
  -This is very slightly modified but mostly exactly lifted code from the Heris MS building footprint rasterization code: 
    https://github.com/mehdiheris/RasterizingBuildingFootprints
  
  -This code intakes a building footprint polygon (which can be obtained with the two codes above), and an input reference raster for extent,
  projection, resolution, etc. I include a Google Earth Engine hotlink to make a reference raster if you do not already have a specific one for use
  
  -This code so far is only working well to account for amount of building footprints per reference raster cell, but is having issue in calculating geometric properties over multiple cells of the reference raster.
  
  
  
 In-progress tools:
 Coastal Buffer Poly: Tool that makes an ROI polygon that is a 10km buffer of the United States coast truncated by input Lat/Lon bounds.
    
    Issue: with too high of a coast resolution, processing the 10km buffer takes too long:
    https://geodata.lib.berkeley.edu/catalog/stanford-xv279yj9196
    With too low of an input coast resolution, areas such as Outer Banks, NC are not considered as the United States Coast in available files: 
    https://geodata.lib.berkeley.edu/catalog/stanford-fb084dj2816
