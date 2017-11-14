# EMODnetSBH-Guidance
Guidance for using the EMODnet Seabed Habitats web services

# EMODnet Seabed Habitats Web Mapping Services (WMS)
EMODnet Seabed Habitats provides an [OGC Web Mapping Service](http://www.opengeospatial.org/standards/wms) for viewing habitat information on  desktop GIS, web portal or other clients.

The feed is provided in two forms, a full verbose and hierarchical structure available at:
http://213.122.160.75/scripts/mapserv.exe?map=D:/Websites/MESHAtlantic/map/MESHAtlanticWMS.map

and a simplified structure (for simple clients and quick web interfaces) at:
http://213.122.160.75/scripts/mapserv.exe?map=D:/Websites/MESHAtlantic/map/MESHAtlantic.map

Both services provide the same data.

The services can be accessed in your client by inputing the above addresses, though the method differs depending on the application.

For information on how to connect to a WMS in QGIS, visit [Adding WMS Layers](http://maps.cga.harvard.edu/qgis/wkshop/wms.php "External Link: Adding WMS Layers on the Harvard University QGIS 2.0 workshop (opens in new window)") on the Harvard University QGIS 2.0 workshop.

For information on how to connect to a WMS in ArcMap, visit [Adding WMS services](http://help.arcgis.com/en/arcgisdesktop/10.0/help/index.html#//00sp0000000s000000.htm "External Link: Adding WMS services on the ArcGIS Resource Center (opens in new window)") on the ArcGIS Resource Center.

For information on how to connect to a WMS in MapInfo, visit [Adding a WMS Server in MapInfo Professional](http://reference.mapinfo.com/software/spectrum/lim/8_0/services/Spatial/source/Services/wms/configuration/addingawmsserver.html "External Link: Adding a WMS Server in MapInfo Professional in the MapInfo reference pages (opens in new window)") in the MapInfo reference pages.

## Filtering WMS layers
Key layers provided under WMS can be filtered (as on the portal) by adding specific parameters alongside the WMS GetMap requests. These parameters are not part of the core WMS standard but are provided as additional functionality.

The template for adding a parameter to a WMS request is in the form of **&*[Parameter]*=*[Value]***, where *[parameter]* is the name of the item being filtered and *[value]* is the filter value (not including square brackets).

Adding custom vendor paramters to WMS requests depends on the client/software being used, please refer to the documentation of your specifc software.

### &HabCode=*[value]*
Filter layer to show only records containing the described EUNIS Habitat code(s), even as a habitat mosaic.


**Affects the following WMS layers:**

_EUSeaMap2016_

EUSM2016_simplified800, EUSM2016_simplified400, EUSM2016_simplified200, EUSM2016_detailed

_EUNIS habitat maps from survey_

EUNISmedium_100, EUNISmedium_FULL, EUNISmedium_SA, EUNISmedium_SAx
EUNISfine50, EUNISfineFULL, EUNISfineSA, EUNISfineSAx
EUNISbroad_100, EUNISbroad_Full, EUNISbroad_SA, EUNISbroad_SAx

**Values:** See Id codes from the official [EEA EUNIS habitats vocabulary](http://dd.eionet.europa.eu/vocabulary/biodiversity/eunishabitats/view).

**Notes on usage:**
* The code is passed through as a regex expression, as suchfilter selections will include all habitats described at a finer detail (i.e. child habitats).
* Separating habitats with a pipe character “|” will allow act as an OR statement. See example below.
*	Filtering on the “EUNIS[ ]_SA” or “EUNIS[ ]_SAx” layers will show bounding boxes only for EUNIS maps containing the selected habitats.

**Examples:**
*	&HabCode=A5.2
    *	This will show only polygons containing the habitat A5.2, including those described to a finer level (e.g. A5.23, A5.253)
*	&HabCode=A3.1|A3.2
    *	This will show only polygons containing EITHER A3.1 OR A3.2

### &OSPCode=*[value]*
Filter layer to show only records describing the OSPAR Habitat, written as a shortened code.

**Affects the following WMS layers:** 

_OSPAR reference dataset_

OSPARHabPoints, OSPARhabPolygons, OSPARhabPolygonLoc

**Values:**

| Code | OSPAR Habitat |
| ---- | ------------- |
| carbmoun | Carbonate mounds |
| coragard | Coral gardens |
| cymomead | Cymodocea meadows |
| deepspag | Deep-sea sponge aggregations |
| ocearidg | Oceanic ridges with hydrothermal vents/fields |
| lophpert | Lophelia pertusa reefs |
| ostredul | Ostrea edulis beds |
| seamount | Seamounts |
| seapenbm | Sea-pen and burrowing megafauna communities |
| zosterab | Zostera beds |
| intermud | Intertidal mudflats |
| litchalk | Littoral chalk communities |
| maerlbed | Maerl beds |
| modimodi | Modiolus modiolus horse mussel beds |
| sabspinu | Sabellaria spinulosa reefs |
| intermyt | Intertidal Mytilus edulis beds on mixed and sandy sediments |

**Notes on usage:**
*	The code is passed through as a regex expression, as such, you may shorten the codes further.
*	Separating habitats with a pipe character “|” will allow act as an OR statement. See example below.
*	Filtering on the layer “OSPARhabPolygonLoc” will show ICES squares containing the selected habitat.

**Examples:**
*	&OSPCode =zosterab
    *	This will filter the layer to show records of Zostera beds
*	&OSPCode =deepspag|coragard
    *	This will filter the layer to show records of Deep-sea sponge aggregations and Coral gardens

### &GUICode=*[value]*
Filter habitat maps from survey to only show specified datasets.

**Affects the following WMS layers:** 

_EUNIS habitat maps from survey_

EUNISmedium_100, EUNISmedium_FULL, EUNISmedium_SA, EUNISmedium_SAx

EUNISfine50, EUNISfineFULL, EUNISfineSA, EUNISfineSAx

EUNISbroad_100, EUNISbroad_Full, EUNISbroad_SA, EUNISbroad_Sax


_Other habitat maps from survey_

Othermedium_100, Othermedium_FULL, Othermedium_SA, Othermedium_SAx

Otherfine50, OtherfineFULL, OtherfineSA, OtherfineSAx

_Habitats directive habitat maps from survey_

N2000_100, N2000_Full, N2000_SA, N2000_SAx


**Values:** “GUI” dataset identifiers, these can be identified by querying a habitat map in the [interactive map](http://www.emodnet-seabedhabitats.eu/map), or through the [metadata search page](http://www.emodnet-seabedhabitats.eu/search).

**Notes on usage:**
*	The code is passed through as a regex expression, as such filters will allow partial matches, this can be useful to view all maps from a specific country as in the example below
*	Separating habitats with a pipe character “|” will allow act as an OR statement. See example below.

**Examples:**
*	&GUICode=GB000217
    *	This will show only the map [“Phase I intertidal survey for Wales”](http://gis.ices.dk/geonetwork/srv/eng/catalog.search#/metadata/3d7055e6-2c8b-4efc-99f8-e4038965bcda) (Note, as this map is a EUNIS map – nothing will be shown when viewing either Habitats Directive or “Other” habitat maps from survey).
*	&GUICode=IT
    *	This will show only maps submitted by Italian organisations
*	&GUICode=ES|GR
    *	This will show only maps submitted by either Spanish or Greek organisations

# EMODnet Seabed Habitats Web Feature Services (WFS)
For machine-to-machine access to true spatial data, EMODnet Seabed Habitats provides an [OGC Web Feature Service](http://www.opengeospatial.org/standards/wfs) for compatible layers.

The service can be accessed via:
http://213.122.160.75/scripts/mapserv.exe?map=D:/Websites/MESHAtlantic/map/EMODnetWFS.map&version=1.1.0


**Currently the layers available through this service are as follows:**

_OSPAR reference dataset_

OSPARHabPoints, OSPARhabPolygons

More layers are added as the possibility arises. However, WFS is not the most efficient form of delivery for complex datasets, such as the habitat maps from survey datasets and EUSeaMap, due to the size of the downloads involved. These datasets are available to download as static download packages from the [EMODnet Seabed Habitats download page](http://www.emodnet-seabedhabitats.eu/download).

Delivery of layers as WFS is constantly reviewed and layers will be made available if this option becomes possible
