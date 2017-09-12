---
title: "Asistente para generar esquemas (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "esquema relacional [Analysis Services]"
ms.assetid: 68bf7ba3-d0cb-437f-9a3e-9edc0999af19
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 16
---
# Asistente para generar esquemas (Analysis Services)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] admite dos métodos para trabajar con esquemas relacionales al definir objetos OLAP en un proyecto o base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Normalmente, los objetos OLAP se definen en función de un modelo de datos lógico creado en una vista de origen de datos de un proyecto o base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Esta vista del origen de datos se define en función de elementos de esquema de uno o varios orígenes de datos relacionales, personalizados en la vista del origen de datos.  
  
 Como alternativa, puede definir los objetos OLAP en primer lugar, y después generar una vista del origen de datos, un origen de datos y el esquema de la base de datos relacional subyacente que admite estos objetos OLAP. Esta base de datos relacional se conoce como base de datos del área de asunto.  
  
 En ocasiones, este método se denomina diseño de arriba abajo, y se usa a menudo para crear prototipos y modelos de análisis. Cuando se emplea este método, se usa el Asistente para generar esquemas para crear la vista del origen de datos y los objetos de origen de datos subyacentes basándose en los objetos OLAP definidos en un proyecto o base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Este es un método iterativo. Es muy probable que tenga que volver a ejecutar el Asistente varias veces mientras cambia el diseño de las dimensiones y los cubos. Cada vez que ejecute el Asistente, este incorporará los cambios en los objetos subyacentes y, en la medida de lo posible, conservará los datos contenidos en las bases de datos subyacentes.  
  
 El esquema que se genera es un esquema de motor de base de datos relacional de SQL Server. El Asistente no genera esquemas para otros productos de bases de datos relacionales.  
  
 Los datos con los que se rellena la base de datos del área de asunto se agregan de forma independiente mediante las herramientas y técnicas que se usan para rellenar una base de datos relacional de SQL Server. En la mayoría de los casos, al ejecutar el Asistente, se conservan los datos, pero hay excepciones. Por ejemplo, si se elimina una dimensión o un atributo que contiene datos, es necesario quitar algunos de ellos. Si el Asistente para generar esquemas debe borrar algunos datos debido a un cambio en el esquema, aparecerá una advertencia antes de eliminar los datos y se podrá cancelar el nuevo proceso de generación.  
  
 Como regla general, todo cambio que se realice en un objeto generado originalmente mediante el Asistente para generar esquemas se sobrescribe cuando el Asistente para generar esquemas vuelve a generar el objeto. La principal excepción a esta regla es cuando se agregan columnas a una tabla que haya generado el Asistente para generar esquemas. En este caso, el Asistente para generar esquemas conserva las columnas que se hayan agregado a la tabla, así como los datos de dichas columnas.  
  
## En esta sección  
 La tabla siguiente contiene una lista de temas adicionales en los que se explica cómo trabajar con el Asistente para generar esquemas.  
  
|Tema|Description|  
|-----------|-----------------|  
|[Usar el Asistente para generar esquemas &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/use-the-schema-generation-wizard-analysis-services.md)|Describe cómo generar el esquema para las bases de datos del área de asunto y del área de ensayo.|  
|[Descripción de esquemas de base de datos](../../analysis-services/multidimensional-models/understanding-the-database-schemas.md)|Describe el esquema que se genera para las bases de datos del área de asunto y del área de ensayo.|  
|[Descripción de la generación incremental](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)|Describe las capacidades de generación incremental del Asistente para generar esquemas.|  
  
## Vea también  
 [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Orígenes de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Orígenes de datos admitidos &#40;SSAS - Multidimensionales&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  