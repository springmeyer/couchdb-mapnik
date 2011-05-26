# CouchDB & Mapnik


## Requirements

 * Couchdb - I tested with CouchDBI Version 1.0.2.0.
 
 * GDAL trunk (>= 1.9.0) with couch support (http://www.gdal.org/ogr/drv_couchdb.html)

 * Mapnik trunk (>= 2.0.0) with GDAL/OGR plugin
 
 * nik2img.py (just to render via commandline)


## Usage

Create a couch document for a given shapefile:

    ogr2ogr -lco UPDATE_PERMISSIONS=ALL -f couchdb couchdb:http://127.0.0.1:5984 world_merc.shp


Then query the document to make sure the geojson is in there:

    ogrinfo couchdb:http://127.0.0.1:5984/ -so -al world_merc

You should get:

```
$ ogrinfo couchdb:http://127.0.0.1:5984/ -so -al world_merc
INFO: Open of `couchdb:http://127.0.0.1:5984/'
      using driver `CouchDB' successful.

Layer name: world_merc
Geometry: Polygon
Feature Count: 245
Extent: (-20037508.342789, -8283343.693883) - (20037508.342789, 18365151.363070)
Layer SRS WKT:
PROJCS["Google Maps Global Mercator",
    GEOGCS["GCS_WGS_1984",
        DATUM["WGS_1984",
            SPHEROID["WGS_84",6378137,298.257223563]],
        PRIMEM["Greenwich",0],
        UNIT["Degree",0.017453292519943295]],
    PROJECTION["Mercator_2SP"],
    PARAMETER["standard_parallel_1",0],
    PARAMETER["latitude_of_origin",0],
    PARAMETER["central_meridian",0],
    PARAMETER["false_easting",0],
    PARAMETER["false_northing",0],
    UNIT["Meter",1]]
_id: String (0.0)
_rev: String (0.0)
FIPS: String (0.0)
ISO2: String (0.0)
ISO3: String (0.0)
UN: Integer (0.0)
NAME: String (0.0)
AREA: Integer (0.0)
POP2005: Integer (0.0)
REGION: Integer (0.0)
SUBREGION: Integer (0.0)
LON: Real (0.0)
LAT: Real (0.0)
```

Then try rendering with nik2img:

    # install first
    sudo easy_install nik2img
    
    # then render
    nik2img.py couchmap.xml world.png
