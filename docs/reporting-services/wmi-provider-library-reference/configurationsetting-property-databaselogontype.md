---
title: Propiedad DatabaseLogonType (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DatabaseLogonType
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseLogonType property
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d9d20259ec79532db2ccbb04da4f83d66f3e2abd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47608600"
---
# <a name="configurationsetting-property---databaselogontype"></a>Propiedad ConfigurationSetting - DatabaseLogonType
  Especifica si el servidor de informes usa una cuenta de servicio de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, una cuenta de usuario de Windows o un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tener acceso a la base de datos del servidor de informes. Solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un objeto **integer** que representa el tipo de inicio de sesión.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Notas  
 Los valores son:  
  
-   0 para el inicio de sesión de Windows  
  
-   1 para el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 para el inicio de sesión como un servicio  
  
 Si especifica 0 (Windows), debe establecer el valor de la propiedad [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md) en una cuenta de usuario de Windows válida correspondiente.  
  
 Si especifica 1 (SQL Server), asegúrese de que el valor de [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md) se corresponda con un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido.  
  
 Si especifica 2 (servicio de Windows), el servidor de informes usará una cuenta de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] y la cuenta de servicio de Windows para tener acceso a la base de datos del servidor de informes. Se omite la propiedad DatabaseLogonAccount.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
