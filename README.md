# NoSQL document modeling

1) Embed or reference
Embedding:
- Data from entities are queried together
- The child is a dependent e.g. Order Line depends on Order
- 1:1 relatioship
- Similar volatility
- The set of values or sub-documents is bounded (1:few)

Refence:
- one-to-many relatioships (unbunded)
- many-to-many relatioships
- related data changes with differing volatility
- referenced entity is a key entity used by many others

Combining embed + reference

2) Normalization vs denormalization
Normalization:
- Normalized data may save some space, but...
  Requires multiple reads
  Doesn't align with classes/objets
  Typically provides faster write speed
  
Denormalization:
- Denormalized data aligns with classes/objets but...
  Requires updates in multiple places
  Typically provides faster read speed
  
3) Homogeneous vs Heterogeneous data
- SELECT c.type, c.id, c.name, c.sessions, c.speakers 
  FROM c
  WHERE c.sessionId = "session1"
  OR ARRAY_CONTAINS(c.sessions, {"sessionId", "session1"})
  ORDER BY c.type
 
4) Hierarchies
- SELECT VALUE org.name FROM org WHERE ARRAY_CONTAINS(org.directs, "Ben")

5) Keyworkds
- SELECT c.id, c.title FROM c WHERE ARRAY_CONTAINS(c.keywords, "design")

6) Telemetry
Consider storage of time-series data
  Device readings: Weather stations, sensors, etc.
  One document per time period, per device

7) Logging
Similar to telemetry; Consider parsing log entries
Partition per time period, event type, region, etc.
