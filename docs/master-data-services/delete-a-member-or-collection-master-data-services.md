---
title: "Eliminar un miembro o colección (Master Data Services) | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collections [Master Data Services], deleting
- leaf members [Master Data Services], deleting
- deleting members [Master Data Services]
- members [Master Data Services], deleting
- consolidated members [Master Data Services], deleting
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 89e49964ef41c7d093a2bdba1673ae8ea44a4a70
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="delete-a-member-or-collection-master-data-services"></a>Eliminar un miembro o una colección (Master Data Services)
  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], elimine un miembro o recopilación cuando ya no lo necesite. Si desea eliminar miembros de forma masiva, en su lugar, utilice las tablas de almacenamiento provisional. Para obtener más información, consulte [Importar datos de tablas &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md)  
  
> [!NOTE]  
>  No puede eliminar un miembro si se utiliza como un valor de atributo basado en dominio para otro miembro.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   Para los miembros, debe tener como mínimo el permiso **Eliminar** para el objeto de modelo hoja del que vaya a eliminar un miembro.  
  
-   Para las colecciones, debe tener como mínimo el permiso **Actualizar** en el objeto de colección hoja que vaya a eliminar.  
  
### <a name="to-delete-a-member-or-collection"></a>Para eliminar un miembro o colección  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , en la lista **Modelo** , seleccione un modelo.  
  
2.  En la lista **Versión** , seleccione una versión.  
  
3.  Haga clic en **Explorador**.  
  
4.  Para eliminar:  
  
    -   Un miembro hoja, en la barra de menús, seleccione **Entidades** y haga clic en el nombre de la entidad que contenga el miembro.  
  
    -   Un miembro consolidado, en la barra de menús, seleccione **Jerarquías** y haga clic en el nombre de la entidad que contenga el miembro. Después, haga clic en el nodo de la jerarquía que contiene el miembro.  
  
    -   Una colección, en la barra de menús, elija **Colecciones** y haga clic en el nombre de la entidad que contenga la colección.  
  
5.  En la cuadrícula, haga clic en la fila correspondiente al miembro o colección que desea eliminar.  
  
6.  Haga clic en **Eliminar miembro**, en **Eliminar**o en **Eliminar colección**.  
  
7.  Los administradores de la entidad también verán una opción de menú para purgar (eliminación permanente) de todos los miembros eliminados temporalmente en la versión de la entidad.  
  
8.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Reactivar un miembro o una colección &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [Los miembros &#40; Master Data Services &#41;](../master-data-services/members-master-data-services.md)   
 [Colecciones de &#40; Master Data Services &#41;](../master-data-services/collections-master-data-services.md)  
  
  