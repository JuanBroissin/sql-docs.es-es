---
title: UnionAggregate (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- UnionAggregate method (geometry)
ms.assetid: dc7929cc-55ca-4a2c-a4b9-f5452f95bde8
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 65759e7e4d7701b36d79b8ce27bb5bfe176ba3e3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="unionaggregate-geometry-data-type"></a>UnionAggregate (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Realiza una operación de unión en un conjunto de objetos geometry.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UnionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_operand*  
 Es un **geometry** columna de tipo de tabla que contiene el conjunto de **geometry** objetos en el que se va a realizar una operación de unión.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geometry**  
  
## <a name="exceptions"></a>Excepciones  
 Produce una excepción `FormatException` cuando hay valores de entrada no válidos. Vea [STIsValid &#40; tipo de datos geometry &#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>Comentarios  
 Método **null** cuando la entrada está vacía o la entrada tiene SRID diferentes. Vea [identificadores de referencia espacial &#40; SRID &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 Método omite **null** entradas.  
  
> [!NOTE]  
>  Método **null** si todos los valores introducidos son **null**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve la unión de un conjunto de **geometry** objetos en una variable de tabla.  
  
 `-- Setup table variable for UnionAggregate example`  
  
 `DECLARE @Geom TABLE`  
  
 `(`  
  
 `shape geometry,`  
  
 `shapeType nvarchar(50)`  
  
 `);`  
  
 `INSERT INTO @Geom(shape,shapeType)`  
  
 `VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),`  
  
 `('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');`  
  
 `-- Perform UnionAggregate on @Geom.shape column`  
  
 `SELECT geometry::UnionAggregate(shape).ToString()`  
  
 `FROM @Geom;`  
  
## <a name="see-also"></a>Vea también  
 [Métodos de geometría estáticos ampliados](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

