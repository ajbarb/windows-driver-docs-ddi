---
UID: NF:wdfusb.WdfUsbTargetDeviceCreateWithParameters
title: WdfUsbTargetDeviceCreateWithParameters function (wdfusb.h)
description: The WdfUsbTargetDeviceCreateWithParameters method creates a framework USB device object for a specified framework device object and opens the USB device for I/O operations.
old-location: wdf\wdfusbtargetdevicecreatewithparameters.htm
tech.root: wdf
ms.assetid: E93A944E-81D5-4059-ADA6-2760A091C30B
ms.date: 02/26/2018
ms.keywords: WdfUsbTargetDeviceCreateWithParameters, WdfUsbTargetDeviceCreateWithParameters method, kmdf.wdfusbtargetdevicecreatewithconfig, kmdf.wdfusbtargetdevicecreatewithparameters, wdf.wdfusbtargetdevicecreatewithparameters, wdfusb/WdfUsbTargetDeviceCreateWithParameters
ms.topic: function
req.header: wdfusb.h
req.include-header: Wdfusb.h
req.target-type: Universal
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.kmdf-ver: 1.11
req.umdf-ver: 2.0
req.ddi-compliance: DriverCreate, RequestForUrbXrb, UsbDeviceCreate, UsbDeviceCreateFail, UsbDeviceCreateTarget
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: Wdf01000.sys (KMDF); WUDFx02000.dll (UMDF)
req.dll: 
req.irql: PASSIVE_LEVEL
topic_type:
- APIRef
- kbSyntax
api_type:
- LibDef
api_location:
- Wdf01000.sys
- Wdf01000.sys.dll
- WUDFx02000.dll
- WUDFx02000.dll.dll
api_name:
- WdfUsbTargetDeviceCreateWithParameters
product:
- Windows
targetos: Windows
req.typenames: 
---

# WdfUsbTargetDeviceCreateWithParameters function


## -description


<p class="CCE_Message">[Applies to KMDF and UMDF]</p>


   
  The <b>WdfUsbTargetDeviceCreateWithParameters</b>  method creates a framework USB device object for a specified framework device object and opens the USB device for I/O operations.
The method also specifies configuration information for the framework USB device object.


## -parameters




### -param Device [in]

A handle to a framework device object.


### -param Config [in]

A pointer to a <a href="https://msdn.microsoft.com/library/windows/hardware/hh406503">WDF_USB_DEVICE_CREATE_CONFIG</a> structure that contains configuration information for the framework USB device object.


### -param Attributes [in, optional]

