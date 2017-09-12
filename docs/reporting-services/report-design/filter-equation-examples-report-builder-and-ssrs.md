---
title: Filtrar los ejemplos de ecuaciones (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtering data [Reporting Services], filter equation examples
ms.assetid: 66bec93d-7c3b-4d4a-8cb6-7a7bb2f34ec6
caps.latest.revision: 18
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6bbd95ac20afbeb00b331efa13492a0036fff20
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="filter-equation-examples-report-builder-and-ssrs"></a>Ejemplos de ecuaciones de filtro (Generador de informes y SSRS)
  Para crear un filtro, debe especificar una o varias ecuaciones de filtro. Una ecuación de filtro incluye una expresión, un tipo de datos, un operador y un valor. En este tema, se proporcionan ejemplos de filtros usados habitualmente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="filter-examples"></a>Ejemplos de filtros  
 En la tabla siguiente, se muestran ejemplos de ecuaciones de filtro que usan tipos de datos y operadores diferentes. El elemento de informe para el que se define un filtro determina el ámbito de la comparación. Por ejemplo, para un filtro definido en un conjunto de datos, **TOP % 10** es el 10 por ciento de los valores más altos del conjunto de datos; para un filtro definido en un grupo, **TOP% 10** es el 10 por ciento de los valores más altos del grupo.  
  
|Expresión simple|Tipo de datos|Operador|Value|Description|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|**Integer**|**>**|`7`|Incluye valores de datos que son mayores que 7.|  
|`[SUM(Quantity)]`|**Integer**|**TOP N**|`10`|Incluye los 10 valores de datos más altos.|  
|`[SUM(Quantity)]`|**Integer**|**TOP %**|`20`|Incluye el 20% de los valores de datos más altos.|  
|`[Sales]`|**Texto**|**>**|`=CDec(100)`|Incluye todos los valores de tipo System.Decimal (tipos de datos "money" de SQL) mayores que $100.|  
|`[OrderDate]`|**DateTime**|**>**|`2008-01-01`|Incluye todas las fechas desde el 1 de enero de 2008 hasta la fecha actual.|  
|`[OrderDate]`|**DateTime**|**BETWEEN**|`2008-01-01`<br /><br /> `2008-02-01`|Incluye las fechas desde el 1 de enero de 2008 hasta el 1 de febrero de 2008, inclusive.|  
|`[Territory]`|**Texto**|**LIKE**|`*east`|Todos los nombres de territorios que terminan en "east".|  
|`[Territory]`|**Texto**|**LIKE**|`%o%th*`|Todos los nombres de territorios que incluyen North y South al principio del nombre.|  
|`=LEFT(Fields!Subcat.Value,1)`|**Texto**|**IN**|`B, C, T`|Todos los valores de subcategoría que comienzan con las letras B, C o T.|  
  
## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40; El generador de informes y el Diseñador de informes &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Tipos de datos en expresiones &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Usar expresiones en informes &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  