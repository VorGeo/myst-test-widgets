---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Test Widgets in MyST

## Simple Widget

```{code-cell} python
import ipywidgets as widgets

widgets.IntSlider()
```

## Two Widgets with jslink Synchronization

```{code-cell} python
caption = widgets.Label(value='The values of slider1 and slider2 are synchronized with jslink')
sliders1, slider2 = widgets.IntSlider(description='Slider 1'),\
                    widgets.IntSlider(description='Slider 2')
l = widgets.jslink((sliders1, 'value'), (slider2, 'value'))

display(caption, sliders1, slider2)
```

## Lonboard (interactive mapping widget)

```{code-cell} python
import geopandas as gpd
from lonboard import Map, PolygonLayer

gdf = gpd.read_parquet("test_ecosystem_polygons.parquet")

layer = PolygonLayer.from_geopandas(
    gdf,
    get_fill_color=[255, 0, 0],
)
m1 = Map(layer)
m1
```

## Lonboard Linked Maps with Layer Toggle

```{code-cell} python
toggle = widgets.ToggleButton(
    value=True,
    button_style='info',
    description='Toggle Layer'
)
m2 = Map(layer)
m3 = Map([])

viewstate_link = widgets.jslink((m2, 'view_state'), (m3, 'view_state'))
layer_link = widgets.jsdlink((toggle, 'value'), (m2.layers[0], 'visible'))

widgets.VBox([
  m2,
  toggle,
  m3
])

```
