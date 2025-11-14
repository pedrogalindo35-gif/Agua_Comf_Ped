**Tarea 4** – Almacenamiento y Consultas de Datos en Big Data (MongoDB)
<br>**Autor:** Pedro Luis Galindo
<br>**Curso:** Big Data  
**Grupo:** 202016911_10  
**Tutor:** Jaime Rubiano Llorente  
**Universidad Nacional Abierta y a Distancia – UNAD** 
<br>**Fecha:** noviembre 2025 

**INTRODUCCIÓN**<br>En este ejercicio vamos a desarrollar una base de datos donde haremos consultas y filtraremos información de los datos obtenidos en la recolección de agua de los barrios en diferentes municipios de la Guajira. Utilizaremos MongoDB Compass como herramienta para crear, cargar y analizar una base de datos denominada `com_agua`, con una colección llamada `beneficiarios`.  

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
  - `frecuencia _accseo` → Cada cuantos dias recolectan agua.
  - `cantidad_promedio` → cuantos litros logran recolectar.
  - `obsevaciones` → anotaciones importantes.
  - `reportado_por` → persona a cargo.
  - `barrio` → zona donde se recibe el agua.
    
 Carga de Base de Datos con los 100 documentos:




