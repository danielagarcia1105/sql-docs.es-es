---
title: ADCPROP_AUTORECALC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb10b3f4fb563275a8f27a92e41c265336c3cb55
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815723"
---
# <a name="adcpropautorecalcenum"></a>ADCPROP_AUTORECALC_ENUM
Especifica cuándo el [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) proveedor vuelve a calcular las columnas agregadas y calculadas en un conjunto de registros jerárquico.  
  
 Estas constantes se utilizan solo con el **MSDataShape** proveedor y el **Recordset** "**recálculo automático**" propiedad dinámica que se hace referencia en el [ADO Índice de propiedades dinámicas](../../../ado/reference/ado-api/ado-dynamic-property-index.md) y documentado en el [servicio de cursores de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) o [servicio de forma de datos de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) documentación.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Predeterminado: Vuelve a calcular cada vez que el **MSDataShape** proveedor determina han cambiado los valores que dependen de las columnas calculadas.|  
|**adRecalcUpFront**|0|Calcula sólo al generar inicialmente el jerárquica **Recordset**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Estas constantes no tienen equivalentes de ADO y WFC.
