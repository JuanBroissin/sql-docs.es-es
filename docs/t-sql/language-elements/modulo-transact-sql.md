---
title: "Módulo (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- modulo
- '% (Modulo)'
- MOD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- '% (modulo operator)'
- remainder of division operation
- modulo operator (%)
ms.assetid: f93c662e-f405-486e-bf23-a2d03907b5bd
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b417bbca6135db2f4ca6279bb9aac75d9d6f328
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="modulo-transact-sql"></a>Módulo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el resto de un número dividido entre otro.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse
    
dividend % divisor  
```  
  
## <a name="arguments"></a>Argumentos  
 *dividend*  
 Es la expresión numérica que se va a dividir. *Dividendo* debe ser válido [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquiera de los tipos de datos en el entero y categorías de tipos de datos de moneda, o la **numérico** tipo de datos.  
  
 *divisor*  
 Es la expresión numérica entre la que se va a dividir el dividendo. *divisor* debe ser cualquier expresión válida de cualquiera de los tipos de datos en el entero y categorías de tipos de datos de moneda, o la **numérico** tipo de datos.  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinados por los tipos de datos de los dos argumentos.  
  
## <a name="remarks"></a>Comentarios  
 Puede usar el módulo operador aritmético en la lista select de la instrucción SELECT con cualquier combinación de nombres de columna, constantes numéricas o cualquier expresión válida de los datos de moneda y entero categorías de tipos o la **numérico** datos tipo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-example"></a>A. Ejemplo sencillo  
 En el ejemplo siguiente se divide el número 38 por 5. Esto da como resultado 7 como la parte entera del resultado y muestra cómo módulo devuelve el resto de 3.  
  
```  
SELECT 38 / 5 AS Integer, 38 % 5 AS Remainder ;  
  
```  
  
### <a name="b-example-using-columns-in-a-table"></a>B. Ejemplo que usa columnas de una tabla  
 En el siguiente ejemplo se devuelve el número de Id. del producto, el precio unitario del producto y el módulo (resto) de la división del precio de cada producto, convertido a un valor entero, por el número de productos del pedido.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(100)ProductID, UnitPrice, OrderQty,  
   CAST((UnitPrice) AS int) % OrderQty AS Modulo  
FROM Sales.SalesOrderDetail;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-example"></a>C: ejemplo sencillo de  
 El ejemplo siguiente muestra los resultados de la `%` operador de división de 3 por 2.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(1) 3%2 FROM dimEmployee;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
1         
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [COMO &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Módulo igual &#40; Transact-SQL &#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)   
 [Compuesta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


