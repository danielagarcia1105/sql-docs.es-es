---
title: "Quitar una base de datos secundaria desde una configuración del trasvase de registros (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting secondary databases
- secondary databases [SQL Server], in log shipping
- removing secondary databases
- secondary data files [SQL Server], removing
- log shipping [SQL Server], secondary databases
ms.assetid: ebe368a4-ca1c-45d0-9a71-3ddbd5b26a8e
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9c0ced4d63693c2d299556a28796e55fccbcc2b5
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="remove-a-secondary-database-from-a-log-shipping-configuration-sql-server"></a>Quitar una base de datos secundaria desde una configuración del trasvase de registros (SQL Server)
  En este tema se describe cómo quitar una base de datos secundaria de trasvase de registros en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para quitar una base de datos secundaria de trasvase de registros con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Los procedimientos almacenados de trasvase de registros requieren que se pertenezca al rol fijo de servidor **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-remove-a-log-shipping-secondary-database"></a>Para quitar una base de datos secundaria de trasvase de registros  
  
1.  Conéctese a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que sea actualmente el servidor principal de trasvase de registros y expándala.  
  
2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos principal de trasvase de registros y, después, haga clic en **Propiedades**.  
  
3.  En **Seleccionar una página**, haga clic en **Trasvase de registro de transacciones**.  
  
4.  En **Instancias de servidores secundarios y bases de datos**, haga clic en la base de datos que desea quitar.  
  
5.  Haga clic en **Quitar**.  
  
6.  Haga clic en **Aceptar** para actualizar la configuración.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-remove-a-secondary-database"></a>Para quitar una base de datos secundaria  
  
1.  En el servidor principal, ejecute [sp_delete_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql.md) para eliminar la información sobre la base de datos secundaria en el servidor principal.  
  
2.  En el servidor secundario, ejecute [sp_delete_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md) para eliminar la base de datos secundaria.  
  
    > [!NOTE]  
    >  Si no hay ninguna otra base de datos secundaria con el mismo identificador secundario, se invoca **sp_delete_log_shipping_secondary_primary** desde **sp_delete_log_shipping_secondary_database** y elimina la entrada del identificador secundario y los trabajos de copia y restauración.  
  
3.  En el servidor secundario, deshabilite los trabajos de copia y restauración. Para obtener más información, consulte [Disable or Enable a Job](http://msdn.microsoft.com/library/5041261f-0c32-4d4a-8bee-59a6c16200dd).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Actualización del trasvase de registros a SQL Server 2016 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Configurar el trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)  
  
-   [Agregar una base de datos secundaria a la configuración de trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [Quitar el trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
-   [Ver el informe de trasvase de registros &#40;SQL Server Management Studio&#41;](../../database-engine/log-shipping/view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [Supervisar el trasvase de registros &#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)  
  
-   [Conmutar por error a una base de datos secundaria de trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Tablas y procedimientos almacenados de trasvase de registros](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  