Gravimetric Soil Water Content
==============================

Draft version 2014-03-27: DWS created, please fix and add to.

Overview
--------

We are primarily using this method to measure soil water content at our microclimate stations (the iButton temperature sensors) throughout the Chisos, Davis and Guadalupe Mountains.  See the climate project: https://github.com/schwilklab/skyisland-climate


Soil collection
---------------

### Materials Needed ###


- Quart ziploc bags (2X number of samples).  Use only freezer/heavy duty ziplocs, and only those with a  double zip, not those with the little tab.
- Gallon bags to organize smaller bags by trail.

### Trip preparation ###

These steps are specific to the Sky Island microclimate measurement project.

1. Upload all sensors to the GPS units you are taking
    - TODO: link to instructions on scripts for making an upload file from the sensor master list and instructions on using gpsbabel
2. Create and print a list of sensors for the range you are headed to.  Note that some sensors in the master list are marked as "Gone"  These do not exist! leave them off the GPS and your printed list.
3. Make sure you have permits in order for the National Parks.

### Collection steps ###

1. Walk to each GPS waypoint. They are all close to trails for access purposes,
so this is mostly just trail hiking. There should be a temperature sensor there.
The sensor is an iButton hanging inside two nested white funnels hanging from a
tree at about 1.75 m height.  The funnels will say "Schwilk" lab and the sensor
id (eg PI 512), but this is often worn off, so you must go by the list.  The
letters indicate which trail/road the sensor is one for keeping track.  I'll
list the codes below.  If the sensor can not be located, make a note but still
collect soil from that waypoint. There are sometimes two sensors at each
location, one temperature and one humidity.  You only need to get one soil
sample and name it the same name as the temperature sensor.

2. The soil is to be collected from within 3m of the sensor. Collect from 2-3
separate holes randomly selected within that radius, but the soil is all mixed
and only one ziploc from each location is collected. Scrape loose litter from
surface. Dig a hole (I use a sharpshooter shovel). The aim is to collect soil
from 10-15cm depth.  Sometimes that is difficult with shallow soil, so averaging
5cm to 15cm is acceptable.  Avoid large stones, etc, to cut down on volume and
weight but we will sift in the lab.

3. Put the collections from the 2-3 holes in a heavy duty quart ziploc. We want
about 1/2 of a quart bag of soil per location. Double (or even triple)
bag each bag, write with sharpie the date and the sensor id.  We cannot have
punctures/tears, it must be airtight.  It is *very important* that the bags are undamaged and airtight.

4. As soon as reasonable, put the ziplocs in a a cooler with ice or a fridge. I
usually organize the sensor locations with the same prefix (Same trail) together
in a large ziploc.

5. Return bags to Schwilk lab (or ship bag to Schwilk lab at TTU).

6. Organize all bags into a box and place in the 4C fridge.  Label the box with the date and mountain range.



Soil prep and weighing
----------------------

### Materials and equipment ###

- Sieve
- ziplocs
- metal weigh boats
- analytical balance
- drying oven
- cookie sheets for placing weigh boats on
- Data entry sheet

1. Prepare the data entry sheet TODO

Example:

| Sample ID | boat   | boat.soil.wet | boat.soil.dry |
| --------- | ------ | ------------- | ------------- |
| PT512     | 1.3148 | 29.8701       | 27.2839       |


2. Go through each bag and sift soil into a new ziploc.  Use the XX mm sieve TODO
3. Weigh a weighboat and record
4. fill a weighboat with soil, weigh and record.
5. Place weighboat on cookie sheet for transfer to the drying oven
6. Repeat steps 2-5 for each bag
7. Dry all soil 48 hours
8. Remove and weigh each sample, and record weight.

Gravimetric Soil Water Content Calculation
------------------------------------------

GSWC = ( ( boat.soil.wet - boat) - (boat.soil.dry - boat)  /  (boat.soil.dry - boat) )

Or, if wet.wt =  boat.soil.wet - boat and dry.wt = boat.soil.dry - boat then just

GSWC = (wet.wt - dry.wt) / dry.wt

