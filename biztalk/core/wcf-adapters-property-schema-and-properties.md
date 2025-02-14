---
description: "Learn more about: WCF Adapters Property Schema and Properties"
title: "WCF Adapters Property Schema and Properties"
ms.custom: ""
ms.date: "02/09/2018"
ms.prod: "biztalk-server"
ms.reviewer: ""
ms.suite: ""
ms.topic: "article"
---
# WCF Adapters Property Schema and Properties

Read about the promoted properties in the WCF adapter property schema. The WCF adapters assign values to the properties that you can use in your application. WCF adapter also provides a mechanism to write but not promote the custom properties to the BizTalk message context, and a mechanism to promote the custom properties to the BizTalk message context. For more details, see [SOAP Headers with Published WCF Services](../core/soap-headers-with-published-wcf-services.md).

## Promoted properties

**Namespace:** `http://schemas.microsoft.com/BizTalk/2006/01/Adapters/WCF-properties`

#### Action

Specify the **SOAPAction** header field for outgoing messages. You can specify this value in two different ways: the single action format and the action mapping format. If you set this property in the single action format—for example, `http://contoso.com/Svc/Op1` — the **SOAPAction** header for outgoing messages is always set to the value specified in this property.

If you set this property in the action mapping format, the outgoing **SOAPAction** header is determined by the **BTS.Operation** context property. For example, if this property is set to the following XML format and the **BTS.Operation** property is set to Op1, the WCF send adapter uses `http://contoso.com/Svc/Op1` for the outgoing **SOAPAction** header.

```xml
<BtsActionMapping>
<Operation Name="Op1" Action="http://contoso.com/Svc/Op1">
<Operation Name="Op2" Action="http://contoso.com/Svc/Op2">
</BtsActionMapping>
```

If outgoing messages come from an orchestration port, orchestration instances dynamically set the **BTS.Operation** property with the operation name of the port. If outgoing messages are routed with content-based routing, you can set the **BTS.Operation** property in pipeline components.
This property is automatically promoted from incoming messages with the single action format.

Type: String
Default value: An empty string
Applies to: All WCF send adapters

#### AffiliateApplicationName

Specify the affiliate application to use for Enterprise Single Sign-On (SSO). This property is required if the **UseSSO** property is set to **True**.

Type: String
Default value: An empty string
Applies to: All WCF send adapters *except* the WCF-NetNamedPipe adapter

#### AlgorithmSuite

Specify the message encryption and key-wrap algorithms. These algorithms map to those specified in the Security Policy Language (WS-SecurityPolicy) specification.

For more information about the applicable values for the **AlgorithmSuite** property, see the **Algorithm suite** property in the **WCF-NetTcp Transport Properties Dialog Box, Send, Security** tab [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)].

Type: String
Default value: **Basic256**
Applies to:

- WCF-BasicHttp adapter
- WCF-NetMsmq adapter
- WCF-NetTcp adapter
- WCF-WSHttp adapter

#### BindingConfiguration

Specify an XML string with the **\<binding\>** element to configure different types of predefined bindings provided by Windows Communication Foundation (WCF). For more information about the system-provided binding and custom binding, see the appropriate topics in See Also.

Example:

```xml
<binding name="wsHttpBinding" transactionFlow="true">
<security><message clientCredentialType="UserName"></security>
</binding>
```

Type: String
Default value: An empty string
Applies to: WCF-Custom adapter, WCF-CustomIsolated adapter

#### BindingType

Specify the type of the binding to use for the endpoint. For more information about the applicable values for the **BindingType** property, see the **Binding Type** property in the **WCF-Custom Transport Properties Dialog Box, Send, Binding** tab [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)].

Type: String
Default value: An empty string
Applies to: WCF-Custom adapter, WCF-CustomIsolated adapter

#### ClientCertificate

Specify the thumbprint of the X.509 certificate for authenticating this send port to services. This property is required if the **ClientCredentialsType** property is set to **Certificate**. The certificate to be used for this property must be installed into the **My** store in the **Current User** location.

