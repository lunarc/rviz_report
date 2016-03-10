# Remote desktop solutions

Unix and Linux have since many years been able to provide remote desktop services using the X11 protocol. However, the X11 protocol requires the user to install a X11 server on the client system, which can be very complicated and not well supported on all platforms. Also, the protocol itself is not inherintly secure and to use it securely it has to be tunneled or used through a VPN, increasing the complexity of using this solution. 

A a more platform independent solution is Virtual Network Computer or VNC. This technology uses the Remote Frame Buffer protocol or RFB. The technology relays mouse and keyboard event to a remote computer and transfers updated portions of the frame buffer over the network. VNC is open source and has spawned several projects providing different implementations of the protocol. By default the VNC implementation uses a unsecure authentication mechanism, but many of the VNC projects add an additional security layer either by tunneling through SSH or implementing its own security layer.

There also exists several proprietary solutions as well implementing their own protocols and authentication. In this project we have evaluated some of these protocols to see what benefits and limitations they provide.  

## Thinlinc

ThinLinc is a VNC implementation from a Swedish company, Cendio. The ThinLinc solution include both a native client for Mac OS X, Linux and Windows and server side components. 

The server side part of ThinLinc can be used to implement a single server solution as well as scalable solution over several servers (agents). The main server load balances desktop sessions over all agents depending on the current load of the agent server.

One of the biggest benefits of using ThinLinc is their support of native, easy to use, clients for all major platforms. With a simple one-click installer the client can be installed on all major platforms.

## Nice DCV

Desktop Cloud Visualisation, DCV, from NICE is a proprietary solution and protocol for providing remote desktop services. DCV supports hardware acceleration using NVIDIA GRID technologies as well as fully supporting hardware acceleration under Windows as well as Linux. 

The server side is built on VNC with custom additions for supporting hardware accelerated graphics. The DCV server can also operate in different modes. 

 * Pass-through mode supporting a single VM with a passthrough GPU
 * XenServer 6.x support vGPUs
 * Standalone server with GPU.
 
The benefits of NICE DCV is the support of multiple OS application servers, enabling users to run hardware accelerated Windows and Linux applications. When evaluating DCV, it was not clear how it's security framework can integrate in a HPC Linux environment. Does it support PAM-modules and integration of external authentication protcols? Pricing of the product is also quite high compared to the Thinlinc solution.

The NICE DCV solution was evaluated on XenServer 6.5 using the NVIDIA K1 and K2 cards. Installation was easy and it supported vGPU sharing under Windows.

## Microsoft Remote Desktop / RemoteFX

Microsoft have had remote desktop services built-in to the professional and enterprise offerings for a long time, with their Remote Desktop Protocol or RDP. Recently they support hardware accelererated graphics through RDP using a technology called RemoteFX. 

The RDP protocol in its non-accelerated form is supported from a Linux client using the rdesktop application. The RemoteFX protocol is however not yet supported. Using RDP, 2D Windows applications can be provided to a Linux based desktop environment using the rdesktop tool.

The RemoteFX protocol has been evaluated on the XenServer 6.5 using the NVIDIA K1 an K2 cards and works vGPUs with a special NVIDIA driver. Performance is good enough to run high-end visualisation software and games.

## XenApp / XenDesktop

The RDP protocol was originally developed by Citrix for Microsoft as their remote desktop product Terminal Server. Citrix has continued their development of RDP and this protocol is what is used in their remote desktop/application solutions XenDesktop and XenApp. 

XenDesktop provides a desktop environment and XenApp is a special derivative of the XenDesktop that only provide remote access to specific graphical applications without the desktop.

The XenDesktop and XenApp solutions can both work with hardware accelerated graphics natively or through vGPU on a hypervisor. Currently the major platform is Windows, but there is work on providing support for Linux based application and dekstop virtualisation.

It was decided not to evaluate this solution as its support for Linux is not yet developed. 