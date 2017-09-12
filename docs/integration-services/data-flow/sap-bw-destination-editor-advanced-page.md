---
title: "Editor de destino de SAP BW (página avanzadas) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sapbwdestination.advanced.f1
ms.assetid: 862957db-bbc6-4dda-bc0e-591457f1baa7
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e15c7e770bc46c3ddc3a9f58ae99a5440617720d
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-destination-editor-advanced-page"></a>Editor de destino de SAP BW (página Avanzadas)
  Use la página **Opciones avanzadas** del **Editor de destino de SAP BW** para establecer los valores de configuración avanzada como el tamaño del paquete y la información de tiempo de espera.  
  
 Para más información sobre el destino SAP BW de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vea [Destino de SAP BW](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 **Para abrir la página Opciones avanzadas**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el destino SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el destino de SAP BW.  
  
3.  En **Editor de destino de SAP BW**, haga clic en **Opciones avanzadas** para abrir la página **Opciones avanzadas** del editor.  
  
## <a name="options"></a>Opciones  
  
> [!NOTE]  
>  Si no conoce todos los valores necesarios para configurar el destino, puede que tenga que ponerse en contacto con el administrador de SAP.  
  
 **Tamaño de paquete**  
 Permite especificar cuántas filas de datos se van a transferir a la vez. El valor óptimo para este parámetro depende del sistema SAP Netweaver BW y del procesamiento de datos adicional que pueda darse. Normalmente, los valores entre 2 000 y 20 000 proporcionan el máximo rendimiento.  
  
 **Cadena de proceso de desencadenador**  
 (Opcional) Permite especificar el nombre de una cadena de procesos que se va a desencadenar una vez se haya completado la carga de datos.  
  
 **Tiempo de espera para InfoPackage**  
 Permite especificar la cantidad máxima de segundos que va a esperar el destino para que finalice el InfoPackage.  
  
 **Esperar a que se complete la transferencia de datos**  
 Permite especificar si el destino debe esperar hasta que el sistema SAP Netweaver BW haya terminado de cargar datos.  
  
 **No iniciar InfoPackage (Solo esperar)**  
 Permite especificar que el destino no va a activar un InfoPackage y que solo va a esperar a recibir la notificación de que el sistema SAP Netweaver BW ha comenzado a cargar datos.  
  
## <a name="see-also"></a>Vea también  
 [Editor de destino de SAP BW &#40; Página Administrador de conexiones &#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Editor de destino de SAP BW &#40; Página Asignaciones &#41;](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)   
 [Editor de destino de SAP BW &#40; Página de salida de error &#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [Ayuda F1 de Microsoft Connector 1.1 for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  