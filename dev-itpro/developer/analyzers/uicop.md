---
title: "UICop Analyzer"
ms.author: solsen
ms.custom: na
ms.date: 10/01/2019
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: SusanneWindfeldPedersen
---
[//]: # (START>DO_NOT_EDIT)
[//]: # (IMPORTANT:Do not edit any of the content between here and the END>DO_NOT_EDIT.)
[//]: # (Any modifications should be made in the .xml or .resx files in the ModernDev repo.)
# UICop Analyzer Rules
UICop is an analyzer that enforces rules that must be respected by extensions meant to be installed for individual tenants.

## Rules

|Id|Title|Description|MessageFormat|Category|Default Severity|IsEnabledbyDefault|
|--|-----|-----------|-------------|--------|----------------|------------------|
|[AW0001](uicop-aw0001-requestpageofxmlportscannotbedisplayed.md)|The Web client does not support displaying the Request page of XMLPorts.|The Web client does not support displaying the Request page of XMLPorts.|The Web client does not support displaying the Request page of the XMLPort '{0}'.|WebClient|Warning|true|
|[AW0002](uicop-aw0002-cuegroupscannotcontainbothactionsandfields.md)|The Web client does not support displaying both Actions and Fields in Cue Groups. Only Fields will be displayed.|The Web client does not support displaying both Actions and Fields in Cue Groups. Only Fields will be displayed.|The Web client does not support displaying both Actions and Fields in the Cue Group '{0}'. Only Fields will be displayed.|WebClient|Warning|true|
|[AW0003](uicop-aw0003-repeaterwithpartscannotbedisplayed.md)|The Web client does not support displaying Repeater controls containing Parts.|The Web client does not support displaying Repeater controls containing Parts.|The Web client does not support displaying Repeater controls containing Parts.|WebClient|Warning|true|
|[AW0004](uicop-aw0004-blobcannotbeusedonpagefield.md)|A Blob cannot be used as a source expression for a page field.|A Blob cannot be used as a source expression for a page field.|A Blob cannot be used as a source expression for a page field.|WebClient|Warning|true|
|[AW0005](uicop-aw0005-useimageproperty.md)|Actions should use the Image property.|Actions should use the Image property.|Action with name '{0}' should have a value for the Image property.|WebClient|Info|true|
|[AW0006](uicop-aw0006-useusagecategoryproperty.md)|Pages and reports should use the UsageCategory and ApplicationArea properties to be searchable.|Pages and reports should use the UsageCategory and ApplicationArea properties to be searchable.|The {0} '{1}' should use the UsageCategory and ApplicationArea properties to be searchable.|WebClient|Info|true|
|[AW0007](uicop-aw0007-repeaterwithflowfiltercannotbedisplayed.md)|The Web client does not support displaying Repeater controls that contain FlowFilter fields.|The Web client does not support displaying Repeater controls that contain FlowFilter fields.|The FlowFiter field '{0}' in the Repeater control '{1}' cannot be displayed by the Web client.|WebClient|Error|true|

[//]: # (IMPORTANT: END>DO_NOT_EDIT)
## See Also  
[Using the Code Analysis Tool](../devenv-using-code-analysis-tool.md)  
[Ruleset for the Code Analysis Tool](../devenv-rule-set-syntax-for-code-analysis-tools.md)  
[Using the Code Analysis Tools with the Ruleset](../devenv-using-code-analysis-tool-with-rule-set.md)