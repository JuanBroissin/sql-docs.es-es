---
title: Referencia de API del controlador SQLSRV | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b55da26-ddeb-4e89-872a-91e0aba57103
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2bd1cf731f49119e54fb9e5a548a8988af1ef9fc
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrv-driver-api-reference"></a>Referencia de API del controlador SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

El nombre de la API del controlador SQLSRV en los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] es **sqlsrv**. Todos los **sqlsrv** funciones empiezan con **sqlsrv_** y van seguidas por un verbo o un sustantivo. Las que van seguidas de un verbo realizan algún tipo de acción, mientras que las que van seguidas de un sustantivo devuelven algún tipo de metadatos.  
  
## <a name="in-this-section"></a>En esta sección  
El controlador SQLSRV contiene las siguientes funciones:  
  
|Función|Description|  
|------------|---------------|  
|[sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)|Inicia una transacción.|  
|[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)|Cancela una instrucción; descarta cualquier resultado pendiente de la instrucción.|  
|[sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)|Proporciona información sobre el cliente.|  
|[sqlsrv_close](../../connect/php/sqlsrv-close.md)|Cierra una conexión. Libera todos los recursos asociados a la conexión.|  
|[sqlsrv_commit](../../connect/php/sqlsrv-commit.md)|Confirma una transacción.|  
|[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)|Cambia el control de errores y las configuraciones de registro.|  
|[sqlsrv_connect](../../connect/php/sqlsrv-connect.md)|Crea y abre una conexión.|  
|[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)|Devuelve información de los errores o las advertencias de la última operación.|  
|[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)|Ejecuta una instrucción preparada.|  
|[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)|Hace que una fila de datos esté disponible para su lectura.|  
|[sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)|Recupera la siguiente fila de datos como una matriz indizada numéricamente, una matriz asociativa o ambas.|  
|[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)|Recupera la siguiente fila siguiente de datos como un objeto.|  
|[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)|Devuelve los metadatos de los campos.|  
|[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)|Cierra una instrucción. Libera todos los recursos asociados a la instrucción.|  
|[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)|Devuelve el valor de la opción de configuración especificada.|  
|[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)|Recupera un campo en la fila actual por índice. Puede especificar el tipo de valor devuelto PHP.|  
|[sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md)|Detecta si un conjunto de resultados tiene una o varias filas.|  
|[sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)|Hace que el resultado siguiente esté disponible para su procesamiento.|  
|[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)|Informa del número de filas de un conjunto de resultados.|  
|[sqlsrv_num_fields](../../connect/php/sqlsrv-num-fields.md)|Recupera el número de campos de un conjunto de resultados activo.|  
|[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)|Prepara una consulta de Transact-SQL sin ejecutarla. Enlaza los parámetros de forma implícita.|  
|[sqlsrv_query](../../connect/php/sqlsrv-query.md)|Prepara y ejecuta una consulta de Transact-SQL.|  
|[sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)|Revierte una transacción.|  
|[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)|Devuelve el número de filas modificadas.|  
|[sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)|Envía hasta ocho kilobytes (8 kB) de datos al servidor con cada llamada a la función.|  
|[sqlsrv_server_info](../../connect/php/sqlsrv-server-info.md)|Proporciona información de la acción.|  
  
## <a name="reference"></a>Referencia  
[Manual de PHP](http://go.microsoft.com/fwlink/?LinkId=105500)  
  
## <a name="see-also"></a>Vea también  
[Introducción al controlador SQL para PHP](../../connect/php/overview-of-the-php-sql-driver.md)
[constantes &#40; Controladores de Microsoft para PHP para SQL Server &#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Guía de programación para el controlador SQL para PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Introducción al controlador SQL para PHP](../../connect/php/getting-started-with-the-php-sql-driver.md)
  
