---
title: Create purchaseOrders  
description: Creates a purchase order object in Dynamics 365 Business Central.
author: SusanneWindfeldPedersen
ms.topic: reference
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/01/2021
ms.author: solsen
---

<!-- NOTE: This article is an auto-generated stub from the metadata file. -->
<!-- The sections marked with an EDIT_IS_REQUIRED require manual editing. -->
# Create purchaseOrders

[!INCLUDE[api_v2_note](../../../includes/api_v2_note.md)]

Creates a purchase order in [!INCLUDE[prod_short](../../../includes/prod_short.md)].

## HTTP request

Replace the URL prefix for [!INCLUDE[prod_short](../../../includes/prod_short.md)] depending on environment following the [guideline](../../v2.0/endpoints-apis-for-dynamics.md).

```
POST businesscentralPrefix/companies({id})/purchaseOrders
```

## Request headers

|Header|Value|
|------|-----|
|Authorization  |Bearer {token}. Required. |
|Content-Type  |application/json|
|If-Match      |Required. When this request header is included and the eTag provided does not match the current tag on the **purchaseOrder**, the **purchaseOrder** will not be updated. |

## Request body

In the request body, supply a JSON representation of a **purchaseOrder** object.

## Response

If successful, this method returns ```201 Created``` response code and a **purchaseOrder** object in the response body.


## Example

**Request**

Here is an example of the request.

```json
POST https://{businesscentralPrefix}/api/v2.0/companies({id})/purchaseOrders
Content-type: application/json
{
   "orderDate": "2021-01-01",
   "postingDate": "2021-01-01",
   "dueDate": "2021-01-01",
   "vendorId" : "",
   "vendorNumber": "20000",
   "payToVendorId": "Evan McIntosh",
   "payToVendorNumber": "20000",
   "shipToName": "First Up Consultants",
   "shipToContact": "Evan McIntosh",
   "buyFromAddressLine1": "100 Day Drive",
   "buyFromAddressLine2": "",
   "buyFromCity": "Chicago",
   "buyFromCountry": "US",
   "buyFromState": "IL",
   "buyFromPostCode": "61236",
   "shipToAddressLine1": "100 Day Drive",
   "shipToAddressLine2": "",
   "shipToCity": "Chicago",
   "shipToCountry": "US",
   "shipToState": "IL",
   "shipToPostCode": "61236",
   "currencyId" : "00000000-0000-0000-0000-000000000000",
   "currencyCode": "USD",
   "pricesIncludeTax" : false,
   "paymentTermsId" : "04a5738a-44e3-ea11-bb43-000d3a2feca1",
   "shipmentMethodId" : "93f5638a-55e3-jk22-aa32-211d3a2fdce5",
   "discountAmount" : 0,
   "discountAppliedBeforeTax" : true,
   "totalAmountExcludingTax": 3122.8,
   "totalTaxAmount": 187.37,
   "totalAmountIncludingTax": 3310.17,
   "lastModifiedDateTime": "2021-01-01"
}
```

**Response**

Here is an example of the response.

```json
HTTP/1.1 201 Created
Content-type: application/json
{
   "id": "5d115c9c-44e3-ea11-bb43-000d3a2feca1",
   "number": "108001",
   "orderDate": "2021-01-01",
   "postingDate": "2021-01-01",
   "dueDate": "2021-01-01",
   "vendorId" : "",
   "vendorNumber": "20000",
   "vendorName": "First Up Consultants",
   "payToName": "First Up Consultants",
   "payToVendorId": "Evan McIntosh",
   "payToVendorNumber": "20000",
   "shipToName": "First Up Consultants",
   "shipToContact": "Evan McIntosh",
   "buyFromAddressLine1": "100 Day Drive",
   "buyFromAddressLine2": "",
   "buyFromCity": "Chicago",
   "buyFromCountry": "US",
   "buyFromState": "IL",
   "buyFromPostCode": "61236",
   "shipToAddressLine1": "100 Day Drive",
   "shipToAddressLine2": "",
   "shipToCity": "Chicago",
   "shipToCountry": "US",
   "shipToState": "IL",
   "shipToPostCode": "61236",
   "payToAddressLine1": "100 Day Drive",
   "payToAddressLine2": "",
   "payToCity": "Chicago",
   "payToCountry": "US",
   "payToState": "IL",
   "payToPostCode": "61236",
   "currencyId" : "00000000-0000-0000-0000-000000000000",
   "currencyCode": "USD",
   "pricesIncludeTax" : false,
   "discountAmount" : 0,
   "discountAppliedBeforeTax" : false,
   "totalAmountExcludingTax": 0,
   "totalTaxAmount": 0,
   "totalAmountIncludingTax": 0,
   "status" : "Draft",
   "lastModifiedDateTime": "2021-01-01T20:34:41.357Z"
}
```

## See Also

[Tips for working with the APIs](../../../developer/devenv-connect-apps-tips.md)  
[purchaseOrder](../resources/dynamics_purchaseOrder.md)  
[GET purchaseOrder](dynamics_purchaseorder_get.md)  
[DELETE purchaseOrder](dynamics_purchaseorder_delete.md)  
[PATCH purchaseOrder](dynamics_purchaseorder_update.md)  
