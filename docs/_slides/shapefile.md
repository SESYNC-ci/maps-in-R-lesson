---
---

## Reading shapefiles

Vector data in shapefiles can be read via the `readOGR` function in `rgdal`,
which is a package linking R to the open source Geospatial Data Abstraction 
Library (GDAL).

Here, we read a shapefile corresponding to county boundaries for the state 
of Maryland. This data was extracted from the full county boundaries
shapefile available on the [US census website](https://www.census.gov/geo/maps-data/data/cbf/cbf_counties.html).



~~~r
library(rgdal)
counties_md <- readOGR('data/cb_2016_md_county_5m', 
                       'cb_2016_md_county_5m')
~~~
{:title="{{ site.data.lesson.handouts[1] }}" .text-document}


Note that the first argument to `readOGR` is the path of the shapefile 
whereas the second argument is the layer name; for simple shapefiles, it is
usually identical to the file name.

===

The shapefile is read as a *SpatialPolygonsDataFrame* object, which contains
both a list of 24 county (multi)polygons (`counties_md@polygons`), as well as a
data frame (`counties_md@data`) where each row stores the attributes of the
corresponding county.



~~~r
> summary(counties_md)
~~~
{:title="Console" .input}


~~~
Object of class SpatialPolygonsDataFrame
Coordinates:
        min       max
x -79.48765 -75.04894
y  37.91172  39.72312
Is projected: FALSE 
proj4string : [+proj=longlat +datum=NAD83 +no_defs]
Data attributes:
   STATEFP            COUNTYFP           COUNTYNS           AFFGEOID        
 Length:24          Length:24          Length:24          Length:24         
 Class :character   Class :character   Class :character   Class :character  
 Mode  :character   Mode  :character   Mode  :character   Mode  :character  
                                                                            
                                                                            
                                                                            
    GEOID               NAME               LSAD               ALAND          
 Length:24          Length:24          Length:24          Min.   :2.096e+08  
 Class :character   Class :character   Class :character   1st Qu.:8.279e+08  
 Mode  :character   Mode  :character   Mode  :character   Median :1.087e+09  
                                                          Mean   :1.048e+09  
                                                          3rd Qu.:1.222e+09  
                                                          Max.   :1.711e+09  
     AWATER         
 Min.   :6.346e+06  
 1st Qu.:2.418e+07  
 Median :2.007e+08  
 Mean   :2.910e+08  
 3rd Qu.:4.558e+08  
 Max.   :1.145e+09  
~~~
{:.output}

