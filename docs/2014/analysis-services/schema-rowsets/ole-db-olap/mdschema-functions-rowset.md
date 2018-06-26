---
title: Conjunto de filas MDSCHEMA_FUNCTIONS | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_FUNCTIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_FUNCTIONS rowset
ms.assetid: 5253fa8c-b1ce-4504-aff6-a246b5e675c7
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8e3086730ad66a0f21d9cc458d34d96a6d0eacc3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197264"
---
# <a name="mdschemafunctions-rowset"></a>Conjunto de filas MDSCHEMA_FUNCTIONS
  Describe las funciones que están disponibles para las aplicaciones cliente conectadas a la base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **MDSCHEMA_FUNCTIONS** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|**NOMBRE_FUNCIÓN**|**DBTYPE_WSTR**||Nombre de la función.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Descripción de la función.|  
|**PARAMETER_LIST**|**DBTYPE_WSTR**||Una lista delimitada por comas de parámetros con formato como en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic.  Por ejemplo, un parámetro podría ser Nombre como Cadena.|  
|**TIPO DEVUELTO**|**DBTYPE_I4**||El **VARTYPE** del tipo de datos de valor devuelto de la función.|  
|**ORIGEN**|**DBTYPE_I4**||Origen de la función:<br /><br /> -1 para las funciones MDX.<br />-2 para funciones definidas por el usuario.|  
|**NOMBRE DE INTERFAZ**|**DBTYPE_WSTR**||El nombre de la interfaz para las funciones definidas por el usuario<br /><br /> El nombre de grupo para las funciones de expresiones multidimensionales (MDX).|  
|**NOMBRE_DE_BIBLIOTECA**|**DBTYPE_WSTR**||Nombre de la biblioteca de tipos para las funciones definidas por el usuario. **NULL** para las funciones MDX.|  
|**NOMBRE_DLL**|**DBTYPE_WSTR**||(Opcional) El nombre del ensamblado que implementa la función definida por el usuario.<br /><br /> Devuelve **VT_NULL** para las funciones MDX.|  
|**HELP_FILE**|**DBTYPE_WSTR**||(Opcional) El nombre del archivo que contiene la documentación de ayuda para la función definida por el usuario.<br /><br /> Devuelve **VT_NULL** para las funciones MDX.|  
|**HELP_CONTEXT**|**DBTYPE_I4**||(Opcional) Devuelve el Id. de contexto de ayuda para esta función.|  
|**OBJETO**|**DBTYPE_WSTR**||(Opcional) El nombre genérico de la clase de objeto a la que hace referencia una propiedad. Por ejemplo, el conjunto de filas correspondientes a < level_name >. Miembros de función devuelve "**nivel**".<br /><br /> Devuelve **VT_NULL** para funciones definidas por el usuario o las funciones MDX sin propiedad.|  
|**TÍTULO**|**DBTYPE_WSTR**||El título de presentación de la función.|  
  
 El conjunto de filas está ordenado en **origen**, **INTERFACE_NAME**, **FUNCTION_NAME**.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **MDSCHEMA_FUNCTIONS** se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**NOMBRE_DE_BIBLIOTECA**|**DBTYPE_WSTR**|Opcional.|  
|**NOMBRE DE INTERFAZ**|**DBTYPE_WSTR**|Opcional.|  
|**NOMBRE_FUNCIÓN**|**DBTYPE_WSTR**|Opcional.|  
|**ORIGEN**|**DBTYPE_I4**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  