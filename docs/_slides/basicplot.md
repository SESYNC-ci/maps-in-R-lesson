---
---

## Basic spatial plots

To display the spatial features (points, lines or polygons) in a *Spatial* object, you can simply use the `plot` function.


~~~r
plot(counties_md)
~~~
{:.text-document title="worksheet-1.R"}

![plot of chunk shp_plot]({{ site.baseurl }}/images/shp_plot-1.png)

===

To show how multiple spatial layers can be superposed in the same plot,
we will create a new *SpatialPolygonsDataFrame* with a single county selected
by name. Note that we can subset `counties_md` just like a regular data frame.

To add a new layer to an existing plot, use the `add = TRUE` argument.


~~~r
howard <- counties_md[counties_md[["NAME"]] == "Howard", ]
plot(counties_md)
plot(howard, col = "red", add = TRUE)
~~~
{:.text-document title="worksheet-1.R"}

![plot of chunk plot_add]({{ site.baseurl }}/images/plot_add-1.png)

===

Other base R functions, such as `text`, always add elements to an existing plot.
In the code below, note that calling `coordinates` on a polygon object returns
the center point of each polygon.


~~~r
plot(counties_md)
plot(howard, col = "red", add = TRUE)
text(coordinates(counties_md), 
     labels = counties_md[["NAME"]],
     cex = 0.7)
~~~
{:.text-document title="worksheet-1.R"}

![plot of chunk plot_text]({{ site.baseurl }}/images/plot_text-1.png)

===

### Exercise

Starting from a fresh map, print numbers on each county in order of the smallest
(1) to largest (24) in land area ("ALAND" attribute). 
*Hint*: Use `rank(x)` to get ranks from a numeric vector x.
