---
title: sqlsrv_connect | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_connect
apitype: NA
helpviewer_keywords:
- connecting to the server
- API Reference, sqlsrv_connect
- connection pooling support
- sqlsrv_connect
ms.assetid: 37836b49-258e-45ce-9549-b8bd85d6952d
caps.latest.revision: 67
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e9491e2b0721f7c7a2ca6b5ed37c52135a4c760
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvconnect"></a>sqlsrv_connect
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Crea un recurso de conexión y abre una conexión. De forma predeterminada, se intentará realizar la conexión mediante la autenticación de Windows.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_connect( string $serverName [, array $connectionInfo])  
```  
  
#### <a name="parameters"></a>Parámetros  
*$serverName*: una cadena que especifica el nombre del servidor con el que se está estableciendo una conexión. Se puede incluir un nombre de instancia (por ejemplo, "miServidor\nombreDeInstancia") o el número de puerto (por ejemplo, "miServidor, 1521") como parte de esta cadena. Para obtener una descripción completa de las opciones disponibles en este parámetro, consulte la palabra clave Server en la sección Palabras clave de la cadena de conexión del controlador ODBC del artículo [Usar palabras clave de cadena de conexión con SQL Server Native Client](http://go.microsoft.com/fwlink/?LinkId=105504).  
  
A partir de la versión 3.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], también puede especificar una instancia de LocalDB con `"(localdb)\instancename"`. Para obtener más información, consulte [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).  
  
También, a partir de la versión 3.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], puede especificar un nombre de red virtual para conectarse a un grupo de disponibilidad AlwaysOn. Para obtener más información sobre el soporte de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vea [Controlador PHP para el soporte de SQL Server para la alta disponibilidad con recuperación ante desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).  
  
*$connectionInfo* [opcional]: una asociativa **matriz** que contiene atributos de conexión (por ejemplo, **matriz**("Database" = > "AdventureWorks")). Consulte [Connection Options](../../connect/php/connection-options.md) para obtener una lista de las claves admitidas para la matriz.  
  
## <a name="return-value"></a>Valor devuelto  
Un recurso de conexión PHP. Si no se crea y abre correctamente una conexión, se devuelve **False** .  
  
## <a name="remarks"></a>Comentarios  
Si los valores de las claves de *UID* y *PWD* no se especifican en el parámetro opcional *$connectionInfo* , se tratará de realizar la conexión usando la autenticación de Windows. Para obtener más información sobre la conexión al servidor, consulte [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md) y [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md).  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se crea y abre una conexión mediante la autenticación de Windows. En el ejemplo se da por hecho que SQL Server y la base de datos de [AdventureWorks](http://www.codeplex.com/SqlServerSamples) están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
```  
<?php  
/*  
Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. To connect using  
SQL Server Authentication, set values for the "UID" and "PWD"  
 attributes in the $connectionInfo parameter. For example:  
$connectionInfo = array("UID" => $uid, "PWD" => $pwd, "Database"=>"AdventureWorks");  
*/  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if( $conn )  
{  
     echo "Connection established.\n";  
}  
else  
{  
     echo "Connection could not be established.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Connecting to the Server](../../connect/php/connecting-to-the-server.md)  
[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
  
