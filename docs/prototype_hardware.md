# The SNIC ET Prototype Hardware

To be able to try different desktop solutions and configurations a prototype system was procured during end of 2014. The procured hardware was chosen in a way that we could evaluate many of the availble solutions as possible. 

The final hardware consisted of:

 * XenServer with NVIDIA Grid K1/K2 cards 
   * 48 GB Memory
   * 2 x 2620v3 Xeon Processors at 2.4 GHz
   * 1 x NVIDIA Grid K1 card
   * 1 x NVIDIA Grid K2 card
   * Storage array with 6 x 1 TB 2.5 inch drives
 * Server with consumer grade NVIDIA cards
   * 64 GB Memory
   * 2 x 2620v3 Xeon Processors at 2.4 GHz
   * 2 x NVIDIA Grid GTX 980
 * Server with Xeon processor with built-in graphics
   * 32 GB Memory
   * 1 x Xeon E3-1268L
 * Infiniband switch
 * Gigabit switch
 
## Virtual environment for sharing GPU:s
 
An interesting development is the ability for virtual environments to provide access to hardware based graphics acceleration to GPU-nodes. Sharing can be done using 2 methods. In the first method, a part of a GPU is shared with a virtual machine. This is often called virtual GPU or vGPU. Similar to the concept of virtual CPU or vCPU in standard virtual environments. The method is currently not well supported for Linux based virtual machines. In the second method, an entire GPU is shared with a virtual machine. The address space of the GPU is passed-through to the virtual machine. The method is often called pass-through GPU.

For Windows based virtual machines the vGPU concept works well and the RemoteFX protocol and client can be used to access the accelerated desktop. Performance is good and the limiting factor here is the network-bandwidth to the client application. The problem with this approach is to find a way of integrating Windows support in a SNIC desktop infrastructure. This issue is covered more in the following sections.

Passing through GPU:s to Linux based virtual machines works well using XenServer as long as a generic Linux is selected when creating the virtual machine. If a supported Linux distribution is selected pass-through is disabled. To be able to take advantage of the GPU the NVIDIA driver has to be installed on the virtual machine and configured for desktop use. As the pass-through GPU does not provide a display in a normal sense. Access to acceleration must be provided through VirtualGL or similar methods of capturing the image stream from the GPU. We have succesfully tested CentOS 7 based virtual machines with pass-through GPU.

Using the installed K1/K2 cards from NVIDIA the prototype can provide 6 (4+2) pass-through GPU:s to Linux based virtual machines. For moderate needs the K2 card can be replaced with a K1 card and the soluion can provide 8 Linux based virtual machines with accelerated graphics. If vGPU gets better Linux support a single XenServer can provide up to 32 virtual machines with accelerated graphics.

## Xeon processors with built-in graphics

Another interesting development is the introduction of built-in graphics in Xeon server processors. Previously Intel support for built-in graphics was limited to desktop machines and laptops, making it difficult to provide a solution that can be used in a data center or HPC context. 

Intel now have several Xeon server processors with built-in graphics with the Xeon E3-1200 family. One of the servers in the prototype uses a E3-1268L processor with built-in graphics. These processors are often provided in a small formfactors, enabling high-density solutions with supporting accelerated graphics. 

The graphics performance of these processors are limited to low-end graphics acceleration, but could be a solution for moderate graphics need. 

## Consumer grade graphics solution

For enterprise and high-end graphics, NVIDIA provides the Quadro series of graphics cards. These are expensive cards often tailored for enterprise applications. An idea we discussed in this project, was to evaluate the use of consumer grade graphics cards such as the NVIDIA GTX 980 to provide high-end graphics performance to a lower cost. A machine with 2 GTX 980 cards where installed in a standard rack-mountable workstation. The performance is very good and they can provide an alternative to the Quadro cards. However, the problem with the consumer cards is that they are designed to be actively cooled with a built-in fan, limiting its use in high-density deployment.  