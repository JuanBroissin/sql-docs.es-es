---
title: Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server | Microsoft Docs
description: Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], connection string keywords
- MSOLEDBSQL, connection string keywords
- connection strings [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, connection string keywords
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: ed200e47d1ce7e579dde3059da1d17b85c6677f6
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744535"
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Algún controlador OLE DB para las API de SQL Server use cadenas de conexión para especificar los atributos de conexión. Las cadenas de conexión son listas de palabras clave y valores asociados; cada palabra clave identifica un atributo de conexión determinado.  
  
> [!NOTE]
> El controlador OLE DB para SQL Server permite la ambigüedad en las cadenas de conexión para mantener la compatibilidad con versiones anteriores (por ejemplo, algunas palabras clave pueden especificarse más de una vez y pueden permitirse palabras clave en conflicto cuya resolución se base en la posición o en la precedencia). Futuras versiones del controlador OLE DB para SQL Server no es posible que permitirá la ambigüedad en las cadenas de conexión. Al modificar aplicaciones, es recomendable usar el controlador OLE DB para SQL Server a fin de eliminar cualquier dependencia sobre la ambigüedad de las cadenas de conexión.  
  
 Las secciones siguientes describen las palabras clave que pueden usarse con el controlador OLE DB para SQL Server y ActiveX Data Objects (ADO) cuando se usa el controlador OLE DB para SQL Server como el proveedor de datos.  

  
## <a name="ole-db-driver-connection-string-keywords"></a>Palabras clave de cadena de conexión del controlador OLE DB  
 Las aplicaciones OLE DB pueden inicializar los objetos de origen de datos de dos formas:  
  
-   **IDBInitialize::Initialize**  
  
-   **IDataInitialize::GetDataSource**  
  
 En el primer caso, se puede usar una cadena de proveedor para inicializar las propiedades de conexión estableciendo la propiedad DBPROP_INIT_PROVIDERSTRING en el conjunto de propiedades DBPROPSET_DBINIT. En el segundo caso, se puede pasar una cadena de inicialización al método **IDataInitialize::GetDataSource** para inicializar las propiedades de conexión. Ambos métodos inicializan las mismas propiedades de conexión OLE DB, pero se utilizan conjuntos diferentes de palabras clave. El conjunto de palabras clave usado por **IDataInitialize::GetDataSource** es, como mínimo, la descripción de propiedades del grupo de propiedades de inicialización.  
  
 En cualquier configuración de cadena de proveedor que tenga una propiedad OLE DB correspondiente establecida en algún valor predeterminado o establecida explícitamente en un valor, el valor de la propiedad OLE DB invalidará la configuración de la cadena de proveedor.  
  
 Las propiedades booleanas establecidas en las cadenas de proveedor a través de los valores DBPROP_INIT_PROVIDERSTRING se establecen utilizando los valores "yes" y "no". Las propiedades booleanas establecidas en las cadenas de inicialización mediante **IDataInitialize::GetDataSource** se establecen con los valores "true" y "false".  
  
 Las aplicaciones que usan **IDataInitialize::GetDataSource** también pueden usar las palabras empleadas por **IDBInitialize::Initialize**, pero solo para las propiedades que no tienen un valor predeterminado. Si una aplicación usa tanto la palabra clave **IDataInitialize::GetDataSource** como la palabra clave **IDBInitialize::Initialize** en la cadena de inicialización, se usa el valor de palabra clave **IDataInitialize::GetDataSource**. Se recomienda encarecidamente que las aplicaciones no usen palabras clave **IDBInitialize::Initialize** en cadenas de conexión **IDataInitialize:GetDataSource**, puesto que es posible que este comportamiento no se mantenga en futuras versiones.  
  
> [!NOTE]  
>  Una cadena de conexión pasada a través de **IDataInitialize::GetDataSource** se convierte en propiedades y se aplica por medio de **IDBProperties::SetProperties**. Si los servicios del componente encuentran la descripción de propiedad en **IDBProperties::GetPropertyInfo**, esta propiedad se aplica como propiedad independiente. De lo contrario, se aplicará a través de la propiedad DBPROP_PROVIDERSTRING. Por ejemplo, si especifica la cadena de conexión **origen de datos = server1; Server = server2**, **origen de datos** se establecerá como una propiedad, pero **Server** pasará a una cadena de proveedor.  
  
 Si especifica varias instancias de la misma propiedad específica del proveedor, se utilizará el primer valor de la primera propiedad.  
  
 Las cadenas de conexión usadas por las aplicaciones OLE DB que emplean DBPROP_INIT_PROVIDERSTRING con **IDBInitialize::Initialize** tienen la siguiente sintaxis:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Los valores de atributo pueden incluirse opcionalmente entre llaves y es una práctica recomendable. Esto evita que se produzcan problemas cuando los valores de atributo contienen caracteres no alfanuméricos. Se supone que la primera llave de cierre del valor termina el valor, de modo que los valores no pueden contener caracteres de llave de cierre.  
  
 Un carácter de espacio después del signo = de una palabra clave de cadena de conexión se interpreta como un literal, aun cuando el valor esté entre comillas.  
  
 En la tabla siguiente se describen las palabras clave que pueden utilizarse con DBPROP_INIT_PROVIDERSTRING.  
  
|Palabra clave|Propiedad de inicialización|Descripción|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|Sinónimo de "Address".|  
|**Dirección**|SSPROP_INIT_NETWORKADDRESS|Dirección de red del servidor en el que se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **Address** suele ser el nombre de red del servidor, pero también puede ser otros nombres, como una canalización, una dirección IP o un puerto TCP/IP y una dirección de socket.<br /><br /> Si especifica una dirección IP, asegúrese de que los protocolos TCP/IP o de canalizaciones con nombre estén habilitados en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> El valor de **dirección** tiene prioridad sobre el valor pasado a **Server** en cadenas de conexión cuando se usa el controlador de OLE DB para SQL Server. Tenga también en cuenta que `Address=;` se conecta al servidor especificado en la palabra clave **Server**, mientras que `Address= ;, Address=.;`, `Address=localhost;` y `Address=(local);` establecen una conexión al servidor local.<br /><br /> La sintaxis completa de la palabra clave **Address** es la siguiente:<br /><br /> [_protocolo_**:**]_dirección_[**,**_puerto &#124;\pipe\pipename_]<br /><br /> _protocolo_ puede ser **tcp** (TCP/IP), **lpc** (memoria compartida) o **np** (canalizaciones con nombre). Para obtener más información acerca de los protocolos, consulte [configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md).<br /><br /> Si no _protocolo_ ni **red** se especifica la palabra clave, el controlador OLE DB para SQL Server usará el orden de protocolo especificado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *port* es el puerto al que se va a conectar en el servidor especificado. De forma predeterminada, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el puerto 1433.|   
|**APP**|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.<br /><br /> El valor predeterminado es **ReadWrite**. Para obtener más información sobre el controlador de OLE DB para la compatibilidad con SQL Server [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server Support for High Availability, Disaster Recovery](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Para usar **AttachDBFileName**, debe especificar también el nombre de la base de datos con la palabra clave Database de la cadena del proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|**Autenticación**<a href="#table1_1"><sup id="table1_authmode">**1**</sup></a>|SSPROP_AUTH_MODE|Especifica la autenticación de Active Directory o SQL utilizada. Los valores válidos son:<br/><ul><li>`(not set)`: Modo de autenticación determinado por otras palabras clave.</li><li>`ActiveDirectoryPassword:` Autenticación de Active Directory con Id. de inicio de sesión y la contraseña.</li><li>`ActiveDirectoryIntegrated:` Autenticación integrada de Active Directory con las credenciales de cuenta de Windows del usuario que ha iniciado sesión actualmente.</li><br/>**Nota:** tiene **recomienda** que las aplicaciones mediante `Integrated Security` (o `Trusted_Connection`) palabras clave de autenticación o sus propiedades correspondientes se establezca el valor de la `Authentication` palabra clave (o su la propiedad correspondiente) a `ActiveDirectoryIntegrated` para habilitar el nuevo comportamiento de validación de cifrado y los certificados.<br/><br/><li>`SqlPassword:` Autenticación con Id. de inicio de sesión y la contraseña.</li><br/>**Nota:** tiene **recomienda** que las aplicaciones mediante `SQL Server` autenticación establece el valor de la `Authentication` palabra clave (o la propiedad correspondiente) a `SqlPassword` para habilitar el cifrado nuevo y comportamiento de validación del certificado.</ul>|
|**Auto Translate**|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "yes" y "no".|  
|**Base de datos**|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que debe utilizarse. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de SQL Server 2000.|  
|**Cifrar**<a href="#table1_1"><sup>**1**</sup></a>|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "yes" y "no". El valor predeterminado es "no".|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que controlador OLE DB para SQL Server puede utilizar el valor predeterminado, SPN generado por el proveedor.|  
|**Lenguaje**|SSPROPT_INIT_CURRENTLANGUAGE|Lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión si el servidor es [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior. Los valores posibles son "yes" y "no". El valor predeterminado es "no".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Especifique siempre **MultiSubnetFailover=Yes** al conectarse a la escucha de grupo de disponibilidad de un grupo de disponibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o a una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **MultiSubnetFailover=Yes** configura el controlador OLE DB para SQL Server para proporcionar una detección del servidor activo y una conexión con él más rápidas. Los valores posibles son **Yes** y **No**. El valor predeterminado es **No**. Por ejemplo:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> Para obtener más información sobre el controlador de OLE DB para la compatibilidad con SQL Server [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server Support for High Availability, Disaster Recovery](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|Sinónimo de "Network".|  
|**Network**|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|Sinónimo de "Network".|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "yes" y "no" como valores. Cuando es "no", no se permite que el objeto de origen de datos conserve ninguna información confidencial de autenticación.|  
|**PWD**|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Server**|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El valor debe ser el nombre de un servidor de la red, una dirección IP o el nombre de un alias del Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> El **dirección** palabra clave invalida la **Server** palabra clave.<br /><br /> Puede conectarse a la instancia predeterminada en el servidor local especificando uno de los valores siguientes:<br /><br /> **Server=;**<br /><br /> **Server=.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\** *instancename* **;**<br /><br /> Para obtener más información sobre la compatibilidad con LocalDB, vea [controlador OLE DB para SQL Server Support for LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md).<br /><br /> Para especificar una instancia con nombre de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], anexar **\\** _nombreDeInstancia_.<br /><br /> Cuando no se especifica ningún servidor, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Si especifica una dirección IP, asegúrese de que los protocolos TCP/IP o de canalizaciones con nombre estén habilitados en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> La sintaxis completa de la palabra clave **Server** es la siguiente:<br /><br /> **Server=**[_protocol_**:**]*Server*[**,**_port_]<br /><br /> _protocolo_ puede ser **tcp** (TCP/IP), **lpc** (memoria compartida) o **np** (canalizaciones con nombre).<br /><br /> A continuación se muestra un ejemplo de la especificación de una canalización con nombre:<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> Esta línea especifica un protocolo de canalización con nombre, una canalización con nombre en el equipo local (`\\.\pipe`), el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (`MSSQL$MYINST01`) y el nombre predeterminado de la canalización con nombre (`sql/query`).<br /><br /> Si no un *protocolo* ni **red** se especifica la palabra clave, el controlador OLE DB para SQL Server usará el orden de protocolo especificado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *port* es el puerto al que se va a conectar en el servidor especificado. De forma predeterminada, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el puerto 1433.<br /><br /> Se omiten los espacios al principio del valor pasado a **Server** en cadenas de conexión cuando se usa el controlador de OLE DB para SQL Server.|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que controlador OLE DB para SQL Server puede utilizar el valor predeterminado, SPN generado por el proveedor.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|Cuando "Sí", indica al controlador de OLE DB para SQL Server para usar el modo de autenticación de Windows para la validación del inicio de sesión. De lo contrario, indica al controlador OLE DB para SQL Server que use un nombre de usuario y una contraseña de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la validación del inicio de sesión, y deben especificarse las palabras clave PWD y UID.|  
|**TrustServerCertificate**<a href="#table1_1"><sup>**1**</sup></a>|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "yes" y "no" como valores. El valor predeterminado es "no", que significa que se validará el certificado del servidor.|  
|**UID**|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**UseFMTONLY**|SSPROP_INIT_USEFMTONLY|Controla cómo se recuperan los metadatos cuando se conecta a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] y versiones más recientes. Los valores posibles son "yes" y "no". El valor predeterminado es "no".<br /><br />De forma predeterminada, usa el controlador OLE DB para SQL Server [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) y [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) procedimientos almacenados para recuperar los metadatos. Estos procedimientos almacenados tienen algunas limitaciones (por ejemplo, producirá un error cuando se trabaja en las tablas temporales). Establecer **UseFMTONLY** a "yes" indica al controlador que use [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md) para la recuperación de metadatos en su lugar.|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|Esta palabra clave está en desuso y su valor se omite el controlador OLE DB para SQL Server.|  
|**WSID**|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
<b id="table1_1">[1]:</b> para mejorar la seguridad, se modifica el comportamiento de cifrado y los certificados de la validación cuando se usa el Token de acceso de autenticación/propiedades de inicialización o sus correspondientes palabras clave de cadena de conexión. Para obtener más información, consulte [cifrado y validación de certificados](../features/using-azure-active-directory.md#encryption-and-certificate-validation).

 Las cadenas de conexión empleadas por las aplicaciones OLE DB que usan **IDataInitialize::GetDataSource** tienen la siguiente sintaxis:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 El uso de la propiedad debe cumplir la sintaxis permitida en su ámbito.  Por ejemplo, **WSID** usa llaves (**{}**) para los caracteres de comillas y **Application Name** usa caracteres de comillas simples (**'**) o dobles (**"**). Solo se pueden entrecomillar las propiedades de cadena. Si se intenta entrecomillar un entero o la propiedad enumerada, se producirá un error que indica que la cadena de conexión no cumple la especificación OLE DB.  
  
 Los valores de atributo pueden incluirse opcionalmente entre comillas simples o dobles, y es una práctica recomendada. Esto evita que se produzcan problemas cuando los valores contienen caracteres no alfanuméricos. El carácter de comillas que se utilice también puede aparecer en los valores, siempre y cuando aparezca duplicado.  
  
 Un carácter de espacio después del signo = de una palabra clave de cadena de conexión se interpreta como un literal, aun cuando el valor esté entre comillas.  
  
 Si una cadena de conexión tiene más de una de las propiedades enumeradas en la tabla siguiente, se utilizará el valor de la última propiedad.  
  
 En la tabla siguiente se describen las palabras clave que pueden usarse con **IDataInitialize::GetDataSource**:  
  
|Palabra clave|Propiedad de inicialización|Descripción|  
|-------------|-----------------------------|-----------------|  
|**Token de acceso**<a href="#table2_1"><sup id="table2_accesstoken">**1**</sup></a>|SSPROP_AUTH_ACCESS_TOKEN|El token de acceso usado para autenticarse en Azure Active Directory. <br/><br/>**Nota:** es un error especificar esta palabra clave y también `UID`, `PWD`, `Trusted_Connection`, o `Authentication` palabras clave de cadena de conexión o sus propiedades o palabras clave correspondientes.|
|**Application Name**|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.<br /><br /> El valor predeterminado es **ReadWrite**. Para obtener más información sobre el controlador de OLE DB para la compatibilidad con SQL Server [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server Support for High Availability, Disaster Recovery](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Autenticación**<a href="#table2_1"><sup>**1**</sup></a>|SSPROP_AUTH_MODE|Especifica la autenticación de Active Directory o SQL utilizada. Los valores válidos son:<br/><ul><li>`(not set)`: Modo de autenticación determinado por otras palabras clave.</li><li>`ActiveDirectoryPassword:` Autenticación de Active Directory con Id. de inicio de sesión y la contraseña.</li><li>`ActiveDirectoryIntegrated:` Autenticación integrada de Active Directory con las credenciales de cuenta de Windows del usuario que ha iniciado sesión actualmente.</li><br/>**Nota:** tiene **recomienda** que las aplicaciones mediante `Integrated Security` (o `Trusted_Connection`) palabras clave de autenticación o sus propiedades correspondientes se establezca el valor de la `Authentication` palabra clave (o su la propiedad correspondiente) a `ActiveDirectoryIntegrated` para habilitar el nuevo comportamiento de validación de cifrado y los certificados.<br/><br/><li>`SqlPassword:` Autenticación con Id. de inicio de sesión y la contraseña.</li><br/>**Nota:** tiene **recomienda** que las aplicaciones mediante `SQL Server` autenticación establece el valor de la `Authentication` palabra clave (o la propiedad correspondiente) a `SqlPassword` para habilitar el cifrado nuevo y comportamiento de validación del certificado.</ul>|
|**Auto Translate**|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "true" y "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|Nombre del lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Origen de datos**|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Para obtener más información sobre la sintaxis válida para las direcciones, vea la descripción de la palabra clave **Server** en este tema.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que debe utilizarse. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)].|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que controlador OLE DB para SQL Server puede utilizar el valor predeterminado, SPN generado por el proveedor.|  
|**Catálogo original**|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|**Nombre de archivo inicial**|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Para usar **AttachDBFileName**, debe especificar también el nombre de la base de datos con la palabra clave DATABASE de la cadena del proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|**Seguridad integrada**|DBPROP_AUTH_INTEGRATED|Acepta el valor "SSPI" para la autenticación de Windows.|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión. Los valores reconocidos son "true" y "false". El valor predeterminado es "false".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Especifique siempre **MultiSubnetFailover=True** al conectarse a la escucha de grupo de disponibilidad de un grupo de disponibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o a una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **MultiSubnetFailover=True** configura el controlador OLE DB para SQL Server para proporcionar una detección del servidor activo y una conexión con él más rápidas. Los valores posibles son **True** o **False**. El valor predeterminado es **False**. Por ejemplo:<br /><br /> `MultiSubnetFailover=True`<br /><br /> Para obtener más información sobre el controlador de OLE DB para la compatibilidad con SQL Server [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server Support for High Availability, Disaster Recovery](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|Dirección de red de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Para obtener más información sobre la sintaxis válida para las direcciones, vea la descripción de la palabra clave **Address** en este tema.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|**Contraseña**|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "true" y "false" como valores. Cuando es "false", no se permite que el objeto de origen de datos almacene información confidencial de autenticación|  
|**Proveedor**||Controlador OLE DB para SQL Server, debe ser "MSOLEDBSQL".|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que controlador OLE DB para SQL Server puede utilizar el valor predeterminado, SPN generado por el proveedor.|  
|**Certificado de servidor de confianza**<a href="#table2_1"><sup>**1**</sup></a>|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "true" y "false" como valores. El valor predeterminado es "false", que significa que se validará el certificado del servidor.|  
|**Utilizar cifrado para los datos**<a href="#table2_1"><sup>**1**</sup></a>|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "true" y "false". El valor predeterminado es "false".|  
|**Use FMTONLY**|SSPROP_INIT_USEFMTONLY|Controla cómo se recuperan los metadatos cuando se conecta a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] y versiones más recientes. Los valores posibles son "true" y "false". El valor predeterminado es "false".<br /><br />De forma predeterminada, usa el controlador OLE DB para SQL Server [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) y [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) procedimientos almacenados para recuperar los metadatos. Estos procedimientos almacenados tienen algunas limitaciones (por ejemplo, producirá un error cuando se trabaja en las tablas temporales). Establecer **utilizar FMTONLY** a "true" indica al controlador que use [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md) para la recuperación de metadatos en su lugar.|  
|**Id. de usuario**|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Workstation ID**|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
<b id="table2_1">[1]:</b> para mejorar la seguridad, se modifica el comportamiento de cifrado y los certificados de la validación cuando se usa el Token de acceso de autenticación/propiedades de inicialización o sus correspondientes palabras clave de cadena de conexión. Para obtener más información, consulte [cifrado y validación de certificados](../features/using-azure-active-directory.md#encryption-and-certificate-validation).

 **Nota** En la cadena de conexión, la propiedad "Old Password" establece SSPROP_AUTH_OLD_PASSWORD, que es la contraseña actual (posiblemente expirada) que no está disponible a través de una propiedad de cadena del proveedor.  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>Palabras clave de la cadena de conexión Objetos de datos ActiveX (ADO)  
 Las aplicaciones ADO establecen la propiedad **ConnectionString** de los objetos **ADODBConnection** o proporcionan una cadena de conexión como parámetro al método **Open** de los objetos **ADODBConnection**.  
  
 Las aplicaciones ADO también pueden usar las palabras clave que emplea el método **IDBInitialize::Initialize** de OLE DB, pero solo para las propiedades que no tienen un valor predeterminado. Si una aplicación usa tanto palabras clave de ADO como palabras clave **IDBInitialize::Initialize** en la cadena de inicialización, se usa el valor de palabra clave de ADO. Se recomienda encarecidamente que las aplicaciones utilicen solamente palabras clave de cadena de conexión ADO.  
  
 Las cadenas de conexión utilizadas por ADO presentan la sintaxis siguiente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Los valores de atributo pueden incluirse opcionalmente entre comillas dobles y es una práctica recomendable. Esto evita que se produzcan problemas cuando los valores contienen caracteres no alfanuméricos. Los valores de atributo no pueden incluir comillas dobles.  
  
 En la tabla siguiente se describen las palabras clave que pueden utilizarse con una cadena de conexión ADO.  
  
|Palabra clave|Propiedad de inicialización|Descripción|  
|-------------|-----------------------------|-----------------|  
|**Token de acceso**<a href="#table3_1"><sup id="table3_accesstoken">**1**</sup></a>|SSPROP_AUTH_ACCESS_TOKEN|El token de acceso usado para autenticarse en Azure Active Directory.<br/><br/>**Nota:** es un error especificar esta palabra clave y también `UID`, `PWD`, `Trusted_Connection`, o `Authentication` palabras clave de cadena de conexión o sus propiedades o palabras clave correspondientes.|
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.<br /><br /> El valor predeterminado es **ReadWrite**. Para obtener más información sobre el controlador de OLE DB para la compatibilidad con SQL Server [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server Support for High Availability, Disaster Recovery](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Application Name**|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|**Autenticación**<a href="#table3_1"><sup>**1**</sup></a>|SSPROP_AUTH_MODE|Especifica la autenticación de Active Directory o SQL utilizada. Los valores válidos son:<br/><ul><li>`(not set)`: Modo de autenticación determinado por otras palabras clave.</li><li>`ActiveDirectoryPassword:` Autenticación de Active Directory con Id. de inicio de sesión y la contraseña.</li><li>`ActiveDirectoryIntegrated:` Autenticación integrada de Active Directory con las credenciales de cuenta de Windows del usuario que ha iniciado sesión actualmente.</li><br/>**Nota:** tiene **recomienda** que las aplicaciones mediante `Integrated Security` (o `Trusted_Connection`) palabras clave de autenticación o sus propiedades correspondientes se establezca el valor de la `Authentication` palabra clave (o su la propiedad correspondiente) a `ActiveDirectoryIntegrated` para habilitar el nuevo comportamiento de validación de cifrado y los certificados.<br/><br/><li>`SqlPassword:` Autenticación con Id. de inicio de sesión y la contraseña.</li><br/>**Nota:** tiene **recomienda** que las aplicaciones mediante `SQL Server` autenticación establece el valor de la `Authentication` palabra clave (o la propiedad correspondiente) a `SqlPassword` para habilitar el cifrado nuevo y comportamiento de validación del certificado.</ul>|
|**Auto Translate**|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "true" y "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|Nombre del lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Origen de datos**|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Para obtener más información sobre la sintaxis válida para las direcciones, vea la descripción de la palabra clave **Server** en este tema.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que se utilizará. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de SQL Server 2000.|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que controlador OLE DB para SQL Server puede utilizar el valor predeterminado, SPN generado por el proveedor.|  
|**Catálogo original**|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|**Nombre de archivo inicial**|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Para usar **AttachDBFileName**, debe especificar también el nombre de la base de datos con la palabra clave DATABASE de la cadena del proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|**Seguridad integrada**|DBPROP_AUTH_INTEGRATED|Acepta el valor "SSPI" para la autenticación de Windows.|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión si el servidor es [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior. Los valores reconocidos son "true" y "false". El valor predeterminado es "false".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Especifique siempre **MultiSubnetFailover=True** al conectarse a la escucha de grupo de disponibilidad de un grupo de disponibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o a una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **MultiSubnetFailover=True** configura el controlador OLE DB para SQL Server para proporcionar una detección del servidor activo y una conexión con él más rápidas. Los valores posibles son **True** o **False**. El valor predeterminado es **False**. Por ejemplo:<br /><br /> `MultiSubnetFailover=True`<br /><br /> Para obtener más información sobre el controlador de OLE DB para la compatibilidad con SQL Server [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server Support for High Availability, Disaster Recovery](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|Dirección de red de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Para obtener más información sobre la sintaxis válida para las direcciones, vea la descripción de la palabra clave **Address** en este tema.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|**Contraseña**|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "true" y "false" como valores. Cuando es "false", no se permite que el objeto de origen de datos conserve ninguna información confidencial de autenticación.|  
|**Proveedor**||Controlador OLE DB para SQL Server, debe ser "MSOLEDBSQL".|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que controlador OLE DB para SQL Server puede utilizar el valor predeterminado, SPN generado por el proveedor.|  
|**Certificado de servidor de confianza**<a href="#table3_1"><sup>**1**</sup></a>|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "true" y "false" como valores. El valor predeterminado es "false", que significa que se validará el certificado del servidor.|  
|**Utilizar cifrado para los datos**<a href="#table3_1"><sup>**1**</sup></a>|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "true" y "false". El valor predeterminado es "false".|  
|**Use FMTONLY**|SSPROP_INIT_USEFMTONLY|Controla cómo se recuperan los metadatos cuando se conecta a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] y versiones más recientes. Los valores posibles son "true" y "false". El valor predeterminado es "false".<br /><br />De forma predeterminada, usa el controlador OLE DB para SQL Server [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) y [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) procedimientos almacenados para recuperar los metadatos. Estos procedimientos almacenados tienen algunas limitaciones (por ejemplo, producirá un error cuando se trabaja en las tablas temporales). Establecer **utilizar FMTONLY** a "true" indica al controlador que use [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md) para la recuperación de metadatos en su lugar.|  
|**Id. de usuario**|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Workstation ID**|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
<b id="table3_1">[1]:</b> para mejorar la seguridad, se modifica el comportamiento de cifrado y los certificados de la validación cuando se usa el Token de acceso de autenticación/propiedades de inicialización o sus correspondientes palabras clave de cadena de conexión. Para obtener más información, consulte [cifrado y validación de certificados](../features/using-azure-active-directory.md#encryption-and-certificate-validation).

 **Nota** En la cadena de conexión, la propiedad "Old Password" establece SSPROP_AUTH_OLD_PASSWORD, que es la contraseña actual (posiblemente expirada) que no está disponible a través de una propiedad de cadena del proveedor.  
  
## <a name="see-also"></a>Vea también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
