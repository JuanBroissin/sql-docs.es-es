---
title: sp_changepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication
- sp_changepublication_TSQL
helpviewer_keywords:
- sp_changepublication
ms.assetid: c36e5865-25d5-42b7-b045-dc5036225081
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5cdd5f3b4c4c1dd8ddac0df34423834c3b09b839
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131245"
---
# <a name="spchangepublication-transact-sql"></a>sp_changepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de una publicación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_changepublication [ [ @publication = ] 'publication' ]  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'**_publicación_**'**  
 Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es null.  
  
 [  **@property =** ] **'**_propiedad_**'**  
 Es la propiedad de publicación que se va a cambiar. *propiedad* es **nvarchar (255)**.  
  
 [  **@value =** ] **'**_valor_**'**  
 Es el nuevo valor de la propiedad. *valor* es **nvarchar (255)**, su valor predeterminado es null.  
  
 Esta tabla describe las propiedades de la publicación que se pueden cambiar y las restricciones de los valores de esas propiedades.  
  
|Property|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|Se pueden crear suscripciones anónimas para la publicación indicada, y *immediate_sync* también debe ser **true**. No se pueden cambiar para publicaciones punto a punto.|  
||**False**|No se pueden crear suscripciones anónimas para la publicación indicada. No se pueden cambiar para publicaciones punto a punto.|  
|**allow_initialize_from_backup**|**true**|Los suscriptores pueden inicializar una suscripción a esta publicación desde una copia de seguridad en lugar de desde una instantánea inicial. No se puede cambiar esta propiedad para que no sean de[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicaciones.|  
||**False**|Los suscriptores deben utilizar la instantánea inicial. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**allow_partition_switch**|**true**|ALTER TABLE... Las instrucciones SWITCH se pueden ejecutar en la base de datos publicada. Para obtener más información, vea [Replicar tablas e índices con particiones](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
||**False**|ALTER TABLE... No se puede ejecutar las instrucciones SWITCH en la base de datos publicada.|  
|**allow_pull**|**true**|Se permiten suscripciones de extracción para la publicación indicada. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**False**|No se permiten suscripciones de extracción para la publicación indicada. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**allow_push**|**true**|Se permiten suscripciones de inserción para la publicación indicada.|  
||**False**|No se permiten suscripciones de inserción para la publicación indicada.|  
|**allow_subscription_copy**|**true**|Habilita la funcionalidad de copia de las bases de datos suscritas a esta publicación. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**False**|Deshabilita la funcionalidad de copia de las bases de datos suscritas a esta publicación. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**alt_snapshot_folder**||Ubicación de la carpeta alternativa de la instantánea.|  
|**centralized_conflicts**|**true**|Los registros de conflictos se almacenan en el publicador. Se puede cambiar únicamente si no hay suscripciones activas. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**False**|Los registros de conflictos se almacenan tanto en el publicador como en el suscriptor que provocó el conflicto. Se puede cambiar únicamente si no hay suscripciones activas. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**compress_snapshot**|**true**|La instantánea de una carpeta de instantáneas alternativa se comprime en el formato de archivo .cab. La instantánea de la carpeta de instantáneas predeterminada no se puede comprimir.|  
||**False**|La instantánea no se comprime, que es el comportamiento predeterminado para la replicación.|  
|**conflict_policy**|**wins pub**|Directiva de resolución de conflictos para actualizar suscriptores en los que el publicador gana el conflicto. Esta propiedad se puede cambiar únicamente si no hay suscripciones activas. No es compatible con publicadores de Oracle.|  
||**Sub reinit**|Para actualizar los suscriptores; si se produce un conflicto, la suscripción debe renicializarse. Esta propiedad se puede cambiar únicamente si no hay suscripciones activas. No es compatible con publicadores de Oracle.|  
||**Sub wins**|Directiva de resolución de conflictos para actualizar suscriptores en los que el suscriptor gana el conflicto. Esta propiedad se puede cambiar únicamente si no hay suscripciones activas. No es compatible con publicadores de Oracle.|  
|**conflict_retention**||**int** que especifica el período de retención de conflictos, en días. El período de retención predeterminado es de 14 días. **0** significa que no es necesaria ninguna limpieza de conflictos. No es compatible con publicadores de Oracle.|  
|**description**||Entrada opcional en la que se describe la publicación.|  
|**enabled_for_het_sub**|**true**|Habilita la publicación para que admita suscriptores que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **enabled_for_het_sub** no se puede cambiar cuando hay suscripciones a la publicación. Es posible que deba ejecutar [procedimientos almacenados de replicación (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) para cumplir con los siguientes requisitos antes de establecer **enabled_for_het_sub** en true:<br /> - **allow_queued_tran** debe ser **false**.<br /> - **allow_sync_tran** debe ser **false**.<br /> Cambiar **enabled_for_het_sub** a **true** puede cambiar la configuración de publicación existente. Para más información, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**False**|La publicación no admite suscriptores que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**enabled_for_internet**|**true**|Se habilita la publicación para Internet y se puede utilizar el protocolo de transferencia de archivos (FTP) para transferir los archivos de instantáneas a un suscriptor. Los archivos de sincronización para la publicación se colocan en el directorio siguiente: C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\ftp. *ftp_address* no puede ser NULL. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**False**|No se habilita la publicación para Internet. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**enabled_for_p2p**|**true**|La publicación admite la replicación punto a punto. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /> Para establecer **enabled_for_p2p** a **true**, se aplican las restricciones siguientes:<br /> - **allow_anonymous** debe ser **false**<br /> - **allow_dts** debe ser **false**.<br /> - **allow_initialize_from_backup** debe ser **true**<br /> - **allow_queued_tran** debe ser **false**.<br /> - **allow_sync_tran** debe ser **false**.<br /> - **enabled_for_het_sub** debe ser **false**.<br /> - **independent_agent** debe ser **true**.<br /> - **repl_freq** debe ser **continua**.<br /> - **replicate_ddl** debe ser **1**.|  
||**False**|La publicación no admite la replicación punto a punto. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_address**||Ubicación de los archivos de instantáneas de la publicación accesible a través de FTP. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_login**||Nombre de usuario que se utiliza para conectar con el servicio FTP; se permite el valor ANONYMOUS. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_password**||Contraseña para el nombre de usuario utilizado para conectarse al servicio FTP. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_port**||Número de puerto del servicio FTP para el distribuidor. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_subdirectory**||Especifica dónde se crean los archivos de instantáneas si la publicación admite la propagación de instantáneas mediante FTP. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**immediate_sync**|**true**|Se crean o vuelven a crear archivos de sincronización para la publicación cada vez que se ejecuta el Agente de instantáneas. Los suscriptores pueden obtener los archivos de sincronización inmediatamente después de la suscripción si el Agente de instantáneas ha terminado su ejecución antes de la creación de la suscripción. Las nuevas suscripciones obtienen los últimos archivos de sincronización generados por la ejecución más reciente del Agente de instantáneas. *independent_agent* también debe ser **true**. Vea Comentarios más adelante para obtener más información acerca de **immediate_sync**.|  
||**False**|Se crean archivos de sincronización solo si hay nuevas suscripciones. Los suscriptores no pueden recibir los archivos de sincronización después de suscribirse hasta que el Agente de instantáneas haya comenzado y terminado.|  
|**independent_agent**|**true**|La publicación tiene su propio Agente de distribución dedicado.|  
||**False**|La publicación utiliza un Agente de distribución compartido, y cada par de bases de datos de publicaciones y suscripciones tiene un agente compartido.|  
|**p2p_continue_onconflict**|**true**|El Agente de distribución continúa procesando los cambios cuando se detecta un conflicto.<br /> **Precaución:** Se recomienda que use el valor predeterminado de `FALSE`. Cuando esta opción se establece en `TRUE`, el agente de distribución intenta converger los datos en la topología aplicando la fila en conflicto del nodo que tiene el identificador de originador más alto. Este método no garantiza la convergencia. Debe asegurarse de que la topología sea coherente una vez detectado un conflicto. Para obtener más información, vea "Controlar los conflictos" en [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
||**False**|El Agente de distribución detiene el procesamiento de los cambios cuando detecta un conflicto.|  
|**post_snapshot_script**||Especifica la ubicación de un archivo de script de [!INCLUDE[tsql](../../includes/tsql-md.md)] que el Agente de distribución ejecutará una vez se hayan aplicado todos los demás datos y scripts de objetos replicados durante una sincronización inicial.|  
|**pre_snapshot_script**||Especifica la ubicación de un archivo de script de [!INCLUDE[tsql](../../includes/tsql-md.md)] que el Agente de distribución ejecutará antes de que se hayan aplicado todos los demás datos y scripts de objetos replicados durante una sincronización inicial.|  
|**publish_to_ActiveDirectory**|**true**|Este parámetro ha quedado desusado y solo se admite para la compatibilidad de scripts con versiones anteriores. Ya no se puede agregar información de publicación a [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.|  
||**False**|Quita la información de publicaciones de Active Directory.|  
|**queue_type**|**sql**|Utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar las transacciones. Esta propiedad se puede cambiar únicamente si no hay suscripciones activas.<br /><br /> Nota: La compatibilidad para utilizar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queue Server ha dejado de incluirse. Si se especifica un valor de **msmq** para *valor* produce un error.|  
|**repl_freq**|**continua**|Publica la salida de todas las transacciones basadas en el registro.|  
||**Instantánea**|Publica solamente los eventos de sincronización programados.|  
|**replicate_ddl**|**1**|Las instrucciones de Lenguaje de definición de datos (DDL) que se ejecutan en el publicador se replican. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**0**|Las instrucciones de DDL no se replican. Esta propiedad no se puede cambiar para publicaciones que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La replicación de los cambios en el esquema no puede deshabilitarse al usar la replicación punto a punto.|  
|**replicate_partition_switch**|**true**|ALTER TABLE... Las instrucciones SWITCH que se ejecutan en la base de datos publicada se deberían replicar en los suscriptores. Esta opción es válida solo si *allow_partition_switch* está establecida en TRUE. Para obtener más información, vea [Replicar tablas e índices con particiones](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
||**False**|ALTER TABLE... Las instrucciones SWITCH no se deben replicar en suscriptores.|  
|**retención**||**int** que representa el período de retención, en horas, para la actividad de suscripción. Si una suscripción no ha estado activa durante el período de retención, se elimina.|  
|**snapshot_in_defaultfolder**|**true**|Los archivos de instantánea se almacenan en la carpeta de instantáneas predeterminada. Si *alt_snapshot_folder*también se especifica, los archivos de instantánea se almacenan en el valor predeterminado y las ubicaciones alternativas.|  
||**False**|Los archivos de instantánea se almacenan en la ubicación alternativa especificada por *alt_snapshot_folder*.|  
|**status**|**Active**|Los datos de la publicación están disponibles inmediatamente para los suscriptores cuando se crea la publicación. No es compatible con publicadores de Oracle.|  
||**inactivo**|Los datos de la publicación no están disponibles para los suscriptores cuando se crea la publicación. No es compatible con publicadores de Oracle.|  
|**sync_method**|**native**|Utiliza la salida de todas las tablas mediante copia masiva en modo nativo al sincronizar las suscripciones.|  
||**carácter**|Utiliza la salida de todas las tablas mediante copia masiva en modo de carácter al sincronizar las suscripciones.|  
||**simultáneas**|Utiliza un programa de copia masiva en modo nativo de todas las tablas, pero no bloquea las tablas durante el proceso de generación de instantáneas. No es válido para la replicación de instantáneas.|  
||**concurrent_c**|Utiliza un programa de copia masiva en modo de carácter de todas las tablas, pero no bloquea las tablas durante el proceso de generación de instantáneas. No es válido para la replicación de instantáneas.|  
|**TaskID**||Esta propiedad ha quedado desusada y ya no se admite.|  
|**allow_drop**|**true**|Permite `DROP TABLE` admiten DLL para artículos que forman parte de la replicación transaccional. Versión mínima admitida: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2 o posterior y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Service Pack 1 o posterior. Referencia adicional: [KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)|
||**False**|Deshabilita `DROP TABLE` DLL se admite para los artículos que forman parte de la replicación transaccional. Se trata de la **predeterminada** valor para esta propiedad.|
|**NULL** (valor predeterminado)||Devuelve la lista de valores admitidos para *propiedad*.|  
  
[  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bit**, su valor predeterminado es **0**.  
  - **0** especifica que los cambios en el artículo no invalidarán la instantánea no es válido. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizarán cambios.  
  - **1** especifica que los cambios en el artículo pueden invalidar la instantánea no es válido. Si existen suscripciones que requieran una nueva instantánea, este valor da permiso para que la instantánea existente se marque como obsoleta y se genere otra nueva.   
Vea en la sección de Notas las propiedades que, si se cambian, requieren que se genere una instantánea nueva.  
  
[ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que la acción realizada por este procedimiento almacenado puede requerir la reinicialización de las suscripciones existentes. *force_reinit_subscription* es un **bit** con un valor predeterminado de **0**.  
  - **0** especifica que los cambios en el artículo no invalidarán la suscripción para reinicializarla. Si el procedimiento almacenado detecta que el cambio requiere la reinicialización de las suscripciones existentes, se producirá un error y no se realizarán cambios.  
  - **1** especifica que los cambios en el artículo que la suscripción para reinicializarla, existente y concede permiso para que se produzca la reinicialización de suscripción.  
  
[ **@publisher** =] **'**_publisher_**'**  
 Especifica que no es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
  > [!NOTE]  
  >  *publicador* no debe usarse cuando se cambia las propiedades del artículo en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changepublication** se utiliza en la replicación de instantáneas y transaccional.  
  
 Después de cambiar cualquiera de las propiedades siguientes, debe generar una instantánea nueva y debe especificar un valor de **1** para el *force_invalidate_snapshot* parámetro.  
-   **alt_snapshot_folder**  
-   **compress_snapshot**  
-   **enabled_for_het_sub**  
-   **ftp_address**  
-   **ftp_login**  
-   **ftp_password**  
-   **ftp_port**  
-   **ftp_subdirectory**  
-   **post_snapshot_script**  
-   **pre_snapshot_script**  
-   **snapshot_in_defaultfolder**  
-   **sync_mode**  
  
Para enumerar los objetos de publicación en Active Directory mediante la **publish_to_active_directory** parámetro, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya se debe crear el objeto en Active Directory.  
  
## <a name="impact-of-immediate-sync"></a>Impacto de la sincronización inmediata  
 Cuando la sincronización inmediata está activada, todos los cambios en el registro de seguimiento se realiza inmediatamente después de que se genera la instantánea inicial incluso si no hay ninguna suscripción. Los cambios registrados se utilizan cuando un cliente utiliza la copia de seguridad para agregar un nuevo nodo del mismo nivel. Una vez restaurada la copia de seguridad, el mismo nivel está sincronizado con los cambios que se producen después de realizar la copia de seguridad. Puesto que se realiza un seguimiento de los comandos en la base de datos de distribución, la lógica de sincronización puede mirar el último LSN de copia de seguridad y usarlo como punto de partida, sabiendo que el comando está disponible si se realizó la copia de seguridad dentro del período de retención máximo. (El valor predeterminado para el período de retención mínimo es el período de retención 0 horas y el máximo es 24 horas.)  
  
 Cuando la sincronización inmediata está desactivada, los cambios se conservan al menos durante el período de retención mínimo y limpian inmediatamente para todas las transacciones que ya se han replicado. Si la sincronización inmediata está desactivada y configurada con el período de retención predeterminado, es probable que se hayan limpiado los cambios necesarios una vez realizada la copia de seguridad y que el nuevo nodo del mismo nivel no se inicialice correctamente. La única opción que queda es poner en modo inactivo la topología. Activar la sincronización inmediata proporciona mayor flexibilidad y es el valor recomendado para la replicación P2P.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_changepublication](../../relational-databases/replication/codesnippet/tsql/sp-changepublication-tra_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_changepublication**.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
