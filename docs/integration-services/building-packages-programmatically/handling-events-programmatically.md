---
title: "Control de eventos mediante programación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services packages, events
- SQL Server Integration Services packages, events
- SSIS events, programmatically handling
- packages [Integration Services], events
- DtsEventHandler object
- SSIS packages, events
- SSIS events
- events [Integration Services], programmatically
- tasks [Integration Services], events
- IDTSEvents interface
ms.assetid: 0f00bd66-efd5-4f12-9e1c-36195f739332
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 7235703f494bd1fb50e696aef537391ba23d1749
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="handling-events-programmatically"></a>Controlar eventos mediante programación
  El motor de tiempo de ejecución de [!INCLUDE[ssIS](../../includes/ssis-md.md)] proporciona una recopilación de eventos que se producen antes, durante y después de la validación y la ejecución de un paquete. Estos eventos se pueden capturar de dos formas. El primer método consiste en implementar la <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> en una clase de interfaz y proporcionar la clase como un parámetro a la **Execute** y **validar** métodos del paquete. El segundo método consiste en crear objetos <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>, que pueden contener otros objetos [!INCLUDE[ssIS](../../includes/ssis-md.md)], como tareas y bucles, que se ejecutan cuando se produce un evento en <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents>. En esta sección se describen ambos métodos y se proporcionan ejemplos de código que muestran su uso.  
  
