---
title: "Reordenar columnas (complemento MDS para Excel) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ac00462e-c0f7-4b8d-86f2-d9eda2598a15
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Reordenar columnas (complemento MDS para Excel)
  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], puede reordenar las columnas si filtra la lista antes de cargar.  
  
 Cuando vuelva a ordenar atributos en el cuadro de diálogo **Filtro** , los datos se cargan en Excel con el orden nuevo. Sin embargo, la próxima vez filtre los datos de atributo, el orden revertirá al orden del diseño original. Para cambiar el orden de forma permanente, un administrador debe cambiar el orden en el área de **Administración del sistema** de Master Data Manager. Para más información, consulte [Change the Order of Attributes](../../master-data-services/change-the-order-of-attributes.md).  
  
## Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
### Para reordenar columnas administradas por MDS  
  
1.  Abra Excel y, en la pestaña **Datos maestros** , conéctese a un repositorio MDS. Para obtener más información, consulte [conectarse a un repositorio MDS & #40; Complemento MDS para Excel y nº 41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  En el panel **Explorador de datos maestros** , seleccione un modelo y una versión. La lista de entidades se rellena.  
  
    -   Si el panel **Explorador de datos maestros** no está visible, en el grupo **Conectar y cargar** , haga clic en **Mostrar explorador**.  
  
    -   Si el **Explorador de datos maestros** panel está deshabilitado, es porque la hoja existente ya contiene datos administrados por MDS. Para habilitar el panel, abra una nueva hoja de cálculo.  
  
3.  En el panel **Explorador de datos maestros** , haga clic en una entidad.  
  
4.  En el grupo **Conectar y cargar** , haga clic en **Filtro**.  
  
5.  En el cuadro de diálogo **Filtro** , en la sección **Columnas** , en la lista de atributos, haga clic en el atributo que desea mover.  
  
6.  A la derecha de la lista, haga clic en la flecha **Arriba** o **Abajo** para mover el atributo a la derecha o a la izquierda en la hoja de cálculo.  
  
7.  Repita el paso 7 para cada atributo hasta que el orden de arriba abajo represente el orden de izquierda a derecha que desee en la hoja de cálculo.  
  
8.  Haga clic en **Cargar datos**. La hoja se rellena con datos administrados por MDS y las columnas se muestran en el orden especificado.  
  
## Vea también  
 [Información general: Exportar datos a Excel y Nº 40; Complemento MDS para Excel y nº 41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  