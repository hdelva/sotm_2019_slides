1. Introduction

2. Quickly explain linked data
   Give everything a URI
   Refer to other data sources by their URIs
   W3C and OGC recommend this for geospatial datasets

3. Quickly explain linked data fragments
   Cheap way of publishing data
   Should be easy to ingest

   Semantics links fragments together
   [image of data dump <-> API]

4. Semantics enable client-side processing
   Takes the load of the service provider
   Better privacy
   Data can be cached for future queries
   Pretty slow though
   [Borrow load-balancing image from LDF paper]

5. OSM as LDF
   Only data relevant for route planning
   Fragmentation = slippy tiles
   Tile size is around 50 kb on zoom level 14.
   [Image of a single tile]

6. Advantages of Routable tiles
   Potential live updates
   Easy data reuse
   Split up data management from route planning

7. Problem statement
   Client-side route planning is slow
   Conventional speedups increase the memory requirements
   We need to reduce the amount of data

8. Move the load
   Can we make it easier for clients to solve queries by doing some preprocessing?

9. Processing pedestrian areas
   Maybe give example of graphhopper/OSRM and the Meir in Antwerp

   Might seem insignificant; but pretty big difference for public transit route planners
   Dynamically deciding how to cross a pedestrian area is slow
   Our shotgun approach: visibility graph of the area and dijkstra queries to filter out the useful ones
   [Image of the added paths ]

10. We are not alone

   Others have solved the same problem, maybe even better
   [screenshot of opentripplanner setting]
   We're all doing the same precomputation on the same data -- why?

11. Local traffic
    [Screenshot of one tile containing stadspark in Antwerp]
    If we're trying to route through a tile, do we really care about all data?
    We can precompute which nodes are never used to pass through a tile

12. Going up
    We can repeat this process on higher zoom levels
    Each time discarding ~50%  data
    Only the 'important' roads remain 
    --> compare to Valhalla tiles; they focus on highway tags -- we focus on how the roads are actually used
    [Image of tile around Lille]

13. Discarding unimportant nodes
    Do we care about the shape of the highway, or do we just care about the length and the tags?
    Discarding untagged non-intersection nodes reduces data by another 50%
    [Screenshot of contracted tile]

14. How it do

    Easy to parallellize

    Results published as LDF
    [Image of processing pipeline]

15. Where do the reductions happen?

    The transit stuff has the most effect on the cities

    The Intersection stuff on the countryside
    [Relative reduction image]

16. Queries
    Less data
    Less time
    Analogy to Customizable Route Planning -> this would technically work for centralized services as well

17. Demo

18. Ecosystem of tiles
    There's a great eco system of map tiles -- what's stopping us from creating one for routing information?
    Cost? Each step is relatively easy, and easy to parallellize, LDF is cheap to host
    Trust? It's hard to verify the quality of routing data

19. Conclusion
    We have developed techniques to make serverless route planning more efficient
    Our challenges are not unique, we should collaborate
    [Cool background image]