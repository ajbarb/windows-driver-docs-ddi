---
UID: NC:wsk.PFN_WSK_ABORT_EVENT
title: PFN_WSK_ABORT_EVENT (wsk.h)
description: The WskAbortEvent event callback function notifies a WSK application that an incoming connection request on a listening socket that has conditional accept mode enabled has been dropped.
old-location: netvista\wskabortevent.htm
tech.root: netvista
ms.assetid: 50e0ef5d-0577-4b5c-b541-fc78079a953c
ms.date: 05/02/2018
ms.keywords: PFN_WSK_ABORT_EVENT, PFN_WSK_ABORT_EVENT callback, WskAbortEvent, WskAbortEvent callback function [Network Drivers Starting with Windows Vista], netvista.wskabortevent, wsk/WskAbortEvent, wskref_592d9a56-6a77-4c24-aaec-e70f84d23e49.xml
ms.topic: callback
req.header: wsk.h
req.include-header: Wsk.h
req.target-type: Windows
req.target-min-winverclnt: Available in Windows Vista and later versions of the Windows operating   systems.
req.target-min-winversvr: 
req.kmdf-ver: 
req.umdf-ver: 
req.ddi-compliance: 
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: 
req.dll: 
req.irql: "<= DISPATCH_LEVEL"
topic_type:
- APIRef
- kbSyntax
api_type:
- UserDefined
api_location:
- wsk.h
api_name:
- WskAbortEvent
product:
- Windows
targetos: Windows
req.typenames: 
---

# PFN_WSK_ABORT_EVENT callback function


## -description


The 
  <i>WskAbortEvent</i> event callback function notifies a WSK application that an incoming connection request
  on a listening socket that has conditional accept mode enabled has been dropped.


## -parameters




### -param SocketContext [in, optional]

A pointer to the socket context for the listening socket on which the incoming connection request
     was received. The WSK application provided this pointer to the WSK subsystem when it called the 
     <a href="https://msdn.microsoft.com/library/windows/hardware/ff571149">WskSocket</a> function to create the listening
     socket.


### -param InspectID [in]

A pointer to a 
     <a href="https://msdn.microsoft.com/library/windows/hardware/ff571170">WSK_INSPECT_ID</a> structure. The contents of
     the structure identify the incoming connection request that has been dropped.


## -returns



A WSK application's 
     <i>WskAbortEvent</i> event callback function must always return STATUS_SUCCESS.




## -remarks



The WSK subsystem calls a WSK application's 
    <i>WskAbortEvent</i> event callback function only when the following conditions are true:

<ul>
<li>
The WSK application created a listening socket that has conditional accept mode enabled.

</li>
<li>
An incoming connection request has been received on the listening socket, and the WSK subsystem has
      called the WSK application's 
      <a href="https://msdn.microsoft.com/40f184ac-4ef3-485a-a529-71c1f2716427">WskInspectEvent</a> event callback
      function.

</li>
<li>
The WSK application returned 
      <b>WskInspectPend</b> or <b>WskInspectAccept</b> from its 
      <i>WskAbortEvent</i> event callback function for the incoming connection request.

</li>
<li>
The incoming connection request has been dropped either locally or remotely before being fully established.

</li>
</ul>
When the WSK subsystem calls a WSK application's 
    <i>WskAbortEvent</i> event callback function, the application should terminate the inspection for the
    incoming connection request. The connection request is identified by the contents of the 
    <a href="https://msdn.microsoft.com/library/windows/hardware/ff571170">WSK_INSPECT_ID</a> structure that is pointed to
    by the 
    <i>InspectID</i> parameter.

If the WSK application calls the 
    <a href="https://msdn.microsoft.com/library/windows/hardware/ff571136">WskInspectComplete</a> function on an incoming connection request that has been aborted, the connection
    will not be established even if 
    <b>WskInspectAccept</b> is specified in the 
    <i>Action</i> parameter.

A WSK application can enable conditional accept mode on a listening socket by enabling the 
    <a href="https://msdn.microsoft.com/library/windows/hardware/ff570829">SO_CONDITIONAL_ACCEPT</a> socket option.
    For more information about conditionally accepting incoming connections, see 
    <a href="https://docs.microsoft.com/windows-hardware/drivers/network/listening-for-and-accepting-incoming-connections">Listening for and
    Accepting Incoming Connections</a>.

The WSK subsystem calls a WSK application's 
    <i>WskAbortEvent</i> event callback function at IRQL <= DISPATCH_LEVEL.

A WSK application's <i>WskAbortEvent</i> event callback function must not wait for completion of other WSK requests in the context of WSK completion or event callback functions. The callback can initiate other WSK requests (assuming that it doesn't spend too much time at DISPATCH_LEVEL), but it must not wait for their completion even when the callback is called at IRQL = PASSIVE_LEVEL.




## -see-also




<a href="https://msdn.microsoft.com/library/windows/hardware/ff571162">WSK_CLIENT_LISTEN_DISPATCH</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff571170">WSK_INSPECT_ID</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff571127">WskControlSocket</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff571136">WskInspectComplete</a>



<a href="https://msdn.microsoft.com/40f184ac-4ef3-485a-a529-71c1f2716427">WskInspectEvent</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff571149">WskSocket</a>
 

 

