---
title: Trabajar con proyectos y bases de datos de desarrollo de Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services, projects
ms.assetid: 39cf9166-fa92-40fe-9962-210a52461257
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c46155050b4772414f2f5e0d706cbca7dd1740db
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="work-with-analysis-services-projects-and-databases-in-development"></a>Trabajar con proyectos y bases de datos de desarrollo de Analysis Services
  Puede desarrollar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en modo de proyecto o en modo en línea.  
  
## <a name="single-developer"></a>Un solo programador  
 Si un solo programador va a desarrollar toda la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y todos los objetos que la forman, puede usar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en el modo de proyecto o en el modo en línea en cualquier momento del ciclo de vida de la solución de Business Intelligence. Si solo hay un programador, el modo que se elija no tiene demasiada importancia. El mantenimiento de un archivo de proyecto sin conexión integrado con un sistema de control de origen tiene muchas ventajas, por ejemplo el archivado y la reversión. Sin embargo, con un solo programador no existirá el problema de comunicación de cambios con otros programadores.  
  
## <a name="multiple-developers"></a>Varios programadores  
 Si hay varios programadores trabajando en una solución de Business Intelligence, se producirán problemas si no trabajan en modo de proyecto con control de origen en la mayoría de los casos, si no en todos. El control de origen garantiza que no haya dos programadores haciendo cambios en el mismo objeto a la vez.  
  
 Por ejemplo, imagine que hay un programador trabajando en modo de proyecto y haciendo cambios en objetos seleccionados. Suponga que, mientras el programador realiza estos cambios, hay otro programador que realiza un cambio en la base de datos implementada en el modo en línea. Cuando el primer programador trate de implementar su proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] modificado, se producirá un problema. Concretamente, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] detectará que los objetos de la base de datos implementada han cambiado y solicitará al programador que sobrescriba toda la base de datos, lo que sobrescribirá los cambios del segundo programador. Puesto que [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no puede resolver los cambios entre la instancia de base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y los objetos del proyecto que se va a sobrescribir, la única opción real que tiene el primer programador es la de rechazar todos sus cambios y volver a empezar desde cero con un nuevo proyecto basado en la versión actual de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
  