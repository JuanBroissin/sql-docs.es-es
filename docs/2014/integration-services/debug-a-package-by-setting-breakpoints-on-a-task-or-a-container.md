---
title: Depurar un paquete estableciendo puntos de interrupción en una tarea o un contenedor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], breakpoints
- breakpoints [Integration Services]
- tasks [Integration Services], breakpoints
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff0f1ef3f7baff1c39b3d338f47eb5eddde286e7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098186"
---
# <a name="debug-a-package-by-setting-breakpoints-on-a-task-or-a-container"></a>Depurar un paquete estableciendo puntos de interrupción en una tarea o un contenedor
  Este procedimiento describe cómo establecer puntos de interrupción en un paquete, una tarea, un contenedor de bucles For o Foreach o un contenedor de secuencias.  
  
### <a name="to-set-breakpoints-in-a-package-a-task-or-a-container"></a>Para establecer puntos de interrupción en un paquete, una tarea o un contenedor  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  Haga doble clic en el paquete en el que desee establecer puntos de interrupción.  
  
3.  En el Diseñador SSIS, siga estos pasos:  
  
    -   Para establecer puntos de interrupción en el objeto de paquete, haga clic en la pestaña **Flujo de control** , coloque el cursor en cualquier lugar del fondo de la superficie de diseño, haga clic con el botón derecho y, después, haga clic en **Editar puntos de interrupción**.  
  
    -   Para establecer puntos de interrupción en un flujo de control de paquete, haga clic en la pestaña **Flujo de control** , haga clic con el botón derecho en una tarea, un contenedor de bucles For o Foreach o un contenedor de secuencias y, después, haga clic en **Editar puntos de interrupción**.  
  
    -   Para establecer puntos de interrupción en un controlador de eventos, haga clic en la pestaña **Controlador de eventos** , haga clic con el botón derecho en una tarea, un contenedor de bucles For o Foreach o un contenedor de secuencias y, después, haga clic en **Editar puntos de interrupción**.  
  
4.  En el cuadro de diálogo **Establecer puntos de interrupción \<nombre de contenedor>**, seleccione los puntos de interrupción que quiere habilitar.  
  
5.  Opcionalmente, modifique el tipo y la cantidad de número de llamadas para cada punto de interrupción.  
  
6.  Para guardar el paquete, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas de las herramientas de desarrollo de paquetes](troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Depurar un Script estableciendo puntos de interrupción en una tarea Script y componente de Script](data-flow/transformations/script-component.md)   
 [Codificar y depurar la tarea Script](control-flow/script-task.md)   
 [Codificar y depurar el componente de script](extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
