---
description: "deleteRow Method (SQLServerResultSet)"
title: "deleteRow Method (SQLServerResultSet) | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2017"
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ""
ms.technology: connectivity
ms.topic: reference
apiname: 
  - "SQLServerResultSet.deleteRow"
apilocation: 
  - "sqljdbc.jar"
apitype: "Assembly"
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
author: David-Engel
ms.author: v-davidengel
---
# deleteRow Method (SQLServerResultSet)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Deletes the current row from this[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) object and from the underlying database.  
  
## Syntax  
  
```cpp
public void deleteRow()  
```  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This deleteRow method is specified by the deleteRow method in the java.sql.ResultSet interface.  
  
 This method cannot be called when the cursor is on the insert row.  
  
 When using keyset cursors, this method leaves a gap in the result set. You can test for this gap by using the [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) method. The row numbers of the rows in the result set do not change.  
  
## See Also  
 [SQLServerResultSet Members](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet Class](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
