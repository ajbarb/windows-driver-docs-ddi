---
UID: NF:wdftimer.WDF_TIMER_CONFIG_INIT_PERIODIC
title: WDF_TIMER_CONFIG_INIT_PERIODIC function (wdftimer.h)
description: The WDF_TIMER_CONFIG_INIT_PERIODIC function initializes a WDF_TIMER_CONFIG structure for a periodic timer.
old-location: wdf\wdf_timer_config_init_periodic.htm
tech.root: wdf
ms.assetid: 44a5b4dd-c654-4af1-afd6-6e59d2cd1ff8
ms.date: 02/26/2018
ms.keywords: DFTimerObjectRef_de3c1624-3004-46e3-b6b4-d47768cd8239.xml, WDF_TIMER_CONFIG_INIT_PERIODIC, WDF_TIMER_CONFIG_INIT_PERIODIC function, kmdf.wdf_timer_config_init_periodic, wdf.wdf_timer_config_init_periodic, wdftimer/WDF_TIMER_CONFIG_INIT_PERIODIC
ms.topic: function
req.header: wdftimer.h
req.include-header: Wdf.h
req.target-type: Universal
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.kmdf-ver: 1.0
req.umdf-ver: 2.0
req.ddi-compliance: 
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: None
req.dll: 
req.irql: Any level
topic_type:
- APIRef
- kbSyntax
api_type:
- LibDef
api_location:
- None
- None.dll
api_name:
- WDF_TIMER_CONFIG_INIT_PERIODIC
product:
- Windows
targetos: Windows
req.typenames: 
---

# WDF_TIMER_CONFIG_INIT_PERIODIC function


## -description


<p class="CCE_Message">[Applies to KMDF and UMDF]</p>

The <b>WDF_TIMER_CONFIG_INIT_PERIODIC</b> function initializes a <a href="https://msdn.microsoft.com/library/windows/hardware/ff552519">WDF_TIMER_CONFIG</a> structure for a periodic timer.


## -parameters




### -param Config [in]

A pointer to a <a href="https://msdn.microsoft.com/library/windows/hardware/ff552519">WDF_TIMER_CONFIG</a> structure.


### -param EvtTimerFunc [in]

A pointer to a driver-supplied <a href="https://msdn.microsoft.com/abe15fd9-620e-4c24-9a82-32d20a7e49cc">EvtTimerFunc</a> callback function.


### -param Period [in]

A time value. For more information about specifying this value, see <a href="https://msdn.microsoft.com/library/windows/hardware/ff552519">WDF_TIMER_CONFIG</a>.


## -returns



None




## -remarks



The <b>WDF_TIMER_CONFIG_INIT_PERIODIC</b> function zeros the specified <a href="https://msdn.microsoft.com/library/windows/hardware/ff552519">WDF_TIMER_CONFIG</a> structure. Then it sets the structure's <b>Size</b> member, stores the <i>EvtTimerFunc</i> pointer and <i>Period</i> value, sets the <b>TolerableDelay</b> member to zero and sets the <b>AutomaticSerialization</b> member to <b>TRUE</b>. 


#### Examples

The following code example initializes a <a href="https://msdn.microsoft.com/library/windows/hardware/ff552519">WDF_TIMER_CONFIG</a> structure and a <a href="https://msdn.microsoft.com/library/windows/hardware/ff552400">WDF_OBJECT_ATTRIBUTES</a> structure and then calls <a href="https://msdn.microsoft.com/library/windows/hardware/ff550050">WdfTimerCreate</a>.

<div class="code"><span codelanguage=""><table>
<tr>
<th></th>
</tr>
<tr>
<td>
<pre>WDF_TIMER_CONFIG  timerConfig;
WDF_OBJECT_ATTRIBUTES  timerAttributes;
WDFTIMER  timerHandle;
NTSTATUS  Status;

WDF_TIMER_CONFIG_INIT_PERIODIC(
                               &timerConfig,
                               EchoEvtTimerFunc,
                               PERIODIC_TIMER_INTERVAL
                               );

WDF_OBJECT_ATTRIBUTES_INIT(&timerAttributes);
timerAttributes.ParentObject = Queue;

Status = WdfTimerCreate(
                        &timerConfig,
                        &timerAttributes,
                        &timerHandle
                        );</pre>
</td>
</tr>
</table></span></div>



## -see-also




<a href="https://msdn.microsoft.com/abe15fd9-620e-4c24-9a82-32d20a7e49cc">EvtTimerFunc</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff552519">WDF_TIMER_CONFIG</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff552522">WDF_TIMER_CONFIG_INIT</a>
 

 

