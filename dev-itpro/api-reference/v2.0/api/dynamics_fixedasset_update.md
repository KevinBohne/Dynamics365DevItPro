---
title: Update fixedAssets
description: Updates a  fixed asset object in Dynamics 365 Business Central.
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
# Update fixedAssets

Updates the properties of a fixed asset object for [!INCLUDE[prod_short](../../../includes/prod_short.md)].

## HTTP request

Replace the URL prefix for [!INCLUDE[prod_short](../../../includes/prod_short.md)] depending on environment following the [guideline](../../v2.0/endpoints-apis-for-dynamics.md).
<!-- START>EDIT_IS_REQUIRED. There URL for accessing the endpoint might be different or there might be more than one-->
```
PATCH businesscentralPrefix/companies({id})/fixedAssets({id})
```
<!-- END>EDIT_IS_REQUIRED-->
## Request headers

|Header|Value|
|------|-----|
|Authorization  |Bearer {token}. Required. |
|Content-Type  |application/json|
|If-Match      |Required. When this request header is included and the eTag provided does not match the current tag on the **fixedAsset**, the **fixed asset** will not be updated. |

## Request body

In the request body, supply the values for relevant fields that should be updated. Existing properties that are not included in the request body will maintain their previous values or be recalculated based on changes to other property values. For best performance you shouldn't include existing values that haven't changed.

## Response

If successful, this method returns a ```200 OK``` response code and an updated **fixedAsset** object in the response body.

## Example

**Request**

Here is an example of the request.
<!-- START>EDIT_IS_REQUIRED. There URL for accessing the endpoint might be different. Fill in the property values) -->
```json
PATCH https://{businesscentralPrefix}/api/v2.0/companies({id})/fixedAssets({id})
Content-type: application/json
{
    "blocked": true
}
```
<!-- END>EDIT_IS_REQUIRED -->
**Response**

Here is an example of the response.

<!-- START>EDIT_IS_REQUIRED. Fill in values for properties -->
```json
HTTP/1.1 200 OK
Content-type: application/json
{
    "id": "4326bf5b-7204-ef11-b3c5-a1596e55036b",
    "number": "FA000100",
    "displayName": "Mercedes 300",
    "fixedAssetLocationCode": "ADM",
    "fixedAssetLocationId": "c5adcedf-b501-ef11-b3c3-83fe9ccecec3",
    "classCode": "TANGIBLE",
    "subclassCode": "VEHICLES",
    "blocked": true,
    "serialNumber": "EA 12 394 Q",
    "employeeNumber": "",
    "employeeId": "00000000-0000-0000-0000-000000000000",
    "underMaintenance": false,
    "lastModifiedDateTime": "2024-04-27T08:46:13.087Z"
}
```
<!-- END>EDIT_IS_REQUIRED-->
## See Also

[Tips for working with the APIs](/dynamics365/business-central/dev-itpro/developer/devenv-connect-apps-tips)  
[fixedAsset](../resources/dynamics_fixedAsset.md)  
[GET fixedAsset](dynamics_fixedasset_get.md)  
[DELETE fixedAsset](dynamics_fixedasset_delete.md)  
[POST fixedAsset](dynamics_fixedasset_create.md)  
