---
description: "dbo.systaskids (Transact-SQL)"
title: "dbo.systaskids (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "08/09/2016"
ms.prod: sql
ms.prod_service: "database-engine"
ms.reviewer: ""
ms.technology: system-objects
ms.topic: "reference"
f1_keywords: 
  - "systaskids_TSQL"
  - "dbo.systaskids"
  - "systaskids"
  - "dbo.systaskids_TSQL"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "systaskids system table"
ms.assetid: 45c56d89-4160-4d84-80bf-a7a05488792d
author: rothja
ms.author: jroth
---
# dbo.systaskids (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contains a mapping of tasks created in earlier versions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] jobs in the current version. This table is stored in the **msdb** database.  
  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|ID of the task|  
|**job_id**|**uniqueidentifier**|ID of the job to which the task is mapped|  
  
  
