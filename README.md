# solarpc
potree visualization of a pointcloud of solar panels in Corvallis, OR

## Repository Folder Structure
```
|-- solarpc
    |-- README.md
    |-- index.html
    |-- lasmap_index.html
    |-- libs
        |-- potree
```

## Pointcloud Generation
Data was acquired with a DJI Inspire 2, and processed with Agisoft Photoscan using "High" accuracy and "High" dense reconstruction.  The data was referenced using the DJI Inspire internal GNSS (WGS84).  The ~80 million points were exported in UTM Zone 10N and the las file format.

## potree processing
The data were processed using PoTreeConverter 1.6, and the following batch script.

```cmd
SET POTREE=".\PotreeConverter_1.6_windows_x64\PotreeConverter.exe"
SET LASFILE="dense_high.las"
SET DIRNAME="\potree"
SET HTMLNAME="index"

%POTREE% %LASFILE% -o %DIRNAME% -p %HTMLNAME% --projection "+proj=utm +zone=10 +ellps=GRS80 +datum=NAD83 +units=m +no_defs" --overwrite
```

## Modifications to index.html
This pointcloud is way too large to host on github.  The data is therefore hosted on the engineering server `http://research.engr.oregonstate.edu/lidar/pointcloud/`, and referenced from the index.html file.

Additionally, the Apache `.htaccess` file was modified to contain:
```
CheckSpelling Off
Header set Access-Control-Allow-Origin "*"
```
This fixed the `Access-Control-Allow-Origin` Error.  

The libraries, except for potree, are also hosted on the external web server.  The potree library only appeared to work when it was hosted on the same server.


