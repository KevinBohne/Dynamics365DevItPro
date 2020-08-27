---
title: Custom Integration with Common Data Service
description: Learn how to integrate your extension with Common Data Service.
author: bholtorf

ms.custom: na
ms.reviewer: solsen
ms.topic: article
ms.service: "dynamics365-business-central"
ms.author: bholtorf
ms.date: 04/01/2020
---

# Customizing an Integration with Common Data Service

This walkthrough describes how to customize an integration between [!INCLUDE[prodshort](../includes/prodshort.md)] and [!INCLUDE[cds_long_md](../includes/cds_long_md.md)]. The walkthrough will guide you through setting up an integration between an employee in [!INCLUDE[prodshort](../includes/prodshort.md)] and a worker in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)]. 

## About this walkthrough

This walkthrough describes how to integrate new and existing extensions with [!INCLUDE[cds_long_md](../includes/cds_long_md.md)]. At a high-level, those process involve the following tasks:  

1. Develop an AL extension to integrate entities in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] and [!INCLUDE[prodshort](../includes/prodshort.md)]. For more information, see [Developing Extensions in AL](../developer/devenv-dev-overview.md).
2. Create an integration table object in [!INCLUDE[prodshort](../includes/prodshort.md)] for mapping a [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] entity to a [!INCLUDE[prodshort](../includes/prodshort.md)] record type.  
3. Use a [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] integration table as the data source for a page in [!INCLUDE[prodshort](../includes/prodshort.md)] that displays data from [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] entity records.  
4. Extend a page in [!INCLUDE[prodshort](../includes/prodshort.md)] for coupling and synchronizing entity records in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] with table records in [!INCLUDE[prodshort](../includes/prodshort.md)].  
5. Use events to create an integration table and a field mapping between a table in [!INCLUDE[prodshort](../includes/prodshort.md)] table and an integration table for [!INCLUDE[cds_long_md](../includes/cds_long_md.md)].  
6. Develop another AL extension to extend an existing integration between entities in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] and [!INCLUDE[prodshort](../includes/prodshort.md)]. 
7. Create a table extension for an existing integration table object.
8. Use events to add custom integration field mappings for existing integration table mappings.

> [!NOTE]  
> The customization in this walkthrough is done entirely in [!INCLUDE[prodshort](../includes/prodshort.md)] online, and does not describe how to modify your [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] solution, such as adding or modify entities and forms.  

## Prerequisites

This walkthrough requires the following:  

- [!INCLUDE[cds_long_md](../includes/cds_long_md.md)], including the following:  
    - Worker entity.

    > [!NOTE]  
    > The worker entity is part of Talent Core HR solution and it must be installed. For more information, see [Common Data Service entities](https://docs.microsoft.com/dynamics365/talent/corehrentities#worker-entities).
    - The URL of your Common Data Service environment.
    - The user name and password of a user account that has full permissions to add and modify entities.  
- [!INCLUDE[prodshort](../includes/prodshort.md)], including the following:  
    - The CRONUS International Ltd. demonstration data.  <!--need to tell them where they can get the data -->
    - Integration with [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] is enabled, including the default synchronization setup and a working connection between [!INCLUDE[prodshort](../includes/prodshort.md)] and [!INCLUDE[cds_long_md](../includes/cds_long_md.md)]. <!--For more information, see []()....  -->
    - Visual Studio Code with the AL Language extension installed. For more information, see [Getting Started with AL](../developer/devenv-get-started.md) and [AL Language Extension Configuration](../developer/devenv-al-extension-configuration.md). The AL Language extension for Visual Studio is free, and you can download it from [Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-dynamics-smb.al).

    > [!NOTE]  
    > Make sure that your integration user has permission to access the Worker entity.

## Create an integration table in [!INCLUDE[prodshort](../includes/prodshort.md)] for the [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] entity  

To integrate data from a Common Data Service entity into [!INCLUDE[prodshort](../includes/prodshort.md)], you must create a table object in [!INCLUDE[prodshort](../includes/prodshort.md)] that is based on the [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] entity, and then import the new table into the [!INCLUDE[prodshort](../includes/prodshort.md)] database. For this walkthrough we will create a table object that describes the schema for the **Worker** entity in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] in the [!INCLUDE[prodshort](../includes/prodshort.md)] database. 

