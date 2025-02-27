---
UID: NF:wdm.KeQueryPerformanceCounter
title: KeQueryPerformanceCounter function (wdm.h)
description: The KeQueryPerformanceCounter routine retrieves the current value and frequency of the performance counter.Use KeQueryPerformanceCounter to acquire high resolution (<1us) time stamps for time interval measurements.
old-location: kernel\kequeryperformancecounter.htm
tech.root: kernel
ms.assetid: ee1dbd20-5502-4448-b39a-4629ddc73d01
ms.date: 04/30/2018
ms.keywords: KeQueryPerformanceCounter, KeQueryPerformanceCounter routine [Kernel-Mode Driver Architecture], k105_39f70923-56fe-42b1-bec3-fe23ae62904d.xml, kernel.kequeryperformancecounter, wdm/KeQueryPerformanceCounter
ms.topic: function
req.header: wdm.h
req.include-header: Wdm.h, Ntddk.h, Ntifs.h
req.target-type: Universal
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
req.lib: Hal.lib
req.dll: Hal.dll
req.irql: Any level
topic_type:
- APIRef
- kbSyntax
api_type:
- DllExport
api_location:
- Hal.dll
api_name:
- KeQueryPerformanceCounter
product:
- Windows
targetos: Windows
req.typenames: 
---

# KeQueryPerformanceCounter function


## -description


The <b>KeQueryPerformanceCounter</b> routine retrieves the current value and frequency of the performance counter.

Use <b>KeQueryPerformanceCounter</b> to acquire high resolution (<1&micro;s) time stamps for time interval measurements.


## -parameters




### -param PerformanceFrequency [out, optional]

A pointer to a variable to which <b>KeQueryPerformanceCounter</b> writes the performance counter frequency, in ticks per second. This parameter is optional and can be NULL if the caller does not need the counter frequency value.


## -returns



<b>KeQueryPerformanceCounter</b> returns the performance counter value in units of ticks.




## -remarks



<b>KeQueryPerformanceCounter</b> returns a 64-bit integer that represents the current value of a high-resolution monotonically nondecreasing counter. 

To obtain the frequency of the performance counter, specify a non-<b>NULL</b> pointer value for the <i>PerformanceFrequency</i> parameter. The frequency of the performance counter is fixed at system boot and is consistent across all processors. Therefore, a driver can cache the frequency of the performance counter during initialization.  

For more info about this function and its usage, see <a href="https://msdn.microsoft.com/D66E0FC2-3AF2-489B-B4B5-78648905B77B">Acquiring high-resolution time stamps</a>. 




## -see-also




[KeQueryInterruptTime](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequeryinterrupttime)



[KeQuerySystemTime](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequerysystemtime~r1)



[KeQueryTickCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kequerytickcount)



[KeQueryTimeIncrement](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequerytimeincrement)



[QueryPerformanceCounter](https://msdn.microsoft.com/library/windows/desktop/ms644904(v=vs.85).aspx)



[QueryPerformanceFrequency](https://msdn.microsoft.com/library/windows/desktop/ms644905(v=vs.85).aspx)
 

