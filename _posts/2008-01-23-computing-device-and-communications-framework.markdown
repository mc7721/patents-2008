---

title: Computing device and communications framework
abstract: A computing device having communications framework for a protocol stack. The framework includes a number of layers, each layer representing a layer in a protocol stack. At each layer, a protocol is a bearer of an upper adjacent layer. Each layer is arranged to monitor the availability of one or more alternate bearer layers below. Where there is more than one alternate bearer layer below, a layer is said to be mobile. In the event of a new bearer layer becoming available at a mobile layer, a decision is made as to whether or not to migrate to that bearer layer based on established policies in the mobile layer and, optionally, on communication with higher layers or with the client application. If the decision to migrate is positive, the mobile layer then ensures establishment of the new bearer layer and initiates and completes migration to it. The client of a connection active over the connection stack need not be disturbed by mobility events within the stack providing the connection.
url: http://patft.uspto.gov/netacgi/nph-Parser?Sect1=PTO2&Sect2=HITOFF&p=1&u=%2Fnetahtml%2FPTO%2Fsearch-adv.htm&r=1&f=G&l=50&d=PALL&S1=08306046&OS=08306046&RS=08306046
owner: Nokia Corporation
number: 08306046
owner_city: Espoo
owner_country: FI
publication_date: 20080123
---
This application was originally filed as PCT Application No. PCT GB2008 000242 filed on Jan. 23 2008 and claims priority to GB Application No. 0701284.2 filed on Jan. 23 2007.

The present invention relates to computing device having a communications framework and to a method of operation of such a device.

Communications between remote computers is enabled through the use of so called protocol stacks . Applications running on remote computers do not communicate directly with each other. Instead messages or other communications are sent via a protocol stacks such as the TCP IP Transmission Control Protocol Internet Protocol stack. Protocol stacks make it easier for applications to communicate with each other. They remove the need for applications to understand the details of for example how data must be sent over an Ethernet connection. Instead the application simply passes the data to the top layer of the protocol stack and the stacks on the local and remote computers ensure that the data gets to the application at the remote end.

Protocol stacks are implemented by communications frameworks which are typically provided as part of the operating system on a computing device. A communications framework typically has an API Application Programming Interface which is the point through which applications gain access to the communications framework. shows a communications model known from the prior art which may be used when for example a user wishes to send an email to a remote computer. The left hand side of the diagram represents components running on the local computer or connected to the local computer and the right hand side of the diagram represents components running on or connected to the remote computer . The local computer has loaded thereon an email client which is arranged to send and receive emails. The remote computer also has an email client . As noted above these clients cannot communicate directly with each other. Instead the email clients must send and receive messages through the communications framework which is available on the respective computers. The communications networks on each computing device include equivalent components. These components include communications framework APIs transport protocols network protocols and link protocols . The communications framework APIs provide the interface to the communications framework. As is well known in the art transport protocols are responsible for delivering data to and receiving data from applications running on a computer. In the present case the transport protocols are the TCP protocol mentioned above. Network protocols ensure that packets of data are correctly delivered from one endpoint to another. In the present case the network protocols are the IP protocol also mentioned above. Link protocols are responsible for delivery of data between adjacent nodes in a network and depend on the bearer technology being used. For example link protocols include Ethernet IEEE 802.11 link layer protocols and GPRS General Packet Radio Service .

At the bottom of the stack are bearers the type of which depends on the hardware . For example if a computer is connected to the Internet via a WiFi access point then the hardware is a WiFi adapter and the bearer is a radio access bearer which is established over the air interface between the computer and the access point.

Before a message is sent the communications framework establishes a particular set of protocols depending on the application concerned the request from the application and the available communications hardware. If a user wishes to send an email from a mobile phone a cellular connection for example via 3G will be established as well as the necessary set of protocols required to send data over the 3G connection. A message may then be sent over the communications stack which has been established.

Ordinarily the communications stack is static and persists for the lifetime of the connection. A particular set of protocols is established over a particular connection and the required communication takes place. The communications stack is then torn down. There is no mobility in this scenario as mobility is not required. In other words all layers of the communications stack provide what is required of them and there is no need to substitute one layer for another.

