---
title: "DATEADD (expresión de SSIS) | Documentos de Microsoft"
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
- dates [Integration Services], DATEADD
- dates [Integration Services]
- DATEADD function
ms.assetid: fa5c37b1-2ddc-4857-8f8e-f6d5643b654f
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 77230956969fb2fd2d27a1dec42140dd91a5cbd5
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="dateadd-ssis-expression"></a>DATEADD (expresión de SSIS)
  Devuelve un nuevo valor de tipo DT_DBTIMESTAMP tras agregar un número que representa una fecha o un intervalo de tiempo a la parte de fecha especificada de una fecha determinada. La evaluación del parámetro number debe devolver un entero y la del parámetro date debe devolver una fecha válida.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DATEADD(datepart, number, date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *parte de fecha*  
 Parámetro que especifica a qué parte de la fecha se agregará un número.  
  
 *number*  
 Valor que se usa para incrementar *datepart*. El valor debe ser de tipo entero y debe conocerse al analizar la expresión.  
  
 *date*  
 Expresión que devuelve una fecha válida o una cadena con formato de fecha.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_DBTIMESTAMP  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se incluyen las partes de fecha y las abreviaturas reconocidas por el evaluador de expresiones. En los nombres de partes de fecha no se distinguen mayúsculas de minúsculas.  
  
|parte de fecha|Abreviaturas|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Trimestre|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Day|dd, d|  
|Semana|wk, ww|  
|Weekday|dw, w|  
|Hour|Hh|  
|Minute|mi, n|  
|Second|ss, s|  
|Millisecond|Ms|  
  
 El argumento *number* debe estar disponible al analizar la expresión. Puede ser una constante o una variable. No pueden usarse valores de columnas porque estos valores no se conocen en el momento de analizar la expresión.  
  
 El argumento *datepart* debe entrecomillarse.  
  
 Un literal de tipo fecha debe convertirse explícitamente en uno de los tipos de datos de fecha. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 DATEADD devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Se producen errores si la fecha no es válida, si la unidad de fecha o de hora no se indica mediante una cadena, o si el incremento no es un entero estático.  
  
## <a name="ssis-expression-examples"></a>Ejemplos de expresiones de SSIS  
 Este ejemplo agrega un mes a la fecha actual.  
  
```  
DATEADD("Month", 1,GETDATE())  
```  
  
 Este ejemplo agrega 21 días a las fechas de la columna **ModifiedDate** .  
  
```  
DATEADD("day", 21, ModifiedDate)  
```  
  
 Este ejemplo agrega 2 años a un literal de fecha.  
  
```  
DATEADD("yyyy", 2, (DT_DBTIMESTAMP)"8/6/2003")  
```  
  
## <a name="see-also"></a>Vea también  
 [DATEDIFF &#40; Expresión de SSIS &#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40; Expresión de SSIS &#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DÍA &#40; Expresión de SSIS &#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MES &#40; Expresión de SSIS &#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [AÑO &#40; Expresión de SSIS &#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funciones &#40; Expresión de SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  