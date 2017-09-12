---
title: Quitar una base de datos principal de un grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.availabilitygroup.removeprimarydb.f1
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 6d4ca31e-ddf0-44bf-be5e-a5da060bf096
caps.latest.revision: 28
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 64c6b353bb46dd08f69823e85826fc93553e6e0d
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="remove-a-primary-database-from-an-availability-group-sql-server"></a>Quitar una base de datos principal de un grupo de disponibilidad (SQL Server)
  En este tema se explica cómo quitar la base de datos principal y las bases de datos secundarias correspondientes del grupo de disponibilidad AlwaysOn mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Antes de empezar:**  
  
     [Requisitos previos y restricciones](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para quitar una base de datos de disponibilidad, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Seguimiento:**  [después de quitar una base de datos de disponibilidad de un grupo de disponibilidad](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos y restricciones  
  
-   Esta tarea solo se admite en las réplicas principales. Debe estar conectado a la instancia del servidor que hospeda la réplica principal.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para quitar una base de datos de disponibilidad**  
  
1.  En el Explorador de objetos, conéctese a la instancia del servidor que hospeda la réplica principal de la base de datos o bases de datos que se van a quitar y expanda el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Seleccione el grupo de disponibilidad y expanda el nodo **Bases de datos de disponibilidad** .  
  
4.  Este paso depende de si desea quitar varios grupos de bases de datos o solo una base de datos, del siguiente modo:  
  
    -   Para quitar varias bases de datos, use el panel **Detalles del Explorador de objetos** para ver y seleccionar todas las bases de datos que desea quitar. Para obtener más información, vea [Usar los detalles del Explorador de objetos para supervisar los grupos de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Para quitar una sola base de datos, selecciónela en el panel **Explorador de objetos** o el panel **Detalles del Explorador de objetos** .  
  
5.  Haga clic con el botón derecho en la base de datos o bases de datos seleccionadas y seleccione **Quitar base de datos del grupo de disponibilidad** en el menú de comandos.  
  
6.  En el cuadro de diálogo **Quitar bases de datos del grupo de disponibilidad** , para quitar todas las bases de datos enumeradas, haga clic en **Aceptar**. Si no desea quitar todos ellas, haga clic en **Cancelar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para quitar una base de datos de disponibilidad**  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica principal.  
  
2.  Use la instrucción [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) del siguiente modo:  
  
     ALTER AVAILABILITY GROUP *group_name* REMOVE DATABASE *availability_database_name*  
  
     donde *group_name* es el nombre del grupo de disponibilidad y *database_name* es el nombre de la base de datos que se va a quitar.  
  
     En el ejemplo siguiente se quita una base de datos denominada `Db6` del grupo de disponibilidad `MyAG` .  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG REMOVE DATABASE Db6;  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para quitar una base de datos de disponibilidad**  
  
1.  Cambie el directorio (**cd**) a la instancia del servidor que hospeda la réplica principal.  
  
2.  Use el cmdlet **Remove-SqlAvailabilityDatabase** , y especifique el nombre de la base de datos de disponibilidad que se va a quitar del grupo de disponibilidad. Cuando esté conectado a la instancia del servidor que hospeda la réplica principal, la base de datos principal y sus bases de datos secundarias correspondientes se quitarán en su totalidad del grupo de disponibilidad.  
  
     Por ejemplo, el comando siguiente quita la base de datos de disponibilidad `MyDb9` del grupo de disponibilidad denominado `MyAg`. Dado que este comando se ejecuta en la instancia del servidor que hospeda la réplica principal, la base de datos principal y todas sus bases de datos secundarias correspondientes se quitarán del grupo de disponibilidad. La sincronización de datos ya no se producirá para esta base de datos en ninguna réplica secundaria.  
  
    ```  
    Remove-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\PrimaryComputer\InstanceName\AvailabilityGroups\MyAg\Databases\MyDb9  
    ```  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet **Get-Help** en el entorno de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de PowerShell de SQL Server](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Seguimiento: después de quitar una base de datos de disponibilidad de un grupo de disponibilidad  
 La acción de quitar una base de datos de disponibilidad de su grupo de disponibilidad finaliza la sincronización de datos entre la base de datos principal anterior y las bases de datos secundarias correspondientes. La base de datos principal anterior permanece en línea. Cada base de datos secundaria correspondiente se pone en estado RESTORING.  
  
 En este momento hay formas alternativas de tratar una base de datos secundaria quitada:  
  
-   Si ya no necesita una base de datos secundaria, puede quitarla.  
  
     Para obtener más información, vea [Eliminar una base de datos](../../../relational-databases/databases/delete-a-database.md).  
  
-   Si desea obtener acceso a una base de datos secundaria quitada después de haberse quitado del grupo de disponibilidad, puede recuperar la base de datos. Sin embargo, si recupera una base de datos secundaria quitada, dos bases de datos independientes divergentes que tienen el mismo nombre estarán en línea. De asegurarse de que los clientes puedan tener acceso solo a una de ellas, generalmente la base de datos principal más reciente.  
  
     Para obtener más información, vea [Recuperar una base de datos sin restaurar los datos &#40;Transact-SQL&#41;](../../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Quitar una base de datos secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
  
