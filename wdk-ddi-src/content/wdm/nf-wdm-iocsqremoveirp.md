---
UID: NF:wdm.IoCsqRemoveIrp
title: IoCsqRemoveIrp function (wdm.h)
description: The IoCsqRemoveIrp routine removes a particular IRP from the queue.
old-location: kernel\iocsqremoveirp.htm
tech.root: kernel
ms.assetid: 72a6327c-01b2-479c-a2eb-f58180193d50
ms.date: 04/30/2018
ms.keywords: IoCsqRemoveIrp, IoCsqRemoveIrp routine [Kernel-Mode Driver Architecture], k104_9a940115-fcbd-4e46-b7a5-10dc7fad7bda.xml, kernel.iocsqremoveirp, wdm/IoCsqRemoveIrp
ms.topic: function
req.header: wdm.h
req.include-header: Wdm.h, Ntddk.h, Ntifs.h
req.target-type: Universal
req.target-min-winverclnt: Available in Windows XP and later versions of Windows. Drivers that must also work in Windows 2000 and Windows 98/Me can instead link to Csq.lib to use the routine.
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
req.lib: NtosKrnl.lib
req.dll: NtosKrnl.exe
req.irql: "<= DISPATCH_LEVEL (see Remarks section)"
topic_type:
- APIRef
- kbSyntax
api_type:
- DllExport
api_location:
- NtosKrnl.exe
api_name:
- IoCsqRemoveIrp
product:
- Windows
targetos: Windows
req.typenames: 
---

# IoCsqRemoveIrp function


## -description


The <b>IoCsqRemoveIrp</b> routine removes a particular IRP from the queue.


## -parameters




### -param Csq [in, out]

Pointer to the <a href="https://msdn.microsoft.com/library/windows/hardware/ff550560">IO_CSQ</a> structure for the driver's cancel-safe IRP queue. This structure must have been initialized by <a href="https://msdn.microsoft.com/library/windows/hardware/ff549054">IoCsqInitialize</a> or <a href="https://msdn.microsoft.com/library/windows/hardware/ff549060">IoCsqInitializeEx</a>.


### -param Context [in, out]

Pointer to the <a href="https://msdn.microsoft.com/library/windows/hardware/ff550567">IO_CSQ_IRP_CONTEXT</a> structure that identifies the IRP to remove. The <b>IO_CSQ_IRP_CONTEXT</b> structure is initialized by <a href="https://msdn.microsoft.com/library/windows/hardware/ff549066">IoCsqInsertIrp</a> or <a href="https://msdn.microsoft.com/library/windows/hardware/ff549067">IoCsqInsertIrpEx</a> when the IRP is first inserted in the queue.


## -returns



This routine returns a pointer to the IRP that was removed from the queue, or <b>NULL</b> if that IRP has been canceled.




## -remarks



<b>IoCsqRemoveIrp</b> uses the queue's dispatch routines to remove the IRP. The <b>IoCsqRemoveIrp</b> routine:

<ol>
<li>
Calls the queue's <a href="https://msdn.microsoft.com/library/windows/hardware/ff542934">CsqAcquireLock</a> routine to lock the queue.

</li>
<li>
Uses the <i>IrpContext</i> parameter to determine which IRP to remove, and calls the queue's <a href="https://msdn.microsoft.com/library/windows/hardware/ff542968">CsqRemoveIrp</a> routine to remove that IRP.

</li>
<li>
Calls the queue's <a href="https://msdn.microsoft.com/library/windows/hardware/ff542965">CsqReleaseLock</a> routine to unlock the queue.

</li>
</ol>
Drivers can use the <a href="https://msdn.microsoft.com/library/windows/hardware/ff549072">IoCsqRemoveNextIrp</a> routine to remove an IRP that matches a specific criterion. For more information, see <a href="https://msdn.microsoft.com/library/windows/hardware/ff540755">Cancel-Safe IRP Queues</a>.

Note that <b>IoCsq<i>Xxx</i></b> routines use the <b>DriverContext[</b>3<b>]</b> member of the IRP to hold IRP context information. Drivers that use these routines to queue IRPs must leave that member unused.

Callers of <b>IoCsqRemoveIrp</b> must be running at an IRQL <= DISPATCH_LEVEL. The driver's callback routines must work correctly at that IRQL.




## -see-also




<a href="https://msdn.microsoft.com/library/windows/hardware/ff542934">CsqAcquireLock</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff542940">CsqCompleteCanceledIrp</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff542947">CsqInsertIrp</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff542956">CsqInsertIrpEx</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff542959">CsqPeekNextIrp</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff542965">CsqReleaseLock</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff542968">CsqRemoveIrp</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff550560">IO_CSQ</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff550567">IO_CSQ_IRP_CONTEXT</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff549054">IoCsqInitialize</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff549060">IoCsqInitializeEx</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff549066">IoCsqInsertIrp</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff549067">IoCsqInsertIrpEx</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff549072">IoCsqRemoveNextIrp</a>
 

 

