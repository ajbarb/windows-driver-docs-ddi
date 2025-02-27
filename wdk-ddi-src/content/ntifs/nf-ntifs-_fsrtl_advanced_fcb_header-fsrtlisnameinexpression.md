---
UID: NF:ntifs._FSRTL_ADVANCED_FCB_HEADER.FsRtlIsNameInExpression
title: FsRtlIsNameInExpression function (ntifs.h)
description: The FsRtlIsNameInExpression routine determines whether a Unicode string matches the specified pattern.
old-location: ifsk\fsrtlisnameinexpression.htm
tech.root: ifsk
ms.assetid: 8d54bf46-dc70-47a1-a391-6e32a7800a9e
ms.date: 04/16/2018
ms.keywords: FsRtlIsNameInExpression, FsRtlIsNameInExpression routine [Installable File System Drivers], fsrtlref_719072fe-274b-482a-ba9c-4a21d4d2be21.xml, ifsk.fsrtlisnameinexpression, ntifs/FsRtlIsNameInExpression
ms.topic: function
req.header: ntifs.h
req.include-header: FltKernel.h, Ntifs.h
req.target-type: Universal
req.target-min-winverclnt: This routine is available in Windows 2000 and later versions of the Windows operating system.
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
req.irql: PASSIVE_LEVEL
topic_type:
- APIRef
- kbSyntax
api_type:
- DllExport
api_location:
- NtosKrnl.exe
api_name:
- FsRtlIsNameInExpression
product:
- Windows
targetos: Windows
req.typenames: 
ms.custom: RS5
---

# FsRtlIsNameInExpression function


## -description


The <b>FsRtlIsNameInExpression</b> routine determines whether a Unicode string matches the specified pattern. 


## -parameters




### -param Expression [in]

A pointer to the pattern string. Can contain wildcard characters. If <i>IgnoreCase</i> is <b>TRUE</b>, <i>Expression</i> must be uppercase. 


### -param Name [in]

A pointer to the string to be compared against the pattern. Cannot contain wildcard characters. 


### -param IgnoreCase [in]

Set to <b>TRUE</b> for case-insensitive matching, <b>FALSE</b> otherwise.


### -param UpcaseTable [in, optional]

Optional pointer to uppercase character table to use for case-insensitive matching. If this value is not supplied, the default system uppercase character table is used.


## -returns



<b>FsRtlIsNameInExpression</b> returns <b>TRUE</b> if the string matches the pattern, <b>FALSE</b> otherwise.




## -remarks



The following wildcard characters can be used in the pattern string.

<table>
<tr>
<th>Wildcard character</th>
<th>Meaning</th>
</tr>
<tr>
<td>
* (asterisk)

</td>
<td>
Matches zero or more characters.

</td>
</tr>
<tr>
<td>
? (question mark)

</td>
<td>
Matches a single character.

</td>
</tr>
<tr>
<td>
DOS_DOT

</td>
<td>
Matches either a period or zero characters beyond the name string.

</td>
</tr>
<tr>
<td>
DOS_QM

</td>
<td>
Matches any single character or, upon encountering a period or end of name string, advances the expression to the end of the set of contiguous DOS_QMs.

</td>
</tr>
<tr>
<td>
DOS_STAR

</td>
<td>
Matches zero or more characters until encountering and matching the final . in the name.

</td>
</tr>
</table>
 

<div class="alert"><b>Note</b>  
     If only one of the string parameters has a length of zero, <b>FsRtlIsNameInExpression</b> returns <b>FALSE</b>. This means that "*" does not match a null string. <p class="note">If both parameters are null strings, <b>FsRtlIsNameInExpression</b> returns <b>TRUE</b>.

</div>
<div> </div>
For information about other string-handling routines, see <a href="https://msdn.microsoft.com/library/windows/hardware/ff563884">Strings</a>. 




## -see-also




<a href="https://msdn.microsoft.com/library/windows/hardware/ff546803">FsRtlIsDbcsInExpression</a>



<a href="https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_unicode_string">UNICODE_STRING</a>
 

 

