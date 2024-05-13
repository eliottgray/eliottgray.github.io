# A Software Engineer's guide to using Geographic Coordinates

_"Oops, I got Lat/Lng backwards and it took me an hour to debug."_


## Intro: "Why you should read this."

Everything is somewhere. This may seem obvious, but day-to-day life is heavily influenced by location. 

Spatial questions are central to many common interactions people have with their ever-increasingly-digital environment:
 - **Search**: "Where is this place?"
 - **Navigation**: "How can I get there?"
 - **Delivery**: "I want to get something here."
 - **Visualization**: "I want to see a map."
 - **Weather/Traffic**: "What are conditions like here/there?"

This is an overview of some common questions that a software engineer or data scientist may encounter when working with spatial data. This article assumes that the reader has minimal knowledge of coordinate reference systems or GIS, and wants to just "make it work" (mastery comes later). Solutions suggested here are cross-applicable to most mainstream programming languages and environments.


## Distance Measurement: "How far away are two things?"

Calculating distance from A to B is one of the most common problems in spatial sciences. 

#### Easy Appoach: Haversine & Vincenty Formulas

The simplest approach is to use formulas that take Lat/Lng as input and return distance as output: There are two popular algorithms:
 - Haversine formula
   - Faster & less accurate than Vincenty's formula.
   - Uses Great Circle distance, which treats the Earth as a perfect sphere (which it's not!)
 - Vincenty's formula
   - Slower & more accurate than Haversine formula.
   - Uses geodesic distance, which treats the Earth as an oblate spheroid (a squashed sphere).

Which to use (and whether it matters!) depends on the use case. Below are some comparisons of measurements at different scales:

| Origin | Destination | Haversine | Vincenty | Delta |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| Paris, France | Mumbai, India | 7009570.80 | 7017461.44 | 7890.65 |
| London, UK | Birmingham, UK | 163460.99 | 163799.64 | 338.65 |
| Empire State Building | Central Park, NY| 2027.423 | 2026.422 | 1.001 |



"Hard: Map Projection & Pythagorean Theorem"
"Gotchas: 
Unprojected Pythagoras"
Apples & Oranges
Lat/Lng Ordering

## Area Measurement: "How large is this area?"

	"Hard: Geodesic Calculations"
	"Also Hard: Planar Calculations"
	Gotchas:
		Invalid Polygons
		Projection Selection

	
## Storage: "Where do I put all these shapes?"

	"Online: PostGIS"
	"Offline & I/O: GeoJSON"
	Honorable Mentions:
		ESRI formats
		Well-Known Text (WKT)
		Well-Known Binary (WKB)


## Visualizing: "Show me these shapes."
	
	On my website
		Map Library
		Map Tiles
	On my computer
		Free: QGIS
		Paid: ArcGIS
		Honorable Mention: geojson.io


## Spatial Analysis: "Does this shape intersect/contain/etc. another shape?"

	Programmatic: "Spatial libraries"
		Python: Shapely, PyProj
		Java: Spatial4j
		C++: GDAL
		Database: PostGIS
	Tools: "GIS Software" 
		Open Source: QGIS
		Paid: ArcGIS
		

## Conclusion

	"Thanks!"