Type: String
Default value: An empty string
Applies to:

- WCF-BasicHttp send adapter
- WCF-WSHttp send adapter
- WCF-NetTcp send adapter
- WCF-NetMsmq send adapter

#### CloseTimeout

Specify a time span value that indicates the interval of time provided for a channel close operation to complete.

Type: String
Default value: 00:01:00
Applies to: All WCF adapters *except* WCF-Custom and WCF-CustomIsolated

#### CustomDeadLetterQueue

Specify the fully qualified URI with the **net.msmq** scheme for the location of the per-application dead-letter queue, where messages that have expired or that have failed transfer or delivery are placed. For example, net.msmq://localhost/deadLetterQueueName. The dead-letter queue is a queue on the queue manager of the sending application for expired messages that have failed to be delivered. This property is required if the **DeadLetterQueue** property is set to **Custom**.

Type: String
Default value: An empty string
Applies to: WCF-NetMsmq send adapter

#### DeadLetterQueue

Specify the dead-letter queue where messages that have failed to be delivered to the application will be transferred. For more information about the messages delivered to the dead-letter queue, see the **WCF-NetMsmq Transport Properties Dialog Box, Send, Binding** tab [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)].

Type: String
Default value: **System**
Applies to: WCF-NetMsmq send adapter

#### DisableLocationOnFailure

Specify whether to disable the receive location that fails inbound processing due to a receive pipeline failure or a routing failure. You may want to set this property to **True** when receive locations can be disabled and Denial-of-Service (DoS) is not a concern.

For example:

- WCF-Custom adapter: When the **BindingType** property is set to **netMsmqBinding**.
- WCF-Custom adapter: When the **BindingType** property is set to **customBinding**, and the **BindingConfiguration** property is configured to use custom channels that rely on queued transports such as MSMQ.
- WCF-CustomIsolated adapter: When the **BindingType** property is set to **customBinding**, and the **BindingConfiguration** property is configured to use custom channels that rely on queued transports such as MSMQ
- WCF-NetMsmq adapter

Type: Boolean
Default: **False**
Applies to:

- WCF-NetMsmq receive adapter
- WCF-Custom receive adapter
- WCF-CustomIsolated receive adapter

#### EnableTransaction

The effect of this property varies depending on the WCF adapter. For more information about this property, see how-to topics for each WCF adapter in [WCF Adapters](../core/wcf-adapters.md).

Type: Boolean
Applies to:

- WCF-WSHttp adapter
- WCF-NetTcp adapter
- WCF-NetNamedPipe adapter
- WCF-NetMsmq adapter

#### EndpointBehaviorConfiguration

Specify an XML string with the **\<behavior\>** element of the **\<endpointBehaviors\>** element to configure the behavior settings of a WCF endpoint. For more information about the **\<endpointBehaviors\>** element, see the appropriate topic in See Also.

Example:

```xml
<behavior name="sampleBehavior"><callbackTimeouts/></behavior>
```

Type: String
Default value: An empty string
Applies to: WCF-Custom send adapter

#### EstablishSecurityContext

Specify whether the security channel establishes a secure session. A secure session establishes a Security Context Token (SCT) before exchanging the application messages.

Type: Boolean
Default value: True
Applied to: WCF-WSHttp adapter

#### FromAddress

Indicate the source endpoint address through which the incoming WCF messages are sent. The property is automatically promoted from incoming messages.

Type: String
Applies to: All WCF adapters *except* the WCF-NetMsmq send adapter

#### Headers

Specify the endpoint references used to provide additional addressing information beyond the URI. When this property is used, this property must have the \<**headers**\> element as the root element. All of the address headers must be placed inside the \<**headers**\> element. This property is automatically promoted for incoming messages.

Example:

```xml
<headers>
<Region xmlns="Uri">"String"</Region>
<Member xmlns="Uri">"String"</Member>
</headers>
```

