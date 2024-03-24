---
toc: false
---

```html
<link href="https://unpkg.com/maplibre-gl/dist/maplibre-gl.css" rel="stylesheet" />
```

```js
import maplibregl from "npm:maplibre-gl"
let pmtiles = await import("npm:pmtiles")
maplibregl.addProtocol('pmtiles', (new pmtiles.Protocol()).tile)

const div = display(document.createElement("div"))
div.style = "height: 600px;"

const style = {
  "version": 8,
  "sources": {
    "gel-raster": {
      "type": "raster",
       "tiles": [
        "http://smart.local:8080/0-0-0/{z}/{x}/{y}.webp"
       ],
       "tileSize": 512,
       "minzoom": 2,
       "maxzoom": 5
    },
    "gel-raster-dem": {
      "type": "raster-dem",
       "tiles": [
        "http://smart.local:8080/0-0-0/{z}/{x}/{y}.webp"
       ],
       "tileSize": 512,
       "minzoom": 2,
       "maxzoom": 5
    }
  },
  "layers": [
    {
      "id": "gel",
      "type": "raster",
      "source": "gel-raster",
    }
  ],
  "terrain": {
    "source": "gel-raster-dem"
  }
}

const map = new maplibregl.Map({
  container: div,
  style: style,
  center: [139.755, 35.691],
  zoom: 3,
  localIdeographFontFamily: '"NotoSansJP-Regular", sans-serif'
})
map.addControl(new maplibregl.FullscreenControl())
map.addControl(new maplibregl.NavigationControl())

invalidation.then(() => map.remove())
```