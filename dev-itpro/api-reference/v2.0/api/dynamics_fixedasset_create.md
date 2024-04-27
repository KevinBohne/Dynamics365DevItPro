---
title: Create fixedAssets
description: Creates a fixed asset object in Dynamics 365 Business Central.
author: SusanneWindfeldPedersen
ms.service: dynamics-365-business-central
ms.topic: reference
ms.devlang: al
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/09/2024
ms.author: solsen
---

<!-- NOTE: This article is an auto-generated stub from the metadata file. -->
<!-- The sections marked with an EDIT_IS_REQUIRED require manual editing. -->
# Create fixedAssets

Creates a fixed asset in [!INCLUDE[prod_short](../../../includes/prod_short.md)].

## HTTP request

Replace the URL prefix for [!INCLUDE[prod_short](../../../includes/prod_short.md)] depending on environment following the [guideline](../../v2.0/endpoints-apis-for-dynamics.md).
<!-- START>EDIT_IS_REQUIRED. There URL for accessing the endpoint might be different or there might be more than one -->
```
POST businesscentralPrefix/companies({id})/fixedAssets({id})
```
<!-- END>EDIT_IS_REQUIRED -->
## Request headers

|Header|Value|
|------|-----|
|Authorization  |Bearer {token}. Required. |
|Content-Type  |application/json|
|If-Match      |Required. When this request header is included and the eTag provided does not match the current tag on the **fixedAsset**, the **fixedAsset** will not be updated. |

## Request body

In the request body, supply a JSON representation of a **fixedAsset** object.

## Response

If successful, this method returns ```201 Created``` response code and a **fixedAsset** object in the response body.


## Example

**Request**

Here is an example of the request.
<!-- START>EDIT_IS_REQUIRED. There URL for accessing the endpoint might be different. Fill in the property values -->
```json
POST https://{businesscentralPrefix}/api/v2.0/companies({id})/fixedAssets({id})
Content-type: application/json
{
    "displayName": "Mercedes 300",
    "fixedAssetLocationCode": "ADM",
    "fixedAssetLocationId": "c5adcedf-b501-ef11-b3c3-83fe9ccecec3",
    "classCode": "TANGIBLE",
    "subclassCode": "VEHICLES",
    "blocked": false,
    "serialNumber": "EA 12 394 Q",
    "employeeNumber": "",
    "employeeId": "00000000-0000-0000-0000-000000000000",
    "underMaintenance": false
}
```
<!-- END>EDIT_IS_REQUIRED -->
**Response**

Here is an example of the response.
<!-- START>EDIT_IS_REQUIRED. Fill in values for properties -->
```json
HTTP/1.1 201 Created
Content-type: application/json
{
    "id": "4326bf5b-7204-ef11-b3c5-a1596e55036b",
    "number": "FA000100",
    "displayName": "Mercedes 300",
    "fixedAssetLocationCode": "ADM",
    "fixedAssetLocationId": "c5adcedf-b501-ef11-b3c3-83fe9ccecec3",
    "classCode": "TANGIBLE",
    "subclassCode": "VEHICLES",
    "blocked": false,
    "serialNumber": "EA 12 394 Q",
    "employeeNumber": "",
    "employeeId": "00000000-0000-0000-0000-000000000000",
    "underMaintenance": false,
    "lastModifiedDateTime": "2024-04-27T08:44:29.88Z"
}
```
<!-- END>EDIT_IS_REQUIRED -->
## See Also

[Tips for working with the APIs](/dynamics365/business-central/dev-itpro/developer/devenv-connect-apps-tips)  
[fixedAsset](../resources/dynamics_fixedAsset.md)  
[GET fixedAsset](dynamics_fixedasset_get.md)  
[DELETE fixedAsset](dynamics_fixedasset_delete.md)  
[PATCH fixedAsset](dynamics_fixedasset_update.md)  
