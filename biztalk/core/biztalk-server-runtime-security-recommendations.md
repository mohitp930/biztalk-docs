---
description: "Learn more about: BizTalk Server Runtime Security Recommendations"
title: "BizTalk Server Runtime Security Recommendations"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""
ms.suite: ""
ms.topic: "article"
---
# BizTalk Server Runtime Security Recommendations
You must install the BizTalk Server runtime, or engine, on all the computers from which you want to receive, send, process, and track messages. In other words, you must install the run time components on any computer where you create a BizTalk Host instance (processing servers). It is recommended you follow these guidelines for securing and deploying the BizTalk Server runtime in your environment.

- Ensure you have the Minimum Security User Rights to perform BizTalk runtime tasks. For more information about the Minimum Security User Rights, see [Minimum Security User Rights](../core/minimum-security-user-rights.md).

  > [!NOTE]
  >  BizTalk Configuration gives the accounts the minimum permissions they need to perform their tasks.

- The service account for each host instance must have log on as service permissions on the computer where the host instance runs.

- Only the service account(s) for a host have access to MessageBox data related to a host and only these services can post to the MessageBox. To minimize the potential for information disclosure attacks, you should not use the same service account for more than one host.

- Processing servers (hosts that do not host tracking) only need to connect to the MessageBox and Management databases, and the master secret server. If you use Internet Protocol security (IPSec), you can restrict the access of the processing servers to these two databases and the master secret server.

- All components running within the same BizTalk Host have the same level of trust as the host. It is up to the BizTalk administrator to determine which components should run under the same host, and therefore, share the same level of trust. BizTalk makes sure that only assemblies installed by BizTalk administrators run in a BizTalk Host. If you want to create further restrictions as to what assemblies BizTalk uses, for example, if you want to restrict BizTalk only to run assemblies signed by a particular vendor or validate the strong name signature for an orchestration, you can use the [!INCLUDE[btsDotNetFramework](../includes/btsdotnetframework-md.md)] Code Access Security Mechanism. For more information about the Microsoft MSDN Web site at [https://go.microsoft.com/fwlink/?LinkId=60947](/dotnet/framework/misc/code-access-security).

- The authorization granularity for posting messages is at the BizTalk Host level. In other words, if you have multiple orchestrations or adapters running within the same BizTalk Host, you cannot restrict one specific orchestration to receive messages sent to the host.

- When a host is not authorized to receive a message, the host places the message in its suspended queue. By default, when receive adapters and orchestrations are running in the same host, the orchestration can read the suspended queue of the host. It is then possible for an orchestration to pick up a message that BizTalk suspended due to authorization failure. Therefore, it is recommended you do not run orchestrations and receive adapters in the same host.

- Host instances are Windows services running on a specific computer. In order to create a host instance, you must be both a BizTalk administrator and a Windows administrator on the computer where you want to create the host instance, as BizTalk creates a Windows service to correspond to the host instance.

- When Microsoft [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] generates an assembly, it uses a custom key generated by the Integrated Developer Environment (IDE). If your environment requires you to sign all assemblies with a specific key, you must either configure the IDE for all development computers to use that key or use delay signing of assemblies..

- All the components in the receive and send pipelines try to keep the memory footprint low. When the data is larger than a particular threshold, these components stream data to disk in the temporary folder (%TEMP%). You must ensure the temporary folders for the service accounts for the host instances have proper discretionary access control lists (DACLs), so that only the service account can read these files. You must also ensure the temporary folder have room to store potentially large files.

## See Also
 [Managing BizTalk Server Security](../core/managing-biztalk-server-security.md)
 [Ports for the Processing Servers](../core/ports-for-the-processing-servers.md)
 [Security Recommendations for a BizTalk Server Deployment](../core/security-recommendations-for-a-biztalk-server-deployment.md)
 [Planning for Security](../core/planning-for-security.md)