---
description: "Learn more about: Limitations"
title: "Limitations2"
ms.custom: ""
ms.date: "11/30/2017"
ms.prod: "host-integration-server"
ms.reviewer: ""
ms.suite: ""
ms.topic: "article"
---
# Limitations
The following describes the limitations on SQL statements for the Managed Provider for Host Files.  
  
## SQL Limitations  
  
-   If the table contains a complex type (for example, Unions), then the `INSERT` and `UPDATE` commands should set the values for all the complex types.  
  
-   Data definition language (DDL) commands like `ALTER` and `CREATE` are not supported.  
  
-   Any form of data control language (DCL) is not supported.  
  
-   The expression: {COLUMN NAME} AS {EXPRESSION} is not supported.  
  
## See Also  
 [SQL Parsing in the Managed Data Provider for Host Files](../core/sql-parsing-in-the-managed-data-provider-for-host-files2.md)
