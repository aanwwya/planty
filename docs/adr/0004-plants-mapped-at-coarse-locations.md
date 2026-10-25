# Plants are mapped individually at coarse locations

Rootly has no Collection, Balcony, or Garden entity. A user has one flat list of Plants. A Plant can be made public by its Owner, in which case it appears on the Owner's Profile and as a pin on the Map at a neighborhood-level coarse location.

All of a user's public Plants share the same coarse area rather than being independently jittered, so the Map cannot be used to triangulate a home from several plants. Exact coordinates are never stored or displayed; the Owner chooses or confirms a coarse area, not an address. This supersedes ADR-0003.

Consequences: the Map is plant-centric, discovery is approximate rather than address-precise, and there is no grouping concept to navigate. Public Profiles list a user's public Plants directly.
