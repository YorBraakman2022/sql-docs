---
title: "Clustered and nonclustered indexes described"
description: "Clustered and nonclustered indexes described"
ms.prod: sql
ms.prod_service: "table-view-index, sql-database"
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords: 
  - "query optimizer [SQL Server], index usage"
  - "index concepts [SQL Server]"
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ""
ms.custom: FY22Q2Fresh
ms.date: 10/25/2021
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Clustered and nonclustered indexes described

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

An index is an on-disk structure associated with a table or view that speeds retrieval of rows from the table or view. An index contains keys built from one or more columns in the table or view. These keys are stored in a structure (B-tree) that enables [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to find the row or rows associated with the key values quickly and efficiently.

[!INCLUDE [sql-b-tree](../../includes/sql-b-tree.md)]

A table or view can contain the following types of indexes:

- Clustered

  - Clustered indexes sort and store the data rows in the table or view based on their key values. These are the columns included in the index definition. There can be only one clustered index per table, because the data rows themselves can be stored in only one order.  
  - The only time the data rows in a table are stored in sorted order is when the table contains a clustered index. When a table has a clustered index, the table is called a clustered table. If a table has no clustered index, its data rows are stored in an unordered structure called a heap.

- Nonclustered

  - Nonclustered indexes have a structure separate from the data rows. A nonclustered index contains the nonclustered index key values and each key value entry has a pointer to the data row that contains the key value.
  - The pointer from an index row in a nonclustered index to a data row is called a row locator. The structure of the row locator depends on whether the data pages are stored in a heap or a clustered table. For a heap, a row locator is a pointer to the row. For a clustered table, the row locator is the clustered index key.

  - You can add nonkey columns to the leaf level of the nonclustered index to by-pass existing index key limits, and execute fully covered, indexed, queries. For more information, see [Create indexes with included columns](../../relational-databases/indexes/create-indexes-with-included-columns.md). For details about index key limits see [Maximum capacity specifications for SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md).

Both clustered and nonclustered indexes can be unique. This means no two rows can have the same value for the index key. Otherwise, the index is not unique and multiple rows can share the same key value. For more information, see [Create unique indexes](../../relational-databases/indexes/create-unique-indexes.md).

Indexes are automatically maintained for a table or view whenever the table data is modified.

See [Indexes](../../relational-databases/indexes/indexes.md) for additional types of special purpose indexes.

## Indexes and constraints

Indexes are automatically created when PRIMARY KEY and UNIQUE constraints are defined on table columns. For example, when you create a table with a UNIQUE constraint, [!INCLUDE[ssDE](../../includes/ssde-md.md)] automatically creates a nonclustered index. If you configure a PRIMARY KEY, [!INCLUDE[ssDE](../../includes/ssde-md.md)] automatically creates a clustered index, unless a clustered index already exists. When you try to enforce a PRIMARY KEY constraint on an existing table and a clustered index already exists on that table, SQL Server enforces the primary key using a nonclustered index.

For more information, see [Create primary keys](../../relational-databases/tables/create-primary-keys.md) and [Create unique constraints](../../relational-databases/tables/create-unique-constraints.md).

## How indexes are used by the Query Optimizer

Well-designed indexes can reduce disk I/O operations and consume fewer system resources therefore improving query performance. Indexes can be helpful for a variety of queries that contain SELECT, UPDATE, DELETE, or MERGE statements. Consider the query `SELECT Title, HireDate FROM HumanResources.Employee WHERE EmployeeID = 250` in the [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] database. When this query is executed, the query optimizer evaluates each available method for retrieving the data and selects the most efficient method. The method may be a table scan, or may be scanning one or more indexes if they exist.

When performing a table scan, the query optimizer reads all the rows in the table, and extracts the rows that meet the criteria of the query. A table scan generates many disk I/O operations and can be resource intensive. However, a table scan could be the most efficient method if, for example, the result set of the query is a high percentage of rows from the table.

When the query optimizer uses an index, it searches the index key columns, finds the storage location of the rows needed by the query and extracts the matching rows from that location. Generally, searching the index is much faster than searching the table because unlike a table, an index frequently contains very few columns per row and the rows are in sorted order.

 The query optimizer typically selects the most efficient method when executing queries. However, if no indexes are available, the query optimizer must use a table scan. Your task is to design and create indexes that are best suited to your environment so that the query optimizer has a selection of efficient indexes from which to select. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provides the [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md) to help with the analysis of your database environment and in the selection of appropriate indexes.

> [!IMPORTANT]
> For more information about index design guidelines and internals, refer to the [SQL Server Index Design Guide](../../relational-databases/sql-server-index-design-guide.md).

## Next steps

- [SQL Server Index Design Guide](../../relational-databases/sql-server-index-design-guide.md)
- [Create Clustered Indexes](../../relational-databases/indexes/create-clustered-indexes.md)
- [Create Nonclustered Indexes](../../relational-databases/indexes/create-nonclustered-indexes.md)
