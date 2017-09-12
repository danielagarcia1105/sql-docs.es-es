---
title: "Tarea Volver a generar &#237;ndice | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.rebuildindextask.f1"
helpviewer_keywords: 
  - "volver a generar índices"
  - "índices [Integration Services]"
  - "Volver a generar índice, tarea"
ms.assetid: 021884dd-e72d-47b2-99e8-b741410509c3
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Tarea Volver a generar &#237;ndice
  La tarea Volver a generar índice vuelve a generar los índices de las tablas y vistas de bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para más información sobre la administración de índices, vea [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Un paquete puede usar la tarea Volver a generar índice para volver a generar los índices de una base de datos individual o de varias bases de datos. Si la tarea solo vuelve a generar los índices de una base de datos individual, puede elegir las vistas y las tablas cuyos índices vuelve a generar la tarea.  
  
 Esta tarea encapsula una instrucción ALTER INDEX REBUILD con las siguientes opciones para volver a generar el índice:  
  
-   Especifique un porcentaje de FILLFACTOR o use el valor original de FILLFACTOR.  
  
-   Establezca SORT_IN_TEMPDB = ON para almacenar el resultado intermedio de ordenación utilizado para volver a generar el índice en tempdb. Si se establece el resultado intermedio de ordenación en OFF, el resultado se almacena en la misma base de datos que el índice.  
  
-   Establezca PAD_INDEX = ON para asignar el espacio disponible especificado por FILLFACTOR a las páginas de nivel intermedio del índice.  
  
-   Establezca IGNORE_DUP_KEY = ON para permitir una operación de inserción de múltiples filas con registros que infringen restricciones UNIQUE para insertar los registros que no infringen las restricciones UNIQUE.  
  
-   Establezca ONLINE = ON para que no se mantengan los bloqueos de tabla, de forma que las consultas o actualizaciones de la tabla subyacente puedan continuar mientras se vuelve a generar el índice.  
  
    > [!NOTE]  
    >  Las operaciones de índices en línea no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
-   Especifique un valor para MAXDOP para establecer un límite para el número de procesadores utilizados en la ejecución de un plan paralelo.  
  
-   Especifique WAIT_AT_LOW_PRIORITY, MAX_DURATION y ABORT_AFTER_WAIT para controlar cuánto tiempo espera la operación de índice los bloqueos de prioridad baja.  
  
 Para más información sobre la instrucción ALTER INDEX y las opciones para volver a generar el índice, vea [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
> [!IMPORTANT]  
>  El tiempo que tarda la tarea en crear la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que va a ejecutar es proporcional al número de índices que se vuelven a generar. Si se configura la tarea para volver a generar los índices de todas las tablas y vistas de una base de datos que contiene una gran cantidad de índices, o para volver a generar los índices de varias bases de datos, la tarea puede tardar mucho tiempo en generar la instrucción Transact-SQL.  
  
## Configuración de la tarea Volver a generar índice  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Esta tarea se encuentra en la sección **Tareas del plan de mantenimiento** del **Cuadro de herramientas** , en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
 [Tarea Volver a generar índice &#40;Plan de mantenimiento&#41;](../../relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md)  
  
## Tareas relacionadas  
 Para más información sobre cómo establecer estas propiedades en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)], vea [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md).  
  
## Vea también  
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  