However in some situations mobility is required in the communications stack. shows a mobile phone which is connected to a WiFi access point . In this scenario the user of the mobile phone is browsing the Web using a Web browser. The communications framework on the phone has established the necessary protocols for this process to take place. If the user becomes mobile in the direction of arrow the phone moves out of the area of coverage of the WiFi access point . In order for the user to continue browsing the Web the communications framework must establish an alternative connection. This can be done by breaking the connection and then re establishing it over a different bearer. However it may be more desirable to do this within the communications stack using some mobility mechanism that keeps the original connection undisturbed as far as the client application is concerned. This particular scenario would require mobility at the link layer of the communications stack. In the communication framework loaded on phone is not capable of mobility. In the scenario shown in the connection with the WiFi access point and hence the connection to the Web would be lost.

Systems are currently being developed which allow mobility in the communications framework. Generic Access Network GAN is one such system which is being developed and which enables a connection to remain active when a user moves away from for example a WiFi hotspot to an area which is only covered by the mobile telephone network or vice versa . This requires a switch in the link layer protocols being used by the communications framework. The communications framework is required to maintain a connection while transferring that connection from for example IEEE 802.11 link layer protocol to a cellular link layer protocol such as 3G.

Such systems allow mobility at the link layer of the communications stack e.g. between WiFi and GPRS protocols . Known systems are not able to provide mobility at any arbitrary layer in a protocol stack.

The aim of mobility is to offer increased connection duration to a device user. The requirement for mobility has dramatically increased recently as a result of smaller and more complex computing devices. Such devices have a wider range of technologies available for them to use for communication. As a result the number of possible protocols which may be supported at any level of a communications stack has increased. For example standards such as Voice Call Continuity VCC require mobility of a voice call between a Circuit Switched Data CSD protocol stack and a Voice over IP VoIP stack. At the same time there is a desire to make the operation of the communications framework transparent to users. There is therefore the need for a more flexible communications framework which is able to support mobility at any level of the communications stack.

The present invention provides a computing device having stored thereon a communications framework the framework comprising a plurality of layers each layer arranged to encapsulate a communications protocol at least one of said layers being a mobile layer arranged to load one of a plurality of lower bearer layers wherein the mobile layer is arranged to a monitor the availability of lower adjacent bearer layers b determine whether or not to migrate to a new bearer layer when that bearer layer becomes available and c initiate migration to a new bearer layer if it is determined that migration should take place.

The present invention provides a method of controlling bearer layer migration in a communications framework the framework comprising a plurality of layers each layer arranged to encapsulate a communications protocol at least one of said layers being a mobile layer arranged to load one of a plurality of lower bearer layers the method comprising the steps of a monitoring the availability of lower adjacent bearer layers b determining whether or not to migrate to a new bearer layer when a bearer becomes available and c migrating to the new bearer layer if it is determined that migration should take place.

Other features of the present invention are defined in the appended claims. Features and advantages associated with the present invention will be apparent from the following description of the preferred embodiments.

Referring to a mobile device comprises an outer casing which includes an earphone and a microphone . The mobile device also includes a keypad and a display . The keypad enables a user to enter information into the mobile device and instruct the mobile device to perform the various functions which it provides. For example a user may enter a telephone number or select another mobile device from a list stored on the mobile device as well as perform functions such as initiating a telephone call.

As seen above in connection with a typical communications framework includes a number of horizontal layers each layer representing a different protocol or set of protocols. Each of these layers may be referred to as a communications framework layer CF layer . The layers shown in represent known protocols which communicate with adjacent upper and lower protocols in order to pass data up and down the communications stack. In this respect represents the flow of data between two endpoints. However the components shown in do not reveal anything about how the stack came into being or how the established connections are controlled. The protocol stack cannot exist by itself there needs to be something to configure it. This is handled by the communications framework.

There are three main types of activity which the communications framework must undertake. Firstly there is decision making based on established polices and configurations. This involves deciding which protocols must be loaded in response to a request from a particular client. Secondly there is the establishment control and tearing down of each instance of a protocol as a result of the above decision. Thirdly there is the actual data transfer which takes place over the protocols which have been established.

