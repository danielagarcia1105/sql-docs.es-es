---
title: "Mi configuración para la integración de Power BI (portal web) | Documentos de Microsoft"
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- pbi
- power bi
- power bi integration
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 8e627f20918a4d6ee5f882677ccc7b2c26616e2f
ms.contentlocale: es-es
ms.lasthandoff: 08/17/2017

---

# <a name="my-settings-for-power-bi-integration-web-portal"></a>La configuración de la integración de Power BI (portal web)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Los usuarios individuales usan la página **My Settings** (Mi configuración) del [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] is used by individual users to manage their sign-in with [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Al seguir los pasos para anclar un elemento de informe, automáticamente se le pedirá que inicie sesión.  Pero puede usar la página **My Settings** (Mi configuración) si necesita iniciar sesión manualmente o si necesita cerrarla.  Si no ve la opción de menú **My Settings** (Mi configuración), se deberá a que el servidor de informes aún no se ha integrado con  [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  Para obtener más información, vea [Integración del servidor de informes de Power BI &#40;Administrador de configuración&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## <a name="why-sign-in"></a>Por qué iniciar sesión

 Al iniciar la sesión, establece una relación entre la cuenta de usuario de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y la cuenta de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .  El inicio de sesión crea un token de seguridad que preserva un buen estado durante 90 días. Si el token expira y tiene elementos anclados a Power BI, verá una notificación.  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
Los iconos de los paneles de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] no se actualizarán hasta que vuelva a iniciar sesión a través de la página **My Settings**(Mi configuración).  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
Una vez que haya iniciado sesión, se creará un token de seguridad.  Los iconos del panel empezarán a actualizarse en los programas configurados anteriormente.  

## <a name="next-steps"></a>Pasos siguientes

[Integración del servidor de informes de BI de energía](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
[Anclado de elementos de Reporting Services en panales de Power BI](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
[Paneles en Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
[Portal Web](../reporting-services/web-portal-ssrs-native-mode.md)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)