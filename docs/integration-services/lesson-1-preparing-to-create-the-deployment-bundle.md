---
title: "Lección 1: Preparar para crear el paquete de implementación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: b6fe283c-9856-4ba1-a497-e3912424fd18
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0850bf9b55f3960736d45b1730f25f6c96c667a9
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="lesson-1-preparing-to-create-the-deployment-bundle"></a>Lección 1: Preparar la creación del paquete de implementación
En esta lección, creará las carpetas de trabajo y la variables de entorno que admiten el tutorial, creará un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , agregará varios paquetes y sus archivos auxiliares al proyecto e implementará las configuraciones en los paquetes.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] implementa paquetes según un proyecto; por tanto, en el primer paso de la creación del paquete de implementación, debe recopilar todos los paquetes y sus dependencias en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. En muchas ocasiones, esto es útil para incluir otra información con los paquetes implementados: por ejemplo, también agregará un archivo Léame al proyecto que proporcione la documentación básica de este grupo de paquetes.  
  
Después de agregar los paquetes y archivos, agregará configuraciones a los paquetes que todavía no usan configuraciones. Las configuraciones actualizan las propiedades de los paquetes y los objetos de paquete en tiempo de ejecución. En una lección posterior, modificará los valores de estas configuraciones durante la implementación de paquetes para que admitan los paquetes en el entorno implementado.  
  
Después de agregar estas configuraciones, debe abrir los paquetes en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , la herramienta gráfica de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para generar paquetes ETL, y examinar las propiedades de los paquetes y sus elementos, así como las configuraciones de paquetes para entender mejor los problemas que la implementación de paquetes debe controlar. Por ejemplo, uno de los paquetes extrae datos de archivos de texto, por lo que la ubicación de los archivos de datos debe actualizarse antes de que se ejecuten correctamente los paquetes implementados.  
  
**Tiempo estimado para completar esta lección:** 1 hora  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: Crear carpetas de trabajo y Variables de entorno](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
-   [Paso 2: Crear el proyecto de implementación](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
-   [Paso 3: Agregar paquetes y otros archivos](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
-   [Paso 4: Agregar configuraciones de paquetes](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
-   [Paso 5: Probar los paquetes actualizados](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
[Paso 1: crear carpetas de trabajo y variables de entorno](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
  
  
