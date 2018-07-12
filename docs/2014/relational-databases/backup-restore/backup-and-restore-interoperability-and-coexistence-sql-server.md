---
title: 'Copias de seguridad y restauración: interoperabilidad y coexistencia (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- file restores [SQL Server], related features
- restoring [SQL Server], files
- restoring files [SQL Server], related features
- backups [SQL Server], files or filegroups
- file backups [SQL Server], related features
ms.assetid: 69f212b8-edcd-4c5d-8a8a-679ced33c128
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 05d61a8b1c6ba7008cf25a4f7ce60fe9e2475de2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200565"
---
# <a name="backup-and-restore-interoperability-and-coexistence-sql-server"></a>Copias de seguridad y restauración: interoperabilidad y coexistencia (SQL Server)
  En este tema se describen las consideraciones de copias de seguridad y restauración para varias características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Entre estas características se incluyen restauración de archivos e inicio de bases de datos, restauración en línea e índices deshabilitados, creación de reflejo de la base de datos, y restauración por etapas e índices de texto completo.  
  
 **En este tema:**  
  
-   [Restaurar archivos e iniciar la base de datos](#FileRestoreAndDbStartup)  
  
-   [Restauración en línea e índices deshabilitados](#OnlineRestoreAndDisabledIndexes)  
  
-   [Creación de reflejo de la base de datos y copias de seguridad y restauración](#DbMandBnR)  
  
-   [Restauración por etapas e índices de texto completo](#PiecemealAndFTIndexes)  
  
-   [Copias de seguridad y restauración, y compresión de archivos](#FileBnRandCompression)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="FileRestoreAndDbStartup"></a> Restaurar archivos e iniciar la base de datos  
 Esta sección solo es pertinente para las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contienen varios grupos de archivos.  
  
> [!NOTE]  
>  Cuando se inicia una base de datos, solo se recuperarán y conectarán los grupos de archivo cuyos archivos estuvieran en línea al cerrar la base de datos.  
  
 Si se detecta algún problema durante el inicio de la base de datos, no se puede llevar a cabo la restauración y la base de datos se marca como SUSPECT. Si es posible aislar el problema en un archivo o una serie de archivos, el administrador de la base de datos puede dejar sin conexión los archivos en cuestión e intentar reiniciar la base de datos. Para dejar sin conexión un archivo se puede utilizar la siguiente instrucción [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) :  
  
 ALTER DATABASE *database_name* MODIFY FILE (nombre **='*`filename`*'**, sin conexión)  
  
 En caso de iniciarse correctamente, los grupos de archivos que contengan algún archivo sin conexión seguirán sin conexión.  
  
##  <a name="OnlineRestoreAndDisabledIndexes"></a> Restauración en línea e índices deshabilitados  
 Esta sección solo es relevante para las bases de datos que tienen varios grupos de archivos y, para el modelo de recuperación simple, al menos un grupo de archivos de solo lectura.  
  
 En estos casos, si una base de datos está en línea, su índice se puede crear, quitar, habilitar o deshabilitar solo si todos los grupos de archivos que contienen alguna parte del índice están en línea.  
  
 Para obtener información sobre cómo restaurar grupos de archivos sin conexión, vea [Restauración con conexión &#40;SQL Server&#41;](online-restore-sql-server.md).  
  
##  <a name="DbMandBnR"></a> Creación de reflejo de la base de datos y copias de seguridad y restauración  
 Esta sección solo es relevante para bases de datos con el modelo completo que contienen varios grupos de archivos.  
  
> [!NOTE]  
>  La característica de creación de reflejo de la base de datos se quitará en una versión futura de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Utilice [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] en su lugar.  
  
 Creación de reflejo de la base de datos es una solución para aumentar la disponibilidad de la base de datos. La creación de reflejo se implementa en cada una de las bases de datos y solo funciona con las que utilizan el modelo de recuperación completa. Para obtener más información, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
> [!NOTE]  
>  Para distribuir copias de un subconjunto de los grupos de archivos de una base de datos, utilice la replicación: replique solo los objetos de los grupos de archivos que desea copiar en otros servidores. Para obtener más información sobre la replicación, vea [Replicación de SQL Server](../../relational-databases/replication/sql-server-replication.md).  
  
### <a name="creating-the-mirror-database"></a>Crear la base de datos reflejada  
 La base de datos reflejada se crea mediante la restauración, WITH NORECOVERY, de copias de seguridad de la base de datos principal en el servidor reflejado. La restauración debe mantener el mismo nombre de la base de datos. Para obtener más información, vea [Preparar una base de datos reflejada para la creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
 Puede crear la base de datos reflejada mediante una secuencia de restauración por etapas, si se admite. Sin embargo, no puede empezar la creación de reflejos hasta que haya restaurado todos los grupos de archivos y, normalmente, las copias de seguridad de registros para que la base de datos reflejada quede suficientemente sincronizada con la base de datos principal. Para obtener más información, vea [Restauraciones por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md).  
  
### <a name="restrictions-on-backup-and-restore-during-mirroring"></a>Restricciones de la copia de seguridad y restauración durante la creación de reflejos  
 Mientras está activa una sesión de creación de reflejo de la base de datos, se aplican las restricciones siguientes:  
  
-   No se admite la copia de seguridad ni la restauración de la base de datos reflejada.  
  
-   Se admite la copia de seguridad de la base de datos principal, pero no se admite BACKUP LOG WITH NORECOVERY.  
  
-   No se admite la restauración de la base de datos principal.  
  
##  <a name="PiecemealAndFTIndexes"></a> Restauración por etapas e índices de texto completo  
 Esta sección solo resulta relevante para las bases de datos que contienen varios grupos de archivos y, en el caso de bases de datos de modelo simple, únicamente para los grupos de archivos de solo lectura.  
  
 Los índices de texto completo se almacenan en grupos de archivos de bases de datos y pueden verse afectados por una restauración por etapas. Si el índice de texto completo reside en el mismo grupo de archivos que alguno de los datos de la tabla asociada, la restauración por etapas funciona como cabría esperar.  
  
> [!NOTE]  
>  Para ver el identificador del grupo de archivos que contiene un índice de texto completo, seleccione la columna data_space_id de [sys.fulltext_indexes](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql).  
  
### <a name="full-text-indexes-and-tables-in-separate-filegroups"></a>Índices de texto completo y tablas en grupos de archivos independientes  
 Si un índice de texto completo reside en un grupo de archivos independiente de todos los datos de tablas asociadas, el comportamiento de la restauración por etapas depende de cuál de los grupos de archivos se restaure y se ponga en línea en primer lugar:  
  
-   Si el grupo de archivos que contiene el índice de texto completo se restaura y se pone en línea antes que los grupos de archivos que contienen los datos de la tabla asociada, la búsqueda de texto completo funciona según lo previsto en cuanto el índice de texto completo está en línea.  
  
-   Si el grupo de archivos que contiene los datos de las tablas se restaura y se pone en línea antes que el que contiene el índice de texto completo, el comportamiento de la búsqueda de texto completo puede verse afectado. Esto se debe a que las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] que desencadenan un rellenado o regeneran o reorganizan el catálogo generan un error hasta que el índice se pone en línea. Entre estas instrucciones se incluyen CREATE FULLTEXT INDEX, ALTER FULLTEXT INDEX, DROP FULLTEXT INDEX y ALTER FULLTEXT CATALOG.  
  
     En este caso, los siguientes factores son importantes:  
  
    -   Si el índice de texto completo dispone de seguimiento de cambios, el DML de usuario producirá un error hasta que el grupo de archivos de índice se ponga en línea. También se producirá un error en la operación de eliminación hasta que el grupo de archivos de índice esté en línea.  
  
    -   Independientemente del seguimiento de cambios, se produce un error en las consultas de texto completo porque el índice no está disponible. Si se intenta una consulta de texto completo cuando el grupo de archivos que contiene el índice de texto completo está sin conexión, se devuelve un error.  
  
    -   Las funciones de estado (por ejemplo, FULLTEXTCATALOGPROPERTY) tienen éxito únicamente cuando no han de obtener acceso al índice de texto completo. Por ejemplo, el acceso a los metadatos de texto completo en línea se realizaría correctamente, pero no sería así en el caso de **uniquekeycount, itemcount** .  
  
     Después de restaurar y poner en línea el grupo de archivos de índice de texto completo, los datos del índice y de las tablas son coherentes.  
  
 Tan pronto como el grupo de archivos de tabla base y el grupo de archivos de índice de texto completo estén en línea, se reanudarán los rellenados de texto completo pausados.  
  
##  <a name="FileBnRandCompression"></a> Copias de seguridad y restauración, y compresión de archivos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la compresión de datos del sistema de archivos NTFS de grupos de archivos y bases de datos de solo lectura.  
  
 Los archivos NTFS comprimidos admiten la restauración de archivos en un grupo de archivos de solo lectura. Las copias de seguridad y restauración de estos grupos de archivos funciona esencialmente de la misma manera que con cualquier grupo de archivos de solo lectura, con las siguientes excepciones:   
  
-   La restauración de un archivo de lectura y escritura (incluido el principal o los archivos de registro de una base de datos de lectura/escritura) en un volumen comprimido genera y muestra un error.  
  
-   Se permite la restauración de una base de datos de solo lectura en un volumen comprimido.  
  
> [!NOTE]  
>  Los archivos de registro de bases de datos de lectura/escritura no se deben almacenar en sistemas de archivos comprimidos.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Preparar una base de datos reflejada para la creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [Realizar copias de seguridad de los catálogos e índices de texto completo y restaurarlos](../search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
## <a name="see-also"></a>Vea también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](back-up-and-restore-of-sql-server-databases.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../replication/administration/back-up-and-restore-replicated-databases.md)   
 [Secundarias activas: Copia de seguridad en réplicas secundarias &#40;grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
  
  