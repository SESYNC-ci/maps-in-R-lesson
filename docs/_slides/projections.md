---
---

## Reading and changing projections 

In order for two spatial objects to be comparable, they must be represented in the same coordinate reference system. This can be a geographic coordinate system or a projected coordinate system.

===

A **geographic coordinate system** (GCS) represents each point on Earth by two angular coordinates, a longitude and a latitude. In effect, it approximates the irregular "sea level" surface of the Earth (the geoid) by an ellipsoid (a sphere flattened at the poles). The specification of this ellipsoid, or *datum*, has changed over times; current global maps are generally based on the WGS 84 datum, but other systems are in use for older or regional maps. 

![Geoid approximation]({% include asset.html path="images/spheroid.png" %})

===

A **projected coordinated system** associates angular coordinates to points on a plane, in order to produce two-dimensional maps. No such projection can faithfully reproduce the three-dimensional relationship between any set of points on the globe. For example, 
the Mercator projection (left) preserves angles, which is useful for navigation, but it greatly inflates areas at the poles. The Lambert equal-area projection (right) preserves areas at the cost of shape distortion away from its center.

![Projections]({% include asset.html path="images/proj.png" %})

[Source](http://www.perrygeo.com/tissot-indicatrix-examining-the-distortion-of-map-projections.html)

Web-based tiled map services like Google Maps use a simplified, less accurate Mercator projection (Web Mercator) to optimize rendering speed.

===

### Projection String

Coordinate systems in R are described in a standard PROJ.4 string format.

The `counties_md` polygons layer uses a geographic coordinate system ("+proj=longlat") based on the *NAD83* datum, whereas the `nlcd` has an Albers equal-area projection ("+proj=aea").



~~~r
> proj4string(counties_md)
~~~
{:title="Console" .input}


~~~
[1] "+proj=longlat +datum=NAD83 +no_defs "
~~~
{:.output}



~~~r
> proj4string(nlcd)
~~~
{:title="Console" .input}


~~~
[1] "+proj=aea +lat_1=29.5 +lat_2=45.5 +lat_0=23 +lon_0=-96 +x_0=0 +y_0=0 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs"
~~~
{:.output}


Question
: Why is the equal-area projection useful for a land cover dataset?

Answer
: {:.fragment} Because each cell has the same area, the proportion of cells with a given land cover class is a good estimate of the fraction of total land area covered by that class

===

Returning to our original problem, we can superpose the two layers by first converting `counties_md` to the same projection as `nlcd`. The `spTransform` function performs this
operation.



~~~r
counties_proj <- spTransform(counties_md, 
                             proj4string(nlcd))
plot(nlcd)
plot(counties_proj, add = TRUE)
~~~
{:title="{{ site.data.lesson.handouts[1] }}" .text-document}
![ ]({% include asset.html path="images/projections/sptransform-1.png" %})
{:.captioned}
