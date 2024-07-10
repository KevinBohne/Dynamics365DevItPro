---
title: "AdditionalSearchTermsML Property"
description: "Specifies search terms (words and phrases) for the page in different languages."
ms.author: solsen
ms.date: 05/14/2024
ms.topic: reference
author: SusanneWindfeldPedersen
ms.reviewer: solsen
---
[//]: # (START>DO_NOT_EDIT)
[//]: # (IMPORTANT:Do not edit any of the content between here and the END>DO_NOT_EDIT.)
[//]: # (Any modifications should be made in the .xml files in the ModernDev repo.)
# AdditionalSearchTermsML Property
> **Version**: _Available or changed with runtime version 3.0._

Specifies search terms (words and phrases) for the page in different languages. In addition to the page caption, the terms are used by the search feature in the Web client and mobile apps. Separate terms with a comma.

## Applies to
-   Page
-   Report

[//]: # (IMPORTANT: END>DO_NOT_EDIT)


## Property Values

|Value           |Description                                  |
|----------------|---------------------------------------------|
|`<language ID>`   |The standard Windows three-letter language ID, such as ENU or DAN. Separate each language by a comma.|
|`<term>`  |The search word or phrase, which can consist of letters, numbers and special characters. Separate each term by a comma.|

## Syntax

```AL
AdditionalSearchTermsML = <language ID> = '<term>[,<term>]'[, <language ID> = '<term>[,<term>]'];
```

## Remarks

For [!INCLUDE[prod_short](../includes/prod_short.md)] on-premises, the [!INCLUDE[webserverinstance](../includes/webserverinstance.md)] configuration file (navsettings.json) includes a setting called `UseAdditionalSearchTerms` that enables or disables the use of additional search terms by the **Tell me**. For more information, see [Configuring [!INCLUDE[webserver](../includes/webserver.md)] Instances](../../administration/configure-web-server.md#Settings).

## Dependent Properties

The [UsageCategory property](devenv-usagecategory-property.md) must be set to a value other than `None` in order for the page to be searchable by **Tell me**. 

## Example

The following code snippet uses the **AdditionalSearchTermsML** property to add search terms in English and Danish to a list page whose caption is **Items**.

```AL
page 50101 SearchTestML
{
    PageType = List;
    ApplicationArea = All;
    SourceTable = Item;
    UsageCategory = Lists;
    CaptionMl = ENU = 'Items', DAN ='Varer';
    AdditionalSearchTermsML = ENU = 'product, merchandise', DAN = 'produkter';
    ...
}
```

## See Also

[Add pages and reports to Tell me](../devenv-al-menusuite-functionality.md)  
[Properties](devenv-properties.md)  
[Page Object](../devenv-page-object.md)  
[Report Object](../devenv-report-object.md)  
