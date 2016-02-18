# RIO (modelled)
More info about the RIO interpolation:
* http://www.irceline.be//nl/documentatie/modellen/modellen#rio%20interpolatiemethode (Dutch)
* http://www.irceline.be/fr/documentation/modeles/modeles#m-thode-d-interpolation-rio (French)
* http://www.irceline.be/en/documentation/publications/scientific-journals/rio-corine
* http://www.sciencedirect.com/science/article/pii/S1352231008001829

## Layers
In:
* http://geo.irceline.be/rio/wms (`WMS` - pre-rendered maps)
* http://geo.irceline.be/rio/wfs (`WFS` - the data itself)

### Hourly mean (hmean)
These layers are interpolated by means of the RIO-interpolation, based on non-validated measurement data transmitted from the three regional networks.

These layers support the `TIME` attribute in the `GetMap` request of the `WMS`. See a detailed description of this specific implementation here:
http://docs.geoserver.org/latest/en/user/services/wms/time.html

The `WFS` does not support the `TIME` attribute. Use e.g `cql_filter` instead:
http://docs.geoserver.org/latest/user/services/wfs/vendor.html

You can filter for a specific location:
```xml
cql_filter=INTERSECTS(the_geom, POINT (161617 170644))
```
or combine with time (or any other attribute, see below):
```xml
cql_filter=timestamp='2016-02-15T08:00:00+01:00' AND INTERSECTS(the_geom, POINT (161617 170644))
```
Full example (you will have to change the timestamp - only the last 72 hours are available as hourly mean):
```html
http://geo.irceline.be/rio/ows?service=WFS&version=1.3.0&request=GetFeature&typeName=rio:no2_hmean&cql_filter=timestamp=%272016-02-14T07:00:00%27%20AND%20INTERSECTS%28the_geom,%20POINT%20%28161617%20170644%29%29
```
Note: you can only querry location with coordinates converted to [`EPSG:31370`](http://spatialreference.org/ref/epsg/belge-1972-belgian-lambert-72/)

The following layers are available (currently at a 4x4km resolution):

Coverage Belgium:
* rio:bc_hmean
* rio:bc_24hmean
* rio:bc_dmean
* rio:no2_hmean
* rio:no2_dmean
* rio:o3_hmean
* rio:o3_maxhmean
* rio:o3_8hmean
* rio:o3_max8hmean
* rio:pm10_hmean
* rio:pm10_24hmean
* rio:pm10_dmean
* rio:pm25_hmean
* rio:pm25_24hmean
* rio:pm25_dmean
* rio:so2_hmean

Attributes:

| Property  | type      | description                                            |
|:----------|:----------|:-------------------------------------------------------|
| id        | Integer   | fixed ID of a 4x4km grid cell of the RIO interpolation |
| timestamp | Timestamp | UTC (e.g. 2016-02-15T10:00:00Z)                        |
| value     | Double    | modeled concentration of a specific pollutant          |
| network   | String    | Monitoring network (Brussels, Flanders, Wallonia)      |
| the_geom  | Geometry  | Geometry of the RIO grid cell (polygon feature)        |

Coverage Flanders (clip):
* rio:no2_hmean_vl
* rio:o3_hmean_vl
* rio:pm10_hmean_vl
* rio:pm25_hmean_vl
* rio:so2_hmean_vl

Attributes:

| Property  | type      | description                                            |
|:----------|:----------|:-------------------------------------------------------|
| id        | Integer   | fixed ID of a 4x4km grid cell of the RIO interpolation |
| timestamp | Timestamp | UTC (e.g. 2016-02-15T10:00:00Z)                        |
| value     | Double    | modeled concentration of a specific pollutant          |
| the_geom  | Geometry  | Geometry of the RIO grid cell (polygon feature)        |

### Yearly mean (anmean)
These layers are interpolated by means of the RIO-interpolation, based on validated measurement data transmitted from the three regional networks.

The following layers are available (currently at a 4x4km resolution):

Coverage Belgium:
* rio:no2_anmean
* rio:o3_anmean
* rio:pm10_anmean
* rio:pm25_anmean

Attributes:

| Property    | type     | description                                                           |
|:------------|:---------|:----------------------------------------------------------------------|
| id          | Integer  | fixed ID of a 4x4km grid cell of the RIO interpolation                |
| year        | Integer  | starting with 1990, trough to current year - 1 (update around Easter) |
| rio_version | String   | version of the RIO model                                              |
| value       | Double   | modeled concentration of a specific pollutant                         |
| network     | String   | Monitoring network (Brussels, Flanders, Wallonia)                     |
| the_geom    | Geometry | Geometry of the RIO grid cell (polygon feature)                       |

Coverage network 'Flanders' (clip):
* rio:no2_anmean_vl
* rio:o3_anmean_vl
* rio:pm10_anmean_vl
* rio:pm25_anmean_vl
* rio:so2_anmean_vl

Attributes:

| Property    | type     | description                                                           |
|:------------|:---------|:----------------------------------------------------------------------|
| id          | Integer  | fixed ID of a 4x4km grid cell of the RIO interpolation                |
| year        | Integer  | starting with 1990, trough to current year - 1 (update around Easter) |
| rio_version | String   | version of the RIO model                                              |
| value       | Double   | modeled concentration of a specific pollutant                         |
| the_geom    | Geometry | Geometry of the RIO grid cell (polygon feature)                       |
