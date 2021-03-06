---
title: Miembros de dimensión deducidos (Asistente para dimensiones de variación lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.inferrdim.f1
ms.assetid: 809e395f-2e10-48ff-8860-56403f130628
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1f6b53ffd05c7076a849b954f478757c12405e34
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804871"
---
# <a name="inferred-dimension-members-slowly-changing-dimension-wizard"></a>Miembros de dimensión deducidos (Asistente para dimensiones variables)
  Utilice el cuadro de diálogo **Miembros de dimensión deducidos** para especificar opciones de la utilización de miembros deducidos. Los miembros deducidos existen cuando una tabla de hechos hace referencia a miembros de dimensión que todavía no se han cargado. Cuando se cargan datos del miembro deducido, se puede actualizar el registro existente en lugar de crear uno nuevo.  
  
 Para obtener más información acerca de este asistente, vea [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Habilitar compatibilidad con miembros deducidos**  
 Si decide habilitar el uso de miembros deducidos, debe seleccionar una de las dos opciones siguientes.  
  
 **Todas las columnas con un tipo de cambio son NULL**  
 Especifique si escribe valores NULL en todas las columnas con un tipo de cambio en el nuevo registro de miembro deducido.  
  
 **Usar una columna de tipo booleano para indicar si el registro actual es un miembro deducido**  
 Especifique si desea utilizar una columna booleana existente para indicar si el registro actual es un miembro deducido.  
  
 **Indicador de miembro deducido**  
 Si ha elegido utilizar una columna booleana para indicar los miembros deducidos, como se ha descrito en la opción anterior, seleccione la columna en la lista.  
  
## <a name="see-also"></a>Vea también  
 [Configurar salidas mediante el Asistente para dimensión de variación lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
