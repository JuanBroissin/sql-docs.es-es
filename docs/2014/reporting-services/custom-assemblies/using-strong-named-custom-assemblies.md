---
title: Usar ensamblados personalizados con nombre seguro | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e4a12c97b476a0231e230dda16eaa667fcf0a642
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020750"
---
# <a name="using-strong-named-custom-assemblies"></a>Usar ensamblados personalizados con nombre seguro
  Un nombre seguro identifica un ensamblado e incluye un nombre para el mismo, un número de versión de cuatro partes, información de la referencia cultural (si se proporciona), una clave pública y una firma digital almacenadas en el manifiesto del ensamblado. Un nombre seguro identifica de forma única un ensamblado para Common Language Runtime (CLR) y se asegura de la integridad binaria.  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>Usar AllowPartiallyTrustedCallersAttribute  
 Para usar ensamblados con nombre seguro con los informes, debe permitir que el código de confianza parcial llame al ensamblado con nombre seguro con el atributo **AllowPartiallyTrustedCallers** del ensamblado. Puede usar **AllowPartiallyTrustedCallersAttribute** para permitir que el Diseñador de informes o el servidor de informes llamen a los ensamblados con nombre seguro en las expresiones de informe. Para permitir que el código con confianza parcial llame a los ensamblados con nombre seguro, agregue el siguiente atributo de nivel de ensamblado al archivo de atributos de ensamblado.  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute** solo es eficaz cuando lo aplica un ensamblado con nombre seguro en el nivel de ensamblado. Para más información sobre cómo aplicar atributos en el nivel de ensamblado, vea "Aplicar atributos" en la documentación del SDK de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
> [!CAUTION]  
>  Cuando **AllowPartiallyTrustedCallersAttribute** está presente, se evitan las comprobaciones de seguridad **FullTrustLinkDemand** predeterminadas, con lo que el ensamblado se puede llamar desde cualquier otro ensamblado con confianza parcial. Todas las comprobaciones de seguridad, incluidos los atributos de seguridad declarativos de nivel de clase o de método, se deben indicar explícitamente.  
  
## <a name="see-also"></a>Vea también  
 [Usar ensamblados personalizados con informes](using-custom-assemblies-with-reports.md)  
  
  
