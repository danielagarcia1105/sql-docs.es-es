---
title: "Importar y exportar conocimiento | Microsoft Docs"
ms.custom: ""
ms.date: "07/31/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 12537c9d-31e4-40b0-a411-cb343abbe96a
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Importar y exportar conocimiento
  Puede crear bases de conocimiento y dominios directamente en la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , o bien importar conocimiento en una base de conocimiento o exportarlo desde esta. En la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , puede usar un archivo de datos para las operaciones de importación y exportación, o un archivo de Excel para las operaciones de importación. El archivo de datos utilizado es un archivo cifrado creado por [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) con la extensión .dqs. Los archivos creados por Microsoft Excel pueden tener la extensión .xlsx, .xls o .csv. Estas operaciones le proporcionan una mayor flexibilidad a la hora de generar y compartir el conocimiento que utiliza para realizar las operaciones de limpieza de datos y búsqueda de coincidencias.  
  
> [!IMPORTANT]  
>  Puede exportar *todos los* las bases de conocimiento en su [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] a un archivo de copia de seguridad de DQS (.dqsb) mediante la ejecución del archivo DQSInstaller.exe desde el símbolo del sistema. De forma similar, puede importar *todos los* las bases de conocimiento de DQS de copia de seguridad archivo (.dqsb) a su [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] mediante la ejecución del archivo DQSInstaller.exe desde el símbolo del sistema. Para obtener más información acerca de cómo hacerlo, vea [Export and Import DQS Knowledge Bases Using DQSInstaller.exe](../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md) en la Guía de instalación de DQS.  
  
## En esta sección  
 Puede realizar las operaciones de importación y exportación siguientes:  
  
|||  
|-|-|  
|Exportar un dominio de una base de conocimiento a un archivo de datos .dqs|[Exportar un dominio a un archivo .dqs](../data-quality-services/export-a-domain-to-a-dqs-file.md)|  
|Importar un dominio desde un archivo de datos .dqs a una base de conocimiento existente|[Importar un dominio desde un archivo .dqs](../data-quality-services/import-a-domain-from-a-dqs-file.md)|  
|Exportar una base de conocimiento completa a un archivo de datos .dqs|[Exportar una base de conocimiento a un archivo .dqs](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)|  
|Importar una base de conocimiento completa desde un archivo de datos .dqs|[Importar una base de conocimiento desde un archivo .dqs](../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)|  
|Importar valores desde un archivo de Excel a un dominio|[Importar valores desde un archivo de Excel a un dominio](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md)|  
|Importar dominios desde un archivo de Excel a una base de conocimiento|[Importar dominios desde un archivo de Excel a la detección del conocimiento](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)|  
|Importar el conocimiento recopilado durante la limpieza en una base de conocimiento|[Importar valores de un proyecto de limpieza en un dominio](../data-quality-services/import-cleansing-project-values-into-a-domain.md)|  
  
## Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Generar una base de conocimiento ejecutando la detección de conocimiento y administrando el conocimiento de forma interactiva|[Crear una base de conocimiento](../data-quality-services/building-a-knowledge-base.md)|  
|Crear un dominio individual y agregarle conocimiento.|[Administrar un dominio](../data-quality-services/managing-a-domain.md)|  
|Crear un dominio compuesto y agregarle conocimiento.|[Administrar un dominio compuesto](../data-quality-services/managing-a-composite-domain.md)|  
  
  