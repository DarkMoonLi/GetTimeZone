# GetTimeZone

A modified version of the GetTimeZone library for the OSM service.

## Requirements
GEOS PHP extension is needed to run library. So, you should download and compile it running the script bin/compile-geos
.sh; then, the library called "geos.so" will be added to /usr/lib/php.
As you can see, this script contains the installation of some php extensions that will be necessary in the next
step of the installation process.

Once you have compiled the GEOS PHP extension, you should create the file geos.ini in order to enable the module and improve the performance consequently.

Finally, you should run the composer file, so the rest of necessary libraries will be installed.


## Usage
There are two main classes:

* UpdaterData: script that downloads the last version of the timezone boundaries data and creates the tree of directories (data.zip). It takes a few hours, so you can use "data.zip" from node-geo-tz to test for the first time. Otherwise, you can run the UpdaterData script in order to get the last version and create the directories tree. Destination folder must have write permisions

```php
    use GeoTimeZone\UpdaterData;

    $updater = new UpdaterData("/path/to/data/");
    $updater->updateData();
```

* Calculator: provides the timezone name or the local date associated to a particular latitude, longitude and timestamp.
```php
    use GeoTimeZone\Calculator;

    $latitude = 39.452800;
    $longitude = -0.347038;
    $timestamp = 1469387760;

    $calculator = new Calculator("/path/to/data/");

    // Local date
    $localDate = $calculator->getLocalDate($latitude, $longitude, $timestamp);
    /* DateTime Object
    (
        [date] => 2016-07-24 21:16:00.000000
        [timezone_type] => 3
        [timezone] => Europe/Madrid
    )
    */

    // TimeZone name
    $timeZoneName = $calculator->getTimeZoneName($latitude, $longitude);
    //Europe/Madrid
```
