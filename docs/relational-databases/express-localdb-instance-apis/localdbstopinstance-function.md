---
title: "Función LocalDBStopInstance | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: LocalDBStopInstance
apilocation: sqluserinstance.dll
apitype: DLLExport
ms.assetid: 4bd73187-0aac-4f03-ac54-2b78e41917e5
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f68a8e8b221783835dfee83dbe2337746064a2dc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="localdbstopinstance-function"></a>Función LocalDBStopInstance
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Detiene la instancia de SQL Server Express LocalDB especificada no se ejecuten.  
  
 **Archivo de encabezado:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT LocalDBStopInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           ULONG ulTimeout   
);  
```  
  
## <a name="parameters"></a>Parámetros  
 *pInstanceName*  
 [Entrada] Nombre de la instancia de LocalDB que se va a detener.  
  
 *dwFlags*  
 [Entrada] Un valor de marcador o una combinación de ellos que especifican la forma en la que detener la instancia.  
  
 Marcadores disponibles:  
  
 LOCALDB_SHUTDOWN_KILL_PROCESS  
 Cierre inmediato mediante el comando del sistema operativo de eliminar proceso.  
  
 LOCALDB_SHUTDOWN_WITH_NOWAIT  
 Cierre mediante el comando de Transact-SQL de la opción WITH NOWAIT.  
  
 Si no se establece ningún marcador, la instancia de LocalDB se cerrará con el comando de Transact-SQL SHUTDOWN. Si se han establecido ambos marcadores, tiene prioridad el marcador LOCALDB_SHUTDOWN_KILL_PROCESS.  
  
 *ulTimeout*  
 [Entrada] Tiempo en segundos que transcurrirá para que se complete esta operación. Si este valor es 0, esta función devolverá resultados inmediatamente sin esperar a que se detenga la instancia de LocalDB.  
  
## <a name="returns"></a>Devuelve  
 S_OK  
 La función se ha realizado correctamente.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB no está instalado en el equipo.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o más parámetros de entrada especificados no son válidos.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 El nombre de instancia de especificado no es válido.  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-instance.md)  
 La instancia no existe.  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../../relational-databases/express-localdb-error-messages/localdb-error-wait-timeout.md)  
 Se ha agotado el tiempo de espera mientras se intentaba adquirir bloqueos de sincronización.  
  
 [LOCALDB_ERROR_INSTANCE_STOP_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-instance-stop-failed.md)  
 La operación de detención no pudo completarse dentro del tiempo especificado.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 La ruta de acceso donde la instancia debe almacenarse es mayor que MAX_PATH.  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 No se puede recuperar una carpeta de perfil de usuario.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 No se puede tener acceso a una carpeta de la instancia.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 No se puede tener acceso a un registro de la instancia.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 Una configuración de instancia está dañada.  
  
 [LOCALDB_ERROR_CALLER_IS_NOT_OWNER](../../relational-databases/express-localdb-error-messages/localdb-error-caller-is-not-owner.md)  
 El autor de llamada de la API no es propietario de la instancia de LocalDB.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Error inesperado. Vea el registro de eventos para obtener detalles.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener un ejemplo de código que utilice LocalDB API, vea [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Información de encabezado y versión de SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  