> [!NOTE]  
> The table can contain some or all of the fields from the Common Data Service entity. However, if you want to set up bi-directional synchronization you must include all fields in the table.  

### To create the integration table for the worker entity in Business Central 

1. Create a new AL extension. For more information, see [Developing Extensions in AL](../developer/devenv-dev-overview.md).
2. Export the **AL Table Proxy Generator** tool called **altpgen.exe** from the Visual Studio Code AL extension. This executable tool allows you to create integration tables. When you have installed the AL Language extension, go to the equivalent of this folder: `C:\Users\<myname>\.vscode\extensions\microsoft.al-4.0.209721\bin` and find the `altpgen.exe` file. For more information, see [AL Table Proxy Generator](../developer/devenv-al-table-proxy-generator.md).
3. In PowerShell, run the tool with the following arguments:
    ```
    -project:<Your AL project folder>
    -packagecachepath:<Your AL project cache folder>
    -serviceuri:<Common Data Service server URL>
    -entities:cds_worker
    -baseid:50000
    ```
    
    This starts the process for creating the table. When completed, the output path contains the `.al` file that contains the description of the **CDS Worker** integration table with ID 50000. This table is set to the table type **CDS**.

## Create a page for displaying [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] data  

For scenarios where we want to view [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] data for a specific entity, we can create a page object that uses the integration table for the [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] entity as its data source. For example, we might want to have a list page that displays the current records in a [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] entity, such as all workers. In this walkthrough we will create a list page that uses the generated integration table **CDS Worker** with ID 50000 as its data source.  

### To create a list page to display [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] workers  

1. Create a new page. For more information, see [Pages Overview](../developer/devenv-pages-overview.md). 
2. Name the page **CDS Worker List**, and specify **50001** as the page ID.  
3. Specify the **CDS Worker** integration table as the source table as shown below:

```
page 50001 "CDS Worker List"
{
    PageType = List;
    SourceTable = "CDS Worker";
    Editable = false;
    ApplicationArea = All;
    UsageCategory = Lists;
    ...
    
    layout
    {
        // add fields to display on the page
    }

    actions
    {
        area(processing)
        {
            action(CreateFromCDS)
            {
                ApplicationArea = All;
                Caption = 'Create in Business Central';
                Promoted = true;
                PromotedCategory = Process;
                ToolTip = 'Generate the entity from the coupled Common Data Service worker.';

                trigger OnAction()
                var
                    CDSWorker: Record "CDS Worker";
                    CRMIntegrationManagement: Codeunit "CRM Integration Management";
                begin
                    CurrPage.SetSelectionFilter(CDSWorker);
                    CRMIntegrationManagement.CreateNewRecordsFromCRM(CDSWorker);
                end;
            }
        }
    }

    var
        CurrentlyCoupledCDSWorker: Record "CDS Worker";

    trigger OnInit()
    begin
        Codeunit.Run(Codeunit::"CRM Integration Management");
    end;

    procedure SetCurrentlyCoupledCDSWorker(CDSWorker: Record "CDS Worker")
    begin
        CurrentlyCoupledCDSWorker := CDSWorker;
    end;
}
``` 

4. Add the fields from the integration table to display on the page in the `layout` section. 


## Enable coupling and synchronization between Worker in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] and in [!INCLUDE[prodshort](../includes/prodshort.md)]

To connect a [!INCLUDE[prodshort](../includes/prodshort.md)] table record with a [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] entity record, you create a coupling. A coupling consists of the primary ID, which is typically a GUID, from a [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] record and the integration ID, also often a GUID, from [!INCLUDE[prodshort](../includes/prodshort.md)].  

<!-- Shouldn't step 0 be: Create a codeunit to manage this?-->

1. Create a new codeunit.
2. In codeunit **CRM Setup Defaults** (ID 5334), subscribe to the **OnGetCDSTableNo** event, as follows:

```
[EventSubscriber(ObjectType::Codeunit, Codeunit::"CRM Setup Defaults", 'OnGetCDSTableNo', '', false, false)]
local procedure HandleOnGetCDSTableNo(BCTableNo: Integer; var CDSTableNo: Integer; var handled: Boolean)
begin
    if BCTableNo = DATABASE::Employee then begin
        CDSTableNo := DATABASE::"CDS Worker";
        handled := true;
    end;
end;
```

