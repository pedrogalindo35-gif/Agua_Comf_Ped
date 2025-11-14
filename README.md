**Tarea 4** – Almacenamiento y Consultas de Datos en Big Data (MongoDB)
<br>**Autor:** Pedro Luis Galindo
<br>**Curso:** Big Data  
**Grupo:** 202016911_10  
**Tutor:** Jaime Rubiano Llorente  
**Universidad Nacional Abierta y a Distancia – UNAD** 
<br>**Fecha:** noviembre 2025 

**INTRODUCCIÓN**<br>En este ejercicio vamos a desarrollar una base de datos donde haremos consultas y filtraremos información de los datos obtenidos en la recolección de agua de los barrios en diferentes municipios de la Guajira. Utilizaremos MongoDB Compass como herramienta para crear, cargar y analizar una base de datos denominada `uni_ped`, con una colección llamada `comf2`.  

Para el caso de uso, he tomado como referencia la falta de agua en La Guajira, ya que en este departamento, muchas personas no tienen acceso al preciado líquido.

Como objetivo, se van a poner en práctica los conceptos estudiados acerca del software MongoDB, con el cual se va a crear una base de datos con 100 elementos, de los cuales vamos a hacer análisis filtrando información mediante códigos.

**Fase 1 – Investigación: Tipos de Bases de Datos NoSQL**
<br>**Cuadro comparativo NoSQL aplicado al monitoreo de agua en La Guajira**

| Tipo de BD NoSQL | Ventajas | Inconvenientes | Caso de uso en monitoreo de agua |
|------------------|----------|----------------|----------------------------------|
| **Clave-valor** | - Muy rápida en lecturas y escrituras<br>- Se puede usar para datos simples | - No soporta consultas complejas<br>- Difícil analizar relaciones | Registro instantáneo de estado de tanques, pozos y tuberías (ej. operativa / inactiva, agua potable). |
| **Documentos (MongoDB)** | - Flexible y escalable<br>- Permite almacenar datos semiestructurados | - Se debe tener cuidado al momento de ingresar los datos<br>- Requiere índices para eficiencia | Almacenar informes de entrega por barrio: fecha, cantidad de litros, responsable, observaciones. |
| **Columnas (Cassandra, HBase)** | - Excelente para grandes volúmenes<br>- Optimizada para consultas analíticas | - Su diseño es complejo<br>- Menos intuitiva para datos pequeños | Tomar datos de recolección de agua por municipio, para análisis de tendencias y planificación. |
| **Grafos (Neo4j)** | - Ideal para relaciones y conexiones<br>- Permite descubrir patrones | - No es eficiente para datos tabulares<br>- Requiere modelado especializado | Distribución de comunidades y rutas de entrega: identificar conexiones entre barrios, puntos de distribución. |

**CONCLUSIÓN** <br>teniendo en cuenta el cuadro comparativo, se ha escogido trabajar con MongoDB porque ofrece la flexibilidad y escalabilidad suficientes para gestionar datos semiestructurados. Teniendo en cuenta la referencia de Miranda et al. (2023) y Sarasa (2016), resulta la opción más adecuada para implementar la base de datos de mi proyecto. 

Fase 2: MongoDB, squema propuesto:
<br>Este va a ser el diseño que se va a implementar en MongoDB el cual posee las colecciones, los documentos y los campos:

- Base de datos: `uni_ped` 
- Colección principal: `comf2`

  - `_id` → Identificador numérico.  
  - `MUNICIPIO` → Localidad de donde se hace el estudio.  
  - `fecha_reporte` → Fecha de donde se toman los datos.  
  - `fuente_agua` → Lugar donde recolectan el agua.
  - `estado_fuente` → Disponibilidad.
  - `calidad_agua` → Si es apta para el consumo.
  - `frecuencia _accseo` → Cada cuántos días recolectan agua.
  - `cantidad_promedio` → cuántos litros logran recolectar.
  - `observaciones` → anotaciones importantes.
  - `reportado_por` → persona a cargo.
  - `barrio` → zona donde se recibe el agua.
    
 Carga de Base de Datos con los 100 documentos:

