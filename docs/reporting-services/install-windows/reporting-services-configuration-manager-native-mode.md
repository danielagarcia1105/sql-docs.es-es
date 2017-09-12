---
title: "Administrador de configuración (modo nativo) de Reporting Services | Documentos de Microsoft"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
ms.assetid: 379eab68-7f13-4997-8d64-38810240756e
caps.latest.revision: 49
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ab787456bd3fdbc727ac1727188edd8ab5db0caa
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---

# <a name="reporting-services-configuration-manager-native-mode"></a>Administrador de configuración de Reporting Services (modo nativo)

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

Utilice el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo. Si ha instalado un servidor de informes usando la opción de instalación de solo archivos, debe usar el Administrador de configuración para configurar el servidor antes de poder usarlo. Si ha instalado un servidor de informes con la opción de instalación de configuración predeterminada, puede usar el Administrador de configuración para comprobar o modificar la configuración especificada durante la instalación. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se puede usar para configurar una instancia local o remota del servidor de informes.

> [!NOTE]
> A partir de la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no está diseñado para administrar servidores de informes en modo de SharePoint. El modo de SharePoint se administra y se configura mediante scripts de Administración central de SharePoint y scripts PowerShell.  
  
##  <a name="bkmk_scenarios"></a> Escenarios para usar el Administrador de configuración de Reporting Services  
 Puede usar el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para realizar las tareas siguientes:  
  
-   Configurar la cuenta del servicio del servidor de informes La cuenta se configura inicialmente durante la instalación, pero se puede modificar utilizando el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si se actualiza la contraseña o se desea utilizar otra cuenta.  
  
-   Crear y configurar direcciones URL. El servidor de informes y [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] son aplicaciones de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] a las que se accede mediante direcciones URL. La dirección URL del servidor de informes proporciona acceso a los extremos SOAP del servidor de informes. La dirección URL de [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] se utiliza para abrir [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] . Puede configurar una o varias direcciones URL para cada aplicación.  
  
-   Crear y configurar la base de datos del servidor de informes El servidor de informes es un servidor sin estado que requiere una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenamiento interno. Puede utilizar el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para crear y configurar una conexión con la base de datos del servidor de informes. También puede seleccionar una base de datos del servidor de informes existente que incluya el contenido que desea utilizar.  
  
-   Configurar una implementación escalada en modo nativo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite una topología de implementación que permite que varias instancias del servidor de informes usen una sola base de datos compartida del servidor de informes. Para implementar una implementación escalada del servidor de informes, se utiliza el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para conectar cada servidor de informes a la base de datos compartida.  
  
-   Realizar copias de seguridad, restaurar o reemplazar la clave simétrica que se utiliza para cifrar las cadenas de conexión almacenadas y las credenciales. Debe tener una copia de seguridad de la clave simétrica si cambia la cuenta de servicio, o mueve una base de datos del servidor de informes a otro equipo.  
  
-   Configurar la cuenta de ejecución desatendida Esta cuenta se utiliza para las conexiones remotas durante las operaciones programado o cuando las credenciales del usuario no están disponibles.  
  
-   Configurar el correo electrónico del servidor de informes. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye una extensión de entrega por correo electrónico del servidor de informes que usa un protocolo simple de transferencia de correo (SMTP) para entregar informes o notificaciones de procesamiento de informes a un buzón electrónico. Puede usar el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para especificar qué puerta de enlace o servidor SMTP de la red se debe usar para la entrega de correo electrónico.  
  
 El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no ayuda a administrar el contenido del servidor de informes, habilitar características adicionales ni conceder acceso al servidor. Implementación completa requiere que también utilice [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para habilitar características adicionales o modificar los valores predeterminados y el portal web para conceder acceso de usuario al servidor.

##  <a name="bkmk_requirements"></a> Requisitos

El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es específico de la versión. El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se instala con esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede usar para configurar una versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si ejecuta versiones anteriores y más recientes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en paralelo en el mismo equipo, debe usar el Administrador de configuración de Reporting Services, que se incluye con cada versión para configurar cada instancia.  

Para utilizar el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , debe disponer de lo siguiente:

- Permisos de administrador del sistema local en el equipo donde se hospede el servidor de informes que desee configurar. Si va a configurar un equipo remoto, debe tener permisos de administrador del sistema local en ese equipo también.

- Debe tener permiso para crear bases de datos en el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] empleado para hospedar la base de datos del servidor de informes.

- El servicio Instrumental de administración de Windows (WMI) debe estar habilitado y en funcionamiento en cualquier servidor de informes que se vaya a configurar. El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa el proveedor WMI del servidor de informes para conectarse a los servidores de informes locales y remotos. Si se va a configurar un servidor de informes remoto, el equipo debe permitir el acceso remoto de WMI. Para obtener más información, vea [Configurar un servidor de informes para la administración remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  

- Para poder conectarse a una instancia del servidor de informes remota y configurarla, debe habilitar las llamadas remotas de Instrumentación de administración de Windows (WMI) para atravesar Firewall de Windows. Para obtener más información, vea [Configurar un servidor de informes para la administración remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

El Administrador de configuración de Reporting Services se instala automáticamente al instalar SQL Server Reporting Services.

##  <a name="bkmk_start_configuration_manager"></a> Para iniciar el Administrador de configuración de Reporting Services

1.  Use el paso siguiente correspondiente a su versión de Microsoft Windows:

    - En la pantalla de inicio de Windows, escriba **informes** y seleccione **Reporting Services Configuration Manager** de los resultados de buscar.

    - Haga clic en **Iniciar**, seleccione **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]y después **Herramientas de configuración**.

         Si desea configurar una instancia del servidor de informes desde una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abra la carpeta de programas correspondiente a esa versión. Por ejemplo, seleccione [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] en lugar de [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] para abrir las herramientas de configuración de los componentes de servidor de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .

         Seleccione **Administrador de configuración de Reporting Services**.

2. Se abre el cuadro de diálogo **Conexión de configuración de Reporting Services** para que seleccione la instancia del servidor de informes que desea configurar. Seleccione **Conectar**.

3. En **Nombre del servidor**, especifique el nombre del equipo en el que está instalada la instancia del servidor de informes. El nombre del equipo local aparece de forma predeterminada, pero puede escribir el nombre de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remota si desea conectarse a un servidor de informes que esté instalado en un equipo remoto.

4. Si especifica un equipo remoto, haga clic en **Buscar** para establecer una conexión.

5. En **Report Server Enstance**, seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que desee configurar. Solo las instancias del servidor de informes correspondientes a esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aparecen en la lista. No es posible configurar versiones anteriores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

6. Seleccione **Conectar**.

## <a name="next-steps"></a>Pasos siguientes

[Portal Web](../../reporting-services/web-portal-ssrs-native-mode.md)   
[Herramientas de Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
[Configurar una conexión de base de datos del servidor de informes](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md)   
[Configurar y administrar un servidor de informes](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)