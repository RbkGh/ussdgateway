## Mobicents USSD Introduction ##

Mobicents implementation of USSD Gateway is first and only open source USSD Gateway available as of today. Mobicents USSD Gateway is 100% Java hence independent of any OS. The Mobicents USSD Gateway makes use of
HTTP and SMPP`**` protocol between gateway and Value Added Service Modules or third party applications. Mobicents USSD Gateway receives the USSD request from subscriber handset/device via GSM Signaling network,
these requests are translated to HTTP or SMPP depending on the rules set by the user and then routed to corresponding Value Added Service (VAS) or 3rd party application. JBoss Drools is used to derive the
protocol between Gateway and USSD Application and also the information of the server (for example IP, port etc) where these applications are deployed.

USSD stands for Unstructured Supplementary Service Data what is a capability of GSM mobile phone much like the Short Message Service (SMS). But there is a difference between USSD and SMS handling.

SMS uses store and forward method of message delivery. Short Message is delivered first to Sender's Short Message Service Center (SMSc) which will try to deliver the message to recipient. So SMS does not guarantee that message will be delivered instantly.

USSD information is sent from mobile handset directly to application platform handling service. So USSD suppose to establish a real time session between mobile handset and application handling the service.
The concept of real time session is very useful for constructing an interactive menu driven application.

A user who is dialing USSD service number initiates dialog with USSD handling application deployed on the Mobicents Platform as depicted on the figure below. The "Network Node" depicted could be MSC, HLR or VLR.
The Mobicents Platform integrates with "Network Node" using MAP ([Mobicents jSS7](http://code.google.com/p/jss7/)) protocol.

![http://wiki.ussdgateway.googlecode.com/git/images/ussd-arch.png](http://wiki.ussdgateway.googlecode.com/git/images/ussd-arch.png)

The detailed description of the allowed MMIs or phone number which user can dial is presented in 3GPP TS 22.090. In the user's home network the following number range is defined for USSD services: _1, 2 or 3 digits from
the set (`*`, #) followed by 1X(Y), where X=any number 0-4, Y=any number 0-9, then, optionally "`*`" followed by any number of any characters, and concluding with # SEND_

For example user can dial `*`#122# to reach a specific USSD service which is deployed in the home network and. The application in its order can reply with menu. One of the biggest benefits is that this service is always
available even when user is currently in roaming.

Below diagram depicts typical MAP message flow for implementing data transfer between "Network Node" and Mobicents platform to implement menu driven application. For more information on mobile- (and network-)
initiated USSD operations and the use of MAP USSD services, refer to [24.090](3GPPTS.md) in the References section.

![http://wiki.ussdgateway.googlecode.com/git/images/ussd-map.png](http://wiki.ussdgateway.googlecode.com/git/images/ussd-map.png)

Mobile initiated USSD service starts when user dials USSD string `*`#122#.

  * The Network sends TCAP Begin message with Component MAP\_PROCESS\_UNSTRUCTURED\_SS\_REQUEST to the Mobicents platform. The Mobicents platform invokes USSD application logic .
  * Application request additional information from user (action one or action two) via MAP\_UNSTRUCTURED\_SS\_REQUEST encapsulated in TCAP Continue message. At this time TCAP Dialogue starts.
  * Application receives user's selection of the action.
  * Application performs its logic and sends a response back to the user. At this time application do not want to get additional information from the user and it sends response using MAP\_PROCESS\_UNSTRUCTURED\_SS\_REQUEST and terminates TCAP dialogue.


Existing MSC, VLR, and HLR network elements are proprietary and run on non-standard operating environments located in trusted operator's zones that make it difficult to build and deploy new applications.
Also, these network elements do not provide the tools and interfaces needed to access and retrieve data from content providers over Internet. The USSD Gateway connects to the MSC, VLR, or HLR and enables the flow of
USSD messages to be extended to an open, standards-based application server located in the IP network. The AS also provides the tools and interfaces to enable access to the content providers through the Internet.

Note : `**` SMPP protocol is not implemented yet and is in roadmap.