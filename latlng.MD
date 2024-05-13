# A Software Engineer's guide to using Geographic Coordinates
_"Oops, Lat/Lng ordering was backwards and it took me an hour to identify."_


## Intro: "Why you should read this."

Everything is somewhere. This may seem obvious, but day-to-day life is heavily reliant on location. 

Spatial questions are central to many common interactions people have with their ever-increasingly digital environment:
 - **Search**: "Where is this thing?"
 - **Navigation**: "How can I get there?"
 - **Delivery**: "I want something to arrive here."
 - **Visualization**: "I want to see a map."
 - **Weather/Traffic**: "What are conditions like here/there?"

This document is an overview of some common problems that a software engineer or data scientist may encounter when working with spatial data. We assume here that the reader has minimal knowledge of coordinate reference systems or GIS, and wants to just "make it work" (mastery comes later). Solutions suggested here are cross-applicable to most mainstream programming languages and environments.


## Distance Measurement: "How far away are two places on Earth?"

There are two popular approaches to deriving a distance between two lat/lng pairs:
 - Haversine formula
 - Vincenty's formulae

### Haversine formula

The [Haversine formula](https://en.wikipedia.org/wiki/Haversine_formula) computes distance between two points by treating the Earth as a perfect sphere (which it is not). This is called the great circle distance, and is simpler to calculate than using Vincenty's formulae.

### Vincenty's formula

[Vincenty's formula](https://en.wikipedia.org/wiki/Vincenty%27s_formulae) computes the distance between two points, similarly to the Haversine formula. However, this approach treats the earth as an oblate spheroid (squashed sphere) which is a more accurate approach. This approach is preferred when greater accuracy is desired.


### Comparison

Which approach to use (and whether it matters!) depends on the use case. Below are some comparisons of measurements at different scales:

| Origin | Destination | Haversine_M | Vincenty_M | Delta_M | Delta_% |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| Paris, France | Mumbai, India | 7009570.80 | 7017461.44 | 7890.65 | 0.112 |
| London, UK | Birmingham, UK | 163460.99 | 163799.64 | 338.65 | 0.207 |
| Empire State Building, NY | Central Park, NY| 2027.423 | 2026.422 | 1.001 | 0.0494 |

The following approach is suggested to choosing an algorithm:

 - **Haversine formula** should be used if:
   - Computation speed is more important than accuracy.
   - Input coordinates are inaccurate or imprecise:
     - approximate/arbitrary locations
	 - consumer-grade (*e.g. smart phone*) GPS coordinates
 - Otherwise **Vincenty's formula** should be used, e.g. when comparing coordinates obtained from high-grade GPS or survey equipment.*)
 
 

### Pitfalls & Considerations

- **Know where your coordinates came from, and don't compare apples to oranges.** 
  - Not all latitude and longitude values are created equal; some coordinates are inaccurate, some can be imprecise, and some can be "correct" and yet still give wrong results when compared. (See: [geodetic datum](https://en.wikipedia.org/wiki/Geodetic_datum)) 
  - **Make sure both coordinates being compared are in the same reference frame, e.g. [WGS84](https://epsg.io/4326). They probably are, but they might not be! The simplest approach is to compare coordinates from the same source.**
- There is no *correct* ordering for Latitude and Longitude, and getting the order wrong can create hard-to-identify bugs.
  - Both are often abbreviated with 3-character terms that start with the same letter (Lat,Lng), and are easy to order incorrectl.
  - Take advantage of programming language features that clarify ordering, such as named parameters (`foo(latitude=lat, longitude=lng)`) or setter methods (`Coord().setLat(latitude).setLng(longitude)`).
- Projecting coordinates is another approach, but is more complex and prone to pitfalls. Cartesian distance can be calculated instead, by first converting to 



Unprojected Pythagoras"


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


Spatial Analysis: "Does this shape intersect/contain/etc. another shape?"

	Programmatic: "Spatial libraries"
		Python: Shapely, PyProj
		Java: Spatial4j
		C++: GDAL
		Database: PostGIS
	Tools: "GIS Software" 
		Open Source: QGIS
		Paid: ArcGIS
		

Conclusion

	"Thanks!"