---
title: Cómo administrar CDC Service local | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7f9be649-cd93-40c1-bc48-0480106f207c
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3e0b19e3069ff540903f22e79dabb0d2646e7f79
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111399"
---
# <a name="how-to-manage-a-local-cdc-service"></a>Cómo administrar un servicio CDC local
  En este procedimiento se describe cómo usar la Consola de configuración del servicio CDC para administrar servicios CDC concretos.  
  
### <a name="to-manage-a-specific-cdc-service"></a>Para administrar un servicio CDC específico  
  
1.  En el menú **Inicio** , seleccione **Configuración del servicio CDC para Oracle**.  
  
2.  En el panel izquierdo de la Consola de configuración del servicio CDC, expanda **Servicios CDC locales**.  
  
3.  Seleccione el servicio CDC con el que desea trabajar.  
  
     También puede hacer clic con el botón secundario en el servicio CDC con el que desea trabajar y seleccionar la acción deseada.  
  
     **O BIEN**  
  
     Seleccione **Servicios CDC locales** en el panel izquierdo de la Consola de configuración del servicio CDC y, a continuación, seleccione el servicio con el que desea trabajar en la sección central de la consola.  
  
     También puede hacer clic con el botón secundario en el servicio CDC con el que desea trabajar y seleccionar la acción deseada.  
  
4.  Puede realizar las tareas siguientes al trabajar con un servicio CDC.  
  
    -   **Eliminar el servicio**  
  
         En el panel **Acciones** del lado derecho de la Consola de configuración del servicio CDC, haga clic en **Eliminar** para eliminar el servicio.  
  
         También puede hacer clic con el botón derecho en el servicio CDC que quiera eliminar y seleccionar **Eliminar**.  
  
         **Nota**: si el servicio se está ejecutando cuando se elimina el servicio, se detendrá el servicio antes de eliminarlo.  
  
         Para eliminar una definición del servicio de Windows CDC de Oracle, el programa necesita acceso de actualización a la base de datos MSXDBCDC en la instancia asociada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al hacer clic en **Aceptar** para eliminar el servicio, el programa intenta eliminar el registro del servicio CDC de Oracle en la base de datos MSXDBCDC. Si se produce un error debido a la falta de permisos, aparecerá un cuadro de diálogo que pedirá al usuario que especifique un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con acceso de actualización para la base de datos MSXDBCDC.  
  
         Para obtener información acerca de los datos que debe especificar en el cuadro de diálogo Conectar con SQL Server, vea [Manage an Oracle CDC Service](manage-an-oracle-cdc-service.md) y [Connection to SQL Server for Delete](connection-to-sql-server-for-delete.md).  
  
    -   **Editar las propiedades del servicio CDC**  
  
         En el panel **Acciones** del lado derecho de la Consola de configuración del servicio CDC, haga clic en **Propiedades**.  
  
         También puede hacer clic con el botón derecho en el servicio CDC cuyas propiedades quiera editar y seleccionar **Propiedades**.  
  
## <a name="see-also"></a>Vea también  
 [Administrar un servicio CDC de Oracle](manage-an-oracle-cdc-service.md)  
  
  