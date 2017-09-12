---
title: "Interfaz de usuario del Diseñador de consultas MDX de Analysis Services | Documentos de Microsoft"
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
f1_keywords:
- "10012"
- sql13.rtp.rptdesigner.dataview.asquerydesigner.f1
helpviewer_keywords:
- MDX [Reporting Services], creating datasets
- query designers [Reporting Services]
ms.assetid: d9c7c0b3-fce4-4a65-b679-408273e6a925
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7f8838c9793cfc4a8e38bea3f0f27e702dd27e4d
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="analysis-services-mdx-query-designer-user-interface"></a>Interfaz de usuario del Diseñador de consultas MDX de Analysis Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona diseñadores gráficos de consultas para crear consultas MDX (Expresiones multidimensionales) y consultas DMX (Expresiones de minería de datos) para un origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . En este tema se describe el diseñador de consultas MDX. Para más información sobre el diseñador de consultas DMX, vea [Tipo de conexión de Analysis Services para DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md).  
  
 El diseñador gráfico de consultas MDX tiene dos modos: modo de diseño y modo de consulta. Cada modo proporciona un panel de metadatos desde el que puede arrastrar miembros de los cubos seleccionados para crear una consulta MDX; ésta recupera datos al procesarse el informe.  
  
> [!IMPORTANT]  
>  Los usuarios tienen acceso a los orígenes de datos cuando crean y ejecutan las consultas. Debe conceder permisos mínimos para los orígenes de datos, por ejemplo permisos de solo lectura.  
  
> [!NOTE]  
>  No se admite la importación de una consulta .mdx desde un archivo.  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>Diseñador gráfico de consultas MDX en modo de diseño  
 Al editar una consulta MDX para un conjunto de datos de informe, el diseñador gráfico de consultas MDX se abre en modo de diseño.  
  
 En la siguiente ilustración se indican los nombres de los paneles del modo de diseño.  
  
 ![Diseñador de consultas de Analysis Services MDX, la vista Diseño](../../reporting-services/report-data/media/rsqd-dsawas-mdx-designmode.gif "Diseñador de consultas MDX de Analysis Services, vista de diseño")  
  
 En la tabla siguiente aparecen los paneles de este modo:  
  
|Panel|Función|  
|----------|--------------|  
|Botón Selección de cubo (**...**)|Muestra el cubo seleccionado actualmente.|  
|Panel Metadatos|Muestra una lista jerárquica de medidas, indicadores clave de rendimiento (KPI) y dimensiones definidas en el cubo seleccionado.|  
|Panel Miembros calculados|Muestra los miembros calculados definidos actualmente que se encuentran disponibles para utilizarse en la consulta.|  
|Panel Filtro|Se utiliza a fin de elegir dimensiones y jerarquías relacionadas para filtrar datos en el origen y limitar datos devueltos al informe.|  
|Panel Datos|Muestra los encabezados de columna del conjunto de resultados mientras arrastra elementos de los paneles Metadatos y Miembros calculados. Actualiza automáticamente el conjunto de resultados si el botón **Ejecución automática** está seleccionado. .|  
  
 Puede arrastrar dimensiones, medidas y KPI desde el panel Metadatos, y los miembros calculados desde el panel Miembros calculados al panel Datos. En el panel Filtro, puede seleccionar dimensiones y jerarquías relacionadas, y establecer expresiones de filtro para limitar los datos disponibles en la consulta. Si el **ejecución automática** (![ejecutar la consulta automáticamente](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "ejecutar la consulta automáticamente")) se selecciona el botón de alternancia en la barra de herramientas, el Diseñador de consultas ejecuta la consulta cada vez que coloque un objeto de metadatos en el panel de datos. También puede ejecutar manualmente la consulta con la **ejecutar** (![ejecutar la consulta](../../reporting-services/report-data/media/rsqdicon-run.gif "ejecutar la consulta")) en la barra de herramientas.  
  
 Al crear una consulta MDX en este modo, se incluyen automáticamente en la consulta las propiedades adicionales siguientes:  
  
 **Propiedades de miembro** MEMBER_CAPTION, MEMBER_UNIQUE_NAME  
  
 **Propiedades de la celda** VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
  
 Si desea especificar sus propias propiedades adicionales, debe modificar manualmente la consulta MDX en el modo de consulta.  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>Barra de herramientas del diseñador gráfico de consultas MDX en modo de diseño  
 La barra de herramientas del diseñador de consultas proporciona botones que le ayudan a diseñar consultas MDX mediante la interfaz gráfica. En la tabla siguiente se describen los botones y sus funciones.  
  
