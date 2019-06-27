# In-situ measurements
## Hourly means (non-validated realtime)
### `WMS` or `WFS`:
* realtime:bc_hmean_station
* realtime:bc_24hmean_station
* realtime:bc_dmean_station
* realtime:no2_hmean_station
* realtime:no2_dmean_station
* realtime:o3_hmean_station
* realtime:o3_maxhmean_station
* realtime:o3_8hmean_station
* realtime:o3_max8hmean_station
* realtime:pm10_hmean_station
* realtime:pm10_24hmean_station
* realtime:pm10_dmean_station
* realtime:pm25_hmean_station
* realtime:pm25_24hmean_station
* realtime:pm25_dmean_station
* realtime:so2_hmean_station

See [list of abbreviations](../readme.md#abbreviations)

Attributes:

| Property    | type       | description                                                                                   |
|:------------|:-----------|:----------------------------------------------------------------------------------------------|
| ab_eoi_code | String     | station code as reported under the [Air Quality Directive](http://aqportal.eionet.europa.eu/) |
| ab_name     | String     | station code used within Belgian measuring networks                                           |
| timestamp   | Timestamp  | UTC (e.g. 2016-02-15T10:00:00Z)                                                               |
| device_id   | Integer    | id to link to metadata of the measuring device used                                           |
| value       | BigDecimal | measured concentration of a specific pollutant                                                |
| network     | String     | Monitoring network (Brussels, Flanders, Wallonia)                                             |
| the_geom    | Geometry   | Geometry of the measuring station (point feature)                                             |

These layers support the `TIME` attribute in the `GetMap` request of the `WMS`. See a detailed description of this specific implementation here:
http://docs.geoserver.org/latest/en/user/services/wms/time.html

The `WFS` does not support the `TIME` attribute. Use e.g `cql_filter` instead:
http://docs.geoserver.org/latest/user/services/wfs/vendor.html

You can filter for a specific location:
```xml
cql_filter=INTERSECTS(the_geom, POLYGON (105720 199791, 117923 199620, 118588 189014, 106005 188481, 105720 199791))
```
or combine with time (or any other attribute, see below):
```xml
cql_filter=timestamp='2016-02-15T08:00:00+01:00' AND INTERSECTS(the_geom, POLYGON (105720 199791, 117923 199620, 118588 189014, 106005 188481, 105720 199791))
```
Full example (you will have to change the timestamp - only the last 48 hours are available as hourly mean):
```html
http://geo.irceline.be/realtime/ows?service=WFS&version=1.3.0&request=GetFeature&typeName=realtime:no2_hmean_station&cql_filter=timestamp=%272016-02-17T07:00:00%27%20AND%20WITHIN%28the_geom,%20POLYGON%20%28%28105720%20199791,%20117923%20199620,%20118588%20189014,%20106005%20188481,%20105720%20199791%29%29%29
```
Note: you can only query location with coordinates converted to [`EPSG:31370`](http://spatialreference.org/ref/epsg/belge-1972-belgian-lambert-72/)

### `SOS`
timeseries per measuring station

#### SOAP-endpoint:
http://geo.irceline.be/sos/client

General documentation of the OGC standard for SOS: http://www.opengeospatial.org/standards/sos

Documentation specific `SOS` implementation:
https://wiki.52north.org/bin/view/SensorWeb/SensorObservationServiceIVDocumentation

#### REST-api:

* http://geo.irceline.be/sos/api/v1/

Documentation:
* http://geo.irceline.be/sos/static/doc/api-doc/

To explore the data here:
* http://geo.irceline.be/sos/static/client/jsClient/
You can also download `CSV` after selecting a specific time series in the map view tab and clicking on the info-icon (legend panel) in the diagram view tab.

## Annual means (validated)
### `WMS` or `WFS`:
* annual:no2_anmean_station
* annual:o3_anmean_station
* annual:pm10_anmean_station
* annual:pm25_anmean_station
* annual:so2_anmean_station

## Hourly means (validated)
As reported to the European Commission:
* http://cdr.eionet.europa.eu/be/eu/aqd/e1a/
