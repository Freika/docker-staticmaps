# Docker Static Maps API

[![Build & Publish](https://github.com/dietrichmax/docker-staticmaps/actions/workflows/pipeline.yml/badge.svg)](https://github.com/dietrichmax/docker-staticmaps/actions/workflows/pipeline.yml) 

## Usage

To get a static map from the endpoint "/staticmaps" several prameters have to be provided

For different styles docker-staticmaps is using exisiting tile-services from various providers. Be sure to check their Terms of Use for your use case or use a `custom` tileserver!

- `zoom` - Set the zoom level for the map.
- `width` - default 300 - Width in pixels of the final image
- `height` - default 300 - Height in pixels of the final image
- `style` - default "osm" - Select the basemap
  - `osm` - [Open Street Map](https://www.openstreetmap.org/)
  - `streets` - Default [Esri street basemap](https://www.arcgis.com/home/webmap/viewer.html?webmap=7990d7ea55204450b8110d57e20c99ab)
  - `satellite` - Esri's [satellite basemap](https://www.arcgis.com/home/webmap/viewer.html?webmap=d802f08316e84c6592ef681c50178f17&center=-71.055499,42.364247&level=15)
  - `hybrid` - Satellite basemap with labels
  - `topo` - Esri [topographic map](https://www.arcgis.com/home/webmap/viewer.html?webmap=a72b0766aea04b48bf7a0e8c27ccc007)
  - `gray` - Esri gray canvas with labels
  - `gray-background` - Esri [gray canvas](https://www.arcgis.com/home/webmap/viewer.html?webmap=8b3d38c0819547faa83f7b7aca80bd76) without labels
  - `oceans` - Esri [ocean basemap](https://www.arcgis.com/home/webmap/viewer.html?webmap=5ae9e138a17842688b0b79283a4353f6&center=-122.255816,36.573652&level=8)
  - `national-geographic` - [National Geographic basemap](https://www.arcgis.com/home/webmap/viewer.html?webmap=d94dcdbe78e141c2b2d3a91d5ca8b9c9)
  - `otm` - [OpenTopoMap](https://www.opentopomap.org/)
  - `stamen-toner` - [Stamen Toner](http://maps.stamen.com/toner/) black and white map with labels
  - `stamen-toner-background` - [Stamen Toner](http://maps.stamen.com/toner-background/) map without labels
  - `stamen-toner-lite` - [Stamen Toner Light](http://maps.stamen.com/toner-lite/) with labels
  - `stamen-terrain` - [Stamen Terrain](http://maps.stamen.com/terrain/) with labels
  - `stamen-terrain-background` - [Stamen Terrain](http://maps.stamen.com/terrain-background/) without labels
  - `stamen-watercolor` - [Stamen Watercolor](http://maps.stamen.com/watercolor/)
  - `carto-light` - [Carto](https://carto.com/location-data-services/basemaps/) Free usage for up to 75,000 mapviews per month, non-commercial services only.
  - `carto-dark` - [Carto](https://carto.com/location-data-services/basemaps/) Free usage for up to 75,000 mapviews per month, non-commercial services only.
  - `carto-voyager` - [Carto](https://carto.com/location-data-services/basemaps/) Free usage for up to 75,000 mapviews per month, non-commercial services only.
  - `custom` - Pass through the tile URL using parameter `tileurl`, requires authentication
- `format` (e.g. "png", "jpg" or "webp")

## Deployment

### Docker

```
docker run -d --name web --network my-net nginx:alpine
docker run -p 3000:3000 mxdcodes/docker-staticmaps

###

```js
git clone https://github.com/dietrichmax/docker-staticmaps
npm i
npm run start#   d o c k e r - s t a t i c m a p s  
 