---
title: "MaxOccurs Property"
description: "Sets a value that indicates the maximum number of times an element can occur."
ms.author: solsen
ms.date: 05/14/2024
ms.topic: reference
author: SusanneWindfeldPedersen
ms.reviewer: solsen
---
[//]: # (START>DO_NOT_EDIT)
[//]: # (IMPORTANT:Do not edit any of the content between here and the END>DO_NOT_EDIT.)
[//]: # (Any modifications should be made in the .xml files in the ModernDev repo.)
# MaxOccurs Property
> **Version**: _Available or changed with runtime version 1.0._

Sets a value that indicates the maximum number of times an element can occur.

## Applies to
-   Xml Port Text Element
-   Xml Port Table Element
-   Xml Port Field Element

## Property Value

|Value|Available or changed with|Description|
|-----------|-----------|---------------------------------------|
|**Once**|runtime version 1.0|The element can occur at most once.|
|**Unbounded**|runtime version 1.0|There is no maximum number of occurrences.|

[//]: # (IMPORTANT: END>DO_NOT_EDIT)


The default values are the following:

|**SourceType**|**Default**|  
|--------------|-----------|  
|**Table**|Unbounded|  
|**Text**|Unbounded|  
|**Field**|Once|  

## Syntax

```AL
MaxOccurs = Once;
```
 
## Remarks

The default value of the **MaxOccurs** property varies depending on the type of this element.  
  
The minimum number of times an element can appear is determined by the value of the [MinOccurs Property](devenv-minoccurs-property.md).  
  
The **MinOccurs** and **MaxOccurs** properties conform to the standard occurrence constraints that are used when defining XML schemas.  
  
The minimum number can be either 1 or 0.  
  
The maximum number can be either 1 or infinite.  
  
## See Also  

[Properties](devenv-properties.md)
