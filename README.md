# base de datos de condenados
## introduccion
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
#### importar
![This is an alt text.](https://github.com/lean-23/trabajo_de_base_de_datos/blob/main/imoirtar%20csv.png) 
![. ](https://github.com/lean-23/trabajo_de_base_de_datos/blob/main/importar%20datos.png).

#creo las tablas con comandos:
``` sql
CREATE TABLE profesion(code_prof INT(11) PRIMARY KEY NOT NULL AUTO_INCREMENT,
profesion VARCHAR(45) NOT NULL );
```
e inserto los datos de la tabla principal a la tabla profesion con el siguiente comando:
``` sql
INSERT INTO profesion (desc_prof)
SELECT DISTINCT profesión
FROM condenado;
```
a continuacion se muestra como inserte y relacione la tabla unidad que contiene la clave secundaria de la tabla provincias
``` sql
 CREATE TABLE provincias(
   code_uni INT (11) PRIMARY KEY NOT NULL AUTO_INCREMENT,
   nom_prov VARCHAR(45) NOT NULL);
```
```sql
  CREATE TABLE unidad(
   code_uni INT (11) PRIMARY KEY NOT NULL AUTO_INCREMENT,
   nom_uni VARCHAR(45) NOT NULL,
   uni_prov VARCHAR (45));
```
``` sql
INSERT INTO unidad (nom_uni,uni_prov)
SELECT DISTINCT unidad, unidad_provincia_id
FROM condenado;
```
cambio tipo de datos
```sql
ALTER TABLE unidad 
MODIFY COLUMN uni_prov INT(11);
```
agrego la clave secundaria
```sql
ALTER TABLE unidad
ADD CONSTRAINT fk_provincias FOREIGN KEY (uni_prov)
        REFERENCES provincias (code_prov);
```

luego cambio el nombre de la columna en la tabla condenado
```sql
ALTER TABLE condenado 
CHANGE  COLUMN unidad_provincia_id cond_prov VARCHAR(45);
```
actualizo los datos
```sql
UPDATE condenado
SET  cond_prov = '6'
WHERE cond_prov = 'Buenos Aires';
```
cambio el tipo de datos
```sql
ALTER TABLE condenado 
MODIFY COLUMN cond_prov INT(11);
```

#agrego clave primaria a la tabla de condenado
```sql
ALTER TABLE condenado 
CHANGE  COLUMN lpu code_cond INT(11);

ALTER TABLE condenado ADD PRIMARY KEY (code_cond);
```
