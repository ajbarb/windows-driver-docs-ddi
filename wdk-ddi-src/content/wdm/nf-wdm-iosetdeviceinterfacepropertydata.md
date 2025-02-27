---
UID: NF:wdm.IoSetDeviceInterfacePropertyData
title: IoSetDeviceInterfacePropertyData function (wdm.h)
description: The IoSetDeviceInterfacePropertyData routine modifies the current value of a device interface property.
old-location: kernel\iosetdeviceinterfacepropertydata.htm
tech.root: kernel
ms.assetid: 346F6FEC-7E06-4DF0-A304-88BD830C591B
ms.date: 04/30/2018
ms.keywords: IoSetDeviceInterfacePropertyData, IoSetDeviceInterfacePropertyData routine [Kernel-Mode Driver Architecture], kernel.iosetdeviceinterfacepropertydata, wdm/IoSetDeviceInterfacePropertyData
ms.topic: function
req.header: wdm.h
req.include-header: Wdm.h, Ntddk.h, Ntifs.h
req.target-type: Universal
req.target-min-winverclnt: Available for Windows 8 and later versions of Windows.
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
req.irql: "<= APC_LEVEL"
topic_type:
- APIRef
- kbSyntax
api_type:
- DllExport
api_location:
- NtosKrnl.exe
api_name:
- IoSetDeviceInterfacePropertyData
product:
- Windows
targetos: Windows
req.typenames: 
---

# IoSetDeviceInterfacePropertyData function


## -description


The <b>IoSetDeviceInterfacePropertyData</b> routine modifies the current value of a <a href="https://msdn.microsoft.com/43aa0ce6-a06b-43e4-a213-300554391ae0">device interface property</a>.


## -parameters




### -param SymbolicLinkName [in]

A pointer to a string that identifies the device interface instance. This string was obtained from a previous call to the <a href="https://msdn.microsoft.com/library/windows/hardware/ff549186">IoGetDeviceInterfaces</a>, <a href="https://msdn.microsoft.com/library/windows/hardware/ff549180">IoGetDeviceInterfaceAlias</a>, or <a href="https://msdn.microsoft.com/library/windows/hardware/ff549506">IoRegisterDeviceInterface</a> routine.


### -param PropertyKey [in]

A pointer to a <a href="https://msdn.microsoft.com/library/windows/hardware/dn315031">DEVPROPKEY</a> structure that contains the device interface property key.


### -param Lcid [in]

Specifies a locale identifier. Set this parameter either to a language-specific LCID value or to <b>LOCALE_NEUTRAL</b>. The <b>LOCALE_NEUTRAL</b> LCID specifies that the property is language-neutral (that is, not specific to any language). Do not set this parameter to <b>LOCALE_SYSTEM_DEFAULT</b> or <b>LOCALE_USER_DEFAULT</b>. For more information about language-specific LCID values, see <a href="https://msdn.microsoft.com/library/cc233968(PROT.10).aspx">LCID Structure</a>.


### -param Flags [in]

Set this parameter to <b>PLUGPLAY_PROPERTY_PERSISTENT</b> if the property value set by this routine should persist across computer restarts. Otherwise, set <i>Flags</i> to zero.


### -param Type [in]

Set this parameter to the <a href="https://msdn.microsoft.com/library/windows/hardware/ff543546">DEVPROPTYPE</a> value that specifies the type of the data that is supplied in the <i>Data</i> buffer.


### -param Size [in]

Specifies the size, in bytes, of the buffer that <i>Data</i> points to.


### -param Data [in, optional]

A pointer to the device interface property data. Set this parameter to <b>NULL</b> to delete the specified property. If <i>Data</i> is non-<b>NULL</b>, the routine stores an internal copy of the property value. The buffer pointed to by <i>Data</i> does not need to remain valid after the call returns.


## -returns



<b>IoSetDeviceInterfacePropertyData</b> returns STATUS_SUCCESS if the call was successful. Possible error return values include the following status codes.

<table>
<tr>
<th>Return code</th>
<th>Description</th>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>STATUS_UNSUCCESSFUL</b></dt>
</dl>
</td>
<td width="60%">
The specified LCID value is not valid.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>STATUS_NOT_IMPLEMENTED</b></dt>
</dl>
</td>
<td width="60%">
The specified property is not supported.

</td>
</tr>
</table>
 




## -remarks



Kernel-mode drivers use the <b>IoSetDeviceInterfacePropertyData</b> routine to modify device interface properties that are defined as part of the <a href="https://msdn.microsoft.com/51105f84-38d8-4005-a3fd-4beccc0a2a39">unified device property model</a>. For more information about device interface properties, see <a href="https://msdn.microsoft.com/f41040c5-0eac-450d-b532-9165c543cc1a">Device Properties</a>.

Drivers can use the <a href="https://msdn.microsoft.com/library/windows/hardware/hh439313">IoGetDeviceInterfacePropertyData</a> routine to obtain the current value for a device interface property.

Callers of <b>IoSetDeviceInterfacePropertyData</b> must be running at IRQL <= APC_LEVEL in the context of a system thread.




## -see-also




<a href="https://msdn.microsoft.com/library/windows/hardware/dn315031">DEVPROPKEY</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff543546">DEVPROPTYPE</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/hh439313">IoGetDeviceInterfacePropertyData</a>
 

 

