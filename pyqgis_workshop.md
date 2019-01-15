# Basic PyQGIS
### Hello Python
```python
print("Hello QGIS3 World!")
```
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
### Open Attribute Table
```python
for field in layer.fields():
…	print(field.name(), field.typeName())

for feature in layer.getFeatures():
…	print(feature["AMP_NAM_T"])

iface.showAttributeTable(layer)
```
### Vector Color
```python
layer.renderer().symbol().setColor(QColor("#98F6B3"))
layer.triggerRepaint()
iface.layerTreeView().refreshLayerSymbology(layer.id())

```
### Add Raster Layer
```python
raslyr = QgsRasterLayer('C:/Workspace/pyqgis/pl_dem30m.tif', 'DEM')
raslyr.isValid()
QgsProject.instance().addMapLayer(raslyr)

```
### Remove Vector Layer
```python
QgsProject.instance().removeMapLayer(raslyr)
iface.mapCanvas().refresh()

### iface add layer
modis = iface.addRasterLayer('C:/Workspace/pyqgis/modis13a2.tif', 'MODIS_Image')
```
### Raster Properties
```python
raslyr.width(), raslyr.height()
raslyr.extent()
raslyr.extent().toString()
raslyr.rasterType()

```
### Raster Color 
```python
raslyr = QgsRasterLayer('C:/Workspace/pyqgis/pl_dem30m.tif', 'DEM')
QgsProject.instance().addMapLayer(raslyr)
fcn = QgsColorRampShader()
fcn.setColorRampType(QgsColorRampShader.Interpolated)
lst = [ QgsColorRampShader.ColorRampItem(0, QColor(166,97,26)), \
QgsColorRampShader.ColorRampItem(1000, QColor(245,245,245)), \
QgsColorRampShader.ColorRampItem(1500, QColor(1,133,133)) ]
fcn.setColorRampItemList(lst)
shader = QgsRasterShader()
shader.setRasterShaderFunction(fcn)
renderer = QgsSingleBandPseudoColorRenderer(raslyr.dataProvider(), 1, shader)
raslyr.setRenderer(renderer)
raslyr.triggerRepaint()

```
### Processing Tool
```python
### Buffer ###
vill = "C:/Workspace/pyqgis/pl_village.shp"
result = processing.run("native:buffer",{'INPUT':vill,'DISTANCE':1000,'SEGMENTS':5,'DISSOLVE':False,'OUTPUT':'memory:'})
QgsProject.instance().addMapLayer(result['OUTPUT'])

processing.runAndLoadResults("native:buffer", {'INPUT':vill,'DISTANCE':5000,'SEGMENTS':50,'DISSOLVE':False,'OUTPUT':'memory:'})

processing.runAndLoadResults("native:buffer", {'INPUT':vill,'DISTANCE':5000,'SEGMENTS':50,'DISSOLVE':True,'OUTPUT':'memory:'})

processing.runAndLoadResults("native:buffer", {'INPUT':vill,'DISTANCE':5000,'SEGMENTS':50,'DISSOLVE':True,'OUTPUT':'C:/Workspace/pyqgis/villbuffer.shp'})

### Clip ###
river = "C:/Workspace/pyqgis/pl_stream.shp"
bndary = "C:/Workspace/pyqgis/pl_amphoe_mueang.shp"

processing.runAndLoadResults("native:clip", {'INPUT':river,'OVERLAY':bndary,'OUTPUT':'memory:'})

processing.runAndLoadResults("native:clip", {'INPUT':river,'OVERLAY':bndary,'OUTPUT':'C:/Workspace/pyqgis/river_clip.shp'})

```
