---
status: accepted
---

# Maps use MapLibre with self-hosted PMTiles

Rootly renders its Map with `@maplibre/maplibre-react-native` using a self-hosted PMTiles archive of OpenStreetMap-derived data. There is no map vendor API and no geocoding. Pins are placed by coordinates, and the map is centered on the device location for radius-based nearby discovery.

This satisfies the open-source, no-map-API constraint while still providing a real local map for a 10–25 km radius. It requires an Expo development build, object-storage/CDN hosting for the PMTiles archive, and OpenStreetMap attribution. Place search and city/neighborhood geocoding are out of scope, and a single static image was rejected because it cannot show local radius detail.