Type: String
Applies to: All WCF adapters

#### Identity

Specify the identity of the service that a receive location provides or a send port expects. The values that can be specified for the **Identity** property differ according to the security configuration. These settings enable clients to authenticate services. In the handshake process between clients and services, the Windows Communication Foundation (WCF) infrastructure will ensure that the identity of the services matches the values of the clients.

Example:

```xml
<identity>
<userPrincipalName value="username@contoso.com"/>
</identity>
```

Type: String
Default value: An empty string
Applies to: All WCF adapters

#### InboundBodyLocation

Specify the data selection for the SOAP **Body** element of incoming WCF messages. For more information about how to use the **InboundBodyLocation** property, see [Specifying the Message Body for the WCF Adapters](../core/specifying-the-message-body-for-the-wcf-adapters.md).

Type: String
Default value: UseBodyElement

Applicable values are:

- UseBodyElement: Use the content of the SOAP **Body** element of an incoming message to create the BizTalk message body part. If the **Body** element has more than one child element, only the first element becomes the BizTalk message body part.
- UseEnvelope: Create the BizTalk message body part from the entire SOAP **Envelope** of an incoming message.
- UseBodyPath: Use the body path expression in the **InboundBodyPathExpression** property to create the BizTalk message body part. The body path expression is evaluated against the immediate child element of the SOAP **Body** element of an incoming message. This property is valid only for solicit-response ports.

Applies to: All WCF adapters *except* WCF-NetMsmq send

#### InboundBodyPathExpression

Specify the body path expression to identify a specific part of an incoming message used to create the BizTalk message body part. This body path expression is evaluated against the immediate child element of the SOAP **Body** node of an incoming message. If this body path expression returns more than one node, only the first node is chosen for the BizTalk message body part. This property is required if the **InboundBodyLocation** property is set to **UseBodyPath**. For more information about how to use the **InboundBodyPathExpression** property, see [WCF Adapters Property Schema and Properties](../core/wcf-adapters-property-schema-and-properties.md).

Type: String
Default value: An empty string
Applies to: All WCF adapters *except* the WCF-NetMsmq send adapter

#### InboundHeaders

