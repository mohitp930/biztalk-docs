---
description: "Learn more about: BizTalk-Specific Properties"
title: "BizTalk-Specific Properties1"
ms.custom: ""
ms.date: "11/30/2017"
ms.prod: "host-integration-server"
ms.reviewer: ""
ms.suite: ""
ms.topic: "article"
---
# BizTalk-Specific Properties
These context properties are only meaningful from BizTalk Server concepts and are available to be used by BizTalk applications.  
  
|Name|Type|Receive and/or Send|Description|  
|----------|----------|--------------------------|-----------------|  
|URI|String|Receive and send|The URI defines the end-point for receive locations and send ports. The URI for receive locations and send ports for MQSC Adapter are in the following format:<br /><br /> mqsc://\<CHANNELNAME>/\<TRANSPORTTYPE>/<br /><br /> \<CONNECTIONNAME>/\<QUEUEMANAGERNAME>/\<QUEUENAME><br /><br /> Receive example: mqsc://MYCHANNEL/tcp/MQSERVER(1414)/QM1/RECVQ<br /><br /> Send example:<br /><br /> mqsc://MYCHANNEL/tcp/MQSERVER(1414)/QM2/SENDQ|  
|BizTalk_CorrelationID|String|Receive|Use this property to have the MQSeries server generate a correlation identifier for use with the message.|