## <a name="receiving-idtsevents-callbacks"></a>Recibir devoluciones de llamada de IDTSEvents  
 Los desarrolladores que generan y ejecutan paquetes mediante programación puede recibir notificaciones de eventos durante el proceso de validación y ejecución utilizando la interfaz <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents>. Esto se hace mediante la creación de una clase que implementa el <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> interfaz y proporciona esta clase como un parámetro a la **validar** y **Execute** métodos de un paquete. Después, el motor en tiempo de ejecución llama a los métodos de la clase cuando se producen los eventos.  
  
 La clase <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> es una clase que ya implementa la interfaz <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents>; por lo tanto, otra alternativa a la implementación directa de <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> es derivar de <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> e invalidar los eventos específicos a los que desea responder. A continuación, proporcione la clase como un parámetro a la **validar** y **Execute** métodos de la <xref:Microsoft.SqlServer.Dts.Runtime.Package> para recibir devoluciones de llamada de evento.  
  
 El ejemplo de código siguiente muestra una clase que deriva de <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> e invalida el método <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnPreExecute%2A>. La clase, a continuación, se proporciona como aparameter a la **validar** y **Execute** métodos del paquete.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      MyEventsClass eventsClass = new MyEventsClass();  
  
      p.Validate(null, null, eventsClass, null);  
      p.Execute(null, null, eventsClass, null, null);  
  
      Console.Read();  
    }  
  }  
  class MyEventsClass : DefaultEvents  
  {  
    public override void OnPreExecute(Executable exec, ref bool fireAgain)  
    {  
      // TODO: Add custom code to handle the event.  
      Console.WriteLine("The PreExecute event of the " +  
        exec.ToString() + " has been raised.");  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim eventsClass As MyEventsClass = New MyEventsClass()  
  
    p.Validate(Nothing, Nothing, eventsClass, Nothing)  
    p.Execute(Nothing, Nothing, eventsClass, Nothing, Nothing)  
  
    Console.Read()  
  
  End Sub  
  
End Module  
  
Class MyEventsClass  
  Inherits DefaultEvents  
  
  Public Overrides Sub OnPreExecute(ByVal exec As Executable, ByRef fireAgain As Boolean)  
  
    ' TODO: Add custom code to handle the event.  
    Console.WriteLine("The PreExecute event of the " & _  
      exec.ToString() & " has been raised.")  
  
  End Sub  
  
End Class  
```  
  
## <a name="creating-dtseventhandler-objects"></a>Crear objetos DtsEventHandler  
 El motor en tiempo de ejecución proporciona un sistema de notificaciones y control de eventos extremadamente flexible y sólido a través del objeto <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>. Estos objetos permiten diseñar flujos de trabajo completos en el controlador de eventos que solamente se ejecutan cuando se produce el evento al que pertenece el controlador de eventos. El objeto <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> es un contenedor que se ejecuta cuando se desencadena el evento correspondiente en su objeto primario. Esta arquitectura permite crear flujos de trabajo aislados que se ejecutan como respuesta a eventos que se producen en un contenedor. Dado que los objetos <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> son sincrónicos, la ejecución no se reanuda hasta que se devuelven los controladores de eventos adjuntados al evento.  
  
 En el código siguiente se muestra cómo se crea un objeto <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>. El código agrega un elemento <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> a la colección <xref:Microsoft.SqlServer.Dts.Runtime.Package.Executables%2A> del paquete y, a continuación, crea un objeto <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> para el evento <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnError%2A> de la tarea. Se agrega un elemento <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> al controlador de eventos, que se ejecuta cuando se produce el evento <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnError%2A> para el primer elemento <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>. En este ejemplo se da por supuesto que tiene un archivo denominado C:\Windows\Temp\DemoFile.txt con fines de pruebas. La primera vez que se ejecuta el ejemplo, copia el archivo correctamente y no se llama al controlador de eventos. La segunda vez que se ejecuta el ejemplo, la primera <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> no puede copiar el archivo (porque el valor de <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask.OverwriteDestinationFile%2A> es **false**), se llama al controlador de eventos, el segundo <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> elimina el archivo de origen y el error de informes de paquete debido al error que se ha producido.  
  
## <a name="example"></a>Ejemplo  
  
```csharp  
using System;  
using System.IO;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string f = "DemoFile.txt";  
      Executable e;  
      TaskHost th;  
      FileSystemTask fst;  
  
      Package p = new Package();  
  
      p.Variables.Add("sourceFile", true, String.Empty,  
        @"C:\Windows\Temp\" + f);  
      p.Variables.Add("destinationFile", true, String.Empty,  
        Path.Combine(Directory.GetCurrentDirectory(), f));  
  
      // Create a first File System task and add it to the package.  
      // This task tries to copy a file from one folder to another.  
      e = p.Executables.Add("STOCK:FileSystemTask");  
      th = e as TaskHost;  
      th.Name = "FileSystemTask1";  
      fst = th.InnerObject as FileSystemTask;  
  
      fst.Operation = DTSFileSystemOperation.CopyFile;  
      fst.OverwriteDestinationFile = false;  
      fst.Source = "sourceFile";  
      fst.IsSourcePathVariable = true;  
      fst.Destination = "destinationFile";  
      fst.IsDestinationPathVariable = true;  
  
      // Add an event handler for the FileSystemTask's OnError event.  
      DtsEventHandler ehOnError = (DtsEventHandler)th.EventHandlers.Add("OnError");  
  
      // Create a second File System task and add it to the event handler.  
      // This task deletes the source file if the event handler is called.  
      e = ehOnError.Executables.Add("STOCK:FileSystemTask");  
      th = e as TaskHost;  
      th.Name = "FileSystemTask2";  
      fst = th.InnerObject as FileSystemTask;  
  
      fst.Operation = DTSFileSystemOperation.DeleteFile;  
      fst.Source = "sourceFile";  
      fst.IsSourcePathVariable = true;  
  
      DTSExecResult vr = p.Validate(null, null, null, null);  
      Console.WriteLine("ValidationResult = " + vr.ToString());  
      if (vr == DTSExecResult.Success)  
      {  
        DTSExecResult er = p.Execute(null, null, null, null, null);  
        Console.WriteLine("ExecutionResult = " + er.ToString());  
        if (er == DTSExecResult.Failure)  
          if (!File.Exists(@"C:\Windows\Temp\" + f))  
            Console.WriteLine("Source file has been deleted by the event handler.");  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim f As String = "DemoFile.txt"  
    Dim e As Executable  
    Dim th As TaskHost  
    Dim fst As FileSystemTask  
  
    Dim p As Package = New Package()  
  
    p.Variables.Add("sourceFile", True, String.Empty, _  
      "C:\Windows\Temp\" & f)  
    p.Variables.Add("destinationFile", True, String.Empty, _  
      Path.Combine(Directory.GetCurrentDirectory(), f))  
  
    ' Create a first File System task and add it to the package.  
    ' This task tries to copy a file from one folder to another.  
    e = p.Executables.Add("STOCK:FileSystemTask")  
    th = CType(e, TaskHost)  
    th.Name = "FileSystemTask1"  
    fst = CType(th.InnerObject, FileSystemTask)  
  
    fst.Operation = DTSFileSystemOperation.CopyFile  
    fst.OverwriteDestinationFile = False  
    fst.Source = "sourceFile"  
    fst.IsSourcePathVariable = True  
    fst.Destination = "destinationFile"  
    fst.IsDestinationPathVariable = True  
  
    ' Add an event handler for the FileSystemTask's OnError event.  
    Dim ehOnError As DtsEventHandler = CType(th.EventHandlers.Add("OnError"), DtsEventHandler)  
  
    ' Create a second File System task and add it to the event handler.  
    ' This task deletes the source file if the event handler is called.  
    e = ehOnError.Executables.Add("STOCK:FileSystemTask")  
    th = CType(e, TaskHost)  
    th.Name = "FileSystemTask1"  
    fst = CType(th.InnerObject, FileSystemTask)  
  
    fst.Operation = DTSFileSystemOperation.DeleteFile  
    fst.Source = "sourceFile"  
    fst.IsSourcePathVariable = True  
  
    Dim vr As DTSExecResult = p.Validate(Nothing, Nothing, Nothing, Nothing)  
    Console.WriteLine("ValidationResult = " + vr.ToString())  
    If vr = DTSExecResult.Success Then  
      Dim er As DTSExecResult = p.Execute(Nothing, Nothing, Nothing, Nothing, Nothing)  
      Console.WriteLine("ExecutionResult = " + er.ToString())  
      If er = DTSExecResult.Failure Then  
        If Not File.Exists("C:\Windows\Temp\" + f) Then  
          Console.WriteLine("Source file has been deleted by the event handler.")  
        End If  
      End If  
    End If  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>Vea también  
 [Integration Services &#40; SSIS &#41; Controladores de eventos](../../integration-services/integration-services-ssis-event-handlers.md)   
 [Agregar un controlador de eventos a un paquete](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  