A pointer to a caller-supplied <a href="https://msdn.microsoft.com/library/windows/hardware/ff552400">WDF_OBJECT_ATTRIBUTES</a> structure that contains attributes for the new framework USB device object. (The structure's <b>ParentObject</b> member must be NULL.) This parameter is optional and can be WDF_NO_OBJECT_ATTRIBUTES.


### -param UsbDevice [out]

A pointer to a location that receives a handle to the new framework USB device object.


## -returns



<b>WdfUsbTargetDeviceCreateWithParameters</b> returns STATUS_SUCCESS if the operation succeeds. Otherwise, this method can return one of the following values:

<table>
<tr>
<th>Return code</th>
<th>Description</th>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>STATUS_INFO_LENGTH_MISMATCH</b></dt>
</dl>
</td>
<td width="60%">
The <i>Config</i> parameter is not the correct size.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>STATUS_INSUFFICIENT_RESOURCES</b></dt>
</dl>
</td>
<td width="60%">
There was insufficient memory to create a new framework USB device object.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>STATUS_INVALID_PARAMETER</b></dt>
</dl>
</td>
<td width="60%">
An invalid parameter was detected.  See the Remarks section for more information.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>STATUS_UNSUCCESSFUL</b></dt>
</dl>
</td>
<td width="60%">
An attempt to get USB configuration information failed.

</td>
</tr>
</table>
 

For a list of other return values that the <b>WdfUsbTargetDeviceCreateWithParameters</b> method might return, see <a href="https://msdn.microsoft.com/f5345c88-1c3a-4b32-9c93-c252713f7641">Framework Object Creation Errors</a>.

This method also might return other <a href="https://msdn.microsoft.com/library/windows/hardware/ff557697">NTSTATUS values</a>.

A bug check occurs if the driver supplies an invalid object handle.






## -remarks



Windows 8 includes a new USB driver stack to support USB 3.0 devices.

Before a framework-based client driver can use the new capabilities of the USB driver stack for Windows 8, the driver must register itself with the underlying USB driver stack that is loaded by Windows for the device. To register the client driver, call <b>WdfUsbTargetDeviceCreateWithParameters</b> and specify a contract version in the <a href="https://msdn.microsoft.com/library/windows/hardware/hh406503">WDF_USB_DEVICE_CREATE_CONFIG</a> structure.

 If the client driver is intended to build, run, and use the improvements and the new capabilities on Windows 8, the client contract version is USBD_CLIENT_CONTRACT_VERSION_602.

Typically, drivers call <b>WdfUsbTargetDeviceCreateWithParameters</b> from within an <a href="https://msdn.microsoft.com/a3d4a983-8a75-44be-bd72-8673d89f9f87">EvtDevicePrepareHardware</a> callback function. Drivers can also call <b>WdfUsbTargetDeviceCreateWithParameters</b> from within an <a href="https://msdn.microsoft.com/b20db029-ee2c-4fb1-bd69-ccd2e37fdc9a">EvtDriverDeviceAdd</a> callback function.

For information about how WDM USB client drivers interact with the USB 3.0 driver stack, see  <a href="https://msdn.microsoft.com/library/windows/hardware/hh406258">Best Practices: Using URBs</a>.

If the driver calls <b>WdfUsbTargetDeviceCreateWithParameters</b> to create a framework USB device object, the driver must create URBs only by calling <a href="https://msdn.microsoft.com/library/windows/hardware/hh439423">WdfUsbTargetDeviceCreateUrb</a> or <a href="https://msdn.microsoft.com/library/windows/hardware/hh439420">WdfUsbTargetDeviceCreateIsochUrb</a>.

If you call this method from a UMDF driver, you must specify the <b>UmdfDispatcher</b> directive in the driver's INF file.  Otherwise, this method may return <b>STATUS_INVALID_PARAMETER</b>.   For more information about this directive, see <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files">Specifying WDF Directives in INF Files</a>.


#### Examples

The following code example is part of an <a href="https://msdn.microsoft.com/a3d4a983-8a75-44be-bd72-8673d89f9f87">EvtDevicePrepareHardware</a> callback function that calls <b>WdfUsbTargetDeviceCreateWithParameters</b>. The example stores the handle to the framework USB device object in driver-defined context space. 

<div class="code"><span codelanguage=""><table>
<tr>
<th></th>
</tr>
<tr>
<td>
<pre>NTSTATUS
MyEvtDevicePrepareHardware(
    IN WDFDEVICE  Device,
    IN WDFCMRESLIST  ResourceList,
    IN WDFCMRESLIST  ResourceListTranslated
    )
{
    NTSTATUS  status;
    PMY_DEVICE_CONTEXT  pMyDeviceContext;
    WDF_USB_DEVICE_CREATE_CONFIG  Config;

    pMyDeviceContext = GetDeviceContext(Device);

    // If object handle is not NULL, MyEvtDevicePrepareHardware
    // was called previously and the handle is still valid.
    if (pMyDeviceContext->UsbDevice != NULL) {
        return STATUS_SUCCESS;
    }

    WDF_USB_DEVICE_CREATE_CONFIG_INIT(
                                      &Config,
                                      USBD_CLIENT_CONTRACT_VERSION_602
                                      );

    status = WdfUsbTargetDeviceCreateWithParameters(
                                      Device,
                                      &Config,
                                      WDF_NO_OBJECT_ATTRIBUTES,
                                      &pMyDeviceContext->UsbDevice
                                      );
    if (!NT_SUCCESS(status)) {
        return status;
    }
...
}</pre>
</td>
</tr>
</table></span></div>



## -see-also




<a href="https://msdn.microsoft.com/library/windows/hardware/hh406241">USBD_CreateHandle</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/hh406503">WDF_USB_DEVICE_CREATE_CONFIG</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/hh406507">WDF_USB_DEVICE_CREATE_CONFIG_INIT</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff550077">WdfUsbTargetDeviceCreate</a>
 

 

