---
UID: NS:61883._CIP_LISTEN
title: _CIP_LISTEN (61883.h)
description: This structure is used for a listen request. The request begins isochronous reception on the specified connection.
old-location: ieee\cip_listen.htm
tech.root: IEEE
ms.assetid: 362ABECF-66D3-4B0B-913B-59F7196D6BFD
ms.date: 02/15/2018
ms.keywords: "*PCIP_LISTEN, 61883/CIP_LISTEN, 61883/PCIP_LISTEN, CIP_LISTEN, CIP_LISTEN structure [Buses], IEEE.cip_listen, PCIP_LISTEN, PCIP_LISTEN structure pointer [Buses], _CIP_LISTEN"
ms.topic: struct
req.header: 61883.h
req.include-header: 
req.target-type: Windows
req.target-min-winverclnt: 
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
- 61883.h
api_name:
- CIP_LISTEN
product:
- Windows
targetos: Windows
req.typenames: CIP_LISTEN, *PCIP_LISTEN
---

# _CIP_LISTEN structure


## -description


This structure is used for a listen request. The request begins isochronous reception on the specified connection. This request will start capturing CIP packets, whether the packets have frames attached. 


## -struct-fields




### -field hConnect

On input, the handle of the connection to begin isochronous reception.


## -remarks



If successful, the IEC-61883 protocol driver sets <b>Irp->IoStatus.Status </b>to STATUS_SUCCESS. 

If an incorrect parameter is passed in, the protocol driver sets <b>Irp->IoStatus.Status </b>to STATUS_INVALID_PARAMETER.

If the protocol driver is unable to allocate resources, it sets <b>Irp->IoStatus.Status </b>to STATUS_INSUFFICIENT_RESOURCES.




## -see-also




<a href="https://msdn.microsoft.com/library/windows/hardware/ff537008">AV_61883_REQUEST</a>
 

 

