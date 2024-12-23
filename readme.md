# Open (geo)data IRCEL-CELINE
License: https://creativecommons.org/licenses/by/4.0/

Also see: https://www.irceline.be/en/documentation/open-data

## Catalog Service for the Web (`CSW`)
Metadata is hosted via:
* https://geo.irceline.be/csw

Documentation specific CSW implementation:
* https://geonetwork-opensource.org/manuals/trunk/eng/users/index.html

General documentation of the OGC standard for `CSW`:
* https://www.opengeospatial.org/standards/cat

## Web Map Service (`WMS`) - viewing service
A WMS serves geo-registered map images

Our end-point:
* https://geo.irceline.be/wms

See `GetCapabilities`:
* https://geo.irceline.be/wms?service=wms&version=1.3.0&request=GetCapabilities (slow due to large amount of layers)
Better request metadata per workspace:
* https://geo.irceline.be/realtime/wms?service=wms&version=1.3.0&request=GetCapabilities
* https://geo.irceline.be/rio/wms?service=wms&version=1.3.0&request=GetCapabilities
* https://geo.irceline.be/annual/wms?service=wms&version=1.3.0&request=GetCapabilities
* https://geo.irceline.be/rioifdm/wms?service=wms&version=1.3.0&request=GetCapabilities

Or even per layer:
* https://geo.irceline.be/realtime/no2_hmean_station/wms?service=wms&version=1.3.0&request=GetCapabilities
* https://geo.irceline.be/rio/no2_hmean/wms?service=wms&version=1.3.0&request=GetCapabilities
* https://geo.irceline.be/annual/no2_anmean/wms?service=wms&version=1.3.0&request=GetCapabilities
* https://geo.irceline.be/rioifdm/no2_anmean_2018_atmostreet/wms?service=wms&version=1.3.0&request=GetCapabilities

The following workspaces serve a subsection of the data:

1. https://geo.irceline.be/rio/wms
    - interpolated maps of RIO 4x4km
    - Coverage Belgium and per region
    - see further [details here](datasets/rio.md)

2. https://geo.irceline.be/realtime/wms
    - real time measurement data per station
    - selection possible via time parameter
    - see further [details here](datasets/measurements.md)

3. https://geo.irceline.be/annual/wms
    - aggregated measurement data per station
    
4. https://geo.irceline.be/rioifdm/wms
    - maps of RIO-IFDM and ATMO-Street
    - Coverage Belgium and per region

