---
UID: NF:spbcx.SpbRequestCaptureIoOtherTransferList
title: SpbRequestCaptureIoOtherTransferList function (spbcx.h)
description: The SpbRequestCaptureIoOtherTransferList method retrieves the SPB_TRANSFER_LIST structure in the input buffer of the custom IOCTL request.
old-location: spb\spbrequestcaptureioothertransferlist.htm
tech.root: SPB
ms.assetid: 7AC76E6F-1250-49EB-BEA1-3807C65AC2B7
ms.date: 04/30/2018
ms.keywords: SPB.spbrequestcaptureioothertransferlist, SpbRequestCaptureIoOtherTransferList, SpbRequestCaptureIoOtherTransferList method [Buses], spbcx/SpbRequestCaptureIoOtherTransferList
ms.topic: function
req.header: spbcx.h
req.include-header: 
req.target-type: Universal
req.target-min-winverclnt: Available starting with Windows 8.
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
req.lib: Spbcxstubs.lib
req.dll: 
req.irql: See Remarks.
topic_type:
- APIRef
- kbSyntax
api_type:
- LibDef
api_location:
- spbcxstubs.lib
- spbcxstubs.dll
api_name:
- SpbRequestCaptureIoOtherTransferList
product:
- Windows
targetos: Windows
req.typenames: 
---

# SpbRequestCaptureIoOtherTransferList function


## -description


The <b>SpbRequestCaptureIoOtherTransferList</b> method retrieves the <a href="https://msdn.microsoft.com/library/windows/hardware/hh406221">SPB_TRANSFER_LIST</a> structure in the input buffer of the custom IOCTL request.


## -parameters




### -param Request

<p>An <a href="https://msdn.microsoft.com/library/Hh450925(v=VS.85).aspx">SPBREQUEST</a> handle to the custom IOCTL request. The SPB controller driver previously received this handle through one of its registered <a href="https://msdn.microsoft.com/library/Hh450911(v=VS.85).aspx">event callback functions</a>.</p>




## -returns



<b>SpbRequestCaptureIoOtherTransferList</b> returns STATUS_SUCCESS if the call is successful. Possible return values include the following error codes.

<table>
<tr>
<th>Return value</th>
<th>Description</th>
</tr>
<tr>
<td width="40%">
<dl>
<dt>STATUS_INVALID_PARAMETER</dt>
</dl>
</td>
<td width="60%">
The <a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-object-handles">SPBREQUEST</a> parameter is invalid or the <a href="https://msdn.microsoft.com/library/windows/hardware/hh406221">SPB_TRANSFER_LIST</a> structure in the request is formatted incorrectly.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt>STATUS_INSUFFICIENT_RESOURCES</dt>
</dl>
</td>
<td width="60%">
Cannot allocate the system resources that are required for this operation.

</td>
</tr>
</table>
 




## -remarks



This method must be called in the context of the process in which the buffer addresses are valid. Typically, the SPB controller driver calls this method from the <a href="https://msdn.microsoft.com/b8bcea29-e404-490e-9d0c-02c96a5690ab">EvtIoInCallerContext</a> event callback function that the driver supplies as an input parameter to the <a href="https://msdn.microsoft.com/library/windows/hardware/hh450907">SpbControllerSetIoOtherCallback</a> method.

The maximum IRQL at which the SPB controller driver can call this method depends on whether the originator of the I/O request is running in user mode or in kernel mode. If the request originated from user mode, the driver must call this method at PASSIVE_LEVEL. If the request originated from kernel mode, the driver must call this method at IRQL <= DISPATCH_LEVEL. The driver can call the <a href="https://msdn.microsoft.com/library/windows/hardware/ff549971">WdfRequestGetRequestorMode</a> method to determine the originator's mode. However, this call is typically unnecessary because the driver can rely on the SPB framework extension (SpbCx) to call the driver's <a href="https://msdn.microsoft.com/b8bcea29-e404-490e-9d0c-02c96a5690ab">EvtIoInCallerContext</a> function at the appropriate IRQL.


#### Examples

The following code example shows how an SPB controller driver's <a href="https://msdn.microsoft.com/b8bcea29-e404-490e-9d0c-02c96a5690ab">EvtIoInCallerContext</a> event callback function can use the <b>SpbRequestCaptureIoOtherTransferList</b> method to obtain the I/O buffer or buffers from a custom IOCTL request.

<div class="code"><span codelanguage=""><table>
<tr>
<th></th>
</tr>
<tr>
<td>
<pre>VOID
EvtIoInCallerContext(
    _In_  WDFDEVICE   SpbController,
    _In_  WDFREQUEST  FxRequest
    ) 
{
    NTSTATUS status;

    //
    // NOTE: The driver should check for custom IOCTLs that this
    // driver handles. If an IOCTL is not recognized, mark the
    // request as STATUS_NOT_SUPPORTED, and complete the request.
    //

    status = SpbRequestCaptureIoOtherTransferList((SPBREQUEST)FxRequest);

    //
    // If the preceding call fails, the driver must complete the
    // request instead of queueing the request.
    //

    if (!NT_SUCCESS(status))
    {
        goto exit;
    }

    status = WdfDeviceEnqueueRequest(SpbController, FxRequest);

    if (!NT_SUCCESS(status))
    {
        goto exit;
    }

exit:

    if (!NT_SUCCESS(status))
    {
        WdfRequestComplete(FxRequest, status);
    }
}
</pre>
</td>
</tr>
</table></span></div>



## -see-also




<a href="https://msdn.microsoft.com/b8bcea29-e404-490e-9d0c-02c96a5690ab">EvtIoInCallerContext</a>



<a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-object-handles">SPBREQUEST</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/hh406221">SPB_TRANSFER_LIST</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/hh450907">SpbControllerSetIoOtherCallback</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff549971">WdfRequestGetRequestorMode</a>
 

 

