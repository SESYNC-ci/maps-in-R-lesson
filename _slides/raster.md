---
---

## Reading rasters into R

While vector spatial layers are composed of geometrical objects defined by their vertices, raster layers are grids of pixels with attached values. 

We start by loading the **raster** package in R and importing a raster file with the eponymous `raster` function. This file is a portion of the [National Land Cover Database](http://www.mrlc.gov/nlcd2011.php), which we already cropped and reduced to a lower resolution in order to speed up processing time for this tutorial.


~~~r
library(raster)
nlcd <- raster("data/nlcd_agg.grd")
~~~
{:.text-document title="lesson-7-1.R"}

<!--split-->

A raster is fundamentally a data matrix with associated spatial properties (e.g. extent, resolution and projection) that allow its values to be mapped onto geographical space. You can view these key properties -- the raster's metadata -- by typing the object name in the console.


~~~r
nlcd
~~~
{:.input}
~~~
class       : RasterLayer 
dimensions  : 2514, 3004, 7552056  (nrow, ncol, ncell)
resolution  : 150, 150  (x, y)
extent      : 1394535, 1845135, 1724415, 2101515  (xmin, xmax, ymin, ymax)
coord. ref. : +proj=aea +lat_1=29.5 +lat_2=45.5 +lat_0=23 +lon_0=-96 +x_0=0 +y_0=0 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs 
data source : /nfs/pmarchand-data/Training/maps-in-R-lesson/_slides/data/nlcd_agg.grd 
names       : nlcd_2011_landcover_2011_edition_2014_03_31 
values      : 0, 95  (min, max)
attributes  :
        ID      COUNT Red Green Blue Land.Cover.Class Opacity
 from:   0 7854240512   0     0    0     Unclassified       1
 to  : 255          0   0     0    0                        0
~~~
{:.output}

<!--split-->

The values in raster cells range from 0 to 255, yet land cover is a categorical variable. The mapping of numbers to categories can be found in the raster's attribute table:

~~~r
attr_table <- nlcd@data@attributes[[1]]
~~~
{:.text-document title="lesson-7-1.R"}

Each land cover category has a distinct color specified by the "Red", "Green" and "Blue" columns. We can visualize the whole raster with `plot`.

~~~r
plot(nlcd)
~~~
{:.text-document title="lesson-7-1.R"}

![plot of chunk raster_plot](/maps-in-R-lesson/images/raster_plot-1.png)

<!--split-->

At this point, we might want to superpose the county boundaries on top of the raster image. However, the following instruction does not show the county polygons. Why not?

~~~r
plot(counties_md, add = TRUE)
~~~
{:.input}
