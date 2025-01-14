---
UID: NF:wdm.RtlCheckBit~r1
title: RtlCheckBit macro (wdm.h)
description: The RtlCheckBit routine determines whether a particular bit in a given bitmap variable is clear or set.
old-location: kernel\rtlcheckbit.htm
tech.root: kernel
ms.assetid: 2c9842de-a256-46ed-84b4-b8a595c01a62
ms.date: 04/30/2018
ms.keywords: RtlCheckBit, RtlCheckBit routine [Kernel-Mode Driver Architecture], k109_1f4676c1-d031-4a2c-8d74-afa9d3a0ed10.xml, kernel.rtlcheckbit, wdm/RtlCheckBit
ms.topic: macro
req.header: wdm.h
req.include-header: Wdm.h, Ntddk.h, Ntifs.h
req.target-type: Desktop
req.target-min-winverclnt: Available starting with Windows 2000.
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
req.irql: "<= APC_LEVEL (see Remarks section)"
topic_type:
- APIRef
- kbSyntax
api_type:
- HeaderDef
api_location:
- Wdm.h
api_name:
- RtlCheckBit
product:
- Windows
targetos: Windows
req.typenames: 
---

# RtlCheckBit macro


## -description


The <b>RtlCheckBit</b> routine determines whether a particular bit in a given bitmap variable is clear or set. 



## -parameters

### -param BitMapHeader

[in]

A pointer to the <a href="https://msdn.microsoft.com/library/windows/hardware/ff563614">RTL_BITMAP</a> structure that describes the bitmap. This structure must have been initialized by the <a href="https://msdn.microsoft.com/library/windows/hardware/ff561925">RtlInitializeBitMap</a> routine. 


### -param BitPosition

[in]

Specifies which bit to check. This is a zero-based value indicating the position of the bit to be tested. 

## -returns

**RtlCheckBit** returns zero if the given bit is clear, or one if the given bit is set.

## -remarks



Callers of <b>RtlCheckBit</b> must be running at IRQL <= APC_LEVEL if the memory that contains the bitmap variable is pageable or the memory at <i>BitMapHeader</i> is pageable. Otherwise, <b>RtlCheckBit</b> can be called at any IRQL.




## -see-also




<a href="https://msdn.microsoft.com/library/windows/hardware/ff563614">RTL_BITMAP</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff561742">RtlAreBitsClear</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff561745">RtlAreBitsSet</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff561925">RtlInitializeBitMap</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff562034">RtlNumberOfClearBits</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff562037">RtlNumberOfSetBits</a>
 

 