Use the **InboundHeaders** property to access the SOAP headers of incoming WCF messages. The WCF adapters copy all the SOAP header values in inbound messages to this property, which include custom SOAP headers and standard SOAP headers that the WCF infrastructure uses for such as WS-Addressing, WS-Security, and WS-AtomicTransaction. The value contained in the context property is a string containing XML data with the \<**headers**\> root element, and the incoming SOAP headers are copied as child elements of the \<**headers**\> element. For more information about how to access SOAP headers with the WCF adapters, see the SDK sample, Using Custom SOAP Headers with the WCF Adapters, from [https://go.microsoft.com/fwlink/?LinkId=79960](https://go.microsoft.com/fwlink/?LinkId=79960).

Type: String
Applies to: All WCF adapters *except* the WCF-NetMsmq send adapter

#### InboundNodeEncoding

Specify the type of encoding that the WCF receive adapter uses to decode the node identified by the body path expression specified in **InboundBodyPathExpression**. This property is required if the **InboundBodyLocation** property is set to **UseBodyPath**.

Type: String
Default value: XML

Applicable values are:

- Base64: Base64 encoding
- Hex: Hexadecimal encoding
- String: Text encoding - UTF-8
- XML: The WCF adapters create the BizTalk message body with the outer XML of the node selected by the body path expression in **InboundBodyPathExpression**.

Applies to: All WCF adapters *except* the WCF-NetMsmq send adapter

#### IsFault

Indicate whether SOAP fault messages are received. The property is automatically promoted from incoming messages.

> [!NOTE]
> The **IsFault** property cannot be used to check the received messages for transport errors such as the HTTP 404 (File or Directory Not Found) error.

Type: Boolean
Applies to: All WCF adapters *except* the WCF-NetMsmq send adapter

#### LeaseTimeout

Specify the maximum lifetime of an active pooled connection. After the specified time elapses, the connection closes after the current request is serviced.

The WCF-NetTcp adapter leverages the [NetTcpBinding](/dotnet/api/system.servicemodel.nettcpbinding) class to communicate with an endpoint. When using the [NetTcpBinding](/dotnet/api/system.servicemodel.nettcpbinding) in load-balanced scenarios, consider reducing the default lease time-out. For more information about load balancing when using the [NetTcpBinding](/dotnet/api/system.servicemodel.nettcpbinding), see the appropriate topic in See Also.

Type: String
Default value: 00:05:00
Applies to: WCF-NetTcp receive adapter

#### MaxConcurrentCalls

Specify the number of concurrent calls to a single service instance. Calls in excess of the limit are queued. Setting this value to 0 is equivalent to setting it to **Int32.MaxValue**.

> [!NOTE]
> This property cannot be tracked in the BAM Primary Import database with tracking profiles.

Type: Integer
Default value: 200
Applies to: All WCF receive adapters *except* the WCF-Custom and WCF-CustomIsolated adapters

#### MaxConnections

Specify the maximum number of connections that the listener can have waiting to be accepted by the application. When this quota value is exceeded, new incoming connections are dropped rather than waiting to be accepted.

> [!NOTE]
> Because this is an adapter handler property, this property cannot be configured in pipeline components and orchestrations.

> [!NOTE]
> This property cannot be tracked in the BAM Primary Import database with tracking profiles.

Type: Integer
Default value: 10
Applies to: WCF-NetNamedPipe adapter, WCF-NetTcp adapter

#### MaxReceivedMessageSize

Specify the maximum size, in bytes, for a message (including headers) that can be received on the wire. The size of the messages is bounded by the amount of memory allocated for each message. You can use this property to limit exposure to denial of service (DoS) attacks.

Type: Integer
Default value: 65536
Applies to:

- WCF-BasicHttp adapter
- WCF-WSHttp adapter
- WCF-NetTcp adapter
- WCF-NetNamedPipe adapter
- WCF-NetMsmq receive adapter

#### MessageClientCredentialType

Specify the type of credential to be used when performing client authentication using message-based security.

The applicable values differ for each WCF adapter. For more information about the **MessageClientCredentialType** property, see how-to topics for each WCF adapter in [WCF Adapters](../core/wcf-adapters.md).

Type: String
Applies to:

- WCF-BasicHttp adapter
- WCF-WSHttp adapter
- WCF-NetTcp adapter
- WCF-NetNamedPipe adapter

#### MessageEncoding

Specify the encoder used to encode the SOAP message.

Type: String
Default value: Text

Applicable values:

- Text: Use a text message encoder
- Mtom: Use a Message Transmission Organization Mechanism 1.0 (MTOM) encoder

Applies to: WCF-BasicHttp adapter, WCF-WSHttp adapter

#### MsmqAuthenticationMode

Specify how the message must be authenticated by the MSMQ transport.

Type: String
Default value: **WindowsDomain**
    For more information about the applicable values for the **MsmqAuthenticationMode** property, see the **MSMQ authentication mode** property in the **WCF-NetMsmq Transport Properties Dialog Box, Send, Security** tab [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)].
Applies to: WCF-NetMsmq adapter

#### MsmqEncryptionAlgorithm

Specify the algorithm to be used for message encryption on the wire when transferring messages between message queue managers. This property is available only if the **MsmqProtectionLevel** property is set to **EncryptAndSign**.

Type: String
Default value: **RC4Stream**

Applicable values are: RC4Stream, AES

Applies to: WCF-NetMsmq adapter

#### MsmqProtectionLevel

Specify the way messages are secured at the level of the MSMQ transport.

Type: String
Default value: **Sign**

Applicable values are:

