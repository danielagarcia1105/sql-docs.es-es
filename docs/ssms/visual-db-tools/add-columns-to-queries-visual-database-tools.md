---
title: Agregar columnas a las consultas (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7190609525c847d4a7ff62899e2e5879d41e04af
ms.lasthandoff: 04/11/2017

---
# <a name="add-columns-to-queries-visual-database-tools"></a>Agregar columnas a las consultas (Visual Database Tools)
Para utilizar una columna en una consulta, deberá agregarla a la consulta. Puede agregar una columna para mostrarla en los resultados de la consulta, para utilizarla al ordenar, para realizar búsquedas en el contenido de la columna o para resumir su contenido. Puede decidir cuáles de las columnas que utiliza en la consulta se van a incluir en el panel Resultados cuando la consulta se ejecute. Para más información, consulte [Remove Columns from Query Results &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md).  
  
> [!NOTE]  
> Para ver el tipo de datos de una columna en el Diseñador de consultas y vistas, seleccione la tabla o el objeto con valores de tabla en el **panel Diagrama** y, en la ventana Propiedades, haga clic en Lista de columnas. A continuación, haga clic en los **puntos suspensivos (…)** para abrir el cuadro de diálogo **Lista de columnas** .  
  
Siempre que utilice una columna en una consulta, también podrá utilizar una expresión formada por cualquier combinación de columnas, literales, operadores y funciones.  
  
### <a name="to-add-an-individual-column"></a>Para agregar una columna individual  
  
-   En el **panel Diagrama**, active la casilla situada junto a la columna que desea incluir.  
  
    - O bien -  
  
-   En el **panel Criterios**, vaya a la primera fila en blanco de la cuadrícula, haga clic en el campo de la columna **Columna** y seleccione un nombre de columna de la lista desplegable.  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>Para agregar todas las columnas correspondientes a una tabla o a un objeto con valores de tabla  
  
-   En el **panel Diagrama**, active la casilla situada junto a **\&#42;(Todas las columnas)**.  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>Para agregar todas las columnas correspondientes a todas las tablas y todos los objetos con estructura de tabla  
  
1.  Compruebe que no hay ninguna línea de combinación seleccionada en el **panel de operaciones de tablas** .  
  
2.  Haga clic con el botón derecho en el espacio vacío de la ventana Diseño y elija **Propiedades** en el menú contextual.  
  
3.  En la ventana Propiedades, haga clic en **Mostrar todas las columnas** y elija **Sí** o **No** en la lista desplegable.  
  
## <a name="see-also"></a>Vea también  
[Quitar columnas de los resultados de una consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
[Quitar columnas de las consultas &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/remove-columns-from-queries-visual-database-tools.md)  
[Especificar criterios de búsqueda &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Resumir los resultados de una consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operaciones básicas con consultas &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
