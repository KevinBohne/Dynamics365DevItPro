---
title: "Notification.AddAction(Text, Integer, Text) Method"
description: "Specifies an action for the notification."
ms.author: solsen
ms.date: 05/14/2024
ms.topic: reference
author: SusanneWindfeldPedersen
ms.reviewer: solsen
---
[//]: # (START>DO_NOT_EDIT)
[//]: # (IMPORTANT:Do not edit any of the content between here and the END>DO_NOT_EDIT.)
[//]: # (Any modifications should be made in the .xml files in the ModernDev repo.)
# Notification.AddAction(Text, Integer, Text) Method
> **Version**: _Available or changed with runtime version 1.0._

Specifies an action for the notification.


## Syntax
```AL
 Notification.AddAction(Caption: Text, CodeunitID: Integer, MethodName: Text)
```
## Parameters
*Notification*  
&emsp;Type: [Notification](notification-data-type.md)  
An instance of the [Notification](notification-data-type.md) data type.  

*Caption*  
&emsp;Type: [Text](../text/text-data-type.md)  
The text string that appears as the caption of the action in the notification UI. The string can be a label that is enabled for multilanguage functionality.  

*CodeunitID*  
&emsp;Type: [Integer](../integer/integer-data-type.md)  
The ID of the Codeunit to run when the action is initiated from the notification UI. The codeunit should contain at least one global method to be called by the notification action. The global method must have a Notification data type parameter for accepting the notification object.  

*MethodName*  
&emsp;Type: [Text](../text/text-data-type.md)  
The name of the method in the Codeunit, which is specified by the CodeunitID parameter, that you want to run for the action.  



[//]: # (IMPORTANT: END>DO_NOT_EDIT)

## Remarks

An action provides a way for you to add an interactive notification that enables users to respond to or take action on the notification. The method that is called by the action contains logic that you want to run for the action.

For more information and a detailed example, see [Notifications](../../devenv-notifications-developing.md).

##  Example

The following code creates two actions for a notification. The actions call the **RunAction1** and **RunAction2** methods in the codeunit **Action Handler**.

```al
MyNotification.Message := 'This is a notification';
MyNotification.Scope := NotificationScope::LocalScope;
MyNotification.AddAction('Action 1',Codeunit::"Action Handler",'RunAction1');
MyNotification.AddAction('Action 2',Codeunit::"Action Handler",'RunAction2');
MyNotification.Send();
```

To handle the actions, the **Action Handler** codeunit has two global methods that have a **Notification** data type parameter:

```al
procedure RunAction1(MyNotification : Notification);
begin
    Message('This is RunAction1');
end;

procedure RunAction2(MyNotification : Notification);
begin
    Message('This is RunAction2');
end;
```

## See Also
[Notification Data Type](notification-data-type.md)  
[Getting Started with AL](../../devenv-get-started.md)  
[Developing Extensions](../../devenv-dev-overview.md)
