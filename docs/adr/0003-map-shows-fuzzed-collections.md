---
status: superseded by ADR-0004
---

# Map markers are opt-in, neighborhood-level collections

The map shows collections, not individual plants. A residential collection (home garden, balcony, indoor collection) appears only after its owner explicitly opts in, and only at a fuzzed neighborhood-level location. Individual plants are viewed inside a public profile, never pinned on the map.

This avoids publishing precise home addresses and prevents individual plants from becoming location beacons. The trade-off is that discovery is less precise and less "walk up and see this plant," and the system must store a coarse, deliberately imprecise location for mapped collections. Exact per-plant geolocation is out of scope for v1.
