---
title: "Tutorial: Replicar datos con clientes móviles | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 89f4810fae7ce3ee89b7b13f93f7f0298b93bace
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="tutorial-replicating-data-with-mobile-clients"></a>Tutorial: Replicar datos con clientes móviles
La replicación es una buena solución al problema de mover datos entre un servidor central y clientes móviles que solo se conectan en determinadas ocasiones. La utilización de asistentes para replicación le facilitará la configuración y administración de una topología de replicación. Este tutorial le mostrará cómo configurar una topología de replicación para clientes móviles.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
En este tutorial utilizará la replicación de mezcla para publicar datos de una base de datos central en uno o más usuarios móviles para que cada usuario obtenga un subconjunto de datos filtrado de manera exclusiva. En la primera lección se muestra cómo utilizar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear una publicación. Las lecciones posteriores muestran cómo crear y sincronizar una suscripción.  
  
## <a name="requirements"></a>Requisitos  
Este tutorial está destinado a usuarios que están familiarizados con las operaciones básicas de las bases de datos, pero que tienen una experiencia limitada en operaciones de replicación. Antes de comenzar este tutorial, debe completar el [Tutorial: Preparar el servidor para la replicación](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
Para utilizar este tutorial, el sistema debe tener instalados los siguientes componentes:  
  
-   En el publicador (servidor de origen):  
  
    -   Cualquier edición de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], excepto Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) o [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Estas ediciones no pueden ser publicadores de replicación.  
  
    -   La base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para mejorar la seguridad, las bases de datos de ejemplo no se instalan de manera predeterminada.  
  
-   En el suscriptor (servidor de destino):  
  
    -   Cualquier edición de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], excepto [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] no es compatible con la publicación creada en este tutorial.  
  
    > [!NOTE]  
    > La replicación no se instala de manera predeterminada en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
> [!NOTE]  
> En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], debe conectarse al publicador y al suscriptor con un inicio de sesión que sea miembro del rol fijo de servidor sysadmin.  
  
**Tiempo estimado para completar este tutorial: 30 minutos.**  
  
## <a name="lessons-in-this-tutorial"></a>Lecciones de este tutorial  
  
-   [Lección 1: Publicar datos con la replicación de mezcla](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)  
  
-   [Lección 2: Crear una suscripción a la publicación de combinación](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md)  
  
[Iniciar el tutorial](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)  
  
## <a name="see-also"></a>Vea también  
[Conceptos de la programación de replicación](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  
  
  
