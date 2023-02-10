


No hace falta hacer la integración con GIS, podés simplemente bajar toda la información como rasters (formato tiff?) e incluirlas en el código como arrays o como vectores. Fijate que el paquete terra de R tiene muchas funcionalidades para sacar cantidades derivadas de la información de los rasters. 

https://github.com/rspatial/terra

Tener en cuenta que los datos espaciales tienen muchos formatos complicados pero que siempre podés trabajar todo con arrays. Terra tiene una clase de objecto que es spatialRaster, que es un vector de valores con el valor de cada pixel y dsps como metadata que te dice en que sistema de coordenadas está, tamaño de pixel, coordinada del bounding box, filas, columnas, etc.


Para transformar raster a tiff conviene usar Terra. 