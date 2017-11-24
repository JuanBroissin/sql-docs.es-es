---
title: dbo.sysjobhistory (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysjobhistory_TSQL
- dbo.sysjobhistory
- sysjobhistory
- sysjobhistory_TSQL
dev_langs: TSQL
helpviewer_keywords: sysjobhistory system table
ms.assetid: 1b1fcdbb-2af2-45e6-bf3f-e8279432ce13
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 63d461ff997a9a438965e039a727999876b3d7a3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobhistory-transact-sql"></a>dbo.sysjobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información acerca de la ejecución de los trabajos programados por el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta tabla se almacena en la **msdb** base de datos.  
  
> **Nota:** datos se actualizan únicamente cuando haya finalizado el paso de trabajo.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**valor de instance_id**|**int**|Identificador único de la fila.|  
|**job_id**|**uniqueidentifier**|Id. del trabajo.|  
|**step_id**|**int**|Id. del paso en el trabajo.|  
|**Step_name**|**sysname**|Nombre del paso.|  
|**sql_message_id**|**int**|Id. de los mensajes de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devueltos si el trabajo genera algún error.|  
|**sql_severity**|**int**|Gravedad de cualquier error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Mensaje**|**nvarchar(4000)**|Texto de un error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si existe.|  
|**run_status**|**int**|Estado de la ejecución del trabajo:<br /><br /> **0** = error<br /><br /> **1** = se ha realizado correctamente<br /><br /> **2** = reintento<br /><br /> **3** = cancelado|  
|**run_date**|**int**|Fecha en que se empezó a ejecutar el trabajo o paso. En el caso de un historial En curso, es la fecha y hora en que fue escrito.|  
|**tiempo de ejecución**|**int**|Hora a la que comenzó el trabajo o paso.|  
|**run_duration**|**int**|Tiempo transcurrido en la ejecución del trabajo o paso en **HHMMSS** formato.|  
|**operator_id_emailed**|**int**|Id. del operador al que se notificó la terminación del trabajo.|  
|**operator_id_netsent**|**int**|Id. del operador al que se notificó con un mensaje la terminación del trabajo.|  
|**operator_id_paged**|**int**|Id. del operador al que se notificó por buscapersonas la terminación del trabajo.|  
|**retries_attempted**|**int**|Número de intentos de ejecución del trabajo o paso.|  
|**servidores**|**sysname**|Nombre del servidor en el que se ejecutó el trabajo.|  
  
  ## <a name="example"></a>Ejemplo
 El siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta convertirá la **tiempo de ejecución** y **run_duration** columnas en un formato descriptivo más.  Ejecute el script en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 
 ```tsql
 SET NOCOUNT ON;
 
 SELECT sj.name,
        sh.run_date,
        sh.step_name,
        STUFF(STUFF(RIGHT(REPLICATE('0', 6) +  CAST(sh.run_time as varchar(6)), 6), 3, 0, ':'), 6, 0, ':') 'run_time',
        STUFF(STUFF(STUFF(RIGHT(REPLICATE('0', 8) + CAST(sh.run_duration as varchar(8)), 8), 3, 0, ':'), 6, 0, ':'), 9, 0, ':') 'run_duration (DD:HH:MM:SS)  '
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobhistory sh
ON sj.job_id = sh.job_id
```