3. Now we must enable integration records for the table in [!INCLUDE[prodshort](../includes/prodshort.md)] that will be used for integration with [!INCLUDE[cds_long_md](../includes/cds_long_md.md)]. In this case, that is table **Employee** (ID 5200). The following code examples are two subscribers to the **OnIsIntegrationRecord** and **OnAfterAddToIntegrationPageList** events in codeunit **Integration Management** (ID 5150) that we can use to enable integration records for the **Employee** table.

```
[EventSubscriber(ObjectType::Codeunit, Codeunit::"Integration Management", 'OnIsIntegrationRecord', '', true, true)]
local procedure HandleOnIsIntegrationRecord(TableID: Integer; var isIntegrationRecord: Boolean)
begin
    if TableID = DATABASE::Employee then
        isIntegrationRecord := true;
end;
```
```
[EventSubscriber(ObjectType::Codeunit, Codeunit::"Integration Management", 'OnAfterAddToIntegrationPageList', '', true, true)]
local procedure HandleOnAfterAddToIntegrationPageList(var TempNameValueBuffer: Record "Name/Value Buffer"; var NextId: Integer)
begin
    TempNameValueBuffer.Init();
    TempNameValueBuffer.ID := NextId;
    NextId := NextId + 1;
    TempNameValueBuffer.Name := Format(Page::"Employee Card");
    TempNameValueBuffer.Value := Format(Database::"Employee");
    TempNameValueBuffer.Insert();
end;
```

When changes occur in the **Employee** table, an integration record will be created or updated with a timestamp. You can now use the table to create a page for coupling [!INCLUDE[prodshort](../includes/prodshort.md)] records with Common Data Service records.

4. In codeunit **Lookup CRM Tables** (ID 5332), subscribe to the **OnLookupCRMTables** event, as follows:

```
[EventSubscriber(ObjectType::Codeunit, Codeunit::"Lookup CRM Tables", 'OnLookupCRMTables', '', true, true)]
local procedure HandleOnLookupCRMTables(CRMTableID: Integer; NAVTableId: Integer; SavedCRMId: Guid; var CRMId: Guid; IntTableFilter: Text; var Handled: Boolean)
begin
    if CRMTableID = Database::"CDS Worker" then
        Handled := LookupCDSWorker(SavedCRMId, CRMId, IntTableFilter);
end;

local procedure LookupCDSWorker(SavedCRMId: Guid; var CRMId: Guid; IntTableFilter: Text): Boolean
var
    CDSWorker: Record "CDS Worker";
    OriginalCDSWorker: Record "CDS Worker";
    CDSWorkerList: Page "CDS Worker List";
begin
    if not IsNullGuid(CRMId) then begin
        if CDSWorker.Get(CRMId) then
            CDSWorkerList.SetRecord(CDSWorker);
        if not IsNullGuid(SavedCRMId) then
            if OriginalCDSWorker.Get(SavedCRMId) then
                CDSWorkerList.SetCurrentlyCoupledCDSWorker(OriginalCDSWorker);
    end;

    CDSWorker.SetView(IntTableFilter);
    CDSWorkerList.SetTableView(CDSWorker);
    CDSWorkerList.LookupMode(true);
    if CDSWorkerList.RunModal = ACTION::LookupOK then begin
        CDSWorkerList.GetRecord(CDSWorker);
        CRMId := CDSWorker.WorkerId;
        exit(true);
    end;
    exit(false);
end;
```

### To create actions on the employee page for managing coupling and synchronization

To enable users to create couplings between records in the two systems, we will extend the **Employee Card** page with actions for creating and deleting couplings, and for synchronizing. The following code example adds those actions to **Employee Card**.

