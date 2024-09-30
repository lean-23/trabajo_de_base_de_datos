# Base de datos de condenados
## 1 introduccion
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
### A)cree la base de datos
![This is an alt text.](https://github.com/lean-23/trabajo_de_base_de_datos/blob/main/tp-1.png)

##### B) la tabala general para inportar el archivo csv
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
### elimino columna estan de mas
![. ](https://github.com/lean-23/trabajo_de_base_de_datos/blob/main/borrar_columna.png)
![. ](https://github.com/lean-23/trabajo_de_base_de_datos/blob/main/borrar_columna1.png)

#elimino tablas que estan de mas
```sql
ALTER TABLE condenado DROP situacion_procesal;
ALTER TABLE condenado DROP unidad_provincia;
ALTER TABLE condenado DROP provincia_nacimiento_id;
ALTER TABLE condenado DROP estado_civil;
ALTER TABLE condenado DROP provincia_nacimiento;
ALTER TABLE condenado DROP subgrupo;
```
#actualizo los datos
```sql
UPDATE provincia
SET nom_prov = 'Ciudad de BS AS'
WHERE code_prov = 1;
```
#cambio el tipo de dato varchar a date
```sql
UPDATE condenado
SET fecha_sentencia_firme = STR_TO_DATE(fecha_sentencia_firme, '%d/%m/%Y');
```
## Descripcion      
![tabla sin usar. ]() 
La base de datos cuenta con 10 tablas    
#Condenado tabla princial donde se ejecuntan todas las consultas           
#Unidad        
#Provincias        
#Profesion          
#Generos           
#Juzgado tabla que no se utiliza      
#Delito        
#Penas       
#Nacionalidad        
#Jurisdiccion      
       

la tabla principal cuenta con aproximadamente 18 con culumnas que son las siguietes  
cond_code = clave primaria de la tabla    
cond_nom = nombre del condenado      
cond_ape = apellido del condenado  
cond_edad = edad    
cond_gene = genero  
cond_nac = nacionalidad   
cond_uni = unidad donde se encuentra el condenado    
cond_prov = provincia a la cual corresponde esa undiad     
cond_prof = profesion que ejercia el condenado   
cond_deli  = delito cometido     
cond_juri = jurisdiccion del delito cometido 

cond_fnac = fecha nacimiento    
cond_fsfi = fecha de sentencia firme    
cond_fing = fecha de ingreso    
cond_anpe = años de penas      
cond_dipe = dias de penas       
cond_mepe = meses pena       

## Clonacion del repositorio

