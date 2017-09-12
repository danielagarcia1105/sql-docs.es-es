---
title: "NULL (expresión de SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- NULL function
- null values [Integration Services]
ms.assetid: df144237-3fbb-41ac-8624-efd92b6522b9
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3c3be5273bd31a2a812c96fac458b8b173e14b3b
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="null-ssis-expression"></a>NULL (expresión de SSIS)
  Devuelve un valor NULL asociado al tipo de datos solicitado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NULL(typespec)  
```  
  
## <a name="arguments"></a>Argumentos  
 *typespec*  
 Tipo de datos válido. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Cualquier tipo de datos válido con valor NULL.  
  
## <a name="remarks"></a>Comentarios  
 NULL devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Para solicitar un valor NULL para algunos tipos de datos es necesario utilizar parámetros. En la tabla siguiente se muestran estos tipos de datos y sus parámetros.  
  
|Tipo de datos|Parámetro|Ejemplo|  
|---------------|---------------|-------------|  
|DT_STR|*charcount*<br /><br /> *codepage*|(DT_STR,30,1252) convierte 30 caracteres al tipo de datos DT_STR con la página de códigos 1252.|  
|DT_WSTR|*charcount*|(DT_WSTR,20) convierte 20 caracteres al tipo de datos DT_WSTR.|  
|DT_BYTES|*bytecount*|(DT_BYTES,50) convierte 50 bytes al tipo de datos DT_BYTES.|  
|DT_DECIMAL|*escala*|(DT_DECIMAL,2) convierte un valor numérico al tipo de datos DT_DECIMAL con una escala de 2.|  
|DT_NUMERIC|*precisión*<br /><br /> *escala*|(DT_NUMERIC,10,3) convierte un valor numérico al tipo de datos DT_NUMERIC con una precisión de 10 decimales y una escala de 3.|  
|DT_TEXT|*codepage*|(DT_TEXT,1252) convierte un valor al tipo de datos DT_TEXT con la página de códigos 1252.|  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Estos ejemplos devuelven el valor NULL asociado a los tipos de datos DT_STR, DT_DATE y DT_BOOL.  
  
```  
NULL(DT_STR,10,1252)  
NULL(DT_DATE)  
NULL(DT_BOOL)  
```  
  
## <a name="see-also"></a>Vea también  
 [ISNULL &#40; Expresión de SSIS &#41;](../../integration-services/expressions/isnull-ssis-expression.md)   
 [Funciones &#40; Expresión de SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  