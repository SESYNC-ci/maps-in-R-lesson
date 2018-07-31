---
---

## Interactive maps with Leaflet

The *leaflet* package is a R interface to the leaflet JavaScript library. It produces interactive maps (with controls to zoom, pan and toggle layers) combining local data with base layers from web mapping services.

===

The `leaflet()` function creates an empty leaflet map to which layers can be added using the pipe (`%>%`) operator. The `addTiles` functions adds a base tiled map; by default, it imports tiles from OpenStreetMap. We center and zoom the map with `setView`. 



~~~r
library(leaflet)
imap <- leaflet() %>%
            addTiles() %>%
            setView(lng = -76.505206, lat = 38.9767231, 
                    zoom = 7)
imap
~~~
{:.text-document .no-eval title="{{ site.handouts[1] }}"}


===

Switch to the "Viewer" tab in RStudio to see the result.

![leaflet1]({{ site.baseurl }}/images/leaflet1.png)

===

To show how leaflet can access open data from various web mapping services (WMS), we add real-time weather radar data from the [Iowa Environmental Mesonet](https://mesonet.agron.iastate.edu/ogc/).



~~~r
imap %>%
    addWMSTiles(
        "http://mesonet.agron.iastate.edu/cgi-bin/wms/nexrad/n0r.cgi",
        layers = "nexrad-n0r-900913", group = "base_reflect",
        options = WMSTileOptions(format = "image/png", transparent = TRUE),
        attribution = "Weather data © 2012 IEM Nexrad"
    )
~~~
{:.text-document .no-eval title="{{ site.handouts[1] }}"}


Use the map controls to zoom away from the current location and find ongoing storm events.
