# base de datos de condenados
Este repositorio contiene documentacion de la base de datos de los internos condenados  del sevicio penintenciario del la nacion,
extraido de la pagina del  ministerio de  justicia  de la nacion
Lo primero que realice fue limpiar los datos de la planilla y pasarlo
a otra planilla sin comas y con columnas
luego defini las tablas

segundo realice las primeras tablas de prueba
hasta que termine el diagrama
de la base de datos y es la siguiente:

[diagrama de base de datos]

Luego:
### 1)cree la base de datos
![This is an alt text.](https://github.com/lean-23/trabajo_de_base_de_datos/blob/main/tp-1.png)

##### 2) la tabala general para inportar el archivo csv
```sql
CREATE TABLE condenado (
	unidad VARCHAR(225), lpu INT(11),
	apellido VARCHAR(225) ,nombre VARCHAR(225),
	situacion_procesal VARCHAR(225),delito VARCHAR(225),
	edad VARCHAR(225),	nacionalidad VARCHAR(225),
	enero VARCHAR(225), jurisdiccion VARCHAR(225),
	fecha_sentencia_firme VARCHAR(225), anios_pena VARCHAR(225),meses_penas VARCHAR(225),
	dias_pena VARCHAR(225),	tipo_pena VARCHAR(225),
	estado_civil VARCHAR(225),	profesion VARCHAR(225),
	subgrupo VARCHAR(225),	fecha_nacimiento VARCHAR(225),
	provincia_nacimiento VARCHAR(225),fecha_ingreso VARCHAR(225),
	juzgado VARCHAR(225),
	provincia_nacimiento_id VARCHAR(225),
	unidad_provincia VARCHAR(225),
	unidad_provincia_id VARCHAR(225) 
)
```
# importar
![This is an alt text.](https://github.com/lean-23/trabajo_de_base_de_datos/blob/main/imoirtar%20csv.png) 
![. ](https://github.com/lean-23/trabajo_de_base_de_datos/blob/main/importar%20datos.png).
