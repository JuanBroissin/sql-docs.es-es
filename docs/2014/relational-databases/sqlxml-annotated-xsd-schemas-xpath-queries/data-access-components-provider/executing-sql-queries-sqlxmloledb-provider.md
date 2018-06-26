---
title: Ejecutar consultas SQL (proveedor SQLXMLOLEDB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXMLOLEDB Provider
- xml root property [SQLXML]
- SQLXMLOLEDB Provider, executing SQL queries
- SQL queries [SQLXML]
ms.assetid: 50334cf5-9c87-4c00-9beb-e08577c4fa82
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 746c3869fb7c10fcedc3452e67acb85b487c11dd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200317"
---
# <a name="executing-sql-queries-sqlxmloledb-provider"></a>Ejecutar consultas SQL (proveedor SQLXMLOLEDB)
  En este ejemplo se muestra el uso de las siguientes propiedades SQLXMLOLEDB específicas del proveedor:  
  
-   ClientSideXML  
  
-   xml root  
  
 En esta aplicación de ejemplo ADO del lado cliente, se ejecuta una consulta SQL simple en el cliente. Porque clientsidexml, propiedad está establecida en True, la instrucción SELECT sin la cláusula FOR XML se envía al servidor. El servidor ejecuta la consulta y devuelve un conjunto de filas al cliente. A continuación, el cliente aplica la transformación FOR XML al conjunto de filas y genera un documento XML.  
  
 La propiedad de la raíz de xml proporciona el elemento raíz de nivel superior único para el documento XML que se genera.  
  
> [!NOTE]  
>  En el código, debe proporcionar el nombre de la instancia de Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la cadena de conexión. Además, este ejemplo especifica el uso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) para el proveedor de datos, que exige la instalación de software cliente de red adicional. Para obtener más información, consulte [requisitos del sistema para SQL Server Native Client](../../native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI ;"  
oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = "SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO"  
oTestStream.Open  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("xml root") = "root"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
  