```
pageextension 50101 "Employee Synch Extension" extends "Employee Card"
{
    actions
    {
        addlast(navigation)
        {
            group(ActionGroupCDS)
            {
                Caption = 'CDS';
                Visible = CDSIntegrationEnabled;

                action(CDSSynchronizeNow)
                {
                    Caption = 'Synchronize';
                    ApplicationArea = All;
                    Visible = true;
                    Image = Refresh;
                    Enabled = CDSIsCoupledToRecord;
                    ToolTip = 'Send or get updated data to or from Common Data Service.';

                    trigger OnAction()
                    var
                        CRMIntegrationManagement: Codeunit "CRM Integration Management";
                    begin
                        CRMIntegrationManagement.UpdateOneNow(RecordId);
                    end;
                }
                action(ShowLog)
                {
                    Caption = 'Synchronization Log';
                    ApplicationArea = All;
                    Visible = true;
                    Image = Log;
                    ToolTip = 'View integration synchronization jobs for the customer table.';

                    trigger OnAction()
                    var
                        CRMIntegrationManagement: Codeunit "CRM Integration Management";
                    begin
                        CRMIntegrationManagement.ShowLog(RecordId);
                    end;
                }
                group(Coupling)
                {
                    Caption = 'Coupling';
                    Image = LinkAccount;
                    ToolTip = 'Create, change, or delete a coupling between the Business Central record and a Common Data Service record.';

                    action(ManageCDSCoupling)
                    {
                        Caption = 'Set Up Coupling';
                        ApplicationArea = All;
                        Visible = true;
                        Image = LinkAccount;
                        ToolTip = 'Create or modify the coupling to a Common Data Service Worker.';

                        trigger OnAction()
                        var
                            CRMIntegrationManagement: Codeunit "CRM Integration Management";
                        begin
                            CRMIntegrationManagement.DefineCoupling(RecordId);
                        end;
                    }
                    action(DeleteCDSCoupling)
                    {
                        Caption = 'Delete Coupling';
                        ApplicationArea = All;
                        Visible = true;
                        Image = UnLinkAccount;
                        Enabled = CDSIsCoupledToRecord;
                        ToolTip = 'Delete the coupling to a Common Data Service Worker.';

                        trigger OnAction()
                        var
                            CRMCouplingManagement: Codeunit "CRM Coupling Management";
                        begin
                            CRMCouplingManagement.RemoveCoupling(RecordId);
                        end;
                    }
                }
            }
        }
    }

    trigger OnOpenPage()
    begin
        CDSIntegrationEnabled := CRMIntegrationManagement.IsCDSIntegrationEnabled();
    end;

    trigger OnAfterGetCurrRecord()
    begin
        if CDSIntegrationEnabled then
            CDSIsCoupledToRecord := CRMCouplingManagement.IsRecordCoupledToCRM(RecordId);
    end;

    var
        CRMIntegrationManagement: Codeunit "CRM Integration Management";
        CRMCouplingManagement: Codeunit "CRM Coupling Management";
        CDSIntegrationEnabled: Boolean;
        CDSIsCoupledToRecord: Boolean;

}
```

## Create default integration table mappings and field mappings

For synchronization to work, mappings must exist to associate the table ID and fields of the integration table (in this case, **CDS Worker**) with the table in [!INCLUDE[prodshort](../includes/prodshort.md)] (in this case table **Employee**). There are two types of mapping:  

- **Integration table mapping** - Integration table mapping links the [!INCLUDE[prodshort](../includes/prodshort.md)] table to the integration table for the [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] entity.  
- **Integration field mapping** - Field mapping links a field in an entity record in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] with a field in a record in [!INCLUDE[prodshort](../includes/prodshort.md)]. This determines which field in [!INCLUDE[prodshort](../includes/prodshort.md)] corresponds to which field in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)]. Typically, there are multiple field mappings for an entity.  

In this scenario, we will create integration table and field mappings so that we can synchronize data for a worker in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] with an employee in [!INCLUDE[prodshort](../includes/prodshort.md)]. 

### To create an integration table mapping  

We can create the integration table mapping by subscribing to the **OnAfterResetConfiguration** event in codeunit **CDS Setup Defaults** (ID 7204).

1. Create a codeunit.  
2. Add a local procedure called **InsertIntegrationTableMapping**, as follows:

    ```
    local procedure InsertIntegrationTableMapping(var IntegrationTableMapping: Record "Integration Table Mapping"; MappingName: Code[20]; TableNo: Integer; IntegrationTableNo: Integer; IntegrationTableUIDFieldNo: Integer; IntegrationTableModifiedFieldNo: Integer; TableConfigTemplateCode: Code[10]; IntegrationTableConfigTemplateCode: Code[10]; SynchOnlyCoupledRecords: Boolean)
    begin
        IntegrationTableMapping.CreateRecord(MappingName, TableNo, IntegrationTableNo,  IntegrationTableUIDFieldNo, IntegrationTableModifiedFieldNo, TableConfigTemplateCode, IntegrationTableConfigTemplateCode, SynchOnlyCoupledRecords, IntegrationTableMapping.Direction::Bidirectional, 'CDS');
    end;
    ```

