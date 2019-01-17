---
title: "Subscribing to Events"
description: This topic describes how to design event subscribers in Dynamics 365 Business Central. 
ms.custom: na
ms.date: 10/01/2018
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: SusanneWindfeldPedersen
---

[!INCLUDE[d365fin_dev_blog](includes/d365fin_dev_blog.md)]

# Subscribing to Events
To handle events, you design event subscribers. Event subscribers determine what actions to take in response to an event that has been raised. An event subscriber is an AL method that subscribes to, or listens for, a specific event that is declared by an event publisher method. The event subscriber includes code that defines the business logic to handle the event. When the published event is raised, the event subscriber is called and its code is run.  

Subscribing to an event tells the runtime that the subscriber method must be called whenever the publisher method is run, either by code (as with business and integration events) or by the system (as with trigger events). The runtime establishes the link between an event raised by the publisher and its subscribers by looking for event subscriber methods.  

There can be multiple subscribers to the same event from various locations in the application code. When an event is raised, the subscriber methods are run one at a time in random order. You cannot specify the order in which the subscriber methods are called.  

Be aware that changing the state may not only impact the publishing code but other subscribers as well.   

## Creating an event subscriber method  
You create an event subscriber method just like other methods except that you specify properties that set up the subscription to an event publisher. The procedure is slightly different for database and page trigger events than business and integration events because business and integration events are raised by event publisher methods in application code. Trigger events are predefined system events that are raised automatically on tables and pages.  

For an explanation about the different types, see [Event Types](devenv-event-types.md).  

### To create an event subscriber method
1.  Decide which codeunit to use for the event subscriber method.  

     You can create a new codeunit or use an existing one.  

2.  Set the **EventSubscriberInstance** property of the codeunit to specify how event subscriber methods in the codeunit are bound to codeunit instance. For more information, see [EventSubscriberInstance Property](properties/devenv-eventsubscriberinstance-property.md).  

3.  Add an AL method to the codeunit.  

     We recommend that you give the method a name that indicates what the subscriber does, and has the format *[Action][Event]*. *[Action]* is text that describes what the method does and *[Event]* is the name of the event publisher method to which it subscribes. <!-- For more information about naming, see [Best Practices with Events](devenv-events-best-practices.md).  -->

4.  Decorate the method with the [EventSubscriber attribute](methods/devenv-eventsubscriber-attribute.md), and change accordingly.

    ```  
    [EventSubscriber(ObjectType::ObjectType, ObjectId, 'OnSomeEvent', 'ElementName', SkipOnMissingLicense, SkipOnMissingPermission)]
    ```    
    > [!TIP]  
    > Use the `teventsub` snippet to get started and typing the keyboard shortcut `Ctrl + space` displays IntelliSense to help you fill the attribute arguments and to discover which events are available to use.    

5.  Add code to the method for handling the event.  


## Example 1
This example creates the codeunit **7000002 MySubscriber** to subscribe to an event that has been published by the event publisher method called `OnAddressLineChanged` in the codeunit **70000001 MyPublishers**. The event is raised by a change to the **Address** field on page **21 Customer Card**. This example assumes the following:

-   The codeunit **70000001 MyPublishers** with the event publisher method `OnAddressLineChanged` already exists. To see how to do this, see [Publishing Event Example](devenv-publishing-events.md#example).
-   The code for raising the `OnAddressLineChanged` event has been added to the **Customer Card** page. To see how to do this, see [Raising Event Example](devenv-raising-events.md#example).

The following code creates a codeunit called **70000002 MySubscriber** that includes an event subscriber method, called `CheckAddressLine`. The method includes code for handling the published event.

```
codeunit 70000002 MySubscriber
{
    EventSubscriberInstance = StaticAutomatic;

    [EventSubscriber(ObjectType::Codeunit, Codeunit::"MyPublishers", 
    
    'OnAddressLineChanged', '', true, true)]
    procedure CheckAddressLine(line : Text[100]);
    begin
        if (STRPOS(line, '+') > 0) then begin
            MESSAGE('Cannot use a plus sign (+) in the address [' + line + ']');
        end;
    end;
}
```

## Example 2
This example achieves the same as example 1, except it subscribes to the page trigger event `OnBeforeValidateEvent` on the `Address` field instead. By using the page trigger, you avoid creating an event publisher and adding code to raise the event because this is done automatically by the system.

```
codeunit 70000002 MySubscriber
{
    EventSubscriberInstance = StaticAutomatic;

    [EventSubscriber(ObjectType::Page, Page::"Customer Card", 'OnBeforeValidateEvent', 'Address', true, true)]
    local procedure CheckAddressLine(var Rec : Record Customer)
    begin
        if (STRPOS('Rec.Address', '+') > 0) then begin
            MESSAGE('Cannot use a plus sign (+) in the address [' + 'Address' + ']');
        end;
    end;
}
```

## See Also  
 [Publishing Events](devenv-publishing-events.md)   
 [Raising Events](devenv-raising-events.md)   
 [Event Types](devenv-event-types.md)   
 [Events in AL](devenv-events-in-al.md)
