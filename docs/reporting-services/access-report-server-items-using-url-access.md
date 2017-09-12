---
title: Obtener acceso a elementos del servidor de informes mediante acceso URL | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- referencing URL items for report server access
- URL access [Reporting Services], report servers
ms.assetid: a58b4ca6-129d-45e9-95c7-e9169fe5bba4
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: fa59193fcedb1d5437d8df14035fadca2b3a28f1
ms.openlocfilehash: 475435073cef3f748e26a2a71c31a55fa7e6304d
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="access-report-server-items-using-url-access"></a>Acceder a elementos del servidor de informes mediante el acceso URL
  Este tema describe cómo tener acceso a los elementos de catálogo de diferentes tipos en un informe los datos del servidor de base o en un sitio de SharePoint mediante *rs: Command*=*valor*. En realidad, no es necesario agregar esta cadena de parámetro. Si la omite, el servidor de informes evalúa el tipo de elemento y selecciona el valor de parámetro apropiado automáticamente. Pero, si se usa la cadena *rs:Command*=*Value* en la dirección URL, mejora el rendimiento del servidor de informes.  
  
 Observe la sintaxis del proxy `_vti_bin` en los ejemplos siguientes. Para obtener más información acerca de cómo usar la sintaxis de proxy, vea [URL Access Parameter Reference](../reporting-services/url-access-parameter-reference.md).  
  
## <a name="access-a-report"></a>Acceder a un informe  
 Para ver un informe en el explorador, use el parámetro *rs:Command*=*Render* . Por ejemplo:  
  
 - **Nativa** `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`  
 - **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`  
  
> [!TIP]  
>  Es importante que la dirección URL incluya la sintaxis de proxy de `_vti_bin` para enrutar la solicitud a través de SharePoint y el proxy HTTP de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . El proxy agrega algún contexto a la solicitud HTTP, contexto que es necesario para garantizar la correcta ejecución del informe para los servidores de informes de modo de SharePoint.  
  
## <a name="access-a-resource"></a>Acceder a un recurso  
 Para tener acceso a un recurso, use el parámetro *rs:Command*=*GetResourceContents* . Si el recurso es compatible con el explorador, como una imagen, se abre en el explorador. De lo contrario, le preguntarán si desea abrir o guardar el archivo o recurso en el disco.  
  
 **Nativa** `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`  
  
## <a name="access-a-data-source"></a>Acceder a un origen de datos  
 Para acceder al origen de datos, use el parámetro *rs:Command*=*GetDataSourceContents* . Si el explorador admite código XML, aparecerá la definición del origen de datos si es un usuario autenticado con el permiso **Read Contents** en el origen de datos. Por ejemplo:  
  
 **Nativa** `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 La estructura XML se parecería al ejemplo siguiente:  
  
```  
<DataSourceDefinition>  
   <Extension>SQL</Extension>  
   <ConnectString>Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security Info=False;Initial Catalog=AdventureWorks2012;Data Source=MYSERVER1;</ConnectString>  
   <CredentialRetrieval>Integrated</CredentialRetrieval>  
   <WindowsCredentials>False</WindowsCredentials>  
   <ImpersonateUser>False</ImpersonateUser>  
   <Prompt />  
   <Enabled>True</Enabled>  
</DataSourceDefinition>  
```  
  
 Se devuelve la cadena de conexión según el valor **SecureConnectionLevel** del servidor de informes. Para obtener más información acerca de la configuración **SecureConnectionLevel** , vea [Using Secure Web Service Methods](../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md).  
  
## <a name="access-the-contents-of-a-folder"></a>Acceder al contenido de una carpeta  
 Para acceder al contenido de una carpeta, use el parámetro *rs:Command*=*GetChildren* . Se devuelve una página de navegación por carpetas genérica que contiene vínculos a las subcarpetas, informes, orígenes de datos y recursos en la carpeta solicitada. Por ejemplo:  
  
 **Nativa** `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rs:Command=GetChildren`  
  
 La interfaz de usuario que se ve es similar al modo de exploración de directorios que usa [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Server (IIS). El número de versión, incluido el número de compilación, del servidor de informes también se muestra debajo de la lista de carpetas.  
  
## <a name="see-also"></a>Vea también  
 [Acceso URL &#40; SSRS &#41;](../reporting-services/url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](../reporting-services/url-access-parameter-reference.md) 
