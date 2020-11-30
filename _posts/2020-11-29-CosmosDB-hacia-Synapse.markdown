---
layout: post
title:  "Una arquitectura para analítica sobre data de microservicios en CosmosDB"
date:   2020-11-29 21:22:36 -0500
categories: tech
---
**Escenario**: Tenemos una aplicación moderna en Azure que usa múltiples microservicios y requiere una latencia de milisegundos. Si bien la magia de la app en sí la tienen resuelta los arquitectos que la diseñaron, lo que toca ahora es analizar la mejor manera de analizar la data. 

Por la forma en la que ha sido pensada esta aplicación, cada microservicio cuenta con su propia base de datos Cosmos DB, lo quiere decir que por diseño no existe consitencia entre estas diversas bases de datos... y eso está bien, pues cada Cosmos solo sabe lo que debe saber para atender a su microservicio. Por otro lado, por temas de economía, los datos en Cosmos DB tienen un TTL de 30 días y solo guardan el último mes de las transacciones. Es por estos motivos que existe la necesidad de consolidar la información para analítica y, al mismo tiempo, para que sirva de fuente al equipo de soporte a los usuarios.

**Solución**: Aprovechar la funcionalidad de Change Feed en Cosmos DB para agregar cada una de las transacciones realizadas en dos destinos: Un SQL Server que soportará los queries de los usuarios de soporte y aquellos reportes operativos más clásicos, y un almacenamiento tipo Azure Data Lake Storage que guardará toda la información generada por la aplicación en formato parquet. Aquí nuestro fiel Databricks se encargará de prepararla, limpiarla y depositarla en un pool dentro de Azure Synapse para los usuarios de analítica por SQL o Spark. 

![Arquitectura antigua](/img/CosmosDB to Synapse (Original).jpg)

**Optimización**: Esta primera arquitectura funciona muy bien pero siempre puede mejorarse. En particular buscamos sacarle provecho a nuevas funcionalidades de los productos en Azure, como es el caso de Synapse Link, para simplificar la arquitectura.

Los Cosmos DB entonces crearán réplicas columnares usando la característica de [Analytical Stores](https://docs.microsoft.com/en-us/azure/cosmos-db/analytical-store-introduction) que estarán expuestas directamente en Synapse, sin un proceso de ETL, en tiempo real. Ahora, ¿podemos optimizar en algo o aprocechar mejor la data en el ADLS? Pues si, gracias a [Query Acceleration](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-query-acceleration) y aprovechando el código en el que viene trabajando Pablo Mugica y su [nodbdb](https://github.com/PabloMugica/nodbdb), ahora las consultas sencillas de soporte pueden responderse haciendo queries directamente al storage.

![Arquitectura nueva](/img/CosmosDB to Synapse (New).jpg)

Y es así como se ve ahora... en el papel. Les cuento cuando la tengamos funcionando.