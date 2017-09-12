---
title: "RTRIM (expresión de SSIS) | Documentos de Microsoft"
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
- RTRIM function
- trailing blanks
ms.assetid: 529bd43e-3f8a-4682-a33e-569176aa7fc4
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 83882b11a5b0f262857c1d291e8dbefcd22a2531
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="rtrim-ssis-expression"></a>RTRIM (expresión de SSIS)
  Devuelve una expresión de caracteres después de quitar los espacios finales.  
  
> [!NOTE]  
>  RTRIM no quita los caracteres de espacio en blanco, como los caracteres de tabulación o de salto de línea. Unicode proporciona puntos de código para muchos tipos distintos de espacios, pero su función solo reconoce el punto de código Unicode 0x0020. Cuando se convierten cadenas del juego de caracteres de doble byte (DBCS) a Unicode, éstas pueden incluir caracteres de espacio distintos de 0x0020 y la función no puede eliminarlos. Para eliminar cualquier tipo de espacio, puede utilizar el método RTrim de Microsoft Visual Basic .NET en un script ejecutado desde el componente Script.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RTRIM(character expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres de la que puede quitar espacios.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentarios  
 RTRIM solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR se convertirá implícitamente al tipo de datos DT_WSTR antes de que RTRIM realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para obtener más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 RTRIM devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo quita los espacios finales de un literal de cadena. El resultado devuelto es "Hello".  
  
```  
RTRIM("Hello   ")  
```  
  
 Este ejemplo quita los espacios finales de una concatenación de las columnas **FirstName** y **LastName** .  
  
```  
RTRIM(FirstName + " " + LastName)  
```  
  
 Este ejemplo quita los espacios finales de la variable **FirstName** .  
  
```  
RTRIM(@FirstName)  
```  
  
## <a name="see-also"></a>Vea también  
 [LTRIM &#40; Expresión de SSIS &#41;](../../integration-services/expressions/ltrim-ssis-expression.md)   
 [RECORTE &#40; Expresión de SSIS &#41;](../../integration-services/expressions/trim-ssis-expression.md)   
 [Funciones &#40; Expresión de SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  