- None: No protection
- Sign: Messages are signed
- EncryptAndSign: Messages are encrypted and signed. To use this protection level, you must enable **Active Directory Integration** for **MSMQ**

Applies to: WCF-NetMsmq adapter

#### MsmqSecureHashAlgorithm

Specify the hash algorithm to be used for computing the message digest. This property is not available if the **MsmqProtectionLevel** property is set to **None**.

Type: String
Default value: **SHA1**

Applicable values are: MD5, SHA1, SHA25, SHA512

Applies to: WCF-NetMsmq adapter

#### NegotiateServiceCredential

Specify whether the service credential is provisioned at the client out of band, or is obtained from the service to the client through a process of negotiation. Such a negotiation is a precursor to the usual message exchange.

If the **MessageClientCredentialType** property equals **None**, **Username**, or **Certificate**, setting this property to **False** implies that the service certificate is available at the client out of band and that the client needs to specify the service certificate. This mode is interoperable with SOAP stacks that implement WS-Trust and WS-SecureConversation.

If the **MessageClientCredentialType** property is set to **Windows**, setting this property to **False** specifies Kerberos-based authentication. This means that the client and service must be part of the same Kerberos domain. This mode is interoperable with SOAP stacks that implement the Kerberos token profile (as defined at OASIS WSS TC) as well as WS-Trust and WS-SecureConversation.

When this property is **True**, it causes a .NET SOAP negotiation that tunnels SPNego exchange over SOAP messages.

Type: Boolean
Default value: True
Applies to: WCF-WSHttp adapter

#### OpenTimeout

Specify a time span value that indicates the interval of time provided for a channel open operation to complete.

> [!NOTE]
> This property cannot be tracked in the BAM Primary Import database with tracking profiles.

Type: String
Default value: 00:01:00
Applies to: All WCF adapters *except* the WCF-Custom and WCF-CustomIsolated adapters

#### OrderedProcessing

Specify whether to process messages serially. When this property is selected, this receive location accommodates ordered message delivery when used in conjunction with a BizTalk messaging or orchestration send port that has the **Ordered Delivery** option set to `True`. For more information about the **Ordered Delivery** option, see the appropriate topics in See Also.

This property is applicable in the following cases:

- WCF-Custom adapter: When the **BindingType** property is set to **netMsmqBinding**
- WCF-Custom adapter: When the **BindingType** property is set to **customBinding**, and the **BindingConfiguration** property is configured to use custom channels that rely on transports supporting ordered delivery such as MSMQ.
- WCF-CustomIsolated adapter: When the **BindingType** property is set to **customBinding**, and the **BindingConfiguration** property is configured to use custom channels that rely on transports supporting ordered delivery.
- WCF-NetMsmq adapter

Type: String
Default value: **False**
Applies to:

- WCF-NetMsmq receive adapter
- WCF-Custom receive adapter
- WCF-CustomIsolated receive adapter

#### OutboundBodyLocation

Specify the data selection for the SOAP **Body** element of outgoing WCF messages. For more information about how to use the **OutboundBodyLocation** property, see [Specifying the Message Body for the WCF Adapters](../core/specifying-the-message-body-for-the-wcf-adapters.md).

Type: String
Default value: UseBodyElement

Applicable values are:

- UseBodyElement: Use the BizTalk message body part to create the content of the SOAP **Body** element for an outgoing message
- **UseTem****plate**: Use the template supplied in the OutboundXMLTemplate property to create the content of the SOAP **Body** element for an outgoing message

Applies to: All WCF adapters *except* the WCF-NetMsmq receive adapter

#### OutboundCustomHeaders

