---
title: "Proporcionar una consulta de origen (Asistente para importaci&#243;n y exportaci&#243;n de SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.providesourcequery.f1"
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
caps.latest.revision: 61
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 57
---
# Proporcionar una consulta de origen (Asistente para importaci&#243;n y exportaci&#243;n de SQL Server)
Si ha especificado que quiere proporcionar una consulta para seleccionar los datos que se van a copiar, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Proporcionar una consulta de origen**. En esta página, escriba y pruebe la consulta SQL que selecciona los datos que se van a copiar desde el origen de datos en el destino. También puede pegar el texto de una consulta guardada o cargarlo desde un archivo.

## <a name="screen-shot-of-the-source-query-page"></a>Captura de pantalla de la página Consulta de origen  
La siguiente captura de pantalla muestra la página del asistente **Proporcionar una consulta de origen**.
 
En este sencillo ejemplo, el usuario quiere copiar todas las filas y columnas de la tabla **Sales.Customer**.
  
 ![Source query page of the Import and Export Wizard](../../integration-services/import-export-data/media/source-query.png "Source query page of the Import and Export Wizard")  

## <a name="provide-the-query-and-check-its-syntax"></a>Proporcionar la consulta y comprobar su sintaxis
**Instrucción SQL**  
 Escriba una consulta SELECT para recuperar filas de datos concretos de la base de datos de origen. También puede pegar el texto de una consulta guardada o cargarlo desde un archivo con la opción **Examinar**. 
  
 Por ejemplo, la siguiente consulta recupera **SalesPersonID**, **SalesQuota**y **SalesYTD** de la base de datos AdventureWorks para los vendedores con un porcentaje de comisión superior al 1,5 por ciento.  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  

Si el origen de datos es Excel, consulte [Proporcionar una consulta de origen para Excel](Provide%20a%20Source%20Query%20%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#excelQueries) más adelante en este tema para obtener información sobre cómo especificar rangos y hojas de cálculo de Excel en una consulta.

 Para más información sobre las consultas SELECT, seleccione [Ejemplos de SELECT Examples &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md) o haga una búsqueda en línea.  
  
 **Analizar**  
 Compruebe la sintaxis de la instrucción SQL que ha introducido en el cuadro de texto **Instrucción SQL**.  
  
> [!NOTE] Si el tiempo necesario para comprobar la sintaxis de la instrucción supera el valor de tiempo de espera de 30 segundos, el análisis se detiene y se genera un error. No podrá pasar esta página del asistente hasta que el análisis se realice correctamente. Una solución para evitar el tiempo de espera es crear una vista de base de datos basada en la consulta que quiere usar y luego consultar la vista desde el asistente, en lugar de escribir directamente el texto de la consulta.  
  
 **Examinar**  
 Seleccione un archivo guardado que contenga el texto de una instrucción SQL mediante el cuadro de diálogo **Abrir**. Al seleccionar un archivo se copiará el texto del archivo en el cuadro de texto **Instrucción SQL** .  
 
## <a name="a-nameexcelqueriesa-provide-a-source-query-for-excel"></a><a name="excelQueries"></a> Proporcionar una consulta de origen para Excel
Hay tres tipos de objetos de Excel que puede consultar.
-   **Hoja de cálculo.** Para consultar una hoja de cálculo, anexe el carácter $ al final del nombre de la hoja y agregue delimitadores alrededor de la cadena (por ejemplo, **[Hoja1$]**).

    ```
    SELECT * FROM [Sheet1$]
    ```

-   **Rango con nombre.** Para consultar un rango con nombre, use simplemente el nombre del rango (por ejemplo, **MiRangoDeDatos**).
    
    ```
    SELECT * FROM MyDataRange
    ```

-   **Rango sin nombre.** Para especificar un rango de celdas al que no ha asignado un nombre, anexe el carácter $ al final del nombre de la hoja, agregue la especificación del rango y agregue delimitadores alrededor de la cadena (por ejemplo, **[Hoja1$A1:B4]**).

    ```
    SELECT * FROM [Sheet1$A1:B4]
    ```

Tanto si especifica una hoja de cálculo o un rango como la tabla de origen, el controlador lee los bloques *contiguos* de celdas, comenzando con la primera celda no vacía en la esquina superior izquierda de la hoja de cálculo o rango. Como resultado, no puede haber filas vacías en los datos de origen. Por ejemplo, no puede haber una fila vacía entre los encabezados de columna y las filas de datos. Si hay un título seguido de filas vacías en la parte superior de la hoja de cálculo por encima de los datos, no se puede consultar la hoja de cálculo. En Excel, tiene que asignar un nombre al rango de datos y consultar el rango con nombre en lugar de la hoja de cálculo.

## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de escribir y probar la consulta SQL que selecciona los datos que se van a copiar, la siguiente página depende el destino de los datos.  
  
-   Para la mayoría de los destinos, la página siguiente es **Seleccionar tablas y vistas de origen**. En esta página, se revisa la consulta proporcionada y, opcionalmente, se eligen las columnas que se van a copiar y se obtiene una vista previa de los datos de ejemplo. Para más información, vea [Seleccionar tablas y vistas de origen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).  
  
-   Si el destino es un archivo plano, la página siguiente es **Configurar el destino del archivo plano**. En esta página, especifique las opciones de formato del archivo de destino plano. (Después de configurar el archivo plano, la página siguiente es **Seleccionar tablas y vistas de origen**). Para más información, vea [Configurar el destino del archivo plano](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  