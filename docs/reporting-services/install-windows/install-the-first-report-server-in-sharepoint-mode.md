---
title: Instalar el primer servidor de informes en modo SharePoint | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b29d0f45-0068-4c84-bd7e-5b8a9cd1b538
caps.latest.revision: 23
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 1bc7295666415d752ab3b803d51e029773d4db8e
ms.contentlocale: es-es
ms.lasthandoff: 08/17/2017

---
# <a name="install-the-first-report-server-in-sharepoint-mode"></a>Instalación del primer servidor de informes en modo de SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Los procedimientos de este tema le guían por la instalación en un solo servidor de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint. Los pasos incluyen la ejecución del Asistente para la instalación de SQL Server, así como tareas de configuración que usan Administración central de SharePoint. El tema también se puede usar para ver procedimientos individuales para actualizar una instalación existente, como crear una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]
> Integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.
  
 Para obtener información acerca de cómo agregar más servidores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a una granja existente, vea lo siguiente:  
  
-   [Agregar un servidor de informes adicional a una granja de servidores &#40;escalado horizontal de SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [Agregar un front-end web adicional de Reporting Services a una granja de servidores](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 Una instalación en un solo servidor es útil para escenarios de desarrollo y pruebas, pero no se recomienda en entornos de producción.  
  
##  <a name="bkmk_singleserver"></a> Ejemplo de implementación en un solo servidor  
 Una instalación en un solo servidor es útil para escenarios de desarrollo y pruebas, pero no se recomienda usar un solo servidor en un entorno de producción. El entorno de un solo servidor hace referencia a un solo equipo que tiene SharePoint y los componentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalados en el mismo equipo. El tema no trata el escalado horizontal con varios servidores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 En el diagrama siguiente se muestran los componentes que forman parte de una implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de un solo servidor.  
 
 > [!NOTE]
 > En SharePoint 2016, Excel Services se ha movido a Office Online Server y no se puede usar en una implementación de servidor único. Office Online Server debe implementarse en un servidor diferente. Para obtener más información, vea [Office Online Server overview](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx) (Información general sobre Office Online Server) y [Configure Excel Online administrative settings](https://technet.microsoft.com/library/jj219698\(v=office.16\).aspx)(Establecer la configuración administrativa de Excel Online).
  
|||  
|-|-|  
|**(1)**|Servicio de SharePoint instalado desde la instalación de SQL Server. Puede crear una o varias aplicaciones de servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(2)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para productos de SharePoint proporciona los componentes de la interfaz de usuario en los servidores de SharePoint.|  
|**(3)**|La aplicación de servicio de Excel usada por Power View y [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Esto no está disponible en una implementación de servidor único de SharePoint 2016. Se necesita [Office Online Server](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx) .|  
|**(4)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
  
 ![Implementación de servidor único de modo de SharePoint SSRS](../../reporting-services/install-windows/media/rs-sharepoint-1server-deployment.gif "implementación de servidor único de modo de SharePoint SSRS")  
  
> [!TIP]  
>  Para obtener ejemplos de implementación más complejos, vea [Topologías de implementación para las características BI de SQL Server](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26).  
  
##  <a name="bkmk_setupaccounts"></a> Cuentas de instalación  
 En esta sección se describen las cuentas y los permisos usados para los principales pasos de implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint.  
  
 **Instalar y registrar el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :**  
  
-   La cuenta actual durante la instalación (denominada cuenta de 'instalación') de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint debe tener derechos administrativos en el equipo local. Si va a instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] después de instalar SharePoint y la cuenta de 'instalación' también es miembro del grupo Administradores de la granja de servidores de SharePoint, la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] registrará el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si instala [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes de instalar SharePoint o la cuenta de 'instalación' no es miembro del grupo de administradores de la granja, debe registrar el servicio manualmente. Vea la sección [Paso 2: registrar e iniciar el servicio SharePoint de Reporting Services](#bkmk_install_SSRS_sharedservice).  
  
 **Crear aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  
  
-   Después de instalar y registrar el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , cree una o más aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La “cuenta del servicio de la granja de servidores de SharePoint“ debe ser temporalmente miembro del grupo local de administradores para que la aplicación de servicio de Reporting Services se pueda crear. Para obtener más información sobre los permisos de cuenta de SharePoint 2013, vea [Configurar la seguridad y los permisos de cuenta en SharePoint 2013](http://technet.microsoft.com/library/cc678863.aspx) (http://technet.microsoft.com/library/cc678863.aspx) o, en el caso de SharePoint 2016, [Configurar la seguridad y los permisos de cuenta en SharePoint Server 2016](https://technet.microsoft.com/library/cc678863\(v=office.16\).aspx).  
  
     Es una práctica recomendada de seguridad que las cuentas de administrador de la granja de servidores de SharePoint no sean también cuentas locales de administrador del sistema operativo. Si agrega una cuenta de administrador de la granja de servidores al grupo local de administradores como parte del proceso de instalación, se recomienda que quite la cuenta del grupo local de administradores una vez completada la instalación.  
  
##  <a name="bkmk_install_SSRS"></a> Paso 1: instalar un servidor de informes de Reporting Services en modo de SharePoint  
 Este paso instala un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint y el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint. Según lo que ya esté instalado en el equipo, quizás no vea algunas de las páginas de instalación que se describen en los pasos siguientes.  
 
 > [!IMPORTANT]
 > En SharePoint 2016, el servidor de SharePoint en el que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se instalará debe tener el rol de servidor **Personalizado** . La implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se realizará correctamente en un servidor de SharePoint que no esté en el rol **Personalizado** pero, durante el siguiente período de mantenimiento de SharePoint, MinRole detendrá el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] porque detecta que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el modo integrado de SharePoint no indica ninguna compatibilidad con los roles de servidor de SharePoint. La aplicación de servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] solo admite el rol **Personalizado** .
 
 > [!NOTE]
 > Si tiene previsto instalar también el servicio de PowerPivot en SharePoint 2016, hágalo antes de instalar Reporting Services. El servicio de PowerPivot no se puede instalar en un servidor de SharePoint en el **Personalizado** . Esto evita tener que cambiar de rol varias veces.
 
 ### <a name="apply-the-custom-server-role-to-a-sharepoint-2016-server"></a>Aplicar el rol de servidor Personalizado a un servidor de SharePoint 2016
 
 > [!NOTE]
 > Este procedimiento no es válido para SharePoint 2013.
 
 1. Inicie sesión en el servidor de SharePoint donde quiera instalar [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)](Establecer la configuración administrativa de Excel Online).
 
 2. Inicie el **Shell de administración de SharePoint 2016** como un administrador. 
  
    Haga clic con el botón derecho en el **Shell de administración de SharePoint 2016** y seleccione **Ejecutar como administrador**.

3. Desde el símbolo del sistema de PowerShell, ejecute el siguiente comando.

    > [!NOTE]
    > Procure especificar el nombre correcto del servidor de SharePoint.
    
        Set-SPServer SERVERNAME -Role Custom

4. Debería ver una respuesta que indica que se ha programado un trabajo del temporizador. Debe esperar a que el trabajo se ejecute.

5. Use el siguiente comando para comprobar el rol asignado del servidor.

        Get-SPServer SERVERNAME 
 
 6. **Rol** debe reflejar **Personalizado**.
 
 ### <a name="install-reporting-services"></a>Instalar Reporting Services
  
1.  Ejecute el Asistente para la instalación de SQL Server (Setup.exe).  
  
2.  Seleccione **Instalación** en el lado izquierdo del asistente y, después, seleccione **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.  

3.  Si ve la página **Clave del producto** , escriba su clave o acepte el valor predeterminado de la edición ‘Enterprise Evaluation’.  
  
     Seleccione **Siguiente**.  
  
4.  Si ve la página Términos de licencia, examine y acepte los términos de licencia. Microsoft aprecia su conformidad con el envío de datos de uso de las características para ayudarle a mejorar las características y el soporte técnico de los productos.  
  
     Seleccione **Siguiente**.  

5.  Se recomienda seleccionar **Usar Microsoft Update para buscar actualizaciones (recomendado)**. Esto es opcional.
  
     Seleccione **Siguiente**.   
  
6.  En la página **Instalar archivos del programa de instalación** , puede que aparezca el siguiente mensaje según lo que ya esté instalado en el equipo:  
  
    -   "Uno o varios archivos afectados tienen operaciones pendientes. Debe reiniciar el equipo una vez completado el proceso de actualización".  
  
    -   Seleccione **Siguiente**.  
  
7.  Si ve la página **Reglas de instalación** . Revise posibles advertencias o problemas de bloqueo. Luego, seleccione **Siguiente**.
 
8. Seleccione lo siguiente en la página **Selección de características** :  
  
    -   **Reporting Services – SharePoint**  
  
    -   **Complemento de Reporting Services para productos de SharePoint**.  
  
    -   Opcionalmente, puede seleccionar **Servicios de Motor de base de datos** para disponer de un entorno completo, pero para ello hay que tener una instancia de motor de base de datos de SQL Server que hospede las bases de datos de SharePoint.  
  
     Seleccione **Siguiente**.  
  
     ![rs_SetupFeatureSelection_SharePoint_with_circles](../../reporting-services/install-windows/media/rs-setupfeatureselection-sharepoint-with-circles.png)
  
9. Si seleccionó los servicios del Motor de base de datos, acepte la instancia predeterminada de **MSSQLSERVER** en la página **Configuración de instancia** y haga clic en **Siguiente**.  
  
     ![Tenga en cuenta](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Nota")arquitectura de SharePoint de Reporting Services el servicio no se basa en una "instancia" de SQL Server como la arquitectura de Reporting Services anterior.  
  
10. Si ve la página **Configuración del servidor** , escriba las credenciales adecuadas. Si desea usar las características de suscripción o alerta de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , necesita cambiar el **Tipo de inicio** para el Agente SQL Server a **Automático**. Quizás no vea la página **Configuración del servidor** , en función de lo que ya esté instalado en el equipo.  
  
     Seleccione **Siguiente**.  
  
11. Si ha seleccionado los servicios de Motor de base de datos, verá la página **Configuración del Motor de base de datos** ; agregue las cuentas adecuadas a la lista de administradores de SQL y seleccione **Siguiente**.  
  
12. En la página **Configuración de Reporting Services** debe ver que la opción **Solo instalar** está seleccionada. Esta opción instala los archivos del servidor de informes y no configura el entorno de SharePoint para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
    > [!NOTE]
    > Una vez completada la instalación de SQL Server, vea las demás secciones de este tema para configurar el entorno de SharePoint. Esto incluye instalar el servicio compartido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y crear las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     ![ssRS-2016-setup-configuration](../../reporting-services/install-windows/media/ssrs-2016-setup-configuration.png)
  
13. Revise las advertencias y, luego, seleccione **Siguiente** en la página **Reglas de configuración de características** si se detiene en esta página.  
  
14. En la página **Preparado para instalar** , repase el resumen de la instalación. El resumen incluirá un nodo secundario **Modo de SharePoint de Reporting Services** que muestra un valor **SharePointFilesOnlyMode**. Seleccione **Instalar**.  
  
15. La instalación tardará varios minutos. Verá la página **Operación completada** en la que se enumeran las características y el estado de cada una de ellas. Puede ver un cuadro de diálogo de información que indica que el equipo debe reiniciarse.  
  
##  <a name="bkmk_install_SSRS_sharedservice"></a> Paso 2: registrar e iniciar el servicio SharePoint de Reporting Services  
 ![Contenido relacionado con PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "contenido relacionado con PowerShell")  
  
> [!NOTE]
> Si va a realizar la instalación en una granja de SharePoint existente, no necesita completar los pasos de esta sección. El servicio SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se instaló e inició cuando ejecutó el Asistente para la instalación de SQL Server como parte de la sección anterior de este documento.  
  
 A continuación se exponen los motivos habituales por los que debe registrar manualmente el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Instaló el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes de instalar SharePoint.  
  
-   La cuenta usada para instalar el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no era miembro del grupo de administradores de la granja de servidores de SharePoint. Para obtener más información, vea la sección [Setup accounts](#bkmk_setupaccounts).  
  
 Los archivos necesarios se instalaron como parte de la instalación del Asistente para la instalación de SQL Server, pero los servicios tienen que ser registrados en la granja de servidores de SharePoint.  
  
 Con los siguientes pasos abrirá el Shell de administración de SharePoint y ejecutará cmdlets de PowerShell:  
  
1.  Seleccione en el botón **Inicio** .  
  
2.  Seleccione los grupos **Productos de Microsoft SharePoint 2016** o **Productos de Microsoft SharePoint 2013** .  
  
3.  Haga clic con el botón derecho en **Shell de administración de SharePoint 2016**o en **Shell de administración de SharePoint 2013**y, luego, seleccione **Ejecutar como administrador**. 

    > [!NOTE]
    > Los comandos de SharePoint no se reconocen en la ventana estándar de Windows PowerShell. Use el **Shell de administración de SharePoint**.  
  
4.  Ejecute el siguiente comando de PowerShell para instalar el servicio de SharePoint de Reporting Services. Si el comando se completa correctamente, muestra una nueva línea en el shell de administración. **No se devuelve ningún mensaje** al shell de administración cuando el comando se completa correctamente:  
  
    ```  
    Install-SPRSService  
    ```  
  
5.  Ejecute el siguiente comando de PowerShell para instalar el servicio de proxy de Reporting Services. Si el comando se completa correctamente, muestra una nueva línea en el shell de administración. **No se devuelve ningún mensaje** al shell de administración cuando el comando se completa correctamente:  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  Ejecute el siguiente comando de PowerShell para iniciar el servicio o vea en las notas siguientes las instrucciones para iniciar el servicio desde Administración central de SharePoint:  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
    > [!IMPORTANT]
    > Si ve un mensaje de error similar al siguiente:  
    >   
    >     Install-SPRSService: El término 'Install-SPRSService' **no se reconoce** como el nombre de un cmdlet, función, archivo de script o un programa ejecutable. Compruebe la ortografía del nombre o si una ruta de acceso se incluyó, compruebe que la ruta de acceso es correcta e inténtelo de nuevo.  
    >
    > Está en Windows Powershell en lugar del Shell de administración de SharePoint o el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no está instalado. Para obtener más información sobre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y PowerShell, vea [Cmdlets de PowerShell para el modo de SharePoint de Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
 También puede iniciar el servicio de Administración central de SharePoint en lugar de ejecutar el tercer comando de PowerShell. Los siguientes pasos también son útiles para comprobar que el servicio se está ejecutando.  
  
1.  En Administración central de SharePoint, haga clic en **Administrar servicios en el servidor** en el grupo **Configuración del sistema** .  
  
2.  Busque **Servicio SQL Server Reporting Services** y haga clic en **Iniciar** en la columna Acción.  
  
3.  El estado del servicio Reporting Services cambiará de **Detenido** a **Iniciado**. Si el servicio Reporting Services no está en la lista, use PowerShell para instalar el servicio.  
  
    > [!NOTE]  
    >  Si el servicio de Reporting Services se queda en estado **Iniciando** y no cambia a **Iniciado**, compruebe que el servicio “Administración de SharePoint 2013” se ha iniciado en el Administrador de Windows Server.  
  
##  <a name="bkmk_create_serrviceapplication"></a> Paso 3: crear una aplicación de servicio de Reporting Services  
 En esta sección se proporcionan los pasos para crear una aplicación de servicio y una descripción de las propiedades, si está revisando una aplicación de servicio existente.  
  
1.  En Administración central de SharePoint, en el grupo **Administración de aplicaciones** , seleccione **Administrar aplicaciones de servicio**.  
  
2.  En la cinta de SharePoint, seleccione el botón **Nuevo** .  
  
3.  En el menú Nuevo, seleccione **Aplicación de servicio de SQL Server Reporting Services**.  
  
    > [!IMPORTANT]  
    >  Si el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] opción no aparece en la lista, es un **indicación de que el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no está instalado el servicio compartido**. Revise la sección anterior sobre cómo utilizar cmdlts de PowerShell para instalar el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  En la página **Crear aplicación de servicio de SQL Server Reporting Services** , escriba un nombre para la aplicación. Si va a crear varias aplicaciones de servicio de Reporting Services, un nombre descriptivo o una convención de nomenclatura le ayudará a organizar las operaciones de administración.  
  
5.  En la sección **Grupo de aplicaciones** , cree un grupo de aplicaciones para la aplicación (recomendado). Si usa el mismo nombre para el grupo de aplicaciones y para la aplicación de servicio, puede simplificar la administración continuada. Esto también puede verse afectado por el número de aplicaciones de servicio que creará y si necesita usar varias aplicaciones de un solo grupo. Consulte la documentación de SharePoint Server para ver recomendaciones y prácticas recomendadas para la administración de grupos de aplicaciones.  
  
     Seleccione o cree una cuenta de seguridad para el grupo de aplicaciones. No olvide especificar una cuenta de usuario de dominio. Una cuenta de usuario de dominio habilita el uso de la característica de cuentas administradas de SharePoint, que permite actualizar la información de cuentas y contraseñas en un solo lugar. Las cuentas de dominio también se necesitan si planea escalar horizontalmente la implementación para incluir instancias de servicio adicionales que se ejecutan bajo la misma identidad.  
  
6.  En **Servidor de bases de datos**, puede usar el servidor actual o elegir otro servidor SQL Server diferente.  
  
7.  En **Nombre de la base de datos** , el valor predeterminado es `ReportingService_<guid>`, que es un nombre de base de datos único. Si escribe un nuevo valor, escriba un valor único. Es la nueva base de datos que se crea específicamente para la aplicación de servicio.  
  
8.  En **Autenticación de base de datos**, el valor predeterminado es Autenticación de Windows. Si elige **Autenticación de SQL**, consulte la documentación de SharePoint para conocer las prácticas recomendadas sobre cómo usar este tipo de autenticación en una implementación de SharePoint.  
  
9. En la sección **Asociación de aplicación web** , seleccione la aplicación web que se va a aprovisionar para el acceso de la aplicación de servicio de Reporting Services. Puede asociar una aplicación de servicio de Reporting Services a una aplicación web. Si todas las aplicaciones web actuales ya están asociadas a una aplicación de servicio de Reporting Services, ve un mensaje de advertencia.  
  
10. Seleccione **Aceptar**.  
  
11. El proceso de creación de la aplicación de servicio podría tardar varios minutos en completarse. Cuando se complete, verá un mensaje de confirmación y un vínculo a una página **Aprovisionar suscripciones y alertas** . Complete el paso de aprovisionamiento si desea usar las características de suscripciones o de alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, consulte [Provision Subscriptions and Alerts for SSRS Service Applications](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
 ![Contenido relacionado con PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "contenido relacionado con PowerShell") para obtener información sobre cómo usar PowerShell para crear una [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicación de servicio, vea:  
  
-   Vea la siguiente sección [Script de Windows PowerShell para los pasos 1 a 4](#bkmk_full_script).  
  
-   Tema [Para crear una aplicación de servicio de Reporting Services mediante PowerShell](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp).  

##  <a name="bkmk_powerview"></a> Paso 4: activar la característica de colección de sitios de Power View

 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una característica de SQL Server 2016 Reporting Services Add-para de [!INCLUDE[msCoName](../../includes/msconame-md.md)] productos de SharePoint, es una característica de colección de sitios. La característica se activa automáticamente para colecciones de sitios raíz y se crean las colecciones de sitios tras instalar el complemento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si tiene previsto utilizar [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], compruebe que la característica está activada.  
  
 Si instala el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint después de instalar SharePoint Server, la característica de integración del servidor de informes y la característica de Power View solo se activarán para las colecciones de sitios raíz. Para las demás colecciones de sitios, active manualmente las características.  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>Para activar o comprobar la característica de colección de sitios de Power View  
  
1.  En los pasos siguientes se da por hecho que el sitio de SharePoint está configurado para la **versión de la experiencia**2013 de SharePoint 2013.  
  
     Abra el explorador en el sitio de SharePoint que desee. Por ejemplo, http://\<servername >/sites/bi  
  
2.  Seleccione **configuración**![configuración de SharePoint](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "configuración de SharePoint").  
  
3.  Seleccione **Configuración del sitio**.  
  
4.  En el grupo **Administración de la colección de sitios** , seleccione **Características de la colección de sitios**.  
  
5.  Busque **Característica Power View Integration** en la lista.  
  
6.  Seleccione **Activar**. El estado de la característica cambiará a **Activo**.  
  
 Este procedimiento se completa en cada colección de sitios. Para más información, consulte [Activate the Report Server and Power View Integration Features in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md).  
  
##  <a name="bkmk_full_script"></a> Script de Windows PowerShell para los pasos 1 a 4  
 El script de PowerShell de esta sección es el equivalente a completar los pasos 1 a 4 de las secciones anteriores. El script hace lo siguiente:  
  
-   Instala el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y el proxy del servicio, e inicia el servicio.  
  
-   Crea un proxy del servicio denominado "Reporting Services".  
  
-   Crea una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] denominada "Reporting Services Application".  
  
-   Habilita la característica [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] para una colección de sitios.  
  
 Parámetros  
  
-   Actualice el parámetro **-Account** del proxy del servicio. La cuenta debe ser una cuenta de servicio administrada en la granja de servidores de SharePoint. Para obtener más información, vea el tema de SharePoint [Planeación de cuentas administrativas y de servicio en SharePoint 2013](http://technet.microsoft.com/library/cc263445.aspx).  
  
-   Actualice el parámetro **–DatabaseServer** para la aplicación de servicio. Este parámetro es la instancia del motor de base de datos  
  
-   Actualice el parámetro **–url** del sitio en el que desea habilitar la característica [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
 **Para utilizar el script:**  
  
1.  Abra Windows PowerShell con privilegios de administrador.  
  
2.  Copie el código siguiente en la ventana de script.  
  
3.  Actualice los tres parámetros descritos en la sección anterior y ejecute el script.  
  
```  
#This script Configures SQL Server Reporting Services SharePoint mode  
  
$starttime=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
  
Write-Host -ForegroundColor Green "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell –EA 0  
  
Write-Host -ForegroundColor Green "Install SSRS Service and Service Proxy, and start the service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
    Write-Host -ForegroundColor Green "Install the Reporting Services Shared Service"  
    Install-SPRSService  
  
    Write-Host -ForegroundColor Green " Install the Reporting Services Service Proxy"  
    Install-SPRSServiceProxy  
  
    # Get the ID of the RS Service Instance and start the service   
    Write-Host -ForegroundColor Green "Start the Reporting Services Service"  
    $RS = Get-SPServiceInstance | Where {$_.TypeName -eq "SQL Server Reporting Services Service"}  
    Start-SPServiceInstance -Identity $RS.Id.ToString()  
  
    # Wait for the Reporting Services Service to start...  
    $Status = Get-SPServiceInstance $RS.Id.ToString()  
    While ($Status.Status -ne "Online")  
    {  
        Write-Host -ForegroundColor Green "SSRS Service Not Online...Current Status = " $Status.Status  
        Start-Sleep -Seconds 2  
        $Status = Get-SPServiceInstance $RS.Id.ToString()  
    }  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
write-host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Create a new application pool and Reporting Services service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Write-Host -ForegroundColor Green "Create a new application pool"  
#!!!! update "-Account" with an existing Managed Service Account  
New-SPServiceApplicationPool -Name "Reporting Services" -Account "<domain>\User name>"  
$appPool = Get-SPServiceApplicationPool "Reporting Services"  
  
Write-Host -ForegroundColor Green " Create the Reporting Services Service Application"  
#!!!! Update "-DatabaseServer", an instance of the SQL Server database engine   
$rsService = New-SPRSServiceApplication -Name "Reporting Services Application" -ApplicationPool $appPool -DatabaseName "Reporting_Services_Application" -DatabaseServer "<server name>"  
  
Write-Host -ForegroundColor Green "Create the Reporting Services Service Application Proxy"  
$rsServiceProxy = New-SPRSServiceApplicationProxy -Name "Reporting Services Application Proxy" -ServiceApplication $rsService  
  
Write-Host -ForegroundColor Green "Associate service application proxy to default web site and grant web applications rights to SSRS application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"     
# Associate the Reporting Services Service Applicatoin Proxy to the default web site...  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $rsServiceProxy  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
write-host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Enable the PowerView and reportserver site features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#!!!! update "-url"  of the site where you want the features enabled  
Enable-SPfeature -identity "powerview" -Url http://server/sites/bi  
Enable-SPfeature -identity "reportserver" -Url http://server/sites/bi  
  
####To Verify, you can run the following:  
#Get-SPRSServiceApplication  
#Get-SPServiceApplicationPool | where {$_.name -like "reporting*"}  
#Get-SPRSServiceApplicationProxy  
  
```  
  
##  <a name="bkmk_additional_config"></a> Configuración adicional  
 En esta sección se describen los pasos de configuración que son importantes para la mayoría de las implementaciones de SharePoint.  
  
###  <a name="bkmk_configure_ECS"></a> Configurar Excel Services y PowerPivot  
 Si quiere ver informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] de un libro de Excel 2016 o de Excel 2013 en SharePoint, Excel Services se debe configurar para que use un servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de Power Pivot. 
 
 En SharePoint 2016, hay que configurar un [Office Online Server](https://technet.microsoft.com/library/jj219456\(v=office.16\).aspx) para poder usar Excel Services. Para ver información detallada, consulte las siguientes notas del producto.
 
 - [Implementación de SQL Server 2016 PowerPivot y Power View en SharePoint 2016](../../analysis-services/instances/install-windows/deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016.md)
 
 - [Implementación de SQL Server 2016 PowerPivot y Power View en una granja de SharePoint 2016 de niveles múltiples](../../analysis-services/instances/install-windows/deploy-powerpivot-and-power-view-multi-tier-sharepoint-2016-farm.md)
 
 En SharePoint 2016, hay que crear y configurar una aplicación de Excel Services. Para obtener más información, vea:  
  
-   La sección “Configurar Excel Services para la integración de Analysis Services” en [Instalación de Analysis Services en el modo PowerPivot](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
-   [Administrar la configuración del modelo de datos de Servicios de Excel (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780.aspx).  

Además, la cuenta de seguridad del grupo de aplicaciones usada por la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] debe ser administrador del servidor de Analysis Services.
  
###  <a name="bkmk_provision_agent"></a> Aprovisionar suscripciones y alertas  
 Las características de alerta de datos y suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pueden requerir la configuración de permisos del Agente SQL Server. Si obtiene un mensaje de error que indica que se requiere el Agente SQL Server y ha comprobado que se está ejecutando, tiene que actualizar los permisos. Puede hacer clic en el vínculo **Aprovisionar suscripciones y alertas** en la página que indica que la aplicación de servicio se creó correctamente para ir a otra página y aprovisionar el Agente SQL Server. El paso de aprovisionamiento es necesario si la implementación cruza los límites del equipo, por ejemplo, cuando la instancia de la base de datos de SQL Server está en un equipo diferente. Para obtener más información, vea [Aprovisionar Subscripciones y alertas para aplicaciones de servicio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>Configurar el correo electrónico para aplicaciones de servicio de SSRS  
 La característica de alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] envía alertas en los mensajes de correo electrónico. Para enviar correo electrónico, quizás tenga que configurar la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y modificar la extensión de entrega de correo electrónico para ella. Si piensa usar la extensión de entrega por correo electrónico para la característica de suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , hay que configurar el correo electrónico. Para obtener más información, vea [configurar el correo electrónico para una aplicación de servicio de Reporting Services &#40; SharePoint 2013 y SharePoint 2016 &#41; ](http://msdn.microsoft.com/en-us/38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f). 
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>Agregar tipos de contenido de Reporting Services a bibliotecas de contenido  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona tipos de contenido predefinidos que se usan para administrar archivos de orígenes de datos compartidos (.rsds), modelos de informe (.smdl) y archivos de definición de informe (.rdl) del Generador de informes. Al agregar un tipo de contenido **Informe del Generador de informes**, **Modelo de informe**y **Origen de datos de informe** a una biblioteca se habilita el comando **Nuevo** para que pueda crear nuevos documentos de ese tipo. Para obtener más información, vea [Add Reporting Services Content Types to a SharePoint Library (Agregar los tipos de contenido de Reporting Services a una biblioteca de SharePoint)](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="activate-the-report-server-file-sync-feature"></a>Activar la característica de sincronización de archivos del servidor de informes  
 Si los usuarios van a cargar con frecuencia elementos de informe publicados directamente en bibliotecas de documentos de SharePoint, la característica de nivel de sitio **Sincronizar archivo del Servidor de informes** será beneficiosa. La característica de sincronización de archivos sincronizará el catálogo del servidor de informes con los elementos de las bibliotecas de documentos con más frecuencia. Para más información, consulte [Activate the Report Server File Sync Feature in SharePoint Central Administration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md).  
  
##  <a name="bkmk_verify_installation"></a> Comprobar la instalación  
 A continuación se muestran los pasos y procedimientos sugeridos para comprobar la implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint.  
  
-   Vea la sección de SharePoint en el tema de comprobación [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
-   En una biblioteca de documentos de SharePoint, cree un informe básico de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que solo contenga un cuadro de texto, por ejemplo un título. El informe no contiene ningún origen de datos o conjuntos de datos. El objetivo es comprobar que puede abrir el Generador de informes, crear un informe básico y obtener una vista previa del mismo.  
  
     Guarde el informe en la biblioteca de documentos y ejecútelo desde la biblioteca. Para obtener más información sobre cómo crear informes con el Generador de informes, vea [Iniciar el Generador de informes (Generador de informes)](http://technet.microsoft.com/library/ms159221.aspx).  
  
## <a name="next-steps"></a>Pasos siguientes

[Cmdlets de PowerShell para el modo de SharePoint de Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
[Actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Ediciones y las características admitidas de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)   
[Aplicaciones de servicio y servicio de SharePoint de Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)