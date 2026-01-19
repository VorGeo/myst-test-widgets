---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Test MyST + widgets

## IntSlider

```{code-cell} python
import ipywidgets as widgets

widgets.IntSlider()
```

```{code-cell} python
caption = widgets.Label(value='The values of slider1 and slider2 are synchronized with jslink')
sliders1, slider2 = widgets.IntSlider(description='Slider 1'),\
                    widgets.IntSlider(description='Slider 2')
l = widgets.jslink((sliders1, 'value'), (slider2, 'value'))

display(caption, sliders1, slider2)
```


## Lonboard

```{code-cell} python
import geopandas as gpd
from shapely.geometry import Polygon
from lonboard import Map, PolygonLayer

# Create a simple polygon
# Coordinates: (longitude, latitude)
rectangle = Polygon([
    (-122.5, 37.5),   # bottom-left
    (-122.5, 38.0),   # top-left
    (-121.5, 38.0),   # top-right
    (-122.5, 37.5)    # close the polygon
])

# Create GeoDataFrame with the rectangle
gdf = gpd.GeoDataFrame({'geometry': [rectangle]}, crs='EPSG:4326')

layer = PolygonLayer.from_geopandas(
    gdf,
    get_fill_color=[255, 0, 0],
    get_line_color=[0, 100, 100, 150],
)
m = Map(layer)
m
```