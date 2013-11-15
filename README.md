![ARC Logo](https://raw.github.com/AmericanRedCross/OSM_for_Garmin/master/img/arc-logo.png)

[OpenStreetMap on Garmin](http://wiki.openstreetmap.org/wiki/OSM_Map_On_Garmin)
=========================

- Garmin compatible files of [OpenStreetMap](http://www.openstreetmap.org/#map=6/12.276/125.255&layers=H) data for the Philippines are located in the PHL folders above
- The date of download is appended to the folder name
- The easiest way to install a map on your Garmin device is to put it in USB mass storage mode and copy the gmapsupp.img file to a directory called Garmin
- OSM data downloaded from [Geofabrik](http://download.geofabrik.de/)
- Processed using [Splitter](http://wiki.openstreetmap.org/wiki/Mkgmap/help/splitter) and [Mkgmap](http://wiki.openstreetmap.org/wiki/Mkgmap)

### Doing it yourself ###

**Note:** The method described here worked for GPSmap62, GPSmap60, Oregon400 and Dakota20. This is only the very basic workflow. The [OSM wiki](http://wiki.openstreetmap.org/wiki/OSM_Map_On_Garmin) goes into much greater detail on this and many other topics. With this workflow the ocean is not styled (coastlines are rendered but land and water have the same fill color); however, the OSM map only displays when zoomed so this shouldn’t be a huge issue (this can be fixed using mkgmap). 

- Install [Java Development Kit](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)
- Create a project folder on your computer (I named mine **osmToGarmin**)
- Download [splitter](http://www.mkgmap.org.uk/download/splitter.html) and unzip to the project folder
- Download [mkgmap](http://www.mkgmap.org.uk/download/mkgmap.html) and unzip to the project folder
- Download OSM data for area of interest from [Geofabrik](http://download.geofabrik.de/)
	- For the Philippines download **Philippines-latest.osm.pbf** from http://download.geofabrik.de/asia/philippines.html
	- Create a data folder in your project and name it using the date given by Geofabrik for the OSM data (in this example I named mine **PHL_2013-11-14**)
- Open Command Prompt ([How do I open command prompt?](http://pcsupport.about.com/od/commandlinereference/f/open-command-prompt.htm))
- Change directory to the splitter folder within the project folder  

```
cd Desktop\osmToGarmin\splitter-r311
```

- Run splitter on the file downloaded from Geofabrik

```
java -Xmx2000m -jar splitter.jar ..\PHL_2013-11-14\philippines-latest.osm.pbf --output-dir=..\PHL_2013-11-14
```

![image1](https://raw.github.com/AmericanRedCross/OSM_for_Garmin/master/img/osmtoGarmin01.png)

- Check your data folder (**PHL_2013-11-14** in this example), it should contain a series 
of files that begin with **6324** and have the file extension **.osm.pbf**

![image2](https://raw.github.com/AmericanRedCross/OSM_for_Garmin/master/img/osmtoGarmin02.png)

- Change directory to your data folder

```
cd ..\PHL_2013-11-14
```

- Run mkgmap to compile the files

```
java -jar ..\mkgmap-r2815\mkgmap.jar --gmapsupp 6324*.osm.pbf
```

![image3](https://raw.github.com/AmericanRedCross/OSM_for_Garmin/master/img/osmtoGarmin03.png)

- Connect your Garmin device and copy the **gmapsupp.img** file into the ‘Garmin’ folder on the Garmin’s internal memory 
	- Not the SD card if one is in the device
	- If no such folder exists, create it
