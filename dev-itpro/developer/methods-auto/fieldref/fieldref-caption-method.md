---
title: "Caption Method"
ms.author: solsen
ms.custom: na
ms.date: 10/01/2019
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: solsen
---
[//]: # (START>DO_NOT_EDIT)
[//]: # (IMPORTANT:Do not edit any of the content between here and the END>DO_NOT_EDIT.)
[//]: # (Any modifications should be made in the .xml files in the ModernDev repo.)
# Caption Method
Gets the current caption of a field as a String.


## Syntax
```
Caption :=   FieldRef.Caption()
```
> [!NOTE]  
> This method can be invoked using property access syntax.  

## Parameters
*FieldRef*  
&emsp;Type: [FieldRef](fieldref-data-type.md)  
An instance of the [FieldRef](fieldref-data-type.md) data type.  

## Return Value
*Caption*  
&emsp;Type: [String](../string/string-data-type.md)  
  


[//]: # (IMPORTANT: END>DO_NOT_EDIT)

## Remarks  
CAPTION returns the caption of a field. CAPTION first looks for a [CaptionML Property](../../properties/devenv-captionml-property.md).  If it does not find one, it will use the [Name Property](../../properties/devenv-name-property.md). This means that CAPTION is enabled for multilanguage functionality.  
  
 This method is similar to the [FIELDCAPTION Method \(Record\)](../../methods-auto/record/record-fieldcaption-method.md).  
  
## Example  
 The following example opens table 18 \(Customer\) as a RecordRef variable that is named CustomerRecref. The code uses the [FIELD Method \(RecordRef\)](../../methods-auto/recordref/recordref-field-method.md) to loop through field 1 through 9 and creates a FieldRef variable that is named MyFieldRef. For each field, the CAPTION method retrieves the caption of the field, stores it in the varCaption variable and displays it in a message box. This example requires that you create the following global variables and text constant.  
  
|Variable name|DataType|  
|-------------------|--------------|  
|CustomerRecref|RecordRef|  
|MyFieldRef|FieldRef|  
|varCaption|Text|  
|i|Integer|  
  
|Text constant|ENU value|  
|-------------------|---------------|  
|Text000|The caption for field %1 is "%2".|  
  
```  
  
CustomerRecref.OPEN(18);  
FOR i := 1 TO 9 DO BEGIN  
  MyFieldRef := CustomerRecref.FIELD(i);  
  varCaption := MyFieldRef.CAPTION;  
  MESSAGE(Text000, i, varCaption);  
END;  
CustomerRecref.CLOSE;  
```  

## See Also
[FieldRef Data Type](fieldref-data-type.md)  
[Getting Started with AL](../../devenv-get-started.md)  
[Developing Extensions](../../devenv-dev-overview.md)