---
UID: NC:ndis.MINIPORT_RETURN_NET_BUFFER_LISTS
title: MINIPORT_RETURN_NET_BUFFER_LISTS (ndis.h)
description: NDIS calls the MiniportReturnNetBufferLists function to return ownership of NET_BUFFER_LIST structures, associated NET_BUFFER structures, and any attached MDLs to a miniport driver.
old-location: netvista\miniportreturnnetbufferlists.htm
tech.root: netvista
ms.assetid: 0f33ae87-164e-40dc-a915-28211a0d74b7
ms.date: 05/02/2018
ms.keywords: MINIPORT_RETURN_NET_BUFFER_LISTS, MINIPORT_RETURN_NET_BUFFER_LISTS callback, MiniportReturnNetBufferLists, MiniportReturnNetBufferLists callback function [Network Drivers Starting with Windows Vista], ndis/MiniportReturnNetBufferLists, ndis_sendrcv_ref_dfe745f1-643d-4834-827c-687aa6404cf2.xml, netvista.miniportreturnnetbufferlists
ms.topic: callback
req.header: ndis.h
req.include-header: Ndis.h
req.target-type: Windows
req.target-min-winverclnt: Supported in NDIS 6.0 and later.
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
- Ndis.h
api_name:
- MiniportReturnNetBufferLists
product:
- Windows
targetos: Windows
req.typenames: 
---

# MINIPORT_RETURN_NET_BUFFER_LISTS callback function


## -description


NDIS calls the 
   <i>MiniportReturnNetBufferLists</i> function to return ownership of 
   <a href="https://msdn.microsoft.com/library/windows/hardware/ff568388">NET_BUFFER_LIST</a> structures, associated 
   <a href="https://msdn.microsoft.com/library/windows/hardware/ff568376">NET_BUFFER</a> structures, and any attached MDLs to a
   miniport driver.
<div class="alert"><b>Note</b>  You must declare the function by using the <b>MINIPORT_RETURN_NET_BUFFER_LISTS</b> type.
   For more information, see the following Examples section.</div><div> </div>

## -parameters




### -param MiniportAdapterContext [in]

A handle to a context area that the miniport driver allocated in its 
     <a href="https://msdn.microsoft.com/b146fa81-005b-4a6c-962d-4cb023ea790e">MiniportInitializeEx</a> function.
     The miniport driver uses this context area to maintain state information about an adapter.


### -param NetBufferLists [in]

A pointer to a linked list of 
     <a href="https://msdn.microsoft.com/library/windows/hardware/ff568388">NET_BUFFER_LIST</a> structures that NDIS is
     returning to the miniport driver. The linked list can contain NET_BUFFER_LIST structures from multiple
     previous calls to the 
     <a href="https://msdn.microsoft.com/b87dba3e-c18f-4ea2-8bd5-ec3cdafc534b">
     NdisMIndicateReceiveNetBufferLists</a> function.


### -param ReturnFlags [in]

NDIS flags that can be combined with an OR operation. This function supports the NDIS_RETURN_FLAGS_DISPATCH_LEVEL flag which, if set, indicates that the
     current IRQL is DISPATCH_LEVEL. For more information about this flag, see 
     <a href="https://msdn.microsoft.com/ac559f4f-0138-4b9a-8f1b-44a2973fd6a1">Dispatch IRQL Tracking</a>.


## -returns



None




## -remarks



<i>MiniportReturnNetBufferLists</i> is a required function for miniport drivers that indicate received
    network data with the 
    <a href="https://msdn.microsoft.com/b87dba3e-c18f-4ea2-8bd5-ec3cdafc534b">
    NdisMIndicateReceiveNetBufferLists</a> function. When an overlying driver calls the 
    <a href="https://msdn.microsoft.com/1a45bc5c-cdc1-46d2-905b-3d5eea3645c1">
    NdisReturnNetBufferLists</a> function, NDIS calls the 
    <i>MiniportReturnNetBufferLists</i> function of the miniport driver that indicated the specified 
    <a href="https://msdn.microsoft.com/library/windows/hardware/ff568388">NET_BUFFER_LIST</a> structures.

<i>MiniportReturnNetBufferLists</i> can prepare a returned NET_BUFFER_LIST structure for use in a
    subsequent receive indication. Although 
    <i>MiniportReturnNetBufferLists</i> can return the NET_BUFFER_LIST structures to a pool (for example, it
    could call the 
    <a href="https://msdn.microsoft.com/library/windows/hardware/ff562583">NdisFreeNetBufferList</a> function), it
    can be more efficient to reuse the structures without returning them to the pool.

NDIS calls 
    <i>MiniportReturnNetBufferLists</i> at IRQL<= DISPATCH_LEVEL.

<h3><a id="Examples"></a><a id="examples"></a><a id="EXAMPLES"></a>Examples</h3>
To define a <i>MiniportReturnNetBufferLists</i> function, you must first provide a function declaration that identifies the type of function you're defining. Windows provides a set of function types for drivers. Declaring a function using the function types helps <a href="https://msdn.microsoft.com/2F3549EF-B50F-455A-BDC7-1F67782B8DCA">Code Analysis for Drivers</a>, <a href="https://msdn.microsoft.com/74feeb16-387c-4796-987a-aff3fb79b556">Static Driver Verifier</a> (SDV), and other verification tools find errors, and it's a requirement for writing drivers for the Windows operating system.

For example, to define a <i>MiniportReturnNetBufferLists</i> function that is named "MyReturnNetBufferLists", use the <b>MINIPORT_RETURN_NET_BUFFER_LISTS</b> type as shown in this code example:

<div class="code"><span codelanguage=""><table>
<tr>
<th></th>
</tr>
<tr>
<td>
<pre>MINIPORT_RETURN_NET_BUFFER_LISTS MyReturnNetBufferLists;</pre>
</td>
</tr>
</table></span></div>
Then, implement your function as follows:

<div class="code"><span codelanguage=""><table>
<tr>
<th></th>
</tr>
<tr>
<td>
<pre>_Use_decl_annotations_
VOID
 MyReturnNetBufferLists(
    NDIS_HANDLE  MiniportAdapterContext,
    PNET_BUFFER_LIST  NetBufferLists,
    ULONG  ReturnFlags
    )
  {...}</pre>
</td>
</tr>
</table></span></div>
The <b>MINIPORT_RETURN_NET_BUFFER_LISTS</b> function type is defined in the Ndis.h header file. To more accurately identify errors when you run the code analysis tools, be sure to add the _Use_decl_annotations_ annotation to your function definition.  The _Use_decl_annotations_ annotation ensures that the annotations that are applied to the <b>MINIPORT_RETURN_NET_BUFFER_LISTS</b> function type in the header file are used.  For more information about the requirements for function declarations, see <a href="https://msdn.microsoft.com/232c4272-0bf0-4a4e-9560-3bceeca8a3e3">Declaring Functions by Using Function Role Types for NDIS Drivers</a>.

For information about  _Use_decl_annotations_, see <a href="https://go.microsoft.com/fwlink/p/?linkid=286697">Annotating Function Behavior</a>. 




## -see-also




<a href="https://msdn.microsoft.com/b146fa81-005b-4a6c-962d-4cb023ea790e">MiniportInitializeEx</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff568376">NET_BUFFER</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff568388">NET_BUFFER_LIST</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff562583">NdisFreeNetBufferList</a>



<a href="https://msdn.microsoft.com/b87dba3e-c18f-4ea2-8bd5-ec3cdafc534b">
   NdisMIndicateReceiveNetBufferLists</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff564534">NdisReturnNetBufferLists</a>
 

 

