---
title: MSSQL_ENG002601 | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG002601 error
ms.assetid: 657c3ae6-9e4b-4c60-becc-4caf7435c1dc
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2454732812315b948f11f3a78fcc531bf87fbf0b
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng002601"></a>MSSQL_ENG002601
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2601|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico|N/A|  
|Texto del mensaje|No se puede insertar una fila de clave duplicada en el objeto '%.*ls' con índice único '%.\*ls'.|  
  
## <a name="explanation"></a>Explicación  
 Se trata de un error general que puede producirse independientemente de que la base de datos esté replicada o no. En las bases de datos replicadas, el error suele producirse cuando las claves principales no se han administrado adecuadamente en la topología. En un entorno distribuido es fundamental asegurarse de que no se inserta el mismo valor en una columna de clave principal o en otra columna única en más de un nodo. Entre las posibles causas figuran:  
  
-   Se están llevando a cabo inserciones y actualizaciones en una fila en más de un nodo. Tanto la replicación de mezcla como las suscripciones actualizables de la replicación transaccional ofrecen detección y resolución de conflictos, aunque es preferible insertar o actualizar una fila concreta solo en un nodo. La replicación transaccional del mismo nivel no ofrece detección y resolución de conflictos; exige que las inserciones y las actualizaciones estén divididas en particiones.  
  
-   Se ha insertado una fila en un suscriptor que debería ser de solo lectura. Los suscriptores de publicaciones de instantáneas deben tratarse como de solo lectura, al igual que los suscriptores de publicaciones transaccionales, a menos que se utilicen suscripciones actualizables o replicación transaccional del mismo nivel.  
  
-   Se está utilizando una tabla con una columna de identidad, pero la columna no está correctamente administrada.  
  
-   En la replicación de mezcla, este error puede producirse también durante una inserción en la tabla del sistema **MSmerge_contents**; el error que se produce es similar al siguiente: No se puede insertar una fila de clave duplicada en el objeto 'MSmerge_contents' con índice único 'ucl1SycContents'.  
  
## <a name="user-action"></a>Acción del usuario  
 La acción que debe llevarse a cabo depende del motivo por el que se produjo el error:  
  
-   Se están llevando a cabo inserciones y actualizaciones en una fila en más de un nodo.  
  
     Independientemente del tipo de replicación utilizada, se recomienda que, siempre que sea posible, las inserciones y las actualizaciones se dividan en particiones, ya que esto reduce el procesamiento necesario para la detección y resolución de conflictos. En la replicación transaccional del mismo nivel, se exige dividir en particiones las inserciones y las actualizaciones. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
-   Se ha insertado una fila en un suscriptor que debería ser de solo lectura.  
  
     No inserte ni actualice filas en el suscriptor a menos que esté utilizando replicación de mezcla, replicación transaccional con suscripciones actualizables o replicación transaccional del mismo nivel.  
  
-   Se está utilizando una tabla con una columna de identidad, pero la columna no está correctamente administrada.  
  
     En la replicación de mezcla y la replicación transaccional con suscripciones actualizables, las columnas de identidad deben ser administradas automáticamente por la replicación. En la replicación transaccional de punto a punto, es necesario administrarlas manualmente. Para obtener más información, vea [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
-   El error se produce durante una inserción en la tabla del sistema **MSmerge_contents**.  
  
     Este error se puede producir debido a un valor incorrecto de la propiedad del filtro de combinación **join_unique_key**. Esta propiedad debe definirse como TRUE solo si la columna combinada de la tabla primaria es única. El error se produce si la propiedad se define como TRUE pero la columna no es única. Para obtener más información acerca de cómo configurar esta propiedad, vea [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  