---
title:  Azure Function Integration Telemetry
description: Learn about telemetry on Azure Function integrations with Business Central
author: KennieNP
ms.topic: conceptual
ms.devlang: al
ms.search.keywords: administration, tenant, telemetry
ms.date: 08/16/2022
ms.author: kepontop
ms.reviewer: jswymer
---
# Analyzing Azure Function Integration Telemetry

Azure Function integration telemetry gathers data about the success or failure of calls from Business Central to Azure Functions using the [Azure Function module](https://github.com/microsoft/BCApps/tree/main/src/System%20Application/App/Azure%20Function) in the System Application.

Failed operations result in a trace log entry that includes a reason for the failure.

## Custom dimensions available in all events

The following dimensions are available in all events described below and not included in the individual event documentation:

|Dimension|Description or value|
|---------|-----|
|aadTenantId|[!INCLUDE[aadTenantId](../includes/include-telemetry-dimension-aadtenantid.md)]|
|alCountryCode| [!INCLUDE[environmentType](../includes/include-telemetry-dimension-country-code.md)] |
|alFunctionHost| The base URL for the Azure function called from Business Central |
|alIsAdmin| [!INCLUDE[environmentType](../includes/include-telemetry-dimension-is-tenant-admin.md)]|
|alIsEvaluationCompany| [!INCLUDE[environmentType](../includes/include-telemetry-dimension-is-evaluation-company.md)] |
|alTenantLicenseState | [!INCLUDE[environmentType](../includes/include-telemetry-dimension-tenant-license-state.md)] |
|clientType|[!INCLUDE[environmentType](../includes/include-telemetry-dimension-client-type.md)]|
|companyName|[!INCLUDE[companyName](../includes/include-telemetry-dimension-company-name.md)]|
|environmentName|[!INCLUDE[environmentName](../includes/include-telemetry-dimension-environment-name.md)]|
|environmentType|[!INCLUDE[environmentType](../includes/include-telemetry-dimension-environment-type.md)]|

## Request sent to Azure function succeeded

Occurs when a request to an Azure function hosted from the URL {alFunctionHost} succeeded.

### General dimensions

|Dimension|Description or value|
|---------|-----|
|message|**Request sent to Azure function succeeded: {alFunctionHost}**|

### Custom dimensions

|Dimension|Description or value|
|---------|-----|
|eventId|**AL0000I74**|
|alStatusCode| The HTTP status code for the request. |

<!--

{"component":"Dynamics 365 Business Central Server","environmentType":"Production","eventId":"AL0000I74","clientType":"WebClient","telemetrySchemaVersion":"1.2","componentVersion":"21.0.44895.0","companyName":"CRONUS International Ltd.","aadTenantId":"common","extensionName":"System Application","extensionId":"63ca2fa4-4f03-4f2b-a480-172fef340d3f","extensionVersion":"21.0.0.0","alObjectName":"System Telemetry Logger","extensionPublisher":"Microsoft","alObjectType":"CodeUnit","alObjectId":"8713","alCallerAppVersion":"1.0.0.0","alCategory":"FeatureTelemetry","alCallerAppVersionMajor":"21","alDataClassification":"SystemMetadata","alIsEvaluationCompany":"No","alCallerPublisher":"Default publisher","alTenantLicenseState":"Evaluation","alClientType":"Web","alCallerAppName":"ALProject2","alCompany":"CRONUS International Ltd.","alCallerAppVersionMinor":"0","alFeatureName":"Connect to Azure Functions","alEventName":"Request sent to Azure function succeeded: testbcapp.azurewebsites.net","alSubCategory":"Usage","alFunctionHost":"testbcapp.azurewebsites.net","alStatusCode":"200"}

-->
## Request sent to Azure function failed

Occurs when a request to an Azure function hosted from the URL {alFunctionHost} failed.

### General dimensions
|Dimension|Description or value|
|---------|-----|
|message|**Request sent to Azure function failed: {alFunctionHost}**|

### Custom dimensions

|Dimension|Description or value|
|---------|-----|
|eventId|**AL0000I7P**|
|alStatusCode| The HTTP status code for the request. |


### Sample KQL code
This KQL code can help you get started analyzing and alerting on request failures to Azure functions:

```kql
traces
| where timestamp > ago(5d) // adjust as needed
| where customDimensions.eventId == 'AL0000I7P'
| project timestamp
, aadTenantId = customDimensions.aadTenantId
, environmentName = customDimensions.environmentName
, environmentType = customDimensions.environmentType
, companyName = customDimensions.companyName
, requestStatusCode = customDimensions.alStatusCode
, functionHost = customDimensions.alFunctionHost
```

[!INCLUDE[telemetry_alert_learn_more](../includes/telemetry-alerting.md)]

<!--
{"component":"Dynamics 365 Business Central Server","environmentType":"Production","eventId":"AL0000I7P","clientType":"WebClient","telemetrySchemaVersion":"1.2","componentVersion":"21.0.44895.0","companyName":"CRONUS International Ltd.","aadTenantId":"common","extensionName":"System Application","extensionId":"63ca2fa4-4f03-4f2b-a480-172fef340d3f","extensionVersion":"21.0.0.0","alObjectName":"System Telemetry Logger","extensionPublisher":"Microsoft","alObjectType":"CodeUnit","alObjectId":"8713","alCallerAppVersion":"1.0.0.0","alCategory":"FeatureTelemetry","alCallerAppVersionMajor":"21","alDataClassification":"SystemMetadata","alIsEvaluationCompany":"No","alCallerPublisher":"Default publisher","alTenantLicenseState":"Evaluation","alClientType":"Web","alCallerAppName":"ALProject2","alCompany":"CRONUS International Ltd.","alCallerAppVersionMinor":"0","alFeatureName":"Connect to Azure Functions","alEventName":"Request sent to Azure function failed: testbcapp.azurewebsites.net","alSubCategory":"Error","alFunctionHost":"testbcapp.azurewebsites.net","alStatusCode":"401","alErrorText":"Request sent to Azure function failed: testbcapp.azurewebsites.net"}

-->

## Authorization failed to Azure function

Occurs when the environment was scheduled to be updated, but it wasn't possible to start the update within the update window defined in the Business Central admin center. For more information about the update window in the admin center, see [Managing Updates in the Business Central Admin Center](tenant-admin-center-update-management.md).

### General dimensions

|Dimension|Description or value|
|---------|-----|
|message|**Authorization failed to Azure function: {alFunctionHost}**|

### Custom dimensions

|Dimension|Description or value|
|---------|-----|
|eventId|**AL0000I75**|
|alErrorText|The reason for the failure.|

### Sample KQL code
This KQL code can help you get started analyzing and alerting on failures to authorize to Azure functions:

```kql
traces
| where timestamp > ago(5d) // adjust as needed
| where customDimensions.eventId == 'AL0000I75'
| project timestamp
, aadTenantId = customDimensions.aadTenantId
, environmentName = customDimensions.environmentName
, environmentType = customDimensions.environmentType
, companyName = customDimensions.companyName
, errorText = customDimensions.alErrorText
, functionHost = customDimensions.alFunctionHost
```

[!INCLUDE[telemetry_alert_learn_more](../includes/telemetry-alerting.md)]

<!--
 {"component":"Dynamics 365 Business Central Server","environmentType":"Production","eventId":"AL0000I75","clientType":"WebClient","telemetrySchemaVersion":"1.2","componentVersion":"21.0.44895.0","companyName":"CRONUS International Ltd.","aadTenantId":"common","extensionName":"System Application","extensionId":"63ca2fa4-4f03-4f2b-a480-172fef340d3f","extensionVersion":"21.0.0.0","alObjectName":"System Telemetry Logger","extensionPublisher":"Microsoft","alObjectType":"CodeUnit","alObjectId":"8713","alCallerAppVersion":"1.0.0.0","alCategory":"FeatureTelemetry","alCallerAppVersionMajor":"21","alDataClassification":"SystemMetadata","alIsEvaluationCompany":"No","alCallerPublisher":"Default publisher","alTenantLicenseState":"Evaluation","alClientType":"Web","alCallerAppName":"ALProject2","alCompany":"CRONUS International Ltd.","alCallerAppVersionMinor":"0","alFeatureName":"Connect to Azure Functions","alEventName":"Acquiring token","alSubCategory":"Error","alFunctionHost":"testbcapp.azurewebsites.net","alErrorText":"Authorization failed to Azure function: testbcapp.azurewebsites.net"}

-->

## See also

[Monitoring and Analyzing Telemetry](telemetry-overview.md)  
[Enable Sending Telemetry to Application Insights](telemetry-enable-application-insights.md)  
[Alert on Telemetry](telemetry-alert.md)  
[Connecting to Azure Functions](https://github.com/microsoft/BCApps/tree/main/src/System%20Application/App/Azure%20Function)  
[Overview of the Application](../developer/devenv-application-overview.md)  
