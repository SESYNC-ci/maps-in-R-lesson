---
---

## Masking a raster

To conclude this presentation of rasters, we introduce the `mask` function. Masking a raster means removing some of its data (i.e. setting it to *NA*) based on a logical condition. 

===

For example, the masking layer `nlcd == 81` returns `TRUE` for cells with land cover class 81 (pasture) and `FALSE` otherwise.  With the setting `maskvalue = FALSE`, the code chunk below masks any non-pasture cells and plots the resulting raster.


~~~r
pasture <- mask(nlcd, nlcd == 81, maskvalue = FALSE)
plot(pasture)
~~~
{:title="{{ site.data.lesson.handouts[1] }}" .text-document}
![ ]({% include asset.html path="images/mask/mask-1.png" %})
{:.captioned}

===

### Exercise 

Create and plot a mask for a different type of land cover. 

You may consult `attr_table` to find the numeric *ID* matching a specific land cover class.
