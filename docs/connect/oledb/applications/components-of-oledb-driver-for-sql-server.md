---
title: Componentes de controlador OLE DB para SQL Server | Documentos de Microsoft
description: Componentes de controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 18b0f0e13fefefe5e3be09d7538150cfccbfcb21
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>Componentes de controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Controlador de OLE DB para SQL Server contiene los siguientes componentes:  

|Componente|Description|  
|---------------|-----------------|  
|msoledbsql.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene todo el controlador OLE DB para la funcionalidad de SQL Server.|  
|msoledbsqlr.rll|El archivo de recursos asociado para el controlador OLE DB para la biblioteca de SQL Server.|   
|msoledbsql.h|El controlador OLE DB para el archivo de encabezado de SQL Server que contiene todas las definiciones nuevas necesarias para poder usar el controlador OLE DB para SQL Server. Este archivo de encabezado reemplaza el archivo de encabezado sqloledb.h.<br /><br /> Nota: Puede hacer referencia a msoledbsql.h y sqloledb.h en el mismo programa siempre que sqloledb.h se defina en primer lugar.|  
|msoledbsql.lib|El archivo de biblioteca necesario para directamente llamada la **bcp** funciones de utilidad que forman parte del controlador OLE DB para SQL Server.<br /><br /> Nota: Si se hace referencia al archivo msoledbsql.lib en el código de programación, tiene que asegurarse de que el archivo msoledbsql.dll está en la ruta del sistema y en la ruta de acceso de sistema de los usuarios que utilizan la aplicación.|  

## <a name="see-also"></a>Vea también  
 [Generar aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  