---
title: "Separar y adjuntar bases de datos de DQS | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 830e33bc-dd15-4f8e-a4ac-d8634b78fe45
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Separar y adjuntar bases de datos de DQS
  En este tema se describe cómo adjuntar y separar las bases de datos de DQS.  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Limitations"></a> Limitaciones y restricciones  
 Para obtener una lista de limitaciones y restricciones, consulte [separar bases de datos y adjuntar & #40; SQL Server & #41;](../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Asegúrese de que no haya actividades o procesos de DQS en ejecución. Utilice la pantalla **Supervisión de actividades** para comprobarlo. Para obtener información detallada sobre cómo utilizar esta pantalla, vea [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md).  
  
-   Asegúrese de que ningún usuario haya iniciado sesión en el [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
  
-   La cuenta de usuario de Windows debe ser miembro del rol fijo de servidor db_owner en la instancia de SQL Server para separar bases de datos de DQS.  
  
-   La cuenta de usuario de Windows debe tener el permiso CREATE DATABASE, CREATE ANY DATABASE o ALTER ANY DATABASE para adjuntar una base de datos.  
  
-   Debe disponer del rol dqs_administrator en la base de datos DQS_MAIN para terminar las actividades o detener los procesos en ejecución en DQS.  
  
##  <a name="Detach"></a> Separar bases de datos de DQS  
 Cuando se separa una base de datos de DQS mediante SQL Server Management Studio, los archivos separados permanecen en el equipo, y se pueden volver a adjuntar a la misma instancia de SQL Server o mover a otro servidor y adjuntarlos allí. Los archivos de base de datos DQS generalmente están disponibles en la siguiente ubicación en el equipo de servicios de calidad de datos: C:\Program Files\Microsoft SQL Server\MSSQL13.*\< Nombre_instancia >*\MSSQL\DATA.  
  
1.  Inicie Microsoft SQL Server Management Studio y conéctese a la instancia adecuada de SQL Server.  
  
2.  En el Explorador de objetos, expanda el nodo **Bases de datos** .  
  
3.  Haga clic en el **DQS_MAIN** base de datos, seleccione **tareas**, y, a continuación, haga clic en **separar**. Aparecerá el cuadro de diálogo **Separar base de datos** .  
  
4.  Active la casilla de verificación en la **Drop** columna y haga clic en **Aceptar** para separar la base de datos DQS_MAIN.  
  
5.  Repita los pasos 3 y 4 con las bases de datos DQS_PROJECTS y DQS_STAGING_DATA para separarlas.  
  
 También puede separar bases de datos de DQS mediante instrucciones Transact-SQL; para ello, utilice el procedimiento almacenado sp_detach_db. Para obtener más información sobre cómo separar bases de datos mediante instrucciones Transact-SQL, consulte [mediante Transact-SQL](../relational-databases/databases/detach-a-database.md#TsqlProcedure) en [separar una base de datos](../relational-databases/databases/detach-a-database.md).  
  
##  <a name="Attach"></a> Adjuntar bases de datos de DQS  
 Utilice las instrucciones siguientes para adjuntar una base de datos de DQS a la misma instancia de SQL Server (de la que se separó) o a una instancia de SQL Server diferente donde se ha instalado [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
1.  Inicie Microsoft SQL Server Management Studio y conéctese a la instancia adecuada de SQL Server.  
  
2.  En el Explorador de objetos, haga clic en **las bases de datos**, y, a continuación, haga clic en **adjuntar**. Aparecerá el cuadro de diálogo **Adjuntar bases de datos** .  
  
3.  Para especificar la base de datos que se va a adjuntar, haga clic en **Agregar**. Aparecerá el cuadro de diálogo **Buscar archivos de base de datos** .  
  
4.  Seleccione la unidad de disco en la que se halla la base de datos y expanda el árbol de directorios para buscar y seleccionar el archivo .mdf de la base de datos. Por ejemplo, para la base de datos DQS_MAIN:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\DQS_MAIN.mdf  
    ```  
  
5.  La **Detalles de la base de datos** panel inferior muestra los nombres de los archivos que se adjuntan. Para comprobar o cambiar la ruta de acceso de un archivo, haga clic en el **Examinar** botón (...).  
  
6.  Haga clic en **Aceptar** adjuntar la base de datos DQS_MAIN.  
  
7.  Repita los pasos 2 a 6 con las bases de datos DQS_PROJECTS y DQS_STAGING_DATA para adjuntarlas.  
  
8.  También se deben ejecutar las instrucciones Transact-SQL del paso siguiente después de restaurar la base de datos DQS_MAIN; de lo contrario, se mostrará un mensaje de error al intentar conectar con el servidor Data Quality Server mediante la aplicación Data Quality Client, y no se podrá conectar. Sin embargo, no es necesario realizar los pasos 9 y 10 si acaba de adjuntar la base de datos DQS_PROJECTS o DQS_STAGING_DATA, no la base de datos DQS_MAIN.  
  
     Para ejecutar las instrucciones Transact-SQL, en el Explorador de objetos, haga clic en el servidor y, a continuación, haga clic en **nueva consulta**.  
  
9. En la ventana del editor de consultas, copie las instrucciones SQL siguientes:  
  
    ```  
    ALTER DATABASE [DQS_MAIN] SET TRUSTWORTHY ON;  
    EXEC sp_configure 'clr enabled', 1;  
    RECONFIGURE WITH OVERRIDE  
    ALTER DATABASE [DQS_MAIN] SET ENABLE_BROKER  
    ALTER AUTHORIZATION ON DATABASE::[DQS_MAIN] TO [##MS_dqs_db_owner_login##]  
    ALTER AUTHORIZATION ON DATABASE::[DQS_PROJECTS] TO [##MS_dqs_db_owner_login##]  
  
    ```  
  
10. Presione F5 para ejecutar las instrucciones. Vea el panel Resultados para comprobar que las instrucciones se han ejecutado correctamente. Aparecerá el mensaje siguiente: `Configuration option 'clr enabled' changed from 1 to 1. Run the RECONFIGURE statement to install.`  
  
11. Conéctese con el servidor Data Quality Server mediante Data Quality Client para comprobar si la conexión funciona correctamente.  
  
 También se pueden adjuntar bases de datos de DQS utilizando las instrucciones Transact-SQL. Para obtener más información acerca de cómo adjuntar bases de datos mediante instrucciones Transact-SQL, consulte [mediante Transact-SQL](../relational-databases/databases/attach-a-database.md#TsqlProcedure) en [adjuntar una base de datos](../relational-databases/databases/attach-a-database.md).  
  
## Vea también  
 [Administrar bases de datos de DQS](../data-quality-services/manage-dqs-databases.md)  
  
  