3. In codeunit **CDS Setup Defaults**, subscribe to the **OnAfterResetConfiguration** event, as follows:

    ```
    [EventSubscriber(ObjectType::Codeunit, Codeunit::"CDS Setup Defaults", 'OnAfterResetConfiguration', '', true, true)]
    local procedure HandleOnAfterResetConfiguration(CDSConnectionSetup: Record "CDS Connection Setup")
    var
        IntegrationTableMapping: Record "Integration Table Mapping";
        IntegrationFieldMapping: Record "Integration Field Mapping";
        CDSWorker: Record "CDS Worker";
        Employee: Record Employee;
    begin
        InsertIntegrationTableMapping(
            IntegrationTableMapping, 'EMPLOYEE-WORKER',
            DATABASE::Employee, DATABASE::"CDS Worker",
            CDSWorker.FieldNo(cdm_workerId), CDSWorker.FieldNo(ModifiedOn),
            '', '', true);

        ...
    end;
    ``` 

   For each integration table mapping entry, there must be integration field mapping entries to map the fields of the records in the table and the integration table. The next step is to add integration field mappings for each field in the **Employee** table in [!INCLUDE[prodshort](../includes/prodshort.md)] that we want to map to the **Worker** entity in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)].  

### To create integration fields mappings  

To create an integration field mapping, follow these steps:  

1. Add a local procedure called **InsertIntegrationFieldMapping** to the codeunit that you created in step 1 of the previous process, as follows:

    ```
    procedure InsertIntegrationFieldMapping(IntegrationTableMappingName: Code[20]; TableFieldNo: Integer; IntegrationTableFieldNo: Integer; SynchDirection: Option; ConstValue: Text; ValidateField: Boolean; ValidateIntegrationTableField: Boolean)
    var
        IntegrationFieldMapping: Record "Integration Field Mapping";
    begin
        IntegrationFieldMapping.CreateRecord(IntegrationTableMappingName, TableFieldNo, IntegrationTableFieldNo, SynchDirection,
            ConstValue, ValidateField, ValidateIntegrationTableField);
    end;
    ```

2. In the event subscriber that we created for our integration table mapping (in step 3 in the previous process), after we insert the integration table mapping we will add field mappings, as follows:

    ```
    InsertIntegrationFieldMapping('EMPLOYEE-WORKER', Employee.FieldNo("First Name"), CDSWorker.FieldNo(cdm_FirstName), IntegrationFieldMapping.Direction::Bidirectional, '', true, false);
    ```      

3. Now repeat these steps for each field that we want to map.  

    > [!TIP]  
    > If a field in one of the tables does not have a corresponding field in the other table, we can use a constant value.

3. After publishing the extension, we can update the default mappings to include our new integration table mapping by opening the **CDS Connection Setup** page in [!INCLUDE[prodshort](../includes/prodshort.md)] and choosing **Use Default Synchronization Setup**.  

Users can now manually synchronize employee records in [!INCLUDE[prodshort](../includes/prodshort.md)] with Worker entity records in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] from the [!INCLUDE[prodshort](../includes/prodshort.md)] client.  

> [!TIP]  
> To learn how to schedule the synchronization by using a job queue entry, examine the code on the **RecreateJobQueueEntry** function in codeunit **CRM Integration Management** (ID 5330) and see how it is called by the integration code for other [!INCLUDE[cds_long_md](../includes/cds_long_md.md)] entities in the codeunit. For more information, see [Scheduling a Synchronization](/dynamics365/business-central/admin-scheduled-synchronization-using-the-synchronization-job-queue-entries).

### Enable customers to reset selected integration table mappings to the default settings
Customers might make changes to the integration table mappings that they later regret. To enable them to reset selected custom integration table mappings to the default, rather than all custom table mappings, follow these steps:

