---
title: 'Las siguientes características no son compatibles con Excel Services y no se muestren o que se muestren solo parcialmente: comentarios, formas u otros objetos | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ade92e15-dfbf-496b-9378-a00bd83ba750
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 16269f5c0d7b3d64c9639862995dee44146efb9e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188705"
---
# <a name="the-following-features-are-not-supported-by-excel-services-and-may-not-display-or-may-display-only-partially-comments-shapes-or-other-objects"></a>Las siguientes características no se admiten en Servicios de Excel y puede que no se muestren o que se muestren solo parcialmente: comentarios, formas u otros objetos
  Este error se produce al agregar segmentaciones a un libro PowerPivot desde una lista de campos de PowerPivot.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a|PowerPivot para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Excel Web Access no puede representar el objeto Forma que se usa para controlar la posición y el formato de las segmentaciones agregadas a un libro de la lista de campos de PowerPivot.|  
|Texto del mensaje|Servicios de Excel no admite las siguientes características y puede que no se muestren o se muestren solo parcialmente:<br /><br /> Comentarios, formas o otros objetos<br /><br /> Algunas características, como las consultas de datos externos, muestran datos en caché que solo pueden actualizarse en Microsoft Excel.|  
  
## <a name="explanation"></a>Explicación  
 Excel Web Access muestra este error al abrir un libro PowerPivot en un explorador y hace clic en el **detalles** botón para el mensaje, **no admitido características libro es posible que no se muestre como está previsto**.  
  
 Este error se produce porque el libro PowerPivot contiene segmentaciones cuyo diseño es controlado por un objeto Forma oculto en Excel. El objeto Forma controla el formato y la posición de las segmentaciones en la posición horizontal y vertical.  
  
 Servicios de Excel no puede representar un objeto Forma, pero dado que el objeto está oculto, este hecho no constituye un problema.  
  
## <a name="user-action"></a>Acción del usuario  
 Se puede omitir este error. Haga clic en **Aceptar** para cerrar el mensaje de error y continuar utilizar el libro y las segmentaciones sin problema.  
  
  
