---
description: "Learn more about: InterAct Adapter Non-Repudiation"
title: "InterAct Adapter Non-Repudiation"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""
ms.suite: ""
ms.topic: "article"
---
# InterAct Adapter Non-Repudiation
Non-repudiation support for an outgoing InterAct message is obtained by setting the SwInt:NRIndicator to TRUE in the SwInt:RequestControl or SwInt:ResponseControl, as appropriate. This is required only if the service does not select non-repudiation support by default, according to the Service Profile.  
  
 Non-repudiation is based on a valid signature created by the SNL, just before transmitting the message. Therefore, in order to obtain non-repudiation support on outgoing request messages, it is mandatory for the SwInt:RequestCrypto element, contained within the SwInt:RequestControl, to be set TRUE in the SwInt:RequestControl.  
  
 For response messages, the requirement is equivalent, except that the elements involved are the SwInt:ResponseCrypto, as contained within the SwInt:ResponseControl; SwInt:ResponseCrypto must be set TRUE.  
  
 For non-repudiation support on a request, it is necessary for the message signature to cover the SwInt:RequestHeader, SwInt:RequestPayload, and the SwInt:SwiftRequestRef of the SwInt:RequestDescriptor. The SwInt:SwiftRequestRef is automatically generated by SWIFTNet Link. In connection with generating the SwInt:SwiftRequestRef, the SNL also automatically adjusts the SwSec:MemberRef value within the SwSec:CryptoControl for generating the required message signature. Similarly, for non-repudiatin support on a Response, it is necessary for the message signature to cover the SwInt:ResponseHeader, SwInt:ResponsePayload, and the SwInt:SwiftResponseRef of the SwInt:ResponseDescriptor. The SwInt:SwiftResponseRef is automatically generated by SWIFTNet Link. In connection with generating the SwInt:SwiftResponseRef, the SNL also automatically adjusts the SwSec:MemberRef value within the SwSec:CryptoControl for generating the required message signature.  
  
 If the business Service Profile selects non-repudiation by default, the necessary message signature is still required to be selected (as just described, in the SwInt:RequestControl or the SwInt:ResponseControl), and must be selected before the message leaves the SNL.  
  
 If Feature Selection according to the business Service Profile invokes Non-repudiation Support on a message, and if the necessary signature is not found with the message, then the message will be rejected by the Switch. A status exception message will be returned to the Sender of the message.  
  
 Payload encryption is not consistent with Non-repudiation Support. If Non-repudiation Support is selected for a message and the payload is encrypted in whole or in part, then the message will be rejected by SWIFTNet Link.  
  
 Note that if the service does not have the non-repudiation feature, any request or response indicating non repudiation in the control, will be rejected.  
  
## See Also  
 [InterAct Adapter Architecture](../../adapters-and-accelerators/fileact-interact/interact-adapter-architecture.md)   
 [InterAct Adapter Components](../../adapters-and-accelerators/fileact-interact/interact-adapter-components.md)   
 [InterAct Adapter Messages for Business Exchange](../../adapters-and-accelerators/fileact-interact/interact-adapter-messages-for-business-exchange.md)   
 [InterAct Adapter Client Application](../../adapters-and-accelerators/fileact-interact/interact-adapter-client-application.md)   
 [InterAct Adapter Server Application](../../adapters-and-accelerators/fileact-interact/interact-adapter-server-application.md)   
 [InterAct Adapter Store and Forward](../../adapters-and-accelerators/fileact-interact/interact-adapter-store-and-forward.md)   
 [InterAct Adapter Security Architecture](../../adapters-and-accelerators/fileact-interact/interact-adapter-security-architecture.md)   
 [InterAct Adapter End-to-End Reliable Delivery](../../adapters-and-accelerators/fileact-interact/interact-adapter-end-to-end-reliable-delivery.md)   
 [InterAct Adapter Status Monitoring](../../adapters-and-accelerators/fileact-interact/interact-adapter-status-monitoring.md)