The communications framework of the present embodiment is therefore split into three planes CF planes each plane being arranged to handle one of the above noted activities. The CF planes are respectively called the management plane the control plane and the data plane. The management plane is for decision making based on established policies and configurations. The control plane is used to establish bind control re bind and tear down the protocol stack based on commands from the management plane and from a client application. The data plane is used to transport data as efficiently as possible based on established protocols.

As the layers of the protocol stack are conceptually thought of in horizontal terms the CF planes are arranged vertically. Each layer of the communications framework has data control and management elements. is a communications framework in accordance with an embodiment of the invention.

As with the communications framework shown in the framework of is divided into a number of layers. At the top of the framework is an application which is able to send messages or communicate in some other way with a remote computer. The adjacent lower layer of the framework is a communication framework API . This provides the interface through which the application communicates with the communications framework . The communications framework also includes three protocol layers which are arranged beneath the communication framework API . These layer s are a transport layer a network layer and a link layer . It will be appreciated that the communications framework is not limited to three layers. Further layers may be provided dependent upon the technology being used. The framework also includes a hardware driver communications bearers and hardware .

Each layer of the communications framework for a particular connection is an Access Point AP . An AP is an instance of the layer technology configured for a particular purpose. An adjacent lower layer AP is the bearer or carrier for an adjacent upper layer AP. Associated with each AP is AP meta data. The AP meta data includes policy information. The AP uses this information when making decisions concerning which AP to use for the bearer layer for the current connection. If the AP has a choice of more than one bearer layer AP it is said to be a mobile AP.

As noted above the communications framework is split into three planes. These planes are separated by the broken lines shown in . On the left of the communications framework is the data plane . In the middle of the framework is control plane . On the right is the management plane . The protocol layers are separated into a number of nodes each of which is associated with a particular CF layer and a particular CF plane. Each CF layer includes a CF Protocol CFP node and in the data plane . These nodes implement the data exchange for a particular CF layer. Within the control plane each layer includes at least two nodes. Firstly there are one or more Sub Connection Provider SCPR nodes and . Secondly there is a Connection Provider CPR node and . The CPR node implements connection establishment and control for the relevant CF layer. The SCPR nodes implement sub connection establishment and control for the relevant CF layer. These sub connections are individual data channels which may be established over a particular connection. Within the management plane each protocol layer includes one Meta Connection Provider MCPR node and . These nodes implement policy management and configuration for connections within a particular CF Access Point. Each MCPR node encapsulates and implements a set of AP meta data.

The above described nodes communicate with each other using message passing. Each node can communicate with adjacent nodes in the same CF layer and adjacent upper and low nodes of the same type in different CF layers. Each node may therefore communicate in four different directions. All communication between nodes in the control and management planes is asynchronous. Vertical movement of payload data between nodes in the data plane is synchronous as is the vertical movement of control information in this plane. Horizontal communication between CFP nodes and an SCPR node is asynchronous.

The above described framework can be used to enable mobility at any protocol layer of the communications framework. Each layer of the protocol stack can encapsulate different protocols. At the link layer the protocol in use will depend upon the physical connection being used by the computing device. For example if the physical connection is a WiFi link then the link layer uses the IEEE 802.11 link layer protocol. If the connection is an Ethernet connection the link layer is the Ethernet link layer protocol. The network layer may be Internet Protocol IP for example. The transport layer may be TCP User Datagram Protocol UDP etc. Protocols for higher layers in the communications stack such as for example SIP Session Initiation Protocol and RTP Real Time Transport Protocol may also be encapsulated as layers in the protocol stack. Many other protocols exist and the communications framework is arranged to handle any such protocol.

At each layer a particular protocol is a bearer for the adjacent upper layer. For example a WiFi link layer protocol may be the bearer for the IP protocol. The IP protocol may in turn be a bearer for the TCP protocol. As noted above each protocol has an associated configuration specified by the AP so it offers a specific instance of the technology as a service for one or more connections.

At any one time a communications stack in a device may host multiple concurrent connections running over multiple different Access Points via multiple different technologies.

