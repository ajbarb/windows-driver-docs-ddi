---
UID: NI:hpmi.IOCTL_HPMI_BATTERY_UTILIZATION_HINT
title: IOCTL_HPMI_BATTERY_UTILIZATION_HINT (hpmi.h)
description: Set command sent to HPMI to provide battery utilization hints.
old-location: powermeter\ioctl_hpmi_battery_utilization_hint.htm
tech.root: powermeter
ms.assetid: CE326F69-64A4-466E-8A02-5C08AFF8490C
ms.date: 05/08/2018
ms.keywords: IOCTL_HPMI_BATTERY_UTILIZATION_HINT, IOCTL_HPMI_BATTERY_UTILIZATION_HINT control, IOCTL_HPMI_BATTERY_UTILIZATION_HINT control code [Power Metering and Budgeting Devices], hpmi/IOCTL_HPMI_BATTERY_UTILIZATION_HINT, powermeter.ioctl_hpmi_battery_utilization_hint
ms.topic: ioctl
req.header: hpmi.h
req.include-header: Hpmi.h
req.target-type: Windows
req.target-min-winverclnt: Available in Windows 10, version 1709 and later versions of the Windows operating systems.
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
req.irql: 
topic_type:
- APIRef
- kbSyntax
api_type:
- HeaderDef
api_location:
- hpmi.h
api_name:
- IOCTL_HPMI_BATTERY_UTILIZATION_HINT
product:
- Windows
targetos: Windows
req.typenames: 
---

# IOCTL_HPMI_BATTERY_UTILIZATION_HINT IOCTL


## -description


<p class="CCE_Message">[Some information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.]

Set command sent to HPMI to provide battery utilization hints.

<div class="alert"><b>Important</b>  Preliminary Information</div><div> </div>

## -ioctlparameters




### -input-buffer

The AssociatedIrp.SystemBuffer member of the I/O request packet (IRP) points to an initiator-allocated buffer that is used both as the input buffer and the output buffer for the request. On input, this buffer contains a <a href="https://msdn.microsoft.com/A974998F-C9AF-496E-88B1-510413C17C4A">HPMI_BATTERY_UTILIZATION_HINT</a> structure  in which the version is set to a valid value. 


### -input-buffer-length

The Parameters.DeviceIoControl.InputBufferLength member of the IRP's current I/O stack location (IO_STACK_LOCATION) is set to the size in bytes of the buffer that is pointed to by the AssociatedIrp.SystemBuffer member. This size must be greater than or equal to sizeof <a href="https://msdn.microsoft.com/A974998F-C9AF-496E-88B1-510413C17C4A">HPMI_BATTERY_UTILIZATION_HINT</a>  structure  or the request will fail with an error status of STATUS_INVALID_PARAMETER.


### -output-buffer

TBD


### -output-buffer-length

TBD


### -in-out-buffer

TBD


### -inout-buffer-length

TBD


### -status-block

<b>Irp->IoStatus.Status</b> is set to STATUS_SUCCESS if the request is successful. Otherwise, <b>Status</b> to the appropriate error condition as a <a href="https://msdn.microsoft.com/7792201b-63bb-4db5-803d-2af02893d505">NTSTATUS</a> code, for example STATUS_INVALID_PARAMETER. 


## -remarks



 This IOCTL may be issued multiple times if HPMI requests HPMI_REQUEST_SERVICE_BATTERY_UTILIZATION_HINTS service.




## -see-also




<a href="https://msdn.microsoft.com/library/windows/hardware/ff542894">Creating IOCTL Requests in Drivers</a>



<a href="https://msdn.microsoft.com/E056400C-A0FE-4740-945D-C529C8804DF3">HPMI_HINT_BOOL</a>



<a href="https://msdn.microsoft.com/CE326F69-64A4-466E-8A02-5C08AFF8490C">IOCTL_HPMI_BATTERY_UTILIZATION_HINT</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff550694">IRP</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff548651">WdfIoTargetSendInternalIoctlOthersSynchronously</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff548656">WdfIoTargetSendInternalIoctlSynchronously</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff548660">WdfIoTargetSendIoctlSynchronously</a>



<a href="https://msdn.microsoft.com/35934D6C-3FB4-4AD4-AA50-BD3A7790269F">hpmi.h</a>
 

 