### Encodings
Available encodings (see [format](https://docs.geoserver.org/latest/en/user/services/wms/outputformats.html#wms-output-formats) parameter):
* png
* png8
* jpeg
* tiff
* kml
* ...

See full list in, e.g.: [GetCapabilities](https://geo.irceline.be/rio/wms?service=wms&version=1.3.0&request=GetCapabilities) under `<GetMap>` `<Format>`

### Projections
Available projections (see [srs](https://docs.geoserver.org/latest/en/user/services/wms/reference.html#wms-getmap) parameter):
* EPSG:31370
* EPSG:4258
* EPSG:4326
* EPSG:900913

### Documentation WMS
Documentation interacting with the specific WMS implementation:
* https://docs.geoserver.org/latest/en/user/services/wms/reference.html

General documentation of the OGC standard for `WMS`:
* https://www.opengeospatial.org/standards/wms

## Web Feature Service (`WFS`) - download service
A WFS serves vector format geographical data.

Our end-point:
* https://geo.irceline.be/wfs

See `GetCapabilities`:
https://geo.irceline.be/wfs?service=wfs&version=2.0.0&request=GetCapabilities

### Encodings
Available encodings (see [output formats](https://docs.geoserver.org/latest/en/user/services/wfs/outputformats.html) parameter):
* gml (`outputFormat=GML2` or `outputFormat=GML3`)
* json (`outputFormat=application/json`)
* csv (`outputFormat=csv`)
* shp (`outputFormat=shape-zip`)
* jsonp (`outputFormat=text/javascript`)

See full list in [GetCapabilities](https://geo.irceline.be/wfs?service=wfs&version=2.0.0&request=GetCapabilities) under `<ows:Parameter name="outputFormat">`

### Projections
Most commonly used projections are supported (cf [EPSG](httpss://www.epsg-registry.org/))

### Documentation WFS
Documentation specific `WFS` implementation:
* https://docs.geoserver.org/latest/en/user/services/wfs/reference.html

General documentation of the OGC standard for `WFS`:
* https://www.opengeospatial.org/standards/wfs

## Web Coverage Service (`WCS`) - download service
A WCS serves raster format geographical data.

Our end-point:
* https://geo.irceline.be/wcs

See `GetCapabilities`:
https://geo.irceline.be/wcs?service=WCS&version=2.0.1&request=GetCapabilities

Use `DescribeCoverage` to get a full description of the coverages by layer:
https://geo.irceline.be/wcs?service=WCS&version=2.0.1&request=DescribeCoverage&coverageid=rioifdm:no2_anmean_2017_atmostreet

Size for output download is limited to 50Mb. 

### Documentation WCS
Documentation specific `WCS` implementation:
* https://docs.geoserver.org/latest/en/user/services/wcs/index.html

General documentation of the OGC standard for `WCS`:
* https://www.ogc.org/standard/wcs/


## Sensor Observation Service (SOS) - download service
A SOS serves sensor data (time series, metadata of stations and measuring devices) collected at a specific geographical location.

Our end-point:
* https://geo.irceline.be/sos

Browse data via the following clients:
* https://geo.irceline.be/sos/static/client/jsClient/#map

### SOAP
Client:
https://geo.irceline.be/sos/client

Documentation specific `SOS` implementation:
https://wiki.52north.org/bin/view/SensorWeb/SensorObservationServiceIVDocumentation

SOS adapted for e-reporting under the Air Quality Directive:
https://wiki.52north.org/bin/view/SensorWeb/AqdEReporting

General documentation of the OGC standard for SOS:
* https://www.opengeospatial.org/standards/sos

### REST-api
* https://geo.irceline.be/sos/api/v1/

Documentation:
* https://geo.irceline.be/sos/static/doc/api-doc/

## Bulk downloads
RIO: http://ftp.irceline.be/rio4x4/

[RIO-IFDM](https://www.irceline.be/en/documentation/models/rio-ifdm): http://ftp.irceline.be/rioifdm

[ATMO-Street](https://www.irceline.be/nl/documentatie/modellen/rio-ifdm-ospm): http://ftp.irceline.be/atmostreet

## Legends
See: https://github.com/irceline/map_legends

## Abbreviations
A list of abbreviations used in het layer names:

| Abbreviation | Description                                                                                   |
|:-------------|:----------------------------------------------------------------------------------------------|
| bc           | Black Carbon (BC)                                                                             |
| no2          | Nitrogen dioxide (NO<sub>2</sub>)                                                             |
| o3           | Ozone (O<sub>3</sub>)                                                                         |
| pm10         | Particulate Matter < 10 µm (PM<sub>10</sub>)                                                  |
| pm25         | Particulate Matter < 2.5 µm (PM<sub>2.5</sub>)                                                |
| so2          | Sulphur dioxide (SO<sub>2</sub>)                                                              |
| belaqi       | the Belgian Air Quality Index                                                                 |
| hmean        | hourly mean (timstamp = end-time of hour)                                                     |
| 24hmean      | Running 24-hour mean (timstamp = end-time of 24 hour period)                                  |
| 8hmean       | Running 8-hour mean (timstamp = end-time of 8 hour period)                                    |
| maxhmean     | Daily (01h00 to 24h00) maximum hmean (timstamp = 01h00 of the running day)                    |
| max8hmean    | Daily (01h00 to 24h00) maximum 8hmean (timstamp = 01h00 of the running day)                   |
| dmean        | Daily mean concentration (hmean 01h00 to 24h00 - timstamp = 01h00 of the following day)       |
| anmean       | Annual mean concentration (calendar year)                                                     |
| rio          | RIO interpolation - see [rio datasets](datasets/rio.md)                                       |
| station      | data measured in a monitoring station - see [measurements datasets](datasets/measurements.md) |
| vl           | the network "Flanders"                                                                        |
| wl           | the network "Wallonia"                                                                        |
| br           | the network "Brussels"                                                                        |
