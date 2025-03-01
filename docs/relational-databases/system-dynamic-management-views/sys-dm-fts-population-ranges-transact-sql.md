---
description: "sys.dm_fts_population_ranges (Transact-SQL)"
title: "sys.dm_fts_population_ranges (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
ms.prod: sql
ms.prod_service: "database-engine, sql-database"
ms.technology: system-objects
ms.topic: "reference"
f1_keywords: 
  - "sys.dm_fts_population_ranges"
  - "sys.dm_fts_population_ranges_TSQL"
  - "dm_fts_population_ranges_TSQL"
  - "dm_fts_population_ranges"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sys.dm_fts_population_ranges dynamic management view"
ms.assetid: 58d8564b-9c43-4965-a31c-2893890334ef
author: rwestMSFT
ms.author: randolphwest
ms.reviewer: mikeray
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.dm_fts_population_ranges (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Returns information about the specific ranges related to a full-text index population currently in progress.  
   
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**memory_address**|**varbinary(8)**|Address of memory buffers allocated for activity related to this subrange of a full-text index population.|  
|**parent_memory_address**|**varbinary(8)**|Address of memory buffers representing the parent object of all ranges of population related to a full-text index.|  
|**is_retry**|**bit**|If the value is 1, this subrange is responsible for retrying rows that encountered errors.|  
|**session_id**|**smallint**|ID of the session that is currently processing this task.|  
|**processed_row_count**|**int**|Number of rows that have been processed by this range. Forward progress is persisted and counted every 5 minutes, rather than with every batch commit.|  
|**error_count**|**int**|Number of rows that have encountered errors by this range. Forward progress is persisted and counted every 5 minutes, rather than with every batch commit.|  
  
## Permissions  

On [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] and SQL Managed Instance, requires `VIEW SERVER STATE` permission.

On SQL Database **Basic**, **S0**, and **S1** service objectives, and for databases in **elastic pools**, the [server admin](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) account, the [Azure Active Directory admin](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) account, or membership in the `##MS_ServerStateReader##` [server role](/azure/azure-sql/database/security-server-roles) is required. On all other SQL Database service objectives, either the `VIEW DATABASE STATE` permission on the database, or membership in the `##MS_ServerStateReader##` server role is required.   
 
## Physical Joins  
 ![Significant joins of this dynamic management view](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-population-ranges-1.gif "Significant joins of this dynamic management view")  
  
## Relationship Cardinalities  
  
|From|To|Relationship|  
|----------|--------|------------------|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|Many-to-one|  
  
## See Also  
  [Full-Text Search and Semantic Search Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
