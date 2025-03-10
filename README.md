# Dataton2019 - Datos 
Datos para usarse en el datatón 2019.

## Contrataciones (Sistema 6)
Datos de compras públicas.

### Datos en formato JSON
| Archivo        | Formato  | Comentarios  |
| :------------- |:-------------| :-----|
| contrataciones_arr.json.zip      | JSON Array| Datos de contrataciones públicas, organizados conforme al estandar [OCDS](https://standard.open-contracting.org/latest/es/) (A.K.A. "EDCA") |
| buyers.json.zip | JSON Array| Instituciones compradoras |
| tenderers_suppliers.json.zip| JSON Array| Proveedores/contratistas|
| cp.json.zip| JSON Array| [Proyección](https://en.wikipedia.org/wiki/Projection_\(relational_algebra\)) de contrataciones_arr.json.zip|

Instrucciones para importar los datos en una instancia local de [MongoDB](https://www.mongodb.com/):
```shell script
# Descomprime los datos:
unzip datos_ejemplo.json.zip

# Importa los datos a MongoDB:
mongoimport -d dataton2019 -c datos_ejemplo --jsonArray datos_ejemplo.json
```

Consultas básicas en MongoDB (línea de comandos):
```shell script
# Ingresa a la línea de comandos de MongoDB:
mongo
```

```javascript
 // Seleccionar base de datos dataton2019
 use dataton2019;

 // Contar registros
 db.datos_ejemplo.count();

 // Buscar y mostrar el primer registro en la colección 
 db.datos_ejemplo.findOne();
```

[Fuente](https://compranetinfo.hacienda.gob.mx/info/datos/archivo.php?idc=3&ida=9)

### Base de datos de grafos
Base de datos [Neo4j](https://neo4j.com/) generada a partir de los datasets anteriores. Permite trazar las relaciones entre las Instituciones de 
Gobierno (buyers), los procesos de contrataciones y los participantes (tenderers, suppliers, etc.).

| Archivo        | Formato  | Comentarios  |
| :------------- |:-------------| :-----|
| [oc_graph.dump](https://drive.google.com/open?id=1EkbFSvMjVXYtNqpHGO-3ac0LvPU95uuB) | Neo4j dump | Base de datos de grafos |

Instrucciones para restaurar la base de datos:
```shell script

# Ingresa al directorio de neo4j y detén la base de datos
$neo4j-home> bin/neo4j stop

# Restaura la base de datos
$neo4j-home> bin/neo4j-admin load --from=/path/to/oc_graph.dump --database=graph.db --force
```
Representación gráfica:
```
$ MATCH p=()-->() RETURN p LIMIT 5000
```
![alt Graph database](https://raw.githubusercontent.com/PDNMX/datosDataton2019/master/S6_Contrataciones/graph.png)


