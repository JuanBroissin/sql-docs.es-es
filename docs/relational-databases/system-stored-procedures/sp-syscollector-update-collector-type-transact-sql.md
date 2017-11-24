---
title: sp_syscollector_update_collector_type (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collector_type_TSQL
- sp_syscollector_update_collector_type
dev_langs: TSQL
helpviewer_keywords:
- sp_syscollector_update_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 3c414dfd-d9ca-4320-81aa-949465b967bf
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 13bdc10abfa915d38dff7b19234ae31f98c042ec
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spsyscollectorupdatecollectortype-transact-sql"></a>sp_syscollector_update_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza un tipo de recopilador para un elemento de recopilación. Dado el nombre y GUID de un tipo de recopilador, actualiza la configuración del tipo de recopilador, incluida la colección y el paquete de carga, el esquema de parámetros y el esquema del formateador de parámetros.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syscollector_update_collector_type [ @collector_type_uid = ] 'collector_type_uid' OUTPUT  
          , [ @name = ] 'name'  
          , [ @parameter_schema = ] 'parameter_schema'  
          , [ @collection_package_id = ] collection_package_id  
          , [ @upload_package_id = ] upload_package_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@collector_type_uid =** ] **'***collector_type_uid***'**  
 Es el GUID para el tipo de recopilador. *collector_type_uid* es **uniqueidentifier**, y si es NULL, se crea y devuelve como OUTPUT automáticamente.  
  
 [  **@name =** ] **'***nombre***'**  
 Es el nombre del tipo de recopilador. *nombre* es **sysname** y deben especificarse.  
  
 [  **@parameter_schema =** ] **'***parameter_schema***'**  
 Es el esquema XML para este tipo de recopilador. *parameter_schema* es **xml** y puede ser necesario para determinados tipos de recopilador. Si no es necesario, este argumento puede ser NULL.  
  
 [  **@collection_package_id =** ] *collection_package_id*  
 Es un identificador local único que apunta al paquete de recopilaciones de [!INCLUDE[ssIS](../../includes/ssis-md.md)] usado por el conjunto de recopilaciones. *collection_package_id* es **uniqueidentifier** y es necesario. Para obtener el valor de *collection_package_id*, consulte la vista de sistema dbo.syscollector_collector_types en la base de datos msdb.  
  
 [  **@upload_package_id =** ] *upload_package_id*  
 Es un identificador local único que apunta al paquete de carga de [!INCLUDE[ssIS](../../includes/ssis-md.md)] usado por el conjunto de recopilaciones. *upload_package_id* es **uniqueidentifier** y es necesario. Para obtener el valor de *upload_package_id*, consulte la vista de sistema dbo.syscollector_collector_types en la base de datos msdb.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **dc_admin** (con permiso EXECUTE) rol fijo de base de datos.  
  
## <a name="example"></a>Ejemplo  
 Este ejemplo actualiza el tipo de recopilador Consultas T-SQL genérico. (En el ejemplo se usa el esquema predeterminado para el tipo de recopilador Consultas T-SQL genérico).  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collector_type  
@collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
@name = 'Generic T-SQL Query Collector Type',  
@parameter_schema = '<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="DataCollectorType">  
  <xs:element name="TSQLQueryCollector">  
<xs:complexType>  
  <xs:sequence>  
<xs:element name="Query" minOccurs="1" maxOccurs="unbounded">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Value" type="xs:string" />  
  <xs:element name="OutputTable" type="xs:string" />  
</xs:sequence>  
  </xs:complexType>  
</xs:element>  
<xs:element name="Databases" minOccurs="0" maxOccurs="1">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Database" minOccurs="0" maxOccurs="unbounded" type="xs:string" />  
</xs:sequence>  
<xs:attribute name="UseSystemDatabases" type="xs:boolean" use="optional" />  
<xs:attribute name="UseUserDatabases" type="xs:boolean" use="optional" />  
  </xs:complexType>  
</xs:element>  
  </xs:sequence>  
</xs:complexType>  
  </xs:element>  
</xs:schema>',  
@collection_package_id = '292B1476-0F46-4490-A9B7-6DB724DE3C0B',  
@upload_package_id = '6EB73801-39CF-489C-B682-497350C939F0';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  