1. In the same codeunit created for this section, add an event subscriber to **OnBeforeHandleCustomIntegrationTableMapping** and point to the default behaviour of the integration defined above, as follows:

    ```
    [EventSubscriber(ObjectType::Codeunit, Codeunit::"CRM Integration Management", 'OnBeforeHandleCustomIntegrationTableMapping', '', false, false)]
    local procedure HandleCustomIntegrationTableMappingReset(var IsHandled: Boolean; IntegrationTableMappingName: Code[20])
    var
        IntegrationTableMapping: Record "Integration Table Mapping";
    begin
        case IntegrationTableMappingName of
            'EMPLOYEE-WORKER':
                begin
                    InsertIntegrationTableMapping(
                        IntegrationTableMapping, 'EMPLOYEE-WORKER',
                        DATABASE::Employee, DATABASE::"CDS Worker", C
                        DSWorker.FieldNo(cdm_workerId), CDSWorker.FieldNo(ModifiedOn),
                        '', '', true);
                    InsertIntegrationFieldMapping('EMPLOYEE-WORKER',
                        Employee.FieldNo("First Name"), CDSWorker.FieldNo(cdm_FirstName),
                        IntegrationFieldMapping.Direction::Bidirectional, '', true, false);
                    ...
                    IsHandled := true;
                end;
                ...
        end;
    end;
    ```
> [!Important]  
> You must set the the IsHandled property to true to avoid triggering the default implementation. Otherwise, the default implementation will reset all custom table mappings to the default, regardless of the user's selection.

## Customizing Synchronization  

When synchronizing data, some entities may require custom code to successfully synchronize data. Other entities might require the initialization of fields, the validation of relationships, or the transformation of data.  

You can either use the standard transformation rules on page **Integration Field Mapping List** (ID 5361) or you can transform data programmatically. For more information, see [Transformation Rules](/dynamics365/business-central/across-how-to-set-up-data-exchange-definitions#transformation-rules).

During the synchronization process, certain events are published and raised by codeunit **Integration Table Synch.** (ID 5335). We can add code that subscribes to these events so that we can add custom logic at different stages of the synchronization process. The following table describes the events that are published by codeunit **Integration Table Synch.**.  

|Event|Description|  
|-----|-----------|  
|**OnFindUnCoupledDestinationRecord**|Occurs when the process tries to synchronize an uncoupled record (new record). Use this event to implement custom resolution algorithms for automatic mapping between records. For example, use this event to automatically map records by fields. For an example, see codeunit **CRM Int. Table. Subscriber**, which includes the event subscriber function **CRMTransactionCurrencyFindUncoupledDestinationRecord**. The event resolves [!INCLUDE[prodshort](../includes/prodshort.md)] currency codes with ISO currency codes in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)].|  
|**OnBeforeApplyRecordTemplate**|Occurs before applying configuration templates to new records, and can be used to implement algorithms for determining which configuration template to use.<!--point to section about templates.-->|  
|**OnAfterApplyRecordTemplate**|Occurs after configuration templates are applied to new records, and can be used to change data after configuration templates have been applied.|  
|**OnBeforeTransferRecordFields**|Occurs before transferring data in modified fields (which are defined in the **Integration Field Mapping** table) from the source table to the destination table. It can be used to validate the source or destination before the data is moved.|  
|**OnAfterTransferRecordFields**|Occurs after transferring modified field data (which are defined in the Integration Field Mapping table) from the source table to the destination table. It can be used to transfer additional data, validate lookups, and so on. Setting the **AdditionalFieldsWereModified** parameter will cause a destination record modification even though no fields were modified.|  
|**OnBeforeInsertRecord**|Occurs before inserting a new destination record, and can be used to initialize fields, such as primary keys.|  
|**OnAfterInsertRecord**|Occurs after a new destination record is inserted, and can be used to perform post-insert operations such as updating related data.|  
|**OnBeforeModifyRecord**|Occurs before modifying an existing destination record, and can be used to validate or change data before modification.|  
|**OnAfterModifyRecord**|Occurs after an existing destination record is modified, and can be used to perform post-modify operations such as updating related data.|  
|**OnTransferFieldData**|Occurs before an existing destination field value is transferred to a source field, and can be used to perform specific transformations of data when the data types of the source and the destination field are different but can be mapped.|  

For more information about how to subscribe to events, see [Subscribing to Events](../developer/devenv-subscribing-to-events.md).

