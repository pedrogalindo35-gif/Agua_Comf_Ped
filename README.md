Tarea 4 – Almacenamiento y Consultas de Datos en Big Data (MongoDB)
Autor: Pedro Luis Galindo
Curso:*Big Data  
Grupo: 202016911_10  
Tutor:Jaime Rubiano Llorente  
Universidad Nacional Abierta y a Distancia – UNAD (2025)  

Se utilizó MongoDB Compass como herramienta para crear, cargar y analizar una base de datos denominada `bigdata_db`, con una colección llamada `sensores`.  
El caso de estudio representa un sistema de **monitoreo ambiental**, donde se registran lecturas de temperatura, humedad y fecha.  
El objetivo fue comprobar la eficiencia de MongoDB en la gestión de datos generados por dispositivos IoT.
Fase 1 – Investigación: Tipos de Bases de Datos NoSQL

| Tipo de Base de Datos | Características | Ventajas | Limitaciones | Casos de Uso |
|------------------------|-----------------|-----------|---------------|--------------|
| Clave–Valor | Almacena información en pares clave y valor. | Rápida, ideal para almacenamiento temporal. | No maneja relaciones entre datos. | Redis, Memcached. |
| Documentos | Usa formatos JSON o BSON. | Flexible y escalable horizontalmente. | Puede ser ineficiente si los documentos son muy grandes. | MongoDB, CouchDB. |
| Columnar | Organiza datos por columnas. | Excelente para análisis masivo. | No apta para transacciones. | Cassandra, HBase. |
| Grafos | Representa nodos y conexiones. | Ideal para redes y relaciones. | Compleja de implementar. | Neo4j, OrientDB. |
Conclusión: 
Entre los diferentes tipos, MongoDB fue elegido por su estructura flexible, su compatibilidad con datos semiestructurados y su capacidad de integración en proyectos de Big Data.
Fase 2 – Implementación en MongoDB
 Diseño de la Base de Datos
- Base: `bigdata_db`  
