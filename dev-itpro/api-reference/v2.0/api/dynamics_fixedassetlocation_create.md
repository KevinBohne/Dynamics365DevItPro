---
title: Create fixedAssetLocations
description: Creates a fixed asset location object in Dynamics 365 Business Central.
author: SusanneWindfeldPedersen
ms.service: dynamics-365-business-central
ms.topic: reference
ms.devlang: al
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2024
ms.author: solsen
ms.reviewer: solsen
---

<!-- NOTE: This article is an auto-generated stub from the metadata file. -->
<!-- The sections marked with an EDIT_IS_REQUIRED require manual editing. -->
# Create fixedAssetLocations

Creates a fixed asset location in [!INCLUDE[prod_short](../../../includes/prod_short.md)].

## HTTP request

Replace the URL prefix for [!INCLUDE[prod_short](../../../includes/prod_short.md)] depending on environment following the [guideline](../../v2.0/endpoints-apis-for-dynamics.md).
<!-- START>EDIT_IS_REQUIRED. There URL for accessing the endpoint might be different or there might be more than one -->
```
POST businesscentralPrefix/companies({id})/fixedAssetLocations({id})
```
<!-- END>EDIT_IS_REQUIRED -->
## Request headers

|Header|Value|
|------|-----|
|Authorization  |Bearer {token}. Required. |
|Content-Type  |application/json|
|If-Match      |Required. When this request header is included and the eTag provided does not match the current tag on the **fixedAssetLocation**, the **fixedAssetLocation** will not be updated. |

## Request body

In the request body, supply a JSON representation of a **fixedAssetLocation** object.

## Response

If successful, this method returns ```201 Created``` response code and a **fixedAssetLocation** object in the response body.


## Example

**Request**

Here is an example of the request.
<!-- START>EDIT_IS_REQUIRED. There URL for accessing the endpoint might be different. Fill in the property values -->
```json
POST https://{businesscentralPrefix}/api/v2.0/companies({id})/fixedAssetLocations({id})
Content-type: application/json
{
    "code": "ADM",
    "displayName": "Administration, Building 1",
    "lastModifiedDateTime": "2024-04-23T21:10:13.737Z"
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
    "id": "c5adcedf-b501-ef11-b3c3-83fe9ccecec3",
    "code": "ADM",
    "displayName": "Administration, Building 1",
    "lastModifiedDateTime": "2024-04-23T21:10:13.737Z"
}
```
<!-- END>EDIT_IS_REQUIRED -->
## See Also

[Tips for working with the APIs](/dynamics365/business-central/dev-itpro/developer/devenv-connect-apps-tips)  
[fixedAssetLocation](../resources/dynamics_fixedAssetLocation.md)  
[GET fixedAssetLocation](dynamics_fixedassetlocation_get.md)  
[DELETE fixedAssetLocation](dynamics_fixedassetlocation_delete.md)  
[PATCH fixedAssetLocation](dynamics_fixedassetlocation_update.md)  
