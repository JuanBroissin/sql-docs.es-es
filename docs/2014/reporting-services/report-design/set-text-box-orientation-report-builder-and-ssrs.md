---
title: Establecer la orientación del cuadro de texto (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 64bd53f4-2f31-4732-8c2e-64c7b54b6972
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3e8beb8a7aa6eec3e62a45b9c3d3a8566f93b540
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296823"
---
# <a name="set-text-box-orientation-report-builder-and-ssrs"></a>Establecer la orientación del cuadro de texto (Generador de informes y SSRS)
  Un cuadro de texto se puede orientar en direcciones diferentes: horizontalmente, verticalmente (el texto se lee de arriba abajo) o girado 270 grados (el texto se lee de abajo arriba). Dado que la orientación se establece en el cuadro de texto y no en el texto, se aplica a todo el texto del cuadro de texto. No puede especificar orientaciones diferentes para las partes del texto. Debe establecer manualmente el ancho de columna y el alto de fila para alojar el texto girado.  
  
 La propiedad WritingMode, que se usa para especificar la orientación del texto, no está disponible en el **propiedades de cuadro de texto** cuadro de diálogo. Debe abrir el panel de propiedades y establecer la propiedad en él. Los valores disponibles para la propiedad WritingMode son **Horizontal** (texto se lee de izquierda a derecha), **Vertical** (el texto se lee de arriba a abajo), **Rotate270** (lectura de texto abajo a arriba). Debe establecer manualmente el ancho de columna y el alto de fila para alojar el texto.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-text-orientation"></a>Para establecer la orientación del texto  
  
1.  Cree un nuevo informe o abra un informe existente.  
  
2.  Si el panel de propiedades no está abierto, haga clic en la pestaña **Ver** y active la casilla **Propiedades** .  
  
3.  Haga clic en el cuadro de texto para el que desea cambiar la orientación del texto.  
  
4.  Busque la propiedad en el panel de propiedades y en la lista desplegable seleccione la orientación del texto para aplicar al cuadro de texto WritingMode.  
  
    > [!NOTE]  
    >  Cuando las propiedades del panel de propiedades se organizan en categorías, WritingMode está en la categoría **Localización** .  
  
5.  En el cuadro de lista, seleccione **Horizontal**, **Vertical**o **Rotate270**.  
  
## <a name="see-also"></a>Vea también  
 [Cuadros de texto &#40;Generador de informes y SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [Tutorial: Dar formato al texto &#40;generador de informes&#41;](../tutorial-format-text-report-builder.md)  
  
  