Within an AP the MCPR node is responsible for monitoring the availability of the lower bearer AP. Within a mobile AP the MCPR is also responsible for monitoring the availability of any APs that are configured as alternatives to the current active bearer AP. At a link layer AP the bottom layer in the stack above the hardware an MCPR is responsible for monitoring the availability of the service from the hardware or the network.

In a mobile AP if a new preferred bearer AP becomes available the MCPR node in the mobile AP may notify its upper layer that a new bearer AP is available. The decision whether or not to migrate is then deferred to an upper layer or to the application. Alternatively the MCPR may decide itself whether or not to initiate migration.

Referring to the mobile device is shown in an environment which includes a mobile phone base station and a WiFi access point . The base station has an area of coverage and the WiFi access point has an associated hotspot . In the diagram the device is in a geographical position such that any communications with remote devices must take place through the mobile phone network not shown . In the user of the device is browsing the Web using a Web browser loaded on device . The communications framework has established a protocol stack. The transport layer is the TCP protocol and the network layer is the IP protocol. The protocol stack is established over a GPRS connection with the base station . The link layer is therefore the GPRS link layer protocol.

As shown by arrow the mobile device moves with the hotspot of WiFi access point . In the present case the device is arranged to transfer a connection to a particular WiFi access point when it is available. The mechanism by which the necessary CF APs migrate to an alternative bearer AP will now be described.

Before any bearer migration can take place the mobile layer must register for availability notifications with lower layer MCPRs. In the present case the network layer MCPR node must register with the link layer for availability notifications. For example it may register with IEEE 802.11 and GPRS link layers for availability notifications. When the link layer MCPR node determines that its service is available it informs the link layer MCPR node that this is the case. In the present case the network layer MCPR node is configured such that an IEEE 802.11 link layer protocol is more preferable than a GPRS link layer protocol. When the mobile device moves into WiFi hotspot the availability of the IEEE 802.11 access point is notified to the link layer MCPR node . This change in availability is passed on to the network layer MCPR node . This node determines that the available AP is more preferable than the existing GPRS link layer bearer and may optionally also request validation of this decision from the client application that owns the connection step not shown .

The network layer MCPR node then decides whether or not to accept the new bearer. In the present case the bearer is accepted and the network layer MCPR node determines that it should create and start the new bearer. This creates and starts a new link layer for the IEEE 802.11 protocol represented up to now just by the MCPR. Once the new layer is created and started the Network MCPR migrates the connection away from the GPRS AP to the IEEE 802.11 AP.

The network layer MCPR node then informs the link layer GPRS MCPR node that the connection is migrating away to a new bearer. The link layer IEEE 802.11 MCPR node then informs the network layer MCPR node that the new bearer is active. The network layer may then optionally inform the client application that owns the connection that the migration is complete so that it may optionally re establish connection sockets step not shown . The GPRS AP will be automatically shutdown at some short time afterwards if it is not still in use for another connection. The MCPR of the abandoned layer will remain and will continue to monitor availability and to report its status to the Mobile AP MCPR.

The mobile AP may choose not to act on an availability change indication from lower layers in which case there is no change in the existing stack behaviour or stack structure. The availability indication is simply ignored at the mobile AP MCPR and no migration ensues the sequence just described would not go further than step .

As noted above the above described system is arranged to provide mobility at any layer of the communications stack. At higher layers in the stack the bearers for a mobile AP would in turn have APs stacked beneath them. The MCPR nodes may be referred to as management nodes. These nodes may be provided as plug ins which may be referred to as decision point plug ins. These plug ins enable the mechanism which provides the service selection and service mobility to be separated from the decision making part of the framework. For example a mobile device can be provided with the above described communications framework but with standard decision point plug ins. The phone vendor is then able to supply their own specialised plug ins which can be configured with any service selection and mobility polices the vendor desires. This feature enables devices to be customised easily which improves time to market and enables manufactures to differentiate products.

It will be appreciated that the term bearer may refer to any layer of the communication framework. In this context one layer may act as bearer for the upper adjacent layer. The term is not limited to for example the very bottom layer as may have been the case with more traditional usage of the term.

Various modifications changes and or alterations may be made to the above described embodiments to provide further embodiments which use the underlying inventive concept falling within the spirit and or scope of the invention. Any such further embodiments are intended to be encompassed by the appended claims.

