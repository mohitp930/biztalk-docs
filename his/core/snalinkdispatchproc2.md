---
description: "Learn more about: SNALinkDispatchProc"
title: "SNALinkDispatchProc2"
ms.custom: ""
ms.date: "11/30/2017"
ms.prod: "host-integration-server"
ms.reviewer: ""
ms.suite: ""
ms.topic: "article"
---
# SNALinkDispatchProc
The **SNALinkDispatchProc** function is the link dispatcher function. The Base calls this function whenever one of the following events occurs:  
  
-   A message arrives for the link.  
  
-   The Base timer expires.  
  
-   Contact is lost with the local node.  
  
```  
VOID SNALinkDispatchProc(  
PTRBFNDR msgptr,  
INTEGER function,  
INTEGER locality   
);  
```  
  
## Parameters  
 *msgptr*  
 The message to be processed, or NULL if some other event is being notified.  
  
 *function*  
 The reason for **SNALinkDispatchProc** being called.  
  
 *locality*  
 L value (only valid for function SBLOST).  
  
## Remarks  
 The *function* parameter can have one of three values:  
  
- 0—Message received.  
  
- SBLOST—Contact lost with local node; L-value of locality.  
  
- SBTICK—Base timer has expired; occurs every five seconds.  
  
  For suggested usage of this function, see [Sample Code for SNALinkDispatchProc](./sample-code-for-snalinkdispatchproc2.md).
