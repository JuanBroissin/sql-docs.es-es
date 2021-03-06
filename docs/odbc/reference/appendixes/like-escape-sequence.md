---
title: Secuencia de Escape LIKE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65447904f32b7e0457ed807f18e942b334ddc236
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626623"
---
# <a name="like-escape-sequence"></a>Secuencia de escape LIKE
ODBC utiliza secuencias de escape para la cláusula LIKE. La sintaxis de esta secuencia de escape es como sigue:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Comentarios  
 En la notación de BNF, la sintaxis es como sigue:  
  
 *Escape de ODBC como* :: =  
  
 *Iniciador de esc de ODBC* escape '*carácter de escape*' *terminador de esc de ODBC*  
  
 *carácter de escape* :: = *caracteres*  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *Terminador de esc de ODBC* :: =}  
  
 Para determinar si el controlador admite el escape LIKE secuencia, puede llamar una aplicación **SQLGetInfo** con el tipo de información SQL_LIKE_ESCAPE_CLAUSE.
