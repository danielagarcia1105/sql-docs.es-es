---
title: ¿Qué es la instancia maestra?
titleSuffix: SQL Server 2019 big data clusters
description: En este artículo se describe la instancia principal de SQL Server en un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 778645079d2585bd86fc01c5d5e1130c564b0de5
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2019
ms.locfileid: "54242016"
---
# <a name="what-is-the-master-instance-in-a-sql-server-2019-big-data-cluster"></a>¿Qué es la instancia maestra en un clúster de macrodatos de 2019 de SQL Server?

En este artículo se describe el rol de la *instancia principal de SQL Server* en un clúster de macrodatos de SQL Server 2019. La instancia maestra es una instancia de SQL Server que se ejecuta en un clúster de SQL Server macrodatos [plano de control](big-data-cluster-overview.md#controlplane).

La instancia principal de SQL Server proporciona la funcionalidad siguiente:

## <a name="connectivity"></a>Conectividad

La instancia principal de SQL Server proporciona un punto de conexión accesible desde el exterior de TDS para el clúster. Puede conectar aplicaciones o herramientas de SQL Server, como Azure Data Studio o SQL Server Management Studio para este extremo, tal como lo haría cualquier otra instancia de SQL Server.

## <a name="scale-out-query-management"></a>Administración de la consulta de escalabilidad horizontal

La instancia principal de SQL Server contiene el motor de consultas de escalabilidad horizontal que se utiliza para distribuir las consultas entre instancias de SQL Server en nodos de la [proceso grupo](concept-compute-pool.md). El motor de consultas de escalado horizontal también proporciona acceso a través de Transact-SQL para todas las tablas de Hive en el clúster sin ninguna configuración adicional. (Compatibilidad con las tablas de hive no está en CTP 2.2)

## <a name="metadata-and-user-databases"></a>Bases de datos de usuario y los metadatos

Además de las bases de sistema de SQL Server estándares, la instancia de SQL principal también contiene lo siguiente:

- Una base de datos de metadatos que contiene los metadatos de la tabla de HDFS
- Un mapa de particiones de plano de datos
- Detalles de las tablas externas que proporcionan acceso al plano de datos de clúster.
- Orígenes de datos externos de PolyBase y tablas externas definidas en las bases de datos de usuario.

También puede agregar sus propias bases de datos de usuario a la instancia principal de SQL Server.

## <a name="machine-learning-services"></a>Servicios Machine learning

Servicios de aprendizaje automático de SQL Server es una característica incluida en el motor de base de datos, utilizado para ejecutar código de Java, R y Python en SQL Server. Esta característica se basa en el marco de extensibilidad de SQL Server que aísla los procesos externos de los procesos del motor principal, pero se integra completamente con los datos relacionales, como procedimientos almacenados, como script de Transact-SQL que contiene instrucciones de R o Python o como Java, R o Código de Python que contiene la instrucción T-SQL.

Como parte de un clúster de macrodatos de SQL Server, servicios de machine learning estará disponibles en la instancia principal de SQL Server de forma predeterminada. Esto significa que una vez que la ejecución de scripts externos está habilitada en la instancia principal de SQL Server, se va a ser posible ejecutar Java, scripts de R y Python mediante sp_execute_external_script.

### <a name="advantages-of-machine-learning-services-in-a-big-data-cluster"></a>Ventajas de machine learning services en un clúster de macrodatos

SQL Server 2019 facilita big data a combinarse con los datos de dimensiones suelen almacenados en la base de datos empresarial. El valor de los datos de gran tamaño aumenta en gran medida cuando no está en manos de partes de una organización, pero también se incluye en los informes, paneles y aplicaciones. Al mismo tiempo, los científicos de datos pueden seguir usar las herramientas del ecosistema de Spark o HDFS y fácil, tener acceso en tiempo real a los datos en la instancia principal de SQL Server y orígenes de datos externos accesibles _a través de_ el maestro de SQL Server instancia de.

Con los clústeres de SQL Server 2019 datos de gran tamaño, puede hacer más con los lagos de datos de empresa. Los analistas y programadores de SQL Server pueden:

* Cree aplicaciones que consumen datos de lagos de datos de empresa.
* Motivo de todos los datos con consultas Transact-SQL.
* Utilice el ecosistema de herramientas de SQL Server y las aplicaciones existente para tener acceso y analizar datos empresariales.
* Reducir la necesidad de movimiento de datos a través de la virtualización de datos y data marts.
* Continuar a usar Spark para escenarios de macrodatos.
* Compilar aplicaciones empresariales inteligentes mediante Spark o SQL Server para entrenar modelos a través de lagos de datos.
* Utilizar modelos de bases de datos de producción para un mejor rendimiento.
* Datos de Stream directamente en puestos de datos empresarial para análisis en tiempo real.
* Explorar datos visualmente mediante un análisis interactivo y herramientas de BI.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, consulte la información general siguiente:

- [¿Qué son los clústeres de macrodatos de 2019 de SQL Server?](big-data-cluster-overview.md)
