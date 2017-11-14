# EMODnetSBH-Guidance
Guidance for using the EMODnet Seabed Habitats web services

# EMODnet Seabed Habitats Web Mapping Services

## Filtering WMS layers

### “HabCode”
Filter layer to show only records containing the described EUNIS Habitat code(s), even as a habitat mosaic.

Affects the following WMS layers: 
EUSeaMap2016
EUSM2016_simplified800, EUSM2016_simplified400, EUSM2016_simplified200, EUSM2016_detailed

EUNIS habitat maps from survey
EUNISmedium_100, EUNISmedium_FULL, EUNISmedium_SA, EUNISmedium_SAx
EUNISfine50, EUNISfineFULL, EUNISfineSA, EUNISfineSAx
EUNISbroad_100, EUNISbroad_Full, EUNISbroad_SA, EUNISbroad_SAx

Values: See Id codes from the official EEA EUNIS habitats vocabulary.

Notes on usage:
•	The code is passed through as a regex expression, as suchfilter selections will include all habitats described at a finer detail (i.e. child habitats).
•	Separating habitats with a pipe character “|” will allow act as an OR statement. See example below.
•	Filtering on the “EUNIS[ ]_SA” or “EUNIS[ ]_SAx” layers will show bounding boxes only for EUNIS maps containing the selected habitats.

Examples:
•	&HabCode=A5.2
o	This will show only polygons containing the habitat A5.2, including those described to a finer level (e.g. A5.23, A5.253)
•	&HabCode=A3.1|A3.2
o	This will show only polygons containing EITHER A3.1 OR A3.2

### “OSPCode”
Filter layer to show only records describing the OSPAR Habitat, written as a shortened code.

Affects the following WMS layers: 
OSPAR reference dataset
OSPARHabPoints, OSPARhabPolygons, OSPARhabPolygonLoc

Notes on usage:
•	The code is passed through as a regex expression, as such, you may shorten the codes further.
•	Separating habitats with a pipe character “|” will allow act as an OR statement. See example below.
•	Filtering on the layer “OSPARhabPolygonLoc” will show ICES squares containing the selected habitat.

Values:
Code	OSPAR Habitat
carbmoun	Carbonate mounds
coragard	Coral gardens
cymomead	Cymodocea meadows
deepspag	Deep-sea sponge aggregations
ocearidg	Oceanic ridges with hydrothermal vents/fields
lophpert	Lophelia pertusa reefs
ostredul	Ostrea edulis beds
seamount	Seamounts
seapenbm	Sea-pen and burrowing megafauna communities
zosterab	Zostera beds
intermud	Intertidal mudflats
litchalk	Littoral chalk communities
maerlbed	Maerl beds
modimodi	Modiolus modiolus horse mussel beds
sabspinu	Sabellaria spinulosa reefs
intermyt	Intertidal Mytilus edulis beds on mixed and sandy sediments


Examples:
•	&OSPCode =zosterab
o	This will filter the layer to show records of Zostera beds
•	&OSPCode =deepspag|coragard
o	This will filter the layer to show records of Deep-sea sponge aggregations and Coral gardens

“GUICode”
Filter habitat maps from survey to only show specified datasets.

Affects the following WMS layers: 
EUNIS habitat maps from survey
EUNISmedium_100, EUNISmedium_FULL, EUNISmedium_SA, EUNISmedium_SAx
EUNISfine50, EUNISfineFULL, EUNISfineSA, EUNISfineSAx
EUNISbroad_100, EUNISbroad_Full, EUNISbroad_SA, EUNISbroad_Sax

Other habitat maps from survey
Othermedium_100, Othermedium_FULL, Othermedium_SA, Othermedium_SAx
Otherfine50, OtherfineFULL, OtherfineSA, OtherfineSAx

Habitats directive habitat maps from survey
EUNISmedium_100, EUNISmedium_FULL, EUNISmedium_SA, EUNISmedium_SAx

Values: “GUI” dataset identifiers, these can be identified by querying a habitat map in the portal, or through the metadata search.

Notes on usage:
•	The code is passed through as a regex expression, as such filters will allow partial matches, this can be useful to view all maps from a specific country as in the example below
•	Separating habitats with a pipe character “|” will allow act as an OR statement. See example below.

Examples:
•	&GUICode=GB000217
o	This will show only the map “” (Note, as this map is a EUNIS map – nothing will be shown when viewing either Habitats Directive or “Other” habitat maps from survey).
•	&GUICode=IT
o	This will show only maps submitted by Italian organisations
•	&GUICode=ES|GR
o	This will show only maps submitted by either Spanish or Greek organisations
