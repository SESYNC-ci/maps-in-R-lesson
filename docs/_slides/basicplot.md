---
---

## Basic spatial plots

To display the spatial features (points, lines or polygons) in a *Spatial* object, you can simply use the `plot` function.


~~~r
plot(counties_md)
~~~

~~~
Error in plot(counties_md): object 'counties_md' not found
~~~
{:.text-document title="worksheet-1.R"}

===

To show how multiple spatial layers can be superposed in the same plot,
we will create a new *SpatialPolygonsDataFrame* with a single county selected
by name. Note that we can subset `counties_md` just like a regular data frame.

To add a new layer to an existing plot, use the `add = TRUE` argument.


~~~r
howard <- counties_md[counties_md[["NAME"]] == "Howard", ]
~~~

~~~
Error in eval(expr, envir, enclos): object 'counties_md' not found
~~~

~~~r
plot(counties_md)
~~~

~~~
Error in plot(counties_md): object 'counties_md' not found
~~~

~~~r
plot(howard, col = "red", add = TRUE)
~~~

~~~
Error in plot(howard, col = "red", add = TRUE): object 'howard' not found
~~~
{:.text-document title="worksheet-1.R"}

===

Other base R functions, such as `text`, always add elements to an existing plot.
In the code below, note that calling `coordinates` on a polygon object returns
the center point of each polygon.


~~~r
plot(counties_md)
~~~

~~~
Error in plot(counties_md): object 'counties_md' not found
~~~

~~~r
plot(howard, col = "red", add = TRUE)
~~~

~~~
Error in plot(howard, col = "red", add = TRUE): object 'howard' not found
~~~

~~~r
text(coordinates(counties_md), 
     labels = counties_md[["NAME"]],
     cex = 0.7)
~~~

~~~
Error in text(coordinates(counties_md), labels = counties_md[["NAME"]], : could not find function "coordinates"
~~~
{:.text-document title="worksheet-1.R"}

===

### Exercise

Starting from a fresh map, print numbers on each county in order of the smallest
(1) to largest (24) in land area ("ALAND" attribute). 
*Hint*: Use `rank(x)` to get ranks from a numeric vector x.
