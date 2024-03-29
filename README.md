# EMODnetSBH-Guidance
Guidance for using the EMODnet Seabed Habitats web services

# EMODnet Seabed Habitats Web Mapping Services (WMS)
EMODnet Seabed Habitats provides an [OGC Web Mapping Service](http://www.opengeospatial.org/standards/wms) for viewing habitat information on  desktop GIS, web portal or other clients.

Due to the large volume of individual habitat survey maps and models, we have separate the OGC services into separate workspaces. 

The WMS for the main EMODnet Seabed Habitats' data products is: 
https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_view/wms 

This includes our main products including, but not limited to, EUSeaMap 2021, the OSPAR Threatened and Declining Habitats database, survey groundtruthing point data and our Essential Ocean Vairable composite products. 

The WMS for all individual habitat maps and models is:
https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_view_maplibrary/wms

## Loading WMS data in GIS clients 

The services can be accessed in your client by inputing the above addresses, though the method differs depending on the application.

For information on how to connect to a WMS in QGIS, visit [Working with WMS Data](https://www.qgistutorials.com/en/docs/working_with_wms.html "External Link: Adding WMS Layers via QGIS Tutorials (opens in new window)") on the QGIS Tutorial website.

For information on how to connect to a WMS in ArcMap, visit [Adding WMS services](http://help.arcgis.com/en/arcgisdesktop/10.0/help/index.html#//00sp0000000s000000.htm "External Link: Adding WMS services on the ArcGIS Resource Center (opens in new window)") on the ArcGIS Resource Center.

For information on how to connect to a WMS in MapInfo, visit [Adding a WMS Server in MapInfo Professional](http://reference.mapinfo.com/software/spectrum/lim/8_0/services/Spatial/source/Services/wms/configuration/addingawmsserver.html "External Link: Adding a WMS Server in MapInfo Professional in the MapInfo reference pages (opens in new window)") in the MapInfo reference pages.

## Filtering WMS layers
Key layers provided under WMS can be filtered (as on the portal) by adding specific parameters alongside the WMS GetMap requests. These parameters are not part of the core WMS standard but are provided as additional functionality.

The template for adding a parameter to a WMS request is in the form of **&*[Parameter]*=*[Value]***, where *[parameter]* is the name of the item being filtered and *[value]* is the filter value (not including square brackets).

Adding custom vendor paramters to WMS requests depends on the client/software being used, please refer to the documentation of your specifc software.

### &Hab_type=*[value]*
Filter layer to show only records containing the described EUNIS Habitat code(s), even as a habitat mosaic.

**Affects the following WMS layers:**

_EUNIS habitat maps from survey_

> eunisMaps_medium_200, eunisMaps_medium_50, eunisMaps_medium_full, habitat_boxes_eunis

> eunisMaps_fine_200, eunisMaps_fine_50, eunisMaps_fine_full, habitat_boxes_eunis 

> eunisMaps_broad_200, eunisMaps_broad_50, eunisMaps_broad_full, habitat_boxes_eunis 

**Values:** See Id codes from the official [EEA EUNIS habitats vocabulary](http://dd.eionet.europa.eu/vocabulary/biodiversity/eunishabitats/view).

**Notes on usage:**
* The code is passed through as a regex expression, as suchfilter selections will include all habitats described at a finer detail (i.e. child habitats).
* Separating habitats with a pipe character “|” will allow act as an OR statement. See example below.

**Examples:**
*	&Hab_type=A5.2
    *	This will show only polygons containing the habitat A5.2, including those described to a finer level (e.g. A5.23, A5.253)
*	&Hab_type=A3.1|A3.2
    *	This will show only polygons containing EITHER A3.1 OR A3.2

### &habtype=*[value]*
Filter layer to show only records describing the OSPAR Habitat, written as a shortened code.

**Affects the following WMS layers:** 

_OSPAR reference dataset_

> ospar2020_points, ospar2020_poly

**Values:**

| OSPAR Habitat |
| --- |
| Carbonate mounds |
| Coral gardens |
| Cymodocea meadows |
| Deep-sea sponge aggregations |
| Oceanic ridges with hydrothermal vents/fields |
| Intertidal mudflats |
| Intertidal Mytilus edulis beds on mixed and sandy sediments |
| Littoral chalk communities |
| Lophelia pertusa reefs |
| Maerl beds |
| Modiolus modiolus horse mussel beds |
| Ostrea edulis beds |
| Seamounts |
| Sea-pen and burrowing megafauna communities |
| Sabellaria spinulosa reefs |
| Zostera beds |

**Notes on usage:**
*	Separating habitats with a pipe character “|” will allow act as an OR statement. See example below.

**Examples:**
*	&habtype=Coral gardens
    *	This will filter the layer to show records of Coral gardens
*	&habtype=Coral gardens|Cymodocea meadows
    *	This will filter the layer to show records of Coral gardens and Cymodocea meadows

### &gui=*[value]*
Filter habitat maps from survey to only show specified datasets.

**Affects the following WMS layers:** 

_EUNIS habitat maps from survey_

> eunisMaps_medium_200, eunisMaps_medium_50, eunisMaps_medium_full, habitat_boxes_eunis 

> eunisMaps_fine_200, eunisMaps_fine_50, eunisMaps_fine_full, habitat_boxes_eunis 

> eunisMaps_broad_200, eunisMaps_broad_50, eunisMaps_broad_full, habitat_boxes_eunis 


_Other habitat maps from survey_

> otherMaps_medium_200, otherMaps_medium_50, otherMaps_medium_full, habitat_boxes_other

> otherMaps_fine_200, otherMaps_fine_50, otherMaps_fine_full, habitat_boxes_other

> otherMaps_broad_200, otherMaps_broad_50, otherMaps_broad_full, habitat_boxes_other

_Habitats directive habitat maps from survey_

> annexiMaps_full, annexiMaps_50, annexiMaps_200, habitat_boxes_n2000


**Values:** “GUI” dataset identifiers, these can be identified by querying a habitat map in the [interactive map](https://emodnet.ec.europa.eu/geoviewer/), or through the [metadata search page](http://gis.ices.dk/geonetwork/srv/eng/catalog.search#/search).

**Notes on usage:**
*	The code is passed through as a regex expression, as such filters will allow partial matches, this can be useful to view all maps from a specific country as in the example below
*	Separating habitats with a pipe character “|” will allow act as an OR statement. See example below.

**Examples:**
*	&gui=GB000217
    *	This will show only the map [“Phase I intertidal survey for Wales”](http://gis.ices.dk/geonetwork/srv/eng/catalog.search#/metadata/3d7055e6-2c8b-4efc-99f8-e4038965bcda) (Note, as this map is a EUNIS map – nothing will be shown when viewing either Habitats Directive or “Other” habitat maps from survey).
*	&gui=IT
    *	This will show only maps submitted by Italian organisations
*	&gui=ES|GR
    *	This will show only maps submitted by either Spanish or Greek organisations

# EMODnet Seabed Habitats Web Feature Services (WFS)
For machine-to-machine access to true spatial vector data, EMODnet Seabed Habitats provides an [OGC Web Feature Service](http://www.opengeospatial.org/standards/wfs) for compatible layers.

As with the WMS workspaces, separate workspaces are provided for the WFS data.

The WFS for the main EMODnet Seabed Habitats' data products is: 
https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_view/wfs? 

This includes our main products including, but not limited to, EUSeaMap 2021, the OSPAR Threatened and Declining Habitats database, survey groundtruthing point data and our Essential Ocean Vairable composite products. 

The WFS for all individual habitat maps is:
https://ows.emodnet-seabedhabitats.eu/geoserver/emodnet_view_maplibrary/wfs?

Please note, that this workspace is habitat maps in vector format only. 

It should be noted that WFS is not the most efficient form of delivery for complex datasets, (e.g. EUSeaMap 2021), due to the size of the downloads involved. These datasets are also available to download as static download packages accessible from the layer information on the EMODnet central viewer [EMODnet viewer](https://emodnet.ec.europa.eu/geoviewer/) or the dataset metadata records.

**Notes on usage:**
* Note that depending on a layer's complexity, it may take some time to load into your GIS or may time out. In the event of consistent time-outs, please download the corresponding static package.
