---
title: "Linking to the Dynamics Business Central App"
ms.custom: na
ms.date: 10/01/2018
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: jswymer
ms.author: jswymer
---
# Linking to the Business Central App
The protocol handler for the [!INCLUDE[d365fin_uni_app_md](includes/d365fin_uni_app_md.md)] lets you construct a URL for starting the app on a device, such as a phone or tablet. You can then distribute this URL by e-mail or from a Web page to the users.  
  
The [!INCLUDE[d365fin_uni_app_md](includes/d365fin_uni_app_md.md)] URL is based on the *ms-businesscentral* URI scheme, which is registered automatically when the app is installed. Invoking a URL based on this scheme will start the app with the provided parameters.  
  
## Constructing the URL  
To construct a URL, start with *ms-businesscentral<!-- ms-dynamicsnav-->* scheme, and then add additional parameters as needed. Some parameters are required and others are optional. 

The structure of a [!INCLUDE[d365fin_uni_app_md](includes/d365fin_uni_app_md.md)] link is very similar to links for the [!INCLUDE[d365fin_web_md](includes/d365fin_web_md.md)], and has the following syntax: 

```
ms-businesscentral://[<domain>][/<aadtenantid>][/sandbox]/?[company=<companyname>][&page =<ID>][&mode=<View|Edit|Create>][&profile=<profileID>][&bookmark=<bookmark>][&filter='<field>'-IS-'<value>'[-AND-'<field>'-IS-'<value>']]
```
<!--
```
ms-businesscentral://[<hostname>:][<port>]/[sandbox/]?[company=<companyname>][&page =<ID>][&mode=<View|Edit|Create>][&profile=<profileID>][&bookmark=<bookmark>][&filter='<field>'-IS-'<value>'[-AND-'<field>'-IS-'<value>']]
```
-->
Parameters in `[]` are optional; all other parameters are required. Do not include the brackets (`[` and `]`).

`<>` indicates values that you provide. Do not include the `<` and `>`.

## Parameters
<!--
The following table describes the parameters for the main part of the URL, which are the parameters up to and including `[/<port>]/` <!-- `[/<instance>]/`. These parameters are ony relavant for ISV Embed solutions.

|Parameter|Description| Example |
|---------|-----------|---------|  
 
|port|The port number for your [!INCLUDE[nav_web](includes/nav_web_md.md)] server instance. If not provided, the standard SSL port \(443\) is used.| `8080` |

|Instance|The [!INCLUDE[nav_web_server_instance_md](includes/nav_web_server_instance_md.md)] instance that you want to connect to.| `dynamicsnav110`|
-->
The following table describes the parameters that you can specify<!-- after `[/<instance>]/`-->. <!-- These parameters are referred to as the *query parameters*.-->

