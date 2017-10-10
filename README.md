# QGIS cheat sheet

Cheat sheet for PyQgis

Canvas
---
__Access Canvas__

	canvas = iface.mapCanvas()

TOC
---
__Access checked Layers__

	iface.mapCanvas().layers()

__Obtain Layers name__

	canvas = iface.mapCanvas()
	layers = [canvas.layer(i) for i in range(canvas.layerCount())]
	layers_names = [ layer.name() for layer in layers ]
	print "layers TOC = ", layers_names
	
__Obtain Layers name from PostGIS database__

	from PyQt4.QtSql import *
	
    	db = QSqlDatabase.addDatabase("QPSQL");
    	db.setHostName("localhost");
    	db.setDatabaseName("postgres");
    	db.setUserName("postgres");
    	db.setPassword("postgres");
    	db.open();
    	names=db.tables( QSql.Tables)
    	print names
	

__Add vector layer__

	layer = iface.addVectorLayer("input.shp", "name", "ogr")
	if not layer:
	  print "Layer failed to load!"

__Find layer by name__

	from qgis.core import QgsMapLayerRegistry
	layer = QgsMapLayerRegistry.instance().mapLayersByName("name")[0]
	print layer.name()

__Set Active layer__

	from qgis.core import QgsMapLayerRegistry
	layer = QgsMapLayerRegistry.instance().mapLayersByName("name")[0]
	iface.setActiveLayer(layer)

__Remove all layers__

	QgsMapLayerRegistry.instance().removeAllMapLayers()
	
Buttons
---
__Adding a button on toolbar__

	from PyQt4.QtGui import QToolButton, QIcon
	button = QToolButton()	
	button.setIcon(QIcon("PATH-TO-FILE"))
	iface.addToolBarWidget(button)
	
OR (Using iface)
	
	from PyQt4.QtGui import QToolButton, QIcon
	iface.toolButton = QToolButton()
	boton.setIcon(QIcon("C:/Users/enocc/Desktop/bolt3.png"))
	iface.addToolBarWidget(iface.toolButton)


Progress Bar
---
__Adding a progress bar__

	from PyQt4.QtGui import QProgressDialog, QProgressBar
	
	def progdialog(progress):
	    dialog = QProgressDialog()
	    dialog.setWindowTitle("En progreso...")
	    dialog.setLabelText("Cargando...")
	    bar = QProgressBar(dialog)
	    bar.setTextVisible(True)
	    bar.setValue(progress)
	    dialog.setBar(bar)
	    dialog.setMinimumWidth(300)
	    dialog.show()
	    return dialog, bar
	    
	def calc(x, y):
	    dialog, bar = progdialog(0)
	    bar.setValue(0)
	    bar.setMaximum(100)
	    sum = 0
	    progress = 0
	    for i in range(x):
		for j in range(y):
		    k = i + j
		    sum += k
		i += 1
		progress = (float(i) / float(x)) * 100
		bar.setValue(progress)
	    print sum
	    
	calc(10000, 2000)
	
Processing algorithms 
---
__Get algorithms list__

	import processing
	processing.alglist()

__Get algorithms Help__

Random selection

	processing.alghelp('qgis:randomselection')


__Get algorithms Options__

Random selection

	processing.algoptions('qgis:randomselection')





Sources
---

<http://docs.qgis.org/testing/en/docs/pyqgis_developer_cookbook/>

<http://qgis.org/api/>

<https://stackoverflow.com/questions/tagged/qgis>

<https://gis.stackexchange.com/questions/tagged/pyqgis>

<https://webgeodatavore.github.io/pyqgis-samples/>




