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
from lonboard import Map, PolygonLayer

gdf = gpd.read_parquet("test_ecosystem_polygons.parquet")

layer = PolygonLayer.from_geopandas(
    gdf,
    get_fill_color=[255, 0, 0],
)
m = Map(layer)
m
```