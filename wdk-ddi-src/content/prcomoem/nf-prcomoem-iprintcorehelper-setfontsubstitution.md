---
UID: NF:prcomoem.IPrintCoreHelper.SetFontSubstitution
title: IPrintCoreHelper::SetFontSubstitution (prcomoem.h)
description: The IPrintCoreHelper::SetFontSubstitution method specifies the device font to print in place of a given TrueType font.
old-location: print\iprintcorehelper_setfontsubstitution.htm
tech.root: print
ms.assetid: 2d0278b0-0011-4946-a095-5fef77a8b194
ms.date: 04/20/2018
ms.keywords: IPrintCoreHelper interface [Print Devices],SetFontSubstitution method, IPrintCoreHelper.SetFontSubstitution, IPrintCoreHelper::SetFontSubstitution, SetFontSubstitution, SetFontSubstitution method [Print Devices], SetFontSubstitution method [Print Devices],IPrintCoreHelper interface, prcomoem/IPrintCoreHelper::SetFontSubstitution, print.iprintcorehelper_setfontsubstitution, print_unidrv-pscript_allplugins_4ac54a23-3b42-4bb7-a078-a53774a537b2.xml
ms.topic: method
req.header: prcomoem.h
req.include-header: Prcomoem.h
req.target-type: Desktop
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
- COM
api_location:
- prcomoem.h
api_name:
- IPrintCoreHelper.SetFontSubstitution
product:
- Windows
targetos: Windows
req.typenames: 
---

# IPrintCoreHelper::SetFontSubstitution


## -description


The <b>IPrintCoreHelper::SetFontSubstitution</b> method specifies the device font to print in place of a given TrueType font. 


## -parameters




### -param pszTrueTypeFontName [in]

A pointer to a null-terminated Unicode string that contains a valid TrueType font name. This parameter must not be <b>NULL</b>.


### -param pszDevFontName [in]

A pointer to a null-terminated Unicode string that contains the name of the device font. 


## -returns



<b>IPrintCoreHelper::SetFontSubstitution</b> should return one of the following values.

<table>
<tr>
<th>Return code</th>
<th>Description</th>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>S_OK</b></dt>
</dl>
</td>
<td width="60%">
The method read the option for the specified feature.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>E_FAIL</b></dt>
</dl>
</td>
<td width="60%">
The font that was requested does not exist or was not a TrueType font.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>E_INVALIDARG</b></dt>
</dl>
</td>
<td width="60%">
One or more of the arguments is invalid.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>E_OUTOFMEMORY</b></dt>
</dl>
</td>
<td width="60%">
The core driver was not able to service the request because there was insufficient memory.

</td>
</tr>
<tr>
<td width="40%">
<dl>
<dt><b>E_UNEXPECTED, or other return codes not listed here</b></dt>
</dl>
</td>
<td width="60%">
The core driver seems to be in an invalid state. The caller should return a failure code.

</td>
</tr>
</table>
 




## -remarks



Setting a device font to use in place of a specified TrueType font can occur only during the device property sheets session and only if full UI replacement is enabled. The font that is represented by the <i>pszTrueTypeFontName</i> parameter must be a valid TrueType font and must be installed on the printer. The device font that is represented by the <i>pszDevFontName</i> parameter must be a valid font for this printer.

If a substitution mapping for the specified TrueType font already exists on this queue, the <b>SetFontSubstitution</b> method will silently replace the mapping. To remove a substitution mapping, call this method with the TrueType font name specified in <i>pszTrueTypeFontName</i> and with <b>NULL</b> specified in <i>pszDevFontName</i>.

To obtain a list of valid device fonts, create an information context for the current printer, and call <b>SetGraphicsMode</b>(hIC, GM_ADVANCED). Then, enumerate device fonts by means of a call to <b>EnumFontFamilies</b>. The callback parameter (see <b>EnumFontFamProc</b> in the Microsoft Windows SDK documentation) of <b>EnumFontFamilies</b> should filter for device fonts by incrementing a counter for each font for which the bitwise AND result (FontType & TRUETYPE_FONTTYPE) is nonzero.

<div class="alert"><b>Note</b>  The <b>SetGraphicsMode</b>, <b>EnumFontFamilies</b>, and <b>EnumFontFamProc</b> functions are described in the Windows SDK documentation.</div>
<div> </div>



## -see-also




<a href="https://msdn.microsoft.com/db13410f-e4cb-4077-bb4b-7963e97b435c">IPrintCoreHelper</a>



<a href="https://msdn.microsoft.com/library/windows/hardware/ff552957">IPrintCoreHelper::GetFontSubstitution</a>
 

 

