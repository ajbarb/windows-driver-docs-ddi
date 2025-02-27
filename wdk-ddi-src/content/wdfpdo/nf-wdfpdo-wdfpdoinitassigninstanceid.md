---
UID: NF:wdfpdo.WdfPdoInitAssignInstanceID
title: WdfPdoInitAssignInstanceID function (wdfpdo.h)
description: The WdfPdoInitAssignInstanceID method updates the instance ID for a child device.
old-location: wdf\wdfpdoinitassigninstanceid.htm
tech.root: wdf
ms.assetid: f843f8ce-81ee-4b8b-8583-dde3becb5460
ms.date: 02/26/2018
ms.keywords: DFDeviceObjectFdoPdoRef_cb462423-ac9a-499c-bdd7-24a276d9adf9.xml, WdfPdoInitAssignInstanceID, WdfPdoInitAssignInstanceID method, kmdf.wdfpdoinitassigninstanceid, wdf.wdfpdoinitassigninstanceid, wdfpdo/WdfPdoInitAssignInstanceID
ms.topic: function
req.header: wdfpdo.h
req.include-header: Wdf.h
req.target-type: Universal
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.kmdf-ver: 1.0
req.umdf-ver: 
req.ddi-compliance: ChildDeviceInitAPI, DriverCreate, InitFreeDeviceCallback, InitFreeDeviceCreate, InitFreeNull, KmdfIrql, KmdfIrql2, PdoDeviceInitAPI, PdoInitFreeDeviceCallback, PdoInitFreeDeviceCreate
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: Wdf01000.sys (see Framework Library Versioning.)
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
api_name:
- WdfPdoInitAssignInstanceID
product:
- Windows
targetos: Windows
req.typenames: 
---

# WdfPdoInitAssignInstanceID function


## -description


<p class="CCE_Message">[Applies to KMDF only]</p>

The <b>WdfPdoInitAssignInstanceID</b> method updates the <a href="https://msdn.microsoft.com/093063a6-1855-4e36-9465-1eedaa3cd0f9">instance ID</a> for a child device.


## -parameters




### -param DeviceInit [in]

A pointer to a <a href="https://msdn.microsoft.com/library/windows/hardware/ff546951">WDFDEVICE_INIT</a> structure.


### -param InstanceID [in]

A pointer to a <a href="https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_unicode_string">UNICODE_STRING</a> structure that contains an <a href="https://msdn.microsoft.com/093063a6-1855-4e36-9465-1eedaa3cd0f9">instance ID</a> string. The driver can allocate the string's buffer from paged pool. 


## -returns



If the operation succeeds, the method returns STATUS_SUCCESS. Additional return values include:

<table>
<tr>
<th>Return code</th>
<th>Description</th>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>STATUS_INVALID_DEVICE_REQUEST</b></dt>
</dl>
</td>
<td width="60%">
The driver is initializing an FDO instead of a PDO.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>STATUS_INSUFFICIENT_RESOURCES</b></dt>
</dl>
</td>
<td width="60%">
The driver could not allocate space to store the instance ID string.

</td>
</tr>
</table>
 

The method might also return other <a href="https://msdn.microsoft.com/library/windows/hardware/ff557697">NTSTATUS values</a>.




## -remarks



For more information about instance IDs, see <a href="https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings">Device Identification Strings</a>.

The driver must call <b>WdfPdoInitAssignInstanceID</b> before calling <a href="https://msdn.microsoft.com/library/windows/hardware/ff545926">WdfDeviceCreate</a>. For more information about calling <b>WdfDeviceCreate</b>, see <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-a-framework-device-object">Creating a Framework Device Object</a>.


#### Examples

The following code example converts a device's serial number to a Unicode string and then registers the Unicode string as the device's instance ID.

<div class="code"><span codelanguage=""><table>
<tr>
<th></th>
</tr>
<tr>
<td>
<pre>DECLARE_UNICODE_STRING_SIZE(instanceID, INSTANCEID_LENGTH);

status =  RtlIntegerToUnicodeString(
                                    SerialNo,
                                    BASE_DEC,
                                    &instanceID
                                    );
status = WdfPdoInitAssignInstanceID(
                                    pDeviceInit,
                                    &instanceID
                                    );</pre>
</td>
</tr>
</table></span></div>



## -see-also




<a href="https://msdn.microsoft.com/library/windows/hardware/ff561941">RtlIntegerToUnicodeString</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff548776">WdfPdoInitAddCompatibleID</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff548784">WdfPdoInitAddHardwareID</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff548797">WdfPdoInitAssignDeviceID</a>
 

 

