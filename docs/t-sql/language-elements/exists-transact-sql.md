---
title: EXISTE (Transact-SQL) | Documentos de Microsoft
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
- EXISTS_TSQL
- EXISTS
dev_langs:
- TSQL
helpviewer_keywords:
- existence testing [SQL Server]
- testing existence
- EXISTS keyword
- subqueries [SQL Server], EXISTS keyword
- queries [SQL Server], comparing
- comparing queries
- NOT EXISTS keyword
- row existence testing [SQL Server]
ms.assetid: b6510a65-ac38-4296-a3d5-640db0c27631
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c620baae23d9cab28142ee890ee103edbe2ee114
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="exists-transact-sql"></a>EXISTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica una subconsulta para probar la existencia de filas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
EXISTS ( subquery )  
```  
  
## <a name="arguments"></a>Argumentos  
 *subconsulta*  
 Es una instrucción SELECT restringida. No se permite la palabra clave INTO. Para obtener más información, consulte la información acerca de las subconsultas en [Seleccionar &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="result-values"></a>Valores de resultado  
 Devuelve TRUE si una subconsulta contiene filas.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-null-in-a-subquery-to-still-return-a-result-set"></a>A. Utilizar NULL en una subconsulta para seguir devolviendo un conjunto de resultados  
 En el ejemplo siguiente se devuelve un conjunto de resultados con `NULL` especificado en la subconsulta, que se sigue evaluando como TRUE al utilizar `EXISTS`.  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name   
FROM HumanResources.Department   
WHERE EXISTS (SELECT NULL)  
ORDER BY Name ASC ;  
```  
  
### <a name="b-comparing-queries-by-using-exists-and-in"></a>B. Comparar consultas mediante EXISTS e IN  
 En el ejemplo siguiente se comparan dos consultas que son semánticamente equivalentes. En la primera consulta se utiliza `EXISTS` y en la segunda `IN`.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.FirstName, a.LastName  
FROM Person.Person AS a  
WHERE EXISTS  
(SELECT *   
    FROM HumanResources.Employee AS b  
    WHERE a.BusinessEntityID = b.BusinessEntityID  
    AND a.LastName = 'Johnson');  
GO  
```  
  
 En la siguiente consulta se usa `IN`.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.FirstName, a.LastName  
FROM Person.Person AS a  
WHERE a.LastName IN  
(SELECT a.LastName  
    FROM HumanResources.Employee AS b  
    WHERE a.BusinessEntityID = b.BusinessEntityID  
    AND a.LastName = 'Johnson');  
GO  
```  
  
 Este es el conjunto de resultados de las consultas.  
  
 `FirstName                                          LastName`  
  
 `-------------------------------------------------- ----------`  
  
 `Barry                                              Johnson`  
  
 `David                                              Johnson`  
  
 `Willis                                             Johnson`  
  
 `(3 row(s) affected)`  
  
### <a name="c-comparing-queries-by-using-exists-and--any"></a>C. Comparar consultas mediante EXISTS y = ANY  
 En el ejemplo siguiente se muestran dos consultas para buscar tiendas cuyo nombre sea el mismo que el de un proveedor. La primera consulta utiliza `EXISTS` y el segundo usa `=``ANY`.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT s.Name  
FROM Sales.Store AS s   
WHERE EXISTS  
(SELECT *  
    FROM Purchasing.Vendor AS v  
    WHERE s.Name = v.Name) ;  
GO  
```  
  
 En la siguiente consulta se usa `= ANY`.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT s.Name  
FROM Sales.Store AS s   
WHERE s.Name = ANY  
(SELECT v.Name  
    FROM Purchasing.Vendor AS v ) ;  
GO  
```  
  
### <a name="d-comparing-queries-by-using-exists-and-in"></a>D. Comparar consultas mediante EXISTS e IN  
 En el siguiente ejemplo se muestran consultas para buscar empleados de departamentos que comiencen por `P`.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p   
JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID   
WHERE EXISTS  
(SELECT *  
    FROM HumanResources.Department AS d  
    JOIN HumanResources.EmployeeDepartmentHistory AS edh  
       ON d.DepartmentID = edh.DepartmentID  
    WHERE e.BusinessEntityID = edh.BusinessEntityID  
    AND d.Name LIKE 'P%');  
