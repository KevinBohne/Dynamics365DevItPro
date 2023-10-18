---
title: "Session.UnbindSubscription(Codeunit) Method"
description: "Unbinds the event subscriber methods from in the codeunit instance."
ms.author: solsen
ms.custom: na
ms.date: 07/07/2021
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
author: SusanneWindfeldPedersen
---
[//]: # (START>DO_NOT_EDIT)
[//]: # (IMPORTANT:Do not edit any of the content between here and the END>DO_NOT_EDIT.)
[//]: # (Any modifications should be made in the .xml files in the ModernDev repo.)
# Session.UnbindSubscription(Codeunit) Method
> **Version**: _Available or changed with runtime version 1.0._

Unbinds the event subscriber methods from in the codeunit instance. This essentially deactivates the subscriber methods for the codeunit instance.


## Syntax
```AL
[Ok := ]  Session.UnbindSubscription(Codeunit: Codeunit)
```
> [!NOTE]
> This method can be invoked without specifying the data type name.
## Parameters
*Codeunit*  
&emsp;Type: [Codeunit](../codeunit/codeunit-data-type.md)  
The codeunit that contains the event subscribers.  


## Return Value
*[Optional] Ok*  
&emsp;Type: [Boolean](../boolean/boolean-data-type.md)  
**true** if the event subscriber methods unbind successfully to the codeunit instance and no errors occurred, otherwise **false**. If you omit this optional return value and the operation does not execute successfully, a runtime error will occur.  


[//]: # (IMPORTANT: END>DO_NOT_EDIT)

## Remarks  
 You can only call this method on codeunits that have the [EventSubscriberInstance Property](../../properties/devenv-eventsubscriberinstance-property.md) set to **Manual**.  
  
 Calling this method on a codeunit that hasn't been bound \(by the [BindSubscription Method](../../methods-auto/session/session-bindsubscription-method.md)\) will result in an error. If the call to this method is successful, all bindings are removed.  
  
 The codeunit instance that is unbound will be the same instance that previously was bound.  
  
## Example  
 The following sample code illustrates a typical use of the BindSubscription method.  
  
```al
procedure MyFunction()  
var  
    Subscriber: Codeunit Subscriber;  
begin 
    // Set global information on the subscriber codeunit if required  
    // You can rely on the instance being the same as the one receiving the event subscriber call  
  
    Subscriber.MySetGlobalInfo(123);
    BindSubscription(Subscriber);  
    DoSomething();  // After binding, all subscriptions on Subscriber are "active".  
    UnbindSubscription(Subscriber);  // Now deactivating again  
    DoStuff();  // This time no events are raised inside Subscriber;  
end;   
```  

## See Also
[Session Data Type](session-data-type.md)  
[Get Started with AL](../../devenv-get-started.md)  
[Developing Extensions](../../devenv-dev-overview.md)