|Botón|Description|  
|------------|-----------------|  
|**Editar como texto**|No está habilitado para este tipo de origen de datos.|  
|**Importar**|Importa una consulta existente desde un archivo de definición de informe (.rdl) del sistema de archivos. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Cambiar a la vista de consulta MDX](../../reporting-services/report-data/media/rsqdicon-commandtypemdx.gif "cambiar a la vista de consulta MDX")|Cambia al tipo de comando MDX.|  
|![Cambiar a la vista de lenguaje de consulta DMX](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "cambiar a la vista de lenguaje de consulta DMX")|Cambia al tipo de comando DMX.|  
|![Actualizar datos de resultados](../../reporting-services/report-data/media/rsqdicon-refresh.gif "actualizar datos de resultados")|Actualiza los metadatos desde el origen de datos.|  
|![Add calculated member](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.gif "Add calculated member")|Muestra el cuadro de diálogo **Generador de miembros calculados** .|  
|![Alternar para mostrar celdas vacías](../../reporting-services/report-data/media/rsqdicon-showemptycells.gif "alternar para mostrar celdas vacías")|Muestra y oculta las celdas vacías del panel Datos. Esto equivale a utilizar la cláusula NON EMPTY en MDX.|  
|![Ejecutar la consulta automáticamente](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "ejecutar la consulta automáticamente")|Ejecuta automáticamente la consulta y muestra el resultado cada vez que se realiza un cambio. Los resultados se mostrarán en el panel Datos.|  
|![Botón Mostrar agregaciones](../../reporting-services/report-data/media/rsqdicon-showaggregations.gif "botón Mostrar agregaciones")|Muestra agregaciones en el panel Datos.|  
|![Eliminar](../../reporting-services/report-data/media/rsqdicon-delete.gif "Eliminar")|Elimina la columna seleccionada en el panel Datos de la consulta.|  
|![Icono para el cuadro de diálogo de parámetros de consulta](../../reporting-services/report-data/media/iconqueryparameter.gif "icono para el cuadro de diálogo de parámetros de consulta")|Muestra el cuadro de diálogo **Parámetros de consulta** . Al especificar valores para un parámetro de consulta, se crea automáticamente un parámetro de informe con el mismo nombre. El valor del parámetro de consulta se establece en una expresión que hace referencia al parámetro de informe.|  
|![Botón de consulta de preparación](../../reporting-services/report-data/media/rsqdicon-preparequery.gif "botón Preparar consulta")|Prepara la consulta.|  
|![Ejecutar la consulta](../../reporting-services/report-data/media/rsqdicon-run.gif "Ejecutar la consulta")|Ejecuta la consulta y muestra los resultados en el panel Datos.|  
|![Cancelar la consulta](../../reporting-services/report-data/media/rsqdicon-cancel.gif "cancelar la consulta")|Cancela la consulta.|  
|![Cambiar al modo de diseño](../../reporting-services/media/rsqdicon-designmode.gif "cambiar al modo de diseño")|Alterna el modo de diseño y el modo de consulta.|  
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>Diseñador gráfico de consultas MDX en modo de consulta  
 Para cambiar el diseñador gráfico de consultas al modo **Consulta** , haga clic en el botón **Modo de diseño** de la barra de herramientas.  
  
 En la ilustración siguiente se indican los nombres de los paneles del modo de consulta.  
  
 ![Vista de diseñador, consultas de Analysis Services MDX consulta](../../reporting-services/report-data/media/rsqd-dsawas-mdx-querymode.gif "diseñador, vista de consulta de MDX de Analysis Services consulta")  
  
 En la tabla siguiente aparecen los paneles de este modo:  
  
|Panel|Función|  
|----------|--------------|  
|Botón Selección de cubo (**...**)|Muestra el cubo seleccionado actualmente.|  
|Panel Metadatos/Funciones/Plantillas|Muestra una lista jerárquica de medidas, KPI y dimensiones definidas en el cubo seleccionado.|  
|Panel de consulta|Muestra el texto de consulta.|  
|Panel Resultado|Muestra los resultados de la ejecución de la consulta.|  
  
 El panel Metadatos muestra pestañas de **Metadatos**, **Funciones**y **Plantillas**. Desde la pestaña **Metadatos** , puede arrastrar dimensiones, jerarquías, KPI y medidas al panel Consulta MDX. Desde la pestaña **Funciones** , puede arrastrar funciones hasta el panel Consulta MDX. Desde la pestaña **Plantillas** , puede agregar plantillas MDX al panel Consulta MDX. Cuando ejecute la consulta, en el panel Resultado se mostrarán los resultados de la consulta MDX.  
  
 Puede ampliar la consulta MDX predeterminada generada en modo de diseño para que incluya propiedades de miembro y de celda adicionales. Al ejecutar la consulta, estos valores no aparecen en el conjunto de resultados. Sin embargo, se devuelven a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y puede usarlos en un informe. Para más información, vea [Propiedades de campo extendidas para una base de datos de Analysis Services &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>Barra de herramientas del diseñador gráfico de consultas en modo de consulta  
 La barra de herramientas del diseñador de consultas proporciona botones que le ayudan a diseñar consultas MDX mediante la interfaz gráfica.  
  
 Los botones de la barra de herramientas son idénticos en los modos de diseño y de consulta. Sin embargo, los siguientes botones no están habilitados para el modo de consulta:  
  
-   **Editar como texto**  
  
-   **Agregar miembro calculado** (![Add calculated member](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **Mostrar celdas vacías** (![alternar para mostrar celdas vacías](../../reporting-services/report-data/media/rsqdicon-showemptycells.gif "alternar para mostrar celdas vacías"))  
  
-   **Ejecución automática** (![ejecutar la consulta automáticamente](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "ejecutar la consulta automáticamente"))  
  
-   **Mostrar agregaciones** (![botón Mostrar agregaciones](../../reporting-services/report-data/media/rsqdicon-showaggregations.gif "botón Mostrar agregaciones"))  
  
## <a name="see-also"></a>Vea también  
 [Definir parámetros en el Diseñador de consultas MDX de Analysis Services &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md)   
 [Crear un conjunto de datos compartido o conjunto de datos incrustado &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Tipo de conexión de Analysis Services para DMX &#40; SSRS &#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [Archivo de configuración RSReportDesigner](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [Tipo de conexión de Analysis Services para MDX &#40; SSRS &#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
  