```json
[uni_ped.comf 2.json](https://github.com/user-attachments/files/23551591/uni_ped.comf.2.json)
[Uploa[{
  "_id": {
    "$oid": "69150764f267ef49570b9568"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69150811f267ef49570b956a"
  },
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Inactiva",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 1000,
  "observaciones": "No les llega agua",
  "reportado_por": "Consejal",
  "barrio": "Dividivi",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "691508f7f267ef49570b956d"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Maicao"
},
{
  "_id": {
    "$oid": "69150949f267ef49570b956f"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "N/A",
  "reportado_por": "Consejal",
  "barrio": "Entre Ríos",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69150a8ef267ef49570b9571"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "N/A",
  "reportado_por": "Lider JAC",
  "barrio": "Cooperativo",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69150b1bf267ef49570b9573"
  },
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "Las tunas",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69150b77f267ef49570b9575"
  },
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 15 días",
  "cantidad_promedio_litros": 50,
  "observaciones": "No llega agua",
  "reportado_por": "Consejal",
  "barrio": "El carmen",
  "Municipio": "Albania"
},
{
  "_id": {
    "$oid": "69150bddf267ef49570b9577"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Con falla",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 20 días",
  "cantidad_promedio_litros": 50,
  "observaciones": "Llega poca agua",
  "reportado_por": "Lider JAC",
  "barrio": "El molino",
  "Municipio": "Albania"
},
{
  "_id": {
    "$oid": "69150be8f267ef49570b9579"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Con falla",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 20 días",
  "cantidad_promedio_litros": 50,
  "observaciones": "Llega poca agua",
  "reportado_por": "Lider JAC",
  "barrio": "El molino",
  "Municipio": "Albania"
},
{
  "_id": {
    "$oid": "69150bf0f267ef49570b957b"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Con falla",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 20 días",
  "cantidad_promedio_litros": 50,
  "observaciones": "Llega poca agua",
  "reportado_por": "Lider JAC",
  "barrio": "El molino",
  "Municipio": "Albania"
},
{
  "_id": {
    "$oid": "69150bf7f267ef49570b957d"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Con falla",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 20 días",
  "cantidad_promedio_litros": 50,
  "observaciones": "Llega poca agua",
  "reportado_por": "Lider JAC",
  "barrio": "El molino",
  "Municipio": "Albania"
},
{
  "_id": {
    "$oid": "69150c01f267ef49570b957f"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Con falla",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 20 días",
  "cantidad_promedio_litros": 50,
  "observaciones": "Llega poca agua",
  "reportado_por": "Lider JAC",
  "barrio": "El molino",
  "Municipio": "Albania"
},
{
  "_id": {
    "$oid": "69150c53f267ef49570b9581"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Pozo artesanal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Ramon de luque",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69150c70f267ef49570b9583"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Pozo artesanal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Los olivos",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69150ca0f267ef49570b9585"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69150ca6f267ef49570b9587"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69150cabf267ef49570b9589"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69150cb1f267ef49570b958b"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69150cb7f267ef49570b958d"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69150cd2f267ef49570b958f"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "691519a6f267ef49570b9591"
  },
  "Municipio": "hatonuevo"
},
{
  "_id": {
    "$oid": "691519cbf267ef49570b9593"
  },
  "fecha_reporte": "2025/10/31"
},
{
  "_id": {
    "$oid": "691519f6f267ef49570b9595"
  },
  "fuente_agua": "Acometida municipal"
},
{
  "_id": {
    "$oid": "69151a0df267ef49570b9597"
  },
  "estado_fuente": "operativa"
},
{
  "_id": {
    "$oid": "69151a2ff267ef49570b9599"
  },
  "calidad_agua": "No apta para consumo"
},
{
  "_id": {
    "$oid": "69151a43f267ef49570b959b"
  },
  "frecuencia_acceso": "Cada 7 días"
},
{
  "_id": {
    "$oid": "69151a5af267ef49570b959d"
  },
  "cantidad_promedio_litros": 100
},
{
  "_id": {
    "$oid": "69151a6cf267ef49570b959f"
  },
  "observaciones": "Se compra por aparte"
},
{
  "_id": {
    "$oid": "69151a8bf267ef49570b95a1"
  },
  "reportado_por": "Lider JAC"
},
{
  "_id": {
    "$oid": "69151a9df267ef49570b95a3"
  },
  "barrio": "Villa comfamiliar"
},
{
  "_id": {
    "$oid": "69151ab3f267ef49570b95a5"
  },
  "barrio": "La loma"
},
{
  "_id": {
    "$oid": "69151ac9f267ef49570b95a7"
  },
  "barrio": "San Martin"
},
{
  "_id": {
    "$oid": "69151ae5f267ef49570b95a9"
  },
  "Municipio": "Maicao"
},
{
  "_id": {
    "$oid": "69151af6f267ef49570b95ab"
  },
  "Municipio": "Fonseca"
},
{
  "_id": {
    "$oid": "69151b0df267ef49570b95ad"
  },
  "Municipio": "Uribia"
},
{
  "_id": {
    "$oid": "69151b27f267ef49570b95af"
  },
  "Municipio": "San Juan"
},
{
  "_id": {
    "$oid": "69151b50f267ef49570b95b1"
  },
  "fuente_agua": "Carrotanque"
},
{
  "_id": {
    "$oid": "69151b60f267ef49570b95b3"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151b65f267ef49570b95b5"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151b6bf267ef49570b95b7"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151b71f267ef49570b95b9"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151b76f267ef49570b95bb"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151b7cf267ef49570b95bd"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151b86f267ef49570b95bf"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151b8bf267ef49570b95c1"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151b96f267ef49570b95c3"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151ba4f267ef49570b95c5"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151babf267ef49570b95c7"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151bb1f267ef49570b95c9"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "Acometiva municipal",
  "estado_fuente": "operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "Se compra por aparte",
  "reportado_por": "Lider JAC",
  "barrio": "Villa comfamiliar",
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151bbcf267ef49570b95ca"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151bbff267ef49570b95cb"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151bc2f267ef49570b95cc"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151bc4f267ef49570b95cd"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151bc6f267ef49570b95ce"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151bc8f267ef49570b95cf"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151bcbf267ef49570b95d0"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151bcdf267ef49570b95d1"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151bd4f267ef49570b95d2"
  },
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151bdaf267ef49570b95d3"
  },
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151bddf267ef49570b95d4"
  },
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Inactiva",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 1000,
  "observaciones": "No les llega agua",
  "reportado_por": "Consejal",
  "barrio": "Dividivi",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151beff267ef49570b95d5"
  },
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Inactiva",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 1000,
  "observaciones": "No les llega agua",
  "reportado_por": "Consejal",
  "barrio": "Dividivi",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151bf2f267ef49570b95d6"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151bf4f267ef49570b95d7"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151bf6f267ef49570b95d8"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151bf8f267ef49570b95d9"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151bf9f267ef49570b95da"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151bfbf267ef49570b95db"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151bfdf267ef49570b95dc"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151bfff267ef49570b95dd"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c02f267ef49570b95de"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c04f267ef49570b95df"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c06f267ef49570b95e0"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c07f267ef49570b95e1"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c09f267ef49570b95e2"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c0cf267ef49570b95e3"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c0ef267ef49570b95e4"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c10f267ef49570b95e5"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c12f267ef49570b95e6"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c14f267ef49570b95e7"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151c26f267ef49570b95e8"
  },
  "reportado_por": "Lider JAC"
},
{
  "_id": {
    "$oid": "69151c31f267ef49570b95e9"
  },
  "Municipio": "San Juan"
},
{
  "_id": {
    "$oid": "69151c3bf267ef49570b95ea"
  },
  "Municipio": "Hatonuevo"
},
{
  "_id": {
    "$oid": "69151c54f267ef49570b95eb"
  },
  "fecha_reporte": "2025/11/01"
},
{
  "_id": {
    "$oid": "69151c65f267ef49570b95ec"
  },
  "estado_fuente": "Sin servicio"
},
{
  "_id": {
    "$oid": "69151c74f267ef49570b95ed"
  },
  "calidad_agua": "Potable"
},
{
  "_id": {
    "$oid": "69151c94f267ef49570b95ee"
  },
  "fuente_agua": "carrotanque"
},
{
  "_id": {
    "$oid": "69151ca7f267ef49570b95ef"
  },
  "fecha_reporte": "2025/11/02"
},
{
  "_id": {
    "$oid": "69151cc6f267ef49570b95f0"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/11/05",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "JAC",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151cccf267ef49570b95f1"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151ccef267ef49570b95f2"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151cd9f267ef49570b95f3"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151ce5f267ef49570b95f4"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/11/05",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151ce8f267ef49570b95f5"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151cf1f267ef49570b95f6"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/11/04",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151d04f267ef49570b95f7"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/11/09",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "ENtre rios"
},
{
  "_id": {
    "$oid": "69151d1af267ef49570b95f8"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/11/07",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "Los olivos"
},
{
  "_id": {
    "$oid": "69151d2df267ef49570b95f9"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/11/12",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "La Lucha"
},
{
  "_id": {
    "$oid": "69151d31f267ef49570b95fa"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 500,
  "observaciones": "No alcanzo el agua",
  "reportado_por": "Consejal",
  "barrio": "7 de agosto"
},
{
  "_id": {
    "$oid": "69151d35f267ef49570b95fb"
  },
  "fecha_reporte": "2025/10/28",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Inactiva",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 7 días",
  "cantidad_promedio_litros": 1000,
  "observaciones": "No les llega agua",
  "reportado_por": "Consejal",
  "barrio": "Dividivi",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151d38f267ef49570b95fc"
  },
  "fecha_reporte": "2025/10/30",
  "fuente_agua": "Carrotanque",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 6 días",
  "cantidad_promedio_litros": 10,
  "observaciones": "Llevar mas agua",
  "reportado_por": "Lider JAC",
  "barrio": "Villa fatima",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69151d3ff267ef49570b95fd"
  },
  "fecha_reporte": "2025/10/31",
  "fuente_agua": "acometida municipal",
  "estado_fuente": "Operativa",
  "calidad_agua": "potable",
  "frecuencia_acceso": "Cada 4 días",
  "cantidad_promedio_litros": 100,
  "observaciones": "N/A",
  "reportado_por": "Lider JAC",
  "barrio": "Cooperativo",
  "Municipio": "Riohacha"
},
{
  "_id": {
    "$oid": "69154f74f267ef49570b9602"
  },
  "MUNICIPIO": "Riohacha",
  "fecha_reporte": "2025/11/12",
  "fuente_agua": "pozo comunitario",
  "estado_fuente": "Operativa",
  "calidad_agua": "No apta para consumo",
  "frecuencia_acceso": "Cada 2 días",
  "cantidad_promedio_litros": 300,
  "observaciones": "Agua con mal olor",
  "reportado_por": "Líder comunitario",
  "barrio": "Villa Fátima"
}]ding uni_ped.comf 2.json…]()

////******////
[
  {
    $group:
      //Esta instruccion es para sumar
      //los litros de agua recolectado en
      //todos los municipios.
      //Lo primero que hacemos es crear
      //una variable (total_litros) para pedir
      //los litros de agua recolectados
      //por cada municipio
      {
        _id: "$Municipio",
        total_litros: {
          $sum: "$cantidad_promedio_litros"
        }
      }
  },
  {
    $sort:
      //Una vez obtenidos los datos,
      //muestra el total de los litros
      //de agua se recolectada se ordenan
      //de mayor a menor.
      {
        total_litros: -1
      }
  },
  {
    $limit:
      //Por ultimo escogemos stage limit
      //para que nos muestre el total de la suma
      1
  }
]
[uni_ped.comf 2_suma.json](https://github.com/user-attachments/files/23551239/uni_ped.comf.2_suma.json)

[{
  "_id": null,
  "total_litros": 10400
}]
///*****////
[
  {
    $match:
      // en esta parte del codigo se
      //envia una instruccion para que me muestre
      //todos los datos referentes a Riohacha
      {
        Municipio: "Riohacha"
      }
    //Hemos realizado varios filtros para
    //poder analizar de manera más detallada
    //los datos recolectados acerca de la
    //recolección de agua para consumo.
    //se ha evidenciado que el municipio de albania
    //es uno de los mas afectados por lo
    //que necsita mayor prioridad para la
    //entrega de agua
  },
  {
    $group:
      //una vez obtenido los datos de
      //Riohacha, se envía para
      //sacar el promedio de litros de
      //agua recolectado por barrio
      {
        _id: "$barrio",
        promedioAguaRecolectada: {
          $avg: "$cantidad_promedio_litros"
        }
      }
  }
]
[uni_ped.comf 2_prom.json](https://github.com/user-attachments/files/23551244/uni_ped.comf.2_prom.json)
[{
  "_id": "Villa fatima",
  "promedioAguaRecolectada": 10
},
{
  "_id": "Cooperativo",
  "promedioAguaRecolectada": 100
},
{
  "_id": "Dividivi",
  "promedioAguaRecolectada": 1000
},
{
  "_id": "Entre Ríos",
  "promedioAguaRecolectada": 100
},
{
  "_id": "Las tunas",
  "promedioAguaRecolectada": 500
}]

//////*******//////
[
  {
    $match:
      //Esta instruccion es para ver
      //la frecuencia con que se recolecta
      //el agua cada 7 días.
      //primero llamamos la variable
      //frecuencia_acceso para que
      //nos muestre los datos
      {
        frecuencia_acceso: "Cada 7 días"
      }
  },
  {
    $group:
      //Una vez obtenidos los datos,
      //llamamos a la función contar
      //para que nos indique con que
      //frecuencia recolectan el agua
      //en cada municipio
      {
        _id: "$Municipio",
        count: {
          $sum: 1
        }
      }
  }
]
[uni_ped.comf 2_contar.json](https://github.com/user-attachments/files/23551246/uni_ped.comf.2_contar.json)
[{
  "_id": null,
  "count": 1
},
{
  "_id": "Hatonuevo",
  "count": 20
},
{
  "_id": "Riohacha",
  "count": 4
},
{
  "_id": "Maicao",
  "count": 1
}]
