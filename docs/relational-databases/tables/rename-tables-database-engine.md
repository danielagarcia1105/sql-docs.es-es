---
title: Cambio de nombre de las tablas (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table renaming [SQL Server]
- table names [SQL Server]
- tables [SQL Server], Visual Database Tools
- renaming tables
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 53d48d2522dc32db775782cf147a3e503b543c9f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601603"
---
# <a name="rename-tables-database-engine"></a>Cambiar el nombre a las tablas (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Cambie el nombre de una tabla en SQL Server o Azure SQL Database.

Para cambiar el nombre de una tabla en Azure SQL Data Warehouse o en Almacenamiento de datos paralelos, use la instrucción [RENAME OBJECT](../../t-sql/statements/rename-transact-sql.md) de Transact-SQL. 
  
> [!CAUTION]  
>  Piénselo bien antes de cambiar el nombre de una tabla. Si las consultas, vistas, funciones definidas por el usuario, procedimientos almacenados o programas existentes hacen referencia a esta tabla, la modificación del nombre hará que estos objetos dejen de ser válidos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para cambiar el nombre de una tabla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Cambiar el nombre de una tabla automáticamente no cambiará las referencias a esa tabla. Es necesario modificar de forma manual los objetos que hacen referencia a la tabla cuyo nombre se ha cambiado. Por ejemplo, si se cambia el nombre de una tabla y en un desencadenador existe una referencia a esa tabla, es necesario modificar el desencadenador para reflejar el nuevo nombre de la tabla. Use [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) para enumerar las dependencias de la tabla antes de cambiarle el nombre.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-rename-a-table"></a>Para cambiar el nombre de una tabla  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la tabla cuyo nombre quiere cambiar y seleccione **Diseño** en el menú contextual.  
  
2.  En el menú **Ver** , elija **Propiedades**.  
  
3.  En el campo del valor **Nombre** de la ventana **Propiedades** , escriba un nuevo nombre para la tabla.  
  
4.  Para cancelar esta acción, presione la tecla ESC antes de salir del campo.  
  
5.  En el menú **Archivo**, elija **Guardar** _nombre de tabla_.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-rename-a-table"></a>Para cambiar el nombre de una tabla  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  En el siguiente ejemplo se cambia el nombre de la tabla `SalesTerritory` por `SalesTerr` en el esquema `Sales` . Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
    ```  
  
 Para ver otros ejemplos, vea [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md).  
  
  
