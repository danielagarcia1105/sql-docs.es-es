---
title: Información general sobre los Cmdlets de PowerShell para grupos de disponibilidad AlwaysOn (SQL Server) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], PowerShell cmdlets
- Availability Groups [SQL Server], about
- PowerShell [SQL Server], cmdlets
ms.assetid: b3fef0d5-b6d7-4386-a0f0-d06c165ad4de
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 3d3b1715a61ed7711217148a3a42bbcd5340308a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113442"
---
# <a name="overview-of-powershell-cmdlets-for-alwayson-availability-groups-sql-server"></a>Información general de los cmdlets de PowerShell para grupos de disponibilidad AlwaysOn (SQL Server)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] PowerShell es un shell de línea de comandos basado en tareas y un lenguaje de scripting diseñado especialmente para la administración del sistema. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] proporciona un conjunto de cmdlets de PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que le permiten implementar, administrar y supervisar grupos de disponibilidad, réplicas de disponibilidad y bases de datos de disponibilidad.  
  
> [!NOTE]  
>  Un cmdlet de PowerShell se puede completar correctamente iniciando una acción. Esto no indica que el trabajo previsto, como la conmutación por error de un grupo de disponibilidad se haya completado. Cuando se genera el script de una secuencia de acciones, puede que tenga que comprobar el estado de las acciones y esperar a que se completen.  
  
 En este tema se describen los cmdlets de los siguientes conjuntos de tareas:  
  
