---
title: "Creación automática de código (Master Data Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 69642f63ac6d1f14090f6f368e1a46e1ab091e3d
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="automatic-code-creation-master-data-services"></a>Creación automática de código (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los valores numéricos pueden generarse automáticamente para el atributo Code o para cualquier otro atributo numérico. Cuando se generan códigos automáticamente, no se impide introducir otros valores para los códigos; en su lugar, se establece automáticamente un valor inicial.  
  
## <a name="generating-code-values"></a>Generar valores de código  
 Los administradores pueden configurar valores generados automáticamente para el atributo Code si modifican las propiedades asociadas de la entidad. Pueden especificar un valor inicial y cada valor subsiguiente aumentará en uno.  
  
 Al escribir valores de código en MDS, bien en una de las herramientas o mediante el proceso de almacenamiento provisional, puede dejar en blanco el valor de código, que se generará automáticamente. O bien, puede especificar el valor de código que desee.  
  
## <a name="generating-other-attribute-values"></a>Generar otros valores de atributo  
 Los administradores pueden generar automáticamente valores de atributos distintos de Code si crean reglas de negocios. Pueden especificar un valor inicial y especificar el número en que se incrementa cada valor siguiente.  
  
 Al escribir valores de atributo en MDS, ya sea en una de las herramientas o mediante el proceso de almacenamiento provisional, puede dejar en blanco el valor de atributo. Cuando se aplican reglas de negocios, los valores se incrementan en función del mayor valor existente. Por ejemplo, si la regla es 'establecer como atributo predeterminado para un valor generado que comienza en 1 y se incrementa en 4' y el valor actual más grande del atributo es 700, el valor del siguiente miembro que se agregue será 704.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Generar automáticamente valores para el atributo Code.|[Generar automáticamente valores para el atributo Code &#40;Master Data Services&#41;](../master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|Generar automáticamente valores para otros atributos.|[Generar automáticamente valores de atributo que no sean Code &#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Introducción a Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  