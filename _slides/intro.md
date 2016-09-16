---
---

Over time, the R community has produced a collection of spatial analysis and visualization packages, giving current R users the ability to implement various tasks that previously required to specialized Geographic Information System (GIS) software. 

This lesson provides a quick tour of popular tools available to read and display spatial data in R. These can be useful whether you want to quickly explore a dataset or to produce high-quality maps for print and web publications. Like for other types of figures, building maps with scripts can take some time at first, but that investment will quickly pay off in terms of reproducibility and re-use value.

<!--split-->

### Spatial data types

All types of spatial data belong in one of two main categories: 
*vectors* (points, lines and polygons) or *rasters* (grids of pixels).

| Raster     | Vector     |
|------------+------------|
| matrix     | table      |
| surface    | shape      |
| pixels     | features   |
| bands      | attributes |
{:.table}

Some raster file formats: GeoTIFF, netCDF

Some vector file formats: shapefiles, WKT, GeoJSON