> [!TIP]  
> In order to have Company ID mapping for custom entities just like the base CDS entities , users can subscribe to the **OnBeforeInsertRecord** event in codeunit **Integration Rec. Synch. Invoke** (ID 5345), as follows:
> ```
>   [EventSubscriber(ObjectType::Codeunit, Codeunit::"Integration Rec. Synch. Invoke", 'OnBeforeInsertRecord', '', false, false)]
>   local procedure HandleOnBeforeInsertRecord(SourceRecordRef: RecordRef; DestinationRecordRef: RecordRef)
>   var
>       CDSIntegrationMgt: Codeunit "CDS Integration Mgt.";
>   begin
>   if DestinationRecordRef.Number() = Database::"CDS Worker" then
>       CDSIntegrationMgt.SetCompanyId(DestinationRecordRef);
>   end;
>``` 
For more information on base CDS entities, see [Data Ownership Models](/dynamics365/business-central/admin-cds-company-concept).

## Create a table extension for an integration table in [!INCLUDE[prodshort](../includes/prodshort.md)]

Let us explore another scenario. If we added an **Industry** field to the **Contact** entity in [!INCLUDE[cds_long_md](../includes/cds_long_md.md)], and now want to include the field in our integration with [!INCLUDE[cds_long_md](../includes/cds_long_md.md)].

### To create the integration table extension for table "CRM Contact" (ID 5342)

1. Create a new AL extension.
2. Locate the **AL Table Proxy Generator** tool. See the previous [section](administration-custom-cds-integration.md#to-create-the-integration-table-for-the-worker-entity-in-business-central).
3. In PowerShell, run the tool with the following arguments:

    ```  
    -project:<Your AL project folder>
    -packagecachepath:<Your AL project cache folder>
    -serviceuri:<CDS server URL>
    -entities:contact
    -baseid:60000
    ```

    The process for creating the table starts. The AL Table Proxy Generator tool finds that an integration table for the **Contact** entity already exists, so it creates a table extension with only new fields; in this case **Industry**. When the process is completed, the output path contains the `WorkerExt.al` file.

## Extend the contact table and page with the Industry field

To synchronize the **Industry** field we need to add the field in [!INCLUDE[prodshort](../includes/prodshort.md)]. The following code example extends table **Contact** and page **Contact Card** with new the field. For example:

```
tableextension 60001 ContactExtension extends Contact
{
    fields
    {
        field(70116; "Industry"; Text[100])
        {
        }
    }
}

pageextension 60001 ContactCardExtension extends "Contact Card"
{
    layout
    {
        addlast(General)
        {
            field("Industry"; "Industry")
            {
                ApplicationArea = All;
                Caption = 'Industry';
            }
        }
    }
}
```

## Add new integration field mapping for Industry

Now that we have the field in both [!INCLUDE[prodshort](../includes/prodshort.md)] and [!INCLUDE[cds_long_md](../includes/cds_long_md.md)], we can add a new integration field mapping for it. To do that we will subscribe to the **OnAfterResetContactContactMapping** event in codeunit **CDS Setup Defaults** (ID 7204), as follows:

```
[EventSubscriber(ObjectType::Codeunit, Codeunit::"CDS Setup Defaults", 'OnAfterResetContactContactMapping', '', true, true)]
local procedure HandleOnAfterResetContactContactMapping(IntegrationTableMappingName: Code[20])
var
    CDSContact: Record "CRM Contact";
    Contact: Record Contact;
    IntegrationFieldMapping: Record "Integration Field Mapping";
begin
    InsertIntegrationFieldMapping(
        IntegrationTableMappingName,
        Contact.FieldNo("Industry"),
        CDSContact.FieldNo(cr07b_Industry),
        IntegrationFieldMapping.Direction::Bidirectional,
        '', true, false);
end;
```

After we publish the extension we can update the mappings by running the **CDS Connection Setup** page and choosing **Use Default Synchronization Setup**.  

## See Also

[Overview](/dynamics365/business-central/admin-common-data-service)  
[Setting Up User Accounts for Integrating with Common Data Service](/dynamics365/business-central/admin-setting-up-integration-with-dynamics-sales)  
[Set Up a Connection to Common Data Service](/dynamics365/business-central/admin-how-to-set-up-a-dynamics-crm-connection) 
[Synchronizing Business Central and Common Data Service](/dynamics365/business-central/admin-synchronizing-business-central-and-sales)  
[Mapping the Tables and Fields to Synchronize](/dynamics365/business-central/admin-how-to-modify-table-mappings-for-synchronization)  
[Manually Synchronize Table Mappings](/dynamics365/business-central/admin-manual-synchronization-of-table-mappings)  
[Schedule a Synchronization](/dynamics365/business-central/admin-scheduled-synchronization-using-the-synchronization-job-queue-entries)  

