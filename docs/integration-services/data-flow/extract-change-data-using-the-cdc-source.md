---
title: Extraer los datos modificados mediante el origen de CDC | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 604fbafb-15fa-4d11-8487-77d7b626eed8
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 343efa882f37276c6921edc72d2bf1e615ff1a18
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="extract-change-data-using-the-cdc-source"></a>Extraer datos de modificaciones mediante el origen de CDC
  Para agregar y configurar un destino CDC, el paquete ya debe incluir por lo menos una tarea Flujo de datos y una tarea Control CDC.  
  
 Para obtener más información acerca del control CDC, vea [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).  
  
 Para obtener más información acerca del origen de CDC, vea [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
### <a name="to-extract-change-data-using-a-cdc-source"></a>Para extraer los datos modificados mediante un origen de CDC  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre el origen de CDC a la superficie de diseño.  
  
4.  Haga doble clic en el origen de CDC.  
  
5.  En el **Editor de origen de CDC** , en la página **Administrador de conexiones** , seleccione un administrador de conexiones ADO.NET de la lista o haga clic en **Nuevo** para crear una nueva conexión. La conexión debe estar en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contenga las tablas de modificaciones que se van a leer.  
  
6.  Seleccione **Tabla CDC** donde desea procesar los cambios.  
  
7.  Seleccione o escriba el nombre de la **instancia de captura CDC** con la tabla CDC que se va a leer.  
  
     Una tabla de origen capturada puede tener una o dos instancias capturadas para controlar que la transición de una definición de tabla a través de los cambios en el esquema se realice sin problemas. Si se define más de una instancia de captura para la tabla de origen que se va a capturar, seleccione aquí la instancia de captura que desee usar. El nombre de instancia de captura predeterminado para una tabla [esquema]. [tabla] es \<esquema > _\<tabla >, pero que pueden ser diferentes nombres de instancia de captura reales en uso. La tabla real que se lee desde es la tabla CDC **cdc.\< instancia de captura > _CT**.  
  
8.  Seleccione el modo de procesamiento que mejor controle las necesidades de procesamiento. Las opciones posibles son:  
  
    -   **Todos**: devuelve los cambios en el intervalo CDC actual sin los valores de **Antes de actualización** .  
  
    -   **Todos con valores antiguos**: devuelve los cambios en el intervalo de procesamiento CDC actual, incluidos los valores antiguos (**Antes de actualización**). Para cada operación de actualización habrá dos filas: una con los valores anteriores a la actualización y otra con los valores posteriores a la actualización.  
  
    -   **Neto**: devuelve una sola fila de cambios por cada fila de origen modificada en el intervalo de procesamiento de CDC actual. Si una fila de origen se actualizó varias veces, se genera el cambio combinado (por ejemplo, se genera insertar+actualizar como una actualización única y se genera actualizar+eliminar como una eliminación única). Al trabajar en el modo de procesamiento de cambios Neto, es posible dividir los cambios en salidas de eliminar, insertar y actualizar y controlarlos todos en paralelo, ya que la fila de origen única aparece en más de un resultado.  
  
    -   **Neto con máscara de actualización**: este modo es similar al modo neto normal pero también agrega columnas booleanas con el patrón de nombre **__ $\<nombre de columna >\__Changed** que indica la fila de cambio de las columnas cambiadas en la actual.  
  
    -   **Neto con combinación**: este modo es similar al modo Neto normal, pero con las operaciones de inserción y actualización combinadas en una sola operación de combinación (UPSERT).  
  
9. Seleccione la variable de paquete de la cadena de SSIS que mantenga el estado CDC para el contexto CDC actual. Para obtener más información sobre la variable de estado CDC, vea [Definir una variable de estado](../../integration-services/data-flow/define-a-state-variable.md).  
  
10. Active la casilla **Include reprocessing indicator column** (Incluir una columna de indicador de reprocesamiento) para crear una columna especial de salida denominada **__$reprocessing**. Esta columna tiene un valor **true** cuando el intervalo de procesamiento CDC se superpone con el intervalo de procesamiento inicial (el intervalo de LSN correspondiente al periodo de carga inicial) o cuando un intervalo de procesamiento CDC se vuelve a procesar tras un error en una ejecución anterior. Con esta columna de indicador, el desarrollador de SSIS puede controlar los errores de manera diferente a cuando se vuelven a procesar los cambios (por ejemplo, se pueden omitir acciones como la eliminación de una fila que no existe o una inserción que causó un error en una clave duplicada).  
  
     Para más información, consulte [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md).  
  
11. Para actualizar la asignación entre las columnas externas y de salida, haga clic en **Columnas** y seleccione diferentes columnas en la lista **Columna externa** .  
  
12. Opcionalmente, actualice los valores de las columnas de salida eliminando los valores en la lista **Columna de salida** .  
  
13. Para configurar la salida de error, haga clic en **Salida de error**.  
  
14. Puede hacer clic en **Vista previa** para ver hasta 200 filas de los datos extraídos por el origen de CDC.  
  
15. Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Editor de origen de CDC &#40; Página Administrador de conexiones &#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [Editor de origen de CDC &#40; Página columnas &#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)   
 [Editor de origen de CDC &#40; Página de salida de error &#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
  