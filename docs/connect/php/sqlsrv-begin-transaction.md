---
title: sqlsrv_begin_transaction | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_begin_transaction
apitype: NA
helpviewer_keywords:
- sqlsrv_begin_transaction
- transaction support
- API Reference, sqlsrv_begin_transaction
ms.assetid: 0b223bc8-4047-4329-9cbf-d350ab0fb886
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a7387890ef61348ed473bee7928a4bebc38d882
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618763"
---
# <a name="sqlsrvbegintransaction"></a>sqlsrv_begin_transaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Inicia una transacción de una conexión especificada. La transacción actual incluye en la conexión especificada todas las instrucciones que se han ejecutado después de la llamada a **sqlsrv_begin_transaction** y antes de realizar cualquier llamada a [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md) o [sqlsrv_commit](../../connect/php/sqlsrv-commit.md).  
  
> [!NOTE]  
> [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] se encuentra de forma predeterminada en modo de confirmación automática. Es decir, todas las consultas se confirman de forma automática cuando se realizan correctamente, salvo que se hayan designado como parte de una transacción explícita mediante **sqlsrv_begin_transaction**.  
  
> [!NOTE]  
> Si se llama a **sqlsrv_begin_transaction** después de que se haya iniciado una transacción en la conexión, pero no se ha completado llamando a **sqlsrv_commit** o **sqlsrv_rollback**, la llamada devuelve **False** y un error *Ya en la transacción* se agrega a la colección de errores.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_begin_transaction( resource $conn)  
```  
  
#### <a name="parameters"></a>Parámetros  
*$conn*: la conexión que está asociada la transacción.  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve un valor booleano **True** si la transacción se ha confirmado correctamente. De lo contrario, se devuelve el valor **False**.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente, se ejecutan dos consultas como parte de una transacción. Si las dos son correctas, se confirma la transacción. Si se produce un error en una de las consultas (o en ambas), se revierte la transacción.  
  
La primera consulta del ejemplo inserta un nuevo pedido de ventas en la tabla *Sales.SalesOrderDetail* de la base de datos de AdventureWorks. El pedido corresponde a 5 unidades del producto con el id. de producto 709. La segunda consulta reduce en 5 unidades la cantidad de inventario del id. de producto 709. Estas consultas se incluyen en una transacción, ya que ambas deben realizarse correctamente para que la base de datos refleje con precisión el estado de los pedidos y la disponibilidad de los productos.  
  
En el ejemplo se da por hecho que SQL Server y la base de datos [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initiate transaction. */  
/* Exit script if transaction cannot be initiated. */  
if ( sqlsrv_begin_transaction( $conn ) === false )  
{  
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initialize parameter values. */  
$orderId = 43659; $qty = 5; $productId = 709;  
$offerId = 1; $price = 5.70;  
  
/* Set up and execute the first query. */  
$tsql1 = "INSERT INTO Sales.SalesOrderDetail   
                     (SalesOrderID,   
                      OrderQty,   
                      ProductID,   
                      SpecialOfferID,   
                      UnitPrice)  
          VALUES (?, ?, ?, ?, ?)";  
$params1 = array( $orderId, $qty, $productId, $offerId, $price);  
$stmt1 = sqlsrv_query( $conn, $tsql1, $params1 );  
  
/* Set up and execute the second query. */  
$tsql2 = "UPDATE Production.ProductInventory   
          SET Quantity = (Quantity - ?)   
          WHERE ProductID = ?";  
$params2 = array($qty, $productId);  
$stmt2 = sqlsrv_query( $conn, $tsql2, $params2 );  
  
/* If both queries were successful, commit the transaction. */  
/* Otherwise, rollback the transaction. */  
if( $stmt1 && $stmt2 )  
{  
     sqlsrv_commit( $conn );  
     echo "Transaction was committed.\n";  
}  
else  
{  
     sqlsrv_rollback( $conn );  
     echo "Transaction was rolled back.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
Con el fin de resaltar el comportamiento de las transacciones, en el ejemplo anterior no se incluyen algunos controles de errores recomendados. En las aplicaciones de producción, se recomienda realizar la comprobación de la posible presencia de errores en todas las llamadas a una función de **sqlsrv** y controlar tales errores del modo pertinente.  
  
> [!NOTE]  
> No utilice instrucciones de Transact-SQL incrustadas para realizar transacciones. Por ejemplo, para iniciar una transacción, no ejecute una instrucción con "BEGIN TRANSACTION" como consulta de Transact-SQL. No se puede garantizar que las transacciones se comporten de la forma esperada cuando se usan instrucciones de Transact-SQL insertadas para realizar transacciones.  
  
## <a name="see-also"></a>Ver también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Realización de transacciones](../../connect/php/how-to-perform-transactions.md)

[Información general de los controladores de Microsoft para PHP para SQL Server](../../connect/php/overview-of-the-php-sql-driver.md) 
  
