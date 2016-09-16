---
---

## Adding data to maps

The *tmap* ("thematic map") package simplifies map-based visualization of data attributes associated with a given shapefile. Its logic and syntax are particularly easy to learn for those users already familiar with the popular graphics package *ggplot2*.

<!--split-->

### Quick mapping with `qtmap`

Like the `qplot` function in ggplot2, `qtmap` serves to make a quick, less customized map from a single line of code. Its first argument is a spatial object forming the base of the map.

~~~r
library(tmap)
qtm(counties_proj)
~~~
{:.text-document title="lesson-7-1.R"}

![plot of chunk qtmap](/maps-in-R-lesson/images/qtmap-1.png)

<!--split-->

If the shapefile has associated data, its column names (as quoted strings) can be mapped to graphical elements of the plot. In the example below, the "fill" color of counties depends on their water area, and county names are shown at the center of each polygon.

~~~r
qtm(counties_proj, fill = "AWATER", text = "NAME")
~~~
{:.text-document title="lesson-7-1.R"}

![plot of chunk qtmap_data](/maps-in-R-lesson/images/qtmap_data-1.png)

<!--split-->

### Layered thematic maps (ggplot style)

For more detailed maps, you can add multiple layers defined by `tm_` functions. In the code below, `tm_shape` sets the spatial object from which the successive layers are derived; `tm_borders` adds the polygon outlines; `tm_fill` and `tm_text` define the same graphical elements as in our previous map, with additional arguments specifying the legend title and text size.


~~~r
map1 <- tm_shape(counties_proj) +
            tm_borders() +
            tm_fill("AWATER", title = "Water Area (sq. m)") +
            tm_text("NAME", size = 0.7)
~~~
{:.text-document title="lesson-7-1.R"}

<!--split-->


~~~r
map1
~~~
{:.text-document title="lesson-7-1.R"}

![plot of chunk tmap_show](/maps-in-R-lesson/images/tmap_show-1.png)

<!--split-->

Since we saved our thematic map in a variable `map1`, we can recall it and add more map elements, as shown below.


~~~r
map1 +
    tm_style_classic(legend.frame = TRUE) +
    tm_scale_bar(position = c("left", "top"))
~~~
{:.text-document title="lesson-7-1.R"}

![plot of chunk tmap_add](/maps-in-R-lesson/images/tmap_add-1.png)

Note that the `tm_style_` functions change the overall theme of the plot.

<!--split-->

### Exercise 

Color scales in tmap are divided into bins by default. 

Consult the help file `?tm_fill` to find which argument controls how the scale is divided. Can you change it to a continuous gradient instead of bins?

<!--split-->

Note that a single thematic map can combine data from multiple vector or raster objects. You can find more tmap examples in the [tmap in a nutshell](https://cran.r-project.org/web/packages/tmap/vignettes/tmap-nutshell.html) R vignette.