-   [Configurar una instancia de servidor para grupos de disponibilidad AlwaysOn](#ConfiguringServerInstance)  
  
-   [Realizar copias de seguridad y restaurar bases de datos y registros de transacciones](#BnRcmdlets)  
  
-   [Crear y administrar un grupo de disponibilidad](#DeployManageAGs)  
  
-   [Crear y administrar un agente de escucha de un grupo de disponibilidad](#AGlisteners)  
  
-   [Crear y administrar una réplica de disponibilidad](#DeployManageARs)  
  
-   [Agregar y administrar una base de datos de disponibilidad](#DeployManageDbs)  
  
-   [Supervisar el estado de grupos de disponibilidad](#MonitorTblshtAGs)  
  
> [!NOTE]  
>  Para obtener una lista de temas de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] libros en pantalla que se describe cómo usar los cmdlets para realizar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] tareas, vea la sección "Tareas relacionadas" de [información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="ConfiguringServerInstance"></a> Configurar una instancia de servidor para grupos de disponibilidad AlwaysOn  
  
|Cmdlets|Descripción|Se admite en|  
|-------------|-----------------|------------------|  
|`Disable-SqlAlwaysOn`|Deshabilita la característica [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en una instancia de servidor.|La instancia de servidor especificada por el parámetro `Path`, `InputObject` o `Name`. (Debe ser una edición de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que admita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]).|  
|`Enable-SqlAlwaysOn`|Habilita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en una instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que admite la característica [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Para obtener información sobre la compatibilidad con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).|Cualquier edición de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que admite [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].|  
|`New-SqlHadrEndPoint`|Crea un nuevo extremo de creación de reflejo de la base de datos en una instancia de servidor. Este extremo es necesario para el movimiento de datos entre las bases de datos principal y secundaria.|Cualquier instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|`Set-SqlHadrEndpoint`|Cambia las propiedades de un extremo de creación de reflejo de la base de datos existente, como el nombre, el estado o las propiedades de autenticación.|Una instancia de servidor que admite [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y no tiene un extremo de creación de reflejo de la base de datos|  
  
##  <a name="BnRcmdlets"></a> Backing Up and Restoring Databases and Transaction Logs  
  
|Cmdlets|Descripción|Se admite en|  
|-------------|-----------------|------------------|  
|`Backup-SqlDatabase`|Crea una copia de seguridad de datos o del registro.|Cualquier base de datos en línea (en el caso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], una base de datos de la instancia del servidor que hospeda la réplica principal)|  
|`Restore-SqlDatabase`|Restaura una copia de seguridad.|Cualquier instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (en el caso de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], una instancia de servidor que hospeda una réplica secundaria)<br /><br /> **\*\* Importante \* \***  al preparar una base de datos secundaria, debe usar el `-NoRecovery` parámetro en cada `Restore-SqlDatabase` comando.|  
  
 Para obtener más información sobre cómo usar estos cmdlets para preparar una base de datos secundaria, vea [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
##  <a name="DeployManageAGs"></a> Creating and Managing an Availability Group  
  
|Cmdlets|Descripción|Se admite en|  
|-------------|-----------------|------------------|  
|`New-SqlAvailabilityGroup`|Crea un nuevo grupo de disponibilidad.|Instancia del servidor para hospedar la réplica principal|  
|`Remove-SqlAvailabilityGroup`|Elimina un grupo de disponibilidad.|Instancia del servidor habilitada para HADR|  
|`Set-SqlAvailabilityGroup`|Establece las propiedades de un grupo de disponibilidad; poner en línea o sin conexión un grupo de disponibilidad|Instancia del servidor que hospeda la réplica principal|  
|`Switch-SqlAvailabilityGroup`|Inicia una de las siguientes formas de conmutación por error<br /><br /> Una conmutación por error forzada de un grupo de disponibilidad (con posible pérdida de datos).<br /><br /> Una conmutación por error manual de un grupo de disponibilidad.|Instancia del servidor que hospeda la réplica secundaria de destino|  
  
##  <a name="AGlisteners"></a> Creating and Managing an Availability Group Listener  
  
|Cmdlet|Descripción|Se admite en|  
|------------|-----------------|------------------|  
|`New-SqlAvailabilityGroupListener`|Crea un nuevo agente de escucha del grupo de disponibilidad y lo adjunta a un grupo de disponibilidad existente.|Instancia del servidor que hospeda la réplica principal|  
|`Set-SqlAvailabilityGroupListener`|Modifica la configuración del puerto en un agente de escucha del grupo de disponibilidad existente.|Instancia del servidor que hospeda la réplica principal|  
|`Add-SqlAvailabilityGroupListenerStaticIp`|Agrega una dirección IP estática a una configuración de agente de escucha del grupo de disponibilidad existente. La dirección IP estática puede ser una dirección IPv4 con subred o una dirección IPv6.|Instancia del servidor que hospeda la réplica principal|  
  
##  <a name="DeployManageARs"></a> Creating and Managing an Availability Replica  
  
|Cmdlets|Descripción|Se admite en|  
|-------------|-----------------|------------------|  
|**New-SqlAvailabilityReplica**|Crea una nueva réplica de disponibilidad. Puede usar el `-AsTemplate` parámetro para crear un objeto de réplica de disponibilidad en memoria para cada nueva réplica de disponibilidad.|Instancia del servidor que hospeda la réplica principal|  
|`Join-SqlAvailabilityGroup`|Combina una réplica secundaria con el grupo de disponibilidad.|Instancia del servidor que hospeda la réplica secundaria|  
|**Remove-SqlAvailabilityReplica**|Elimina una réplica de disponibilidad.|Instancia del servidor que hospeda la réplica principal|  
|`Set-SqlAvailabilityReplica`|Establece las propiedades de una réplica de disponibilidad.|Instancia del servidor que hospeda la réplica principal|  
  
##  <a name="DeployManageDbs"></a> Adding and Managing an Availability Database  
  
|Cmdlets|Descripción|Se admite en|  
|-------------|-----------------|------------------|  
|**Add-SqlAvailabilityDatabase**|En la réplica principal, agrega una base de datos a un grupo de disponibilidad.<br /><br /> En una réplica secundaria, une una base de datos secundaria a un grupo de disponibilidad.|Cualquier instancia del servidor que hospeda una réplica de disponibilidad (el comportamiento difiere entre las réplicas principal y secundaria)|  
|**Remove-SqlAvailabilityDatabase**|En la réplica principal, quita del grupo de disponibilidad la base de datos.<br /><br /> En una réplica secundaria, quita la base de datos secundaria local de la réplica secundaria local.|Cualquier instancia del servidor que hospeda una réplica de disponibilidad (el comportamiento difiere entre las réplicas principal y secundaria)|  
|`Resume-SqlAvailabilityDatabase`|Reanuda el movimiento de datos en una base de datos de disponibilidad suspendida.|La instancia de servidor en la que se ha suspendido la base de datos.|  
|`Suspend-SqlAvailabilityDatabase`|Suspende el movimiento de datos en una base de datos de disponibilidad.|Cualquier instancia de servidor que hospeda una réplica de disponibilidad.|  
  
##  <a name="MonitorTblshtAGs"></a> Monitoring Availability Group Health  
 Los cmdlets siguientes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permiten supervisar el estado de un grupo de disponibilidad y sus réplicas y bases de datos.  
  
> [!IMPORTANT]  
>  Debe tener permisos CONNECT, VIEW SERVER STATE y VIEW ANY DEFINITION para ejecutar estos cmdlets.  
  
|Cmdlet|Descripción|Se admite en|  
|------------|-----------------|------------------|  
|`Test-SqlAvailabilityGroup`|Evalúa el estado de un grupo de disponibilidad mediante la evaluación de las directivas de administración basada en directivas (PBM) de SQL Server.|Cualquier instancia de servidor que hospeda una réplica de disponibilidad.*|  
|`Test-SqlAvailabilityReplica`|Evalúa el estado de las réplicas de disponibilidad mediante la evaluación de las directivas de administración basada en directivas (PBM) de SQL Server.|Cualquier instancia de servidor que hospeda una réplica de disponibilidad.*|  
|`Test-SqlDatabaseReplicaState`|Evalúa el estado de una base de datos de disponibilidad en todas las réplicas de disponibilidad mediante la evaluación de directivas de administración basada en directivas (PBM) de SQL Server.|Cualquier instancia de servidor que hospeda una réplica de disponibilidad.*|  
  
 *Para ver información acerca de todas las réplicas de disponibilidad en un grupo de disponibilidad, use la instancia del servidor que hospeda la réplica principal.  
  
 Para obtener más información, consulte [usar directivas de AlwaysOn para ver el estado de un grupo de disponibilidad &#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
  