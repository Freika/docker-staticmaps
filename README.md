# Docker Static Maps API

[![Build & Publish](https://github.com/dietrichmax/docker-staticmaps/actions/workflows/pipeline.yml/badge.svg)](https://github.com/dietrichmax/docker-staticmaps/actions/workflows/pipeline.yml)

A containerized web version for [staticmaps](https://www.npmjs.com/package/staticmaps) with [express](https://github.com/expressjs/express).

## Usage

To get a static map from the endpoint `/staticmaps` several prameters have to be provided.

- `center` - Center coordinates of the map in the format `lon, lat`
- `zoom` - Set the zoom level for the map.
- `width` - default `300` - Width in pixels of the final image
- `height` - default `300` - Height in pixels of the final image
- `format` - default `png` (e.g. `png`, `jpg` or `webp`)

### Basemap

For different basemaps docker-staticmaps is using exisiting tile-services from various providers. Be sure to check their Terms of Use for your use case or use a `custom` tileserver with the `tileUrl` parameter!

- `basemap` - default "osm" - Select the basemap
  - `osm` - default - [Open Street Map](https://www.openstreetmap.org/)
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
  - `custom` - Pass through the tile URL using parameter `tileurl`

### Drawing Polylines

Polylines can be added to a map. Therefore you have to add a parameter `path=color:{color}|weight:{lineWeight}|{point1({lat},{lon})}|{point2({lat},{lon})}`, e.g. `path=color:0000FFBB|weight:7|40.736202,-74.006138|40.720982,-73.982277|40.708751,-74.009228`.

- `color`: specify the hex color code without hash symbol
- `weight`: thickness of line in pixel
- `coordinates`: pair of coordinates in `{lat1},{lon1}|{lat2},{lon2}` seperated by `|`. At least two are needed for a polyline

## Deployment

**with Docker**

```
docker run -d  --name='static-maps-api' -p '3003:3000/tcp' 'mxdcodes/docker-staticmaps:latest'
```

**with Node.js**

```js
git clone https://github.com/dietrichmax/docker-staticmaps
npm i
npm run start
```

## Example requests

- `http://localhost:3000/staticmaps?width=300&height=300&center=-119.49280,37.81084&zoom=9&format=png`

![example request 1](https://github.com/dietrichmax/docker-staticmaps/blob/main/examples/example1.png "example request 1")

- `http://localhost:3000/staticmaps?width=500&height=500&center=-73.99515,40.76761&zoom=10&format=webp&basemap=carto-voyager`

![example request 2](https://raw.githubusercontent.com/dietrichmax/docker-staticmaps/refs/heads/main/examples/example2.webp "example request 2")

- `http://localhost:3000/staticmaps?width=500&height=500&center=-73.99515,40.76761&zoom=10&format=png&tileUrl=https://server.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Light_Gray_Base/MapServer/tile/{z}/{y}/{x}`

![example request with custom tileUrl](https://github.com/dietrichmax/docker-staticmaps/blob/main/examples/example3.png "example request with custom tileUrl")

- `http://localhost:3000/staticmaps?width=500&height=500&center=-73.99515,40.76761&zoom=10&format=png&tileUrl=https://server.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Light_Gray_Base/MapServer/tile/{z}/{y}/{x}`

- `http://localhost:3000/staticmaps?center=40.737102,-73.990318&zoom=12&width=1000&height=1000&basemap=gray-background&path=color:0000FFBB|weight:7|40.736202,-74.006138|40.720982,-73.982277|40.708751,-74.009228`

![example request with polyline](https://github.com/dietrichmax/docker-staticmaps/blob/main/examples/polyline_example.png "example request with polyline")