GO  
```  
  
 En la siguiente consulta se usa `IN`.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID   
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
   ON e.BusinessEntityID = edh.BusinessEntityID   
WHERE edh.DepartmentID IN  
(SELECT DepartmentID  
   FROM HumanResources.Department  
   WHERE Name LIKE 'P%');  
GO  
```  
  
### <a name="e-using-not-exists"></a>E. Utilizar NOT EXISTS  
 NOT EXISTS funciona de forma contraria a EXISTS. La cláusula WHERE de NOT EXISTS se cumple si la subconsulta no devuelve ninguna fila. En el siguiente ejemplo se buscan empleados que no sean de departamentos cuyos nombres empiecen por `P`.  
  
```  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p   
JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID   
WHERE NOT EXISTS  
(SELECT *  
   FROM HumanResources.Department AS d  
   JOIN HumanResources.EmployeeDepartmentHistory AS edh  
      ON d.DepartmentID = edh.DepartmentID  
   WHERE e.BusinessEntityID = edh.BusinessEntityID  
   AND d.Name LIKE 'P%')  
ORDER BY LastName, FirstName  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `FirstName                      LastName                       Title`  
  
 `------------------------------ ------------------------------ ------------`  
  
 `Syed                           Abbas                          Pacific Sales Manager`  
  
 `Hazem                          Abolrous                       Quality Assurance Manager`  
  
 `Humberto                       Acevedo                        Application Specialist`  
  
 `Pilar                          Ackerman                       Shipping & Receiving Superviso`  
  
 `François                       Ajenstat                       Database Administrator`  
  
 `Amy                            Alberts                        European Sales Manager`  
  
 `Sean                           Alexander                      Quality Assurance Technician`  
  
 `Pamela                         Ansman-Wolfe                   Sales Representative`  
  
 `Zainal                         Arifin                         Document Control Manager`  
  
 `David                          Barber                         Assistant to CFO`  
  
 `Paula                          Barreto de Mattos              Human Resources Manager`  
  
 `Shai                           Bassli                         Facilities Manager`  
  
 `Wanida                         Benshoof                       Marketing Assistant`  
  
 `Karen                          Berg                           Application Specialist`  
  
 `Karen                          Berge                          Document Control Assistant`  
  
 `Andreas                        Berglund                       Quality Assurance Technician`  
  
 `Matthias                       Berndt                         Shipping & Receiving Clerk`  
  
 `Jo                             Berry                          Janitor`  
  
 `Jimmy                          Bischoff                       Stocker`  
  
 `Michael                        Blythe                         Sales Representative`  
  
 `David                          Bradley                        Marketing Manager`  
  
 `Kevin                          Brown                          Marketing Assistant`  
  
 `David                          Campbell                       Sales Representative`  
  
 `Jason                          Carlson                        Information Services Manager`  
  
 `Fernando                       Caro                           Sales Representative`  
  
 `Sean                           Chai                           Document Control Assistant`  
  
 `Sootha                         Charncherngkha                 Quality Assurance Technician`  
  
 `Hao                            Chen                           HR Administrative Assistant`  
  
 `Kevin                          Chrisulis                      Network Administrator`  
  
 `Pat                            Coleman                        Janitor`  
  
 `Stephanie                      Conroy                         Network Manager`  
  
 `Debra                          Core                           Application Specialist`  
  
 `Ovidiu                         Crãcium                        Sr. Tool Designer`  
  
 `Grant                          Culbertson                     HR Administrative Assistant`  
  
 `Mary                           Dempsey                        Marketing Assistant`  
  
 `Thierry                        D'Hers                         Tool Designer`  
  
 `Terri                          Duffy                          VP Engineering`  
  
 `Susan                          Eaton                          Stocker`  
  
 `Terry                          Eminhizer                      Marketing Specialist`  
  
 `Gail                           Erickson                       Design Engineer`  
  
 `Janice                         Galvin                         Tool Designer`  
  
 `Mary                           Gibson                         Marketing Specialist`  
  
 `Jossef                         Goldberg                       Design Engineer`  
  
 `Sariya                         Harnpadoungsataya              Marketing Specialist`  
  
 `Mark                           Harrington                     Quality Assurance Technician`  
  
 `Magnus                         Hedlund                        Facilities Assistant`  
  
 `Shu                            Ito                            Sales Representative`  
  
 `Stephen                        Jiang                          North American Sales Manager`  
  
 `Willis                         Johnson                        Recruiter`  
  
 `Brannon                        Jones                          Finance Manager`  
  
 `Tengiz                         Kharatishvili                  Control Specialist`  
  
 `Christian                      Kleinerman                     Maintenance Supervisor`  
  
 `Vamsi                          Kuppa                          Shipping & Receiving Clerk`  
  
 `David                          Liu                            Accounts Manager`  
  
 `Vidur                          Luthra                         Recruiter`  
  
 `Stuart                         Macrae                         Janitor`  
  
 `Diane                          Margheim                       Research & Development Enginee`  
  
 `Mindy                          Martin                         Benefits Specialist`  
  
 `Gigi                           Matthew                        Research & Development Enginee`  
  
 `Tete                           Mensa-Annan                    Sales Representative`  
  
 `Ramesh                         Meyyappan                      Application Specialist`  
  
 `Dylan                          Miller                         Research & Development Manager`  
  
 `Linda                          Mitchell                       Sales Representative`  
  
 `Barbara                        Moreland                       Accountant`  
  
 `Laura                          Norman                         Chief Financial Officer`  
  
 `Chris                          Norred                         Control Specialist`  
  
 `Jae                            Pak                            Sales Representative`  
  
 `Wanda                          Parks                          Janitor`  
  
 `Deborah                        Poe                            Accounts Receivable Specialist`  
  
 `Kim                            Ralls                          Stocker`  
  
 `Tsvi                           Reiter                         Sales Representative`  
  
 `Sharon                         Salavaria                      Design Engineer`  
  
 `Ken                            Sanchez                        Chief Executive Officer`  
  
 `José                           Saraiva                        Sales Representative`  
  
 `Mike                           Seamans                        Accountant`  
  
 `Ashvini                        Sharma                         Network Administrator`  
  
 `Janet                          Sheperdigian                   Accounts Payable Specialist`  
  
 `Candy                          Spoon                          Accounts Receivable Specialist`  
  
 `Michael                        Sullivan                       Sr. Design Engineer`  
  
 `Dragan                         Tomic                          Accounts Payable Specialist`  
  
 `Lynn                           Tsoflias                       Sales Representative`  
  
 `Rachel                         Valdez                         Sales Representative`  
  
 `Garrett                        Vargar                         Sales Representative`  
  
 `Ranjit                         Varkey Chudukatil              Sales Representative`  
  
 `Bryan                          Walton                         Accounts Receivable Specialist`  
  
 `Jian Shuo                      Wang                           Engineering Manager`  
  
 `Brian                          Welcker                        VP Sales`  
  
 `Jill                           Williams                       Marketing Specialist`  
  
 `Dan                            Wilson                         Database Administrator`  
  
 `John                           Wood                           Marketing Specialist`  
  
 `Peng                           Wu                             Quality Assurance Supervisor`  
  
 `(91 row(s) affected)`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-using-exists"></a>F. Utilizar EXISTS  
 En el ejemplo siguiente se identifica si alguno filas en el `ProspectiveBuyer` tabla podría ser coincidencias en las filas de la `DimCustomer` tabla. La consulta devolverá filas solo cuando tanto el `LastName` y `BirthDate` valores en la búsqueda de coincidencias de dos tablas.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.LastName, a.BirthDate  
FROM DimCustomer AS a  
WHERE EXISTS  
(SELECT *   
    FROM dbo.ProspectiveBuyer AS b  
    WHERE (a.LastName = b.LastName) AND (a.BirthDate = b.BirthDate));  
```  
  
### <a name="g-using-not-exists"></a>G. Utilizar NOT EXISTS  
 NOT EXISTS funciona el efecto contrario como EXISTS. La cláusula WHERE de NOT EXISTS se cumple si la subconsulta no devuelve ninguna fila. En el ejemplo siguiente se busca las filas de la `DimCustomer` tabla en la que el `LastName` y `BirthDate` no coincide con ninguna entrada en el `ProspectiveBuyers` tabla.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.LastName, a.BirthDate  
FROM DimCustomer AS a  
WHERE NOT EXISTS  
(SELECT *   
    FROM dbo.ProspectiveBuyer AS b  
    WHERE (a.LastName = b.LastName) AND (a.BirthDate = b.BirthDate));  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


