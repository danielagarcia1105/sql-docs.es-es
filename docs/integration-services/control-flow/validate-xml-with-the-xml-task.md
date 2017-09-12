---
title: Validar XML con la tarea XML | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML validation
- XML, validating
ms.assetid: 224fc025-c21f-4d43-aa9d-5ffac337f9b0
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 15e3873505601704c4a14d4e5701875b7dc104f5
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="validate-xml-with-the-xml-task"></a>Validar XML con la tarea XML
  Valide documentos XML y obtenga una salida de error enriquecida habilitando la propiedad **ValidationDetails** de la tarea XML.  
  
 La siguiente captura de pantalla muestra el **Editor de la tarea XML** con la configuración necesaria para la validación de XML con la salida de error completa.  
  
 ![Propiedades de la tarea XML en el Editor de la tarea XML](../../integration-services/control-flow/media/xmltaskproperties.jpg "propiedades de la tarea XML en el Editor de la tarea XML")  
  
 Antes de que la propiedad **ValidationDetails** estuviera disponible, la validación de XML efectuada mediante la tarea XML solo devolvía un resultado true o false, sin información sobre errores o sus ubicaciones. Ahora, al establecer **ValidationDetails** como true, el archivo de salida contiene información detallada sobre cada uno de los errores, incluido el número de línea y su posición. Puede usar esta información para comprender, buscar y corregir errores en documentos XML.  
  
 La funcionalidad de validación de XML se escala fácilmente en el caso de documentos XML grandes y un gran número de errores. Puesto que el propio archivo de salida está en formato XML, puede consultar y analizar la salida. Por ejemplo, si la salida contiene un gran número de errores, puede agruparlos mediante una consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] , como se describe en este tema.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) introdujo la **ValidationDetails** propiedad en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 2. La propiedad también está disponible en [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
## <a name="sample-output-for-xml-thats-valid"></a>Ejemplo de salida de un archivo XML que no es válido  
 Este es un ejemplo de archivo de salida con los resultados de validación de un archivo XML válido.  
  
```xml  
  
<root xmlns:ns="http://schemas.microsoft.com/xmltools/2002/xmlvalidation">  
    <metadata>  
        <result>true</result>  
        <errors>0</errors>  
        <warnings>0</warnings>  
        <startTime>2015-05-28T10:27:22.087</startTime>  
        <endTime>2015-05-28T10:29:07.007</endTime>  
        <xmlFile>d:\Temp\TestData.xml</xmlFile>  
        <xsdFile>d:\Temp\TestSchema.xsd</xsdFile>  
    </metadata>  
    <messages />  
</root>  
```  
  
## <a name="sample-output-for-xml-thats-not-valid"></a>Ejemplo de salida de un archivo XML que no es válido  
 Este es un ejemplo de archivo de salida con los resultados de validación de un archivo XML que contiene un pequeño número de errores. El texto de la \<error > elementos se ha ajustado para mejorar la legibilidad.  
  
```xml  
  
<root xmlns:ns="http://schemas.microsoft.com/xmltools/2002/xmlvalidation">  
    <metadata>  
        <result>false</result>  
        <errors>2</errors>  
        <warnings>0</warnings>  
        <startTime>2015-05-28T10:45:09.538</startTime>  
        <endTime>2015-05-28T10:45:09.558</endTime>  
        <xmlFile>C:\Temp\TestData.xml</xmlFile>  
        <xsdFile>C:\Temp\TestSchema.xsd</xsdFile>  
    </metadata>  
    <messages>  
        <error line="5" position="26">The 'ApplicantRole' element is invalid - The value 'wer3' is invalid  
    according to its datatype 'ApplicantRoleType' - The Enumeration constraint failed.</error>  
        <error line="16" position="28">The 'Phone' element is invalid - The value 'we3056666666' is invalid  
     according to its datatype 'phone' - The Pattern constraint failed.</error>  
    </messages>  
</root>  
```  
  
## <a name="analyze-xml-validation-output-with-a-transact-sql-query"></a>Analizar la salida de validación XML con una consulta de Transact-SQL  
 Si la salida de validación XML contiene un gran número de errores, puede usar una consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] para cargar la salida en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Luego, puede analizar la lista de errores con todas las funcionalidades del lenguaje T-SQL, como WHERE, GROUP BY, ORDER BY, JOIN, etc.  
  
```tsql  
DECLARE @xml XML;  
  
SELECT @xml = XmlDoc     
FROM OPENROWSET (BULK N'C:\Temp\XMLValidation_2016-02-212T10-41-00.xml', SINGLE_BLOB) AS Tab(XmlDoc);  
  
-- Query # 1, flat list of errors  
-- convert to relational/rectangular  
;WITH XMLNAMESPACES ('http://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS  
(  
SELECT col.value('@line','INT') AS line  
     , col.value('@position','INT') AS position  
     , col.value('.','VARCHAR(1024)') AS error  
FROM @XML.nodes('/root/messages/error') AS tab(col)  
)  
SELECT * FROM rs;  
-- WHERE error LIKE ‘%whatever_string%’  
  
-- Query # 2, count of errors grouped by the error message  
-- convert to relational/rectangular  
;WITH XMLNAMESPACES ('http://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS  
(  
SELECT col.value('@line','INT') AS line  
     , col.value('@position','INT') AS position  
     , col.value('.','VARCHAR(1024)') AS error  
FROM @XML.nodes('/root/messages/error') AS tab(col)  
)  
SELECT COALESCE(error,'Total # of errors:') AS [error], COUNT(*) AS [counter]  
FROM rs  
GROUP BY GROUPING SETS ((error), ())  
ORDER BY 2 DESC, COALESCE(error, 'Z');  
  
```  
  
 Este es el resultado de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] de la segunda consulta de ejemplo que se muestra en el texto anterior.  
  
 ![Consulta para agrupar errores de XML en Management Studio](../../integration-services/control-flow/media/queryforxmlerrors.jpg "consulta para agrupar errores de XML en Management Studio")  
  
## <a name="see-also"></a>Vea también  
 [Tarea XML](../../integration-services/control-flow/xml-task.md)   
 [Editor de la tarea XML &#40; Página general &#41;](../../integration-services/control-flow/xml-task-editor-general-page.md)  
  
  