|Parameter|Description| Example |
|---------|-----------|---------| 
|domain|Domain name for the solution. This is required for an ISV Embed solution. For Business Central, you use `businesscentral.dynamics.com` or you can omit this parameter.| `ms-businesscentral://businesscentral.dynamics.com/`<br /><br />`ms-businesscentral:///`<br /><br />`ms-businesscentral://businesscentral.mysolution.com/`| 
|aadtenantid|The unique identifier for an Azure Active Directory (AAD) tenant. The value can be formatted as a GUID or domain name. This is useful to those who work across multiple AAD organizations, such as delegated administrators, support personnel or external accountants, because it allows explicitly targeting an AAD tenant. If this is omitted, you will be directed to the primary AAD tenant or the same AAD tenant that you are currently signed in to.|`ms-businesscentral://businesscentral.mysolution.com/mysolutionaadtenant.onmicrosoft.com`|
|sandbox|Specifies that the URL should target the the Dynamics 365 Business Central sandbox environment instead of a production environment.|`ms-businesscentral:/businesscentral.dynamics.com/sandbox/`<br /><br />`ms-businesscentral://businesscentral.mysolution.com/sandbox/`|
|company|The company that you want to open in the client. If not provided, the default company is used.|`ms-businesscentral:///?'company=CRONUS%20International%20Ltd.'`<br /><br />`ms-businesscentral://businesscentral.mysolution.com/?'company=CRONUS%20International%20Ltd.'`|
|page	|The ID of the page that you want to open directly.|`ms-businesscentral:///?page=21`<br /><br />`ms-businesscentral://businesscentral.mysolution.com/?page=21`|
|mode|Whether the page opens in view, edit, or create mode. `view` only lets you see the data on the page, not modify data. `edit` lets you to modify data on the page. `create` lets you to modify data on the page and add new entities. |`ms-businesscentral:///?page=21&mode=create`<br /><br />`ms-businesscentral://businesscentral.mysolution.com/?page=21&mode=create`|
|profile|The name of the profile that you want to use in the client. This determines the Role Center that is opened. If not provided, the default profile is used.|`ms-businesscentral:///?profile=BUSINESS%20%MANAGER`<br /><br />`ms-businesscentral://businesscentral.mysolution.com/?profile=BUSINESS%20%MANAGER`|
|bookmark|	The bookmark of the record you want to open. The value of a bookmark is an alphanumeric string of characters, for example, `19%3bGwAAAAJ7BDEAMAAwADA%3d`.<br /><br /> For the page types Card, CardPart, and Document, the bookmark specifies the record that is shown in the page. For page types List, ListPart, and Worksheet, the bookmark specifies the record that is selected in the list on the page.<br /><br /> **Important:**  Bookmarks are generated automatically. You can only determine a value for the bookmark by displaying the page in the client and looking at its address. Therefore, a bookmark is only relevant when the address you are working with has been copied from another instance of the page.|`ms-businesscentral:///?bookmark=19%3bGwAAAAJ7BDEAMAAwADA%3d`<br /><br />`ms-businesscentral://businesscentral.mysolution.com/?bookmark=19%3bGwAAAAJ7BDEAMAAwADA%3d`|
|filter	|The filter you want to apply to the page.<br /><br />The filter parameter enables you to display only records from the underlying table of the page that have specific values for one or more fields.	For more information about filters, see [Filtering Data on the Page](devenv-web-client-urls.md#Filtering).|`ms-businesscentral:///?page9305&filter='No.'%20IS%20'1001'`<br /><br />`ms-businesscentral:///?page9305&filter='Sell-to-Customer-No.'-IS-'10000'-AND-'Location-Code'-IS-'BLUE'`<br /><br />`ms-businesscentral://businesscentral.mysolution.com/?page9305&filter='No.'%20IS%20'1001'`<br /><br />`ms-businesscentral://businesscentral.mysolution.com/?page9305&filter='Sell-to-Customer-No.'-IS-'10000'-AND-'Location-Code'-IS-'BLUE'`|

<!--
|tenant	|The ID of the tenant that you want to connect to. If not provided, the default tenant is used.|`ms-businesscentral:///?tenant=mytenant2-1`|
-->


The parameters can be in any order. However, the first parameter must be preceded by the `?` symbol, and any additional parameters must be preceded by the `&` symbol.

<!--

> [!NOTE]  
> It is not possible to specify which client/device type to open up the URL in; the last used client will open up when clicking the URL.
-->
<!-- add for onprem
The URL `ms-businesscentral:///?page=21` or `ms-dynamicsnav:///?page=21` will open the server that you last connected to on the specified page.  -->

<!-- 
## URL Examples  
 The following examples demonstrate how to use the parameters from the table earlier in this section:  
  
-   *ms-businesscentral://myserver/myinstance/*  
  
-   *ms-businesscentral://myserver:440/myinstance/*  
  
-   *ms-businesscentral://myserver/myinstance/?company=MyOtherCompany*  
  
-   *ms-businesscentral://myserver/myinstance/?tenant=myTenant2&company=MyCompany2*  

-   *ms-dynamicsnav://myserver/myinstance/*  
  
-   *ms-dynamicsnav://myserver:440/myinstance/*  
  
-   *ms-dynamicsnav://myserver/myinstance/?company=MyOtherCompany*  
  
-   *ms-dynamicsnav://myserver/myinstance/?tenant=myTenant2&company=MyCompany2*  
  
-->

<!-- Add this as note in onprem
 
[!IMPORTANT]  
The *ms-businesscentral or ms-dynamicsnav * scheme only translates to a secure server connection. Therefore the [!INCLUDE[nav_tablet](includes/nav_tablet_md.md)] and [!INCLUDE[nav_phone](includes/nav_phone_md.md)] must be exposed through an https connection. For more information, see [How to: Configure SSL to Secure the Connection to Microsoft Dynamics NAV Web Client](How-to--Configure-SSL-to-Secure-the-Connection-to-Microsoft-Dynamics-NAV-Web-Client.md). 
-->

<!--
  
## Adding a user name to the URL  
 The *ms-businesscentral* scheme also supports sending the user name in the URL for pre-filling the user name. The password must be entered by the user. To send the user name, you must URL encode the value and prefix the server address by using *\<encoded username>@*. Examples are as follows:  
  
-   *ms-businesscentral://demouser%40mycompany.com@myserver/myinstance/*  
  
-   *ms-businesscentral://user1:@myserver/myinstance/*  
-->
<!-- 

-   *ms-dynamicsnav://demouser%40mycompany.com@myserver/myinstance/*  
  
-   *ms-dynamicsnav://user1:@myserver/myinstance/*  

-->  

<!--
> [!IMPORTANT]  
>  We recommend that you do not share a user name in the URL. This technique should only be used in demonstration scenarios and other instances where the accidental sharing of a URL will not compromise the system.  
-->  
## See Also  
<!-- [Developing for the Microsoft Dynamics NAV Universal App](Developing-for-the-Microsoft-Dynamics-NAV-Universal-App.md) -->
<!-- [How to: Open the Microsoft Dynamics NAV Tablet or Phone Client from a Browser](How-to--Open-the-Microsoft-Dynamics-NAV-Tablet-or-Phone-Client-from-a-Browser.md) -->  
[Web Client URLs](devenv-web-client-urls.md)  