Specify the custom SOAP headers for outgoing messages. When this property is used, the property must have the \<**headers**\> element as the root element. All of the custom SOAP headers must be placed inside the \<**headers**\> element. If the custom SOAP header value is an empty string, you must assign \<**headers**\>\</**headers**\> or \<**headers**\> to this property. For more information about how to use SOAP headers with the WCF adapters, see the SDK sample, Using Custom SOAP Headers with the WCF Adapters, from [https://go.microsoft.com/fwlink/?LinkId=79960](https://go.microsoft.com/fwlink/?LinkId=79960).

Type: String
Applies to: All WCF adapters *except* the WCF-NetMsmq receive adapter

#### OutboundXmlTemplate

Specify the XML-formatted template for the content of the SOAP **Body** element of an outgoing message. This property is required if the **OutboundBodyLocation** property is set to **UseTemplate**. For more information about how to use the **OutboundXMLTemplate** property, see [Specifying the Message Body for the WCF Adapters](../core/specifying-the-message-body-for-the-wcf-adapters.md).

Type: String
Default value: An empty string
Applies to: All WCF adapters *except* the WCF-NetMsmq receive adapter

#### Password

Specify the password to use for authentication with the destination server when the **UseSSO** property is set to **False**.

Type: String
Default value: An empty string
Applies to: All WCF send adapters *except* the WCF-NetNamedPipe adapter

#### PropagateFaultMessage

Specify whether to route or suspend messages that fail in outbound processing. This property is valid only for solicit-response ports.

> [!NOTE]
> This property cannot be tracked in the BAM Primary Import database with tracking profiles.

Type: Boolean
Default value: **True**

Applicable values are:

- True: Route the message that fails outbound processing to a subscribing application (such as another receive port or orchestration schedule)
- False: Suspend failed messages and generate a negative acknowledgment (NACK)

Applies to: All WCF send adapters *except* the WCF-NetMsmq adapter

#### ProxyAddress

Specify the address of the proxy server. Use the **https** or the **http** scheme depending on the security configuration. This address can be followed by a colon and the port number. The property is required if the **ProxyToUse** property is set to **UserSpecified** (For example, `http://127.0.0.1:8080`)

Type: String
Default value: An empty string
Applies to: WCF-BasicHttp send adapter, WCF-WSHttp send adapter

#### ProxyPassword

Specify the password to use for the proxy server specified in the **ProxyAddress** property.

Type: String
Default value: An empty string
Applies to: WCF-BasicHttp send adapter, WCF-WSHttp send adapter

#### ProxyToUse

Specify which proxy server to use for outgoing HTTP traffic.

Type: String
Default value: **None**

Applicable values are:

- None: Do not use a proxy server for this send port
- Default: Use the proxy settings in the send handler hosting this send port
- UserSpecified: Use the proxy server specified in the **ProxyAddress** property

Applies to: WCF-BasicHttp send adapter, WCF-WSHttp send adapter

#### ProxyUserName

Specify the user name to use for the proxy server specified in the **ProxyAddress** property. The property is required if the **ProxyToUse** property is set to **UserSpecified**.

For more information about this property, see [How to Configure a WCF-WSHttp Send Port](../core/how-to-configure-a-wcf-wshttp-send-port.md) and [Configure a WCF-BasicHttp Send Port](wcf-basichttp-adapter.md).

Type: String
Applies to: WCF-BasicHttp send adapter, WCF-WSHttp send adapter

#### ReplyToAddress

Indicate the reply endpoint address for the outgoing WCF messages corresponding to incoming messages received through the request-response receive locations. The property is automatically promoted from incoming messages.

Type: String
Default value: An empty string
Applies to: All WCF adapters *except* the WCF-NetMsmq adapter

#### SecurityMode

Specify the type of security that is used. The applicable values differ for each WCF adapter. For more information about the **SecurityMode** property, see how-to topics for each WCF adapter in [WCF Adapters](../core/wcf-adapters.md).

> [!NOTE]
> This property cannot be tracked in the BAM Primary Import database with tracking profiles.

Type: String
Applies to: All WCF adapters *except* the WCF-Custom and WCF-CustomIsolated adapters

#### SendTimeout

Specify a time span value that indicates the interval of time provided for a send operation to complete. This value specifies a time span for the whole interaction to complete, even if the correspondent sends a large message.

Type: String
Default value: 00:01:00
Applies to: All WCF adapters *except* the WCF-Custom and WCF-CustomIsolated adapters

#### ServiceBehaviorConfiguration

Specify an XML string with the **\<behavior\>** element of the **\<serviceBehaviors\>** element to configure the behavior settings of a WCF service. For more information about the **\<serviceBehaviors\>** element, see the appropriate topic in See Also.

Example:

```xml
<behavior name="SampleServiceBehavior">
<serviceAuthorization principalPermissionMode="UseAspNetRoles"/>
<serviceCredentials>
<serviceCertificate findValue="539d9ab3089bb6dc187fa7dbb382cf01f8d78f5f" storeLocation="CurrentUser" x509FindType="FindByThumbprint"/>
</serviceCredentials>
<serviceMetadata httpGetEnabled="true"/>
</behavior>
```

Type: String
Default value: An empty string
Applies to: WCF-Custom receive adapter, WCF-CustomIsolated adapter

#### ServiceCertificate

If this property is used for receive locations, specify the thumbprint of the X.509 certificate for the receive locations that clients use to authenticate the service. The certificate to be used for this property must be installed into the **My** store in the **Current User** location.

If this property is used for send ports, specify the thumbprint of the X.509 certificate for authenticating the service to which this send port sends messages. The certificate to be used for this property must be installed into the **Other People** store in the **Local Machine** location.

Type: String
Default value: An empty string
Applies to:

- WCF-BasicHttp adapter
- WCF-NetMsmq adapter
- WCF-WSHttp adapter
- WCF-NetTcp receive adapter

#### SuspendMessageOnFailure

Specify whether to suspend the request message that fails inbound processing due to a receive pipeline failure or a routing failure.

Type: Boolean
Default value: True
Applies to: All WCF receive adapters

#### TextEncoding

Specify the character set encoding to be used for emitting messages on the binding when the **MessageEncoding** property is set to **Text**.

> [!NOTE]
> This property cannot be tracked in the BAM Primary Import database with tracking profiles.

Type: String
Default value: utf-8

Applicable values are:

- unicodeFFF: Unicode BigEndian encoding
- utf-16: 16-bit encoding
- utf-8: 8-bit encoding

Applies to: WCF-BasicHttp adapter, WCF-WSHttp adapter

#### TimeToLive

Specify a time span for how long the messages are valid before they are expired and put into the dead-letter queue. This property is set to ensure that time-sensitive messages do not become stale before they are processed by a send port. A message in a queue that is not consumed by this send port within the time interval specified is said to be expired. Expired messages are sent to special queue called the dead-letter queue. The location of the dead-letter queue is set with the **DeadLetterQueue** property.

Type: String
Default value: 1.00:00:00
Applies to: WCF-NetMsmq send adapter

#### To

Specify the destination endpoint address for outgoing WCF messages that the WCF send ports send.

Type: String
Default value: An empty string
Applies to: All WCF send adapters

#### TransactionProtocol

Specify the transaction protocol to be used with this binding. This property is required if the **EnableTransaction** property is set to **True**.

Type: String
Default value: OleTransaction

Applicable values are: OleTransaction, WS-AtomicTransaction

Applies to: WCF-NetNamedPipe adapter,  WCF-NetTcp adapter

#### TransportClientCredentialType

Specify the type of credential to be used when performing the send port authentication. The applicable values differ for each WCF adapter. For more information about the **TransportClientCredentialType** property, see how-to topics for each WCF adapter in [WCF Adapters](../core/wcf-adapters.md).

Type: String
Applies to: WCF-Basic adapter, WCF-NetTcp adapter, WCF-WSHttp adapter

#### TransportProtectionLevel

Specify security at the level of the TCP transport. Signing messages mitigates the risk of a third party tampering with the message while it is being transferred. Encryption provides data-level privacy during transport.

Type: String
Default value: **EncryptAndSign**

Applicable values are:

- None: No protection
- Sign: Messages are signed
- EncryptAndSign: Messages are encrypted and signed

Applies to: WCF-NetTcp adapter, WCF-NetNamedPipe adapter

#### UserName

Specify the user name to use for authentication with the destination server when the **UseSSO** property is set to **False**. You do not have to use the domain\user format for this property.

Type: String
Default value: An empty string
Applies to: All WCF send adapters *except* the WCF-NetNamedPipe adapter

#### UseSourceJournal

Specify whether copies of messages processed by this send port should be stored in the source journal queue.

Type: Boolean
Default value: False
Applies to: WCF-NetMsmq send adapter

#### UseSSO

Specify whether to use Single Sign-On to retrieve client credentials for authentication with the destination server.

**Note**
This property cannot be tracked in the BAM Primary Import database with tracking profiles.

Type: Boolean
Default value: False
Applies to: All WCF send adapters *except* the WCF-NetNamedPipe adapter

#### ReferencedBindings

Specify the binding configurations referenced by the **bindingConfiguration** attribute of the **\<issuer\>** element for the **wsFederationHttpBinding** and **customBinding**, which indicates the Security Token Service (STS) that issues security tokens. For more information about the **\<issuer\>** element, see the topic, "\<issuer\>" at [https://go.microsoft.com/fwlink/?LinkId=83476](/dotnet/framework/configure-apps/file-schema/wcf/issuer).

The binding information including the **\<issuer\>** element for the **wsFederationHttpBinding** and **customBinding** can be configured through the **BindingConfiguration** property of the WCF-Custom and WCF-CustomIsolated adapters. All of the referenced binding configurations for this property must be placed in the form of the [\<bindings\>](/dotnet/framework/configure-apps/file-schema/wcf/bindings) element.

> [!NOTE]
> The **bindingConfiguration** attribute of the **\<issuer\>** element must refer to a valid binding name in this property.

> [!NOTE]
> The **\<issuer\>** element in the referenced binding configurations can also refer to a different binding configuration in this property if this reference chain does not make a circular dependency.

Example:

```
WCF.BindingConfiguration = @"<wsFederationHttpBinding>
<binding name=""sampleBinding"">
<security mode=""Message"">
<message issuedKeyType=""AsymmetricKey"">
<issuer address=""http://www.contoso.com/samplests"" binding=""wsFederationHttpBinding"" bindingConfiguration=""**contosoSTSBinding**""/>
</message>
</security>
</binding>
</wsFederationHttpBinding>";
WCF.ReferencedBinding =@"<bindings>
<wsFederationHttpBinding>
<binding name=""**contosoSTSBinding**"">
<security mode=""Message"">
<message negotiateServiceCredential=""false"">
<issuer address=""https://northwind.com/samplests"" bindingConfiguration=""**northwindBinding**"" binding=""wsHttpBinding"">
</issuer>
</message>
</security>
</binding>
</wsFederationHttpBinding>
<wsHttpBinding>
<binding name=""**northwindBinding**"">
<security mode=""Message"">
<message clientCredentialType=""Certificate""/>
</security>
</binding>
</wsHttpBinding>
</bindings>"
```

> [!NOTE]
> **ReferencedBinding** property must not contain the binding configuration used in the **BindingConfiguration** property.

Type: String
Default value: An empty string
Applies to: WCF-Custom adapter, WCF-CustomIsolated adapter

## See Also

 [WCF Adapters](../core/wcf-adapters.md)
 [\<behavior\> of \<endpointBehaviors\>](/dotnet/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors)
 [\<bindings\>](/dotnet/framework/configure-apps/file-schema/wcf/bindings)
 [\<behavior\> of \<serviceBehaviors\>](/dotnet/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors)
 [Ordered Delivery of Messages](../core/ordered-delivery-of-messages.md)
 [Load Balancing](/dotnet/framework/wcf/load-balancing)
