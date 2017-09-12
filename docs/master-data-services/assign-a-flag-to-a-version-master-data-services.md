---
title: "Asignar una marca a una versión (Master Data Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- version flags [Master Data Services], assigning flags
- versions [Master Data Services], assigning flags
ms.assetid: 6629ec7e-32e7-4a1e-8b31-eb43c5923766
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2fe233f28ef0fd602e775f90b5fae083a96a1848
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="assign-a-flag-to-a-version-master-data-services"></a>Asignar una marca a una versión (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], asigne una marca a una versión para indicar la versión que los usuarios o los sistemas que se suscriben deberían utilizar.  
  
> [!NOTE]  
>  Solo se pueden asignar marcas de versión a una versión al mismo tiempo. Si asigna una marca que ya está asignada a otra versión, se mueve a la versión que seleccionó.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer del permiso para tener acceso al área funcional de **Administración de versiones** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Debe haber creado una marca de versión para asignarla. Para obtener más información, vea [Crear una marca de versión &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md).  
  
-   Debe disponer del permiso para tener acceso al área funcional de Administración de versiones. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### <a name="to-assign-a-flag-to-a-version"></a>Asignar una marca a una versión  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración de versiones**.  
  
2.  En la página **Administrar versiones** , en la fila de la versión a la que quiere asignar una marca, haga doble clic en la celda de la columna **Marca** .  
  
3.  En la lista, seleccione la marca que desea asignar.  
  
    > [!NOTE]  
    >  Si la marca que desea no está disponible, puede que solo esté disponible para versiones **Confirmado** . Para confirmar, ir a la página **Administrar marcas de versión** y ver el campo **Solo versiones confirmadas** para la marca.  
  
4.  Presione ENTRAR para guardar el cambio.  
  
## <a name="see-also"></a>Vea también  
 [Crear una marca de versión &#40; Master Data Services &#41;](../master-data-services/create-a-version-flag-master-data-services.md)   
 [Versiones de &#40; Master Data Services &#41;](../master-data-services/versions-master-data-services.md)  
  
  