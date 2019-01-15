# Basic PyQGIS
### Hello Python
print("Hello QGIS3 World!")

### Add Vector Layer
```python
layer = QgsVectorLayer('C:/Workspace/pyqgis/pl_amphoe.shp', 'pl_amphoe', 'ogr')
layer
layer.isValid()
QgsProject.instance().addMapLayer(layer)

```
### Remove Vector Layer
```python
QgsProject.instance().removeMapLayer(layer)
iface.mapCanvas().refresh()

### iface add layer
vill = iface.addVectorLayer('C:/Workspace/pyqgis/pl_village.shp', 'pl_village', 'ogr')
river = iface.addVectorLayer('C:/Workspace/pyqgis/pl_stream.shp', 'pl_stream', 'ogr')

```
