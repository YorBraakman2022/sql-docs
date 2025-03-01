---
description: "sys.dm_fts_memory_pools (Transact-SQL)"
title: "sys.dm_fts_memory_pools (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
ms.prod: sql
ms.prod_service: "database-engine, sql-database"
ms.reviewer: ""
ms.technology: system-objects
ms.topic: "reference"
f1_keywords: 
  - "dm_fts_memory_pools_TSQL"
  - "sys.dm_fts_memory_pools_TSQL"
  - "sys.dm_fts_memory_pools"
  - "dm_fts_memory_pools"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sys.dm_fts_memory_pools dynamic management view"
ms.assetid: 24747239-cd78-4d55-a00a-19233a457f42
author: rwestMSFT
ms.author: randolphwest
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.dm_fts_memory_pools (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Returns information about the shared memory pools available to the Full-Text Gatherer component for a full-text crawl or a full-text crawl range.  
   
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|ID of the allocated memory pool.<br /><br /> 0 = Small buffers<br /><br /> 1 = Large buffers|  
|**buffer_size**|**int**|Size of each allocated buffer in the memory pool.|  
|**min_buffer_limit**|**int**|Minimum number of buffers allowed in the memory pool.|  
|**max_buffer_limit**|**int**|Maximum number of buffers allowed in the memory pool.|  
|**buffer_count**|**int**|Current number of shared memory buffers in the memory pool.|  
  
## Permissions  

On [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] and SQL Managed Instance, requires `VIEW SERVER STATE` permission.

On SQL Database **Basic**, **S0**, and **S1** service objectives, and for databases in **elastic pools**, the [server admin](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) account, the [Azure Active Directory admin](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) account, or membership in the `##MS_ServerStateReader##` [server role](/azure/azure-sql/database/security-server-roles) is required. On all other SQL Database service objectives, either the `VIEW DATABASE STATE` permission on the database, or membership in the `##MS_ServerStateReader##` server role is required.   
 
## Physical Joins  
 ![Significant joins of this dynamic management view](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-pools-1.gif "Significant joins of this dynamic management view")  
  
## Relationship Cardinalities  
  
|From|To|Relationship|  
|----------|--------|------------------|  
|dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|Many-to-one|  
  
## Examples  
 The following example returns the total shared memory owned by the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Full-Text Gatherer component of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] process:  
  
```  
SELECT SUM(buffer_size * buffer_count) AS "total memory"   
    FROM sys.dm_fts_memory_pools;  
```  
  
## See Also  
 [Full-Text Search and Semantic Search Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
