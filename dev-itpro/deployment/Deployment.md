---
title: Deployment overview for Business Central
description: Get an overview of your options for deploying Dynamics 365 Business Central
author: edupont04
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
ms.author: edupont
ms.date: 10/01/2019
---
# Deployment of [!INCLUDE[prodlong](../developer/includes/prodlong.md)]

The topics in the Deployment section are intended to help an administrator configure a [!INCLUDE[prodshort](../developer/includes/prodshort.md)] solution online or on-premises.  

## Take prospects and customers online

You can give prospects a quick introduction to [!INCLUDE[prodshort](../developer/includes/prodshort.md)] by asking them to get a [free trial](https://go.microsoft.com/fwlink/?linkid=847861), and by showing them the apps in [AppSource](https://appsource.microsoft.com/en-us/marketplace/apps?page=1&product=dynamics-365%3Bdynamics-365-business-central), for example. You can also create [online sandboxes](/dynamics365/business-central/across-how-create-sandbox-environment) and tailor these tenants with demonstration experiences that will attract prospects in your market space. With [!INCLUDE[prodshort](../developer/includes/prodshort.md)] online, data is stored in the Microsoft cloud, removing the need to install SQL Server locally, for example. So for you as a reseller, deployments of [!INCLUDE [prodshort](../developer/includes/prodshort.md)] online are taken care of for you so that you can focus on your prospects and customers.  

### Get set up in the Partner Center

You must enroll in the [Cloud Solution Provider program](https://partner.microsoft.com/en-US/membership/cloud-solution-provider) in order to service [!INCLUDE[prodshort](../developer/includes/prodshort.md)] online. For more information, see [Cloud Solution Provider program - selling in-demand cloud solutions](/partner-center/csp-overview). In the Microsoft Partner Center documentation, you can also learn how to [add a customer](/partner-center/add-a-new-customer), [assign licenses to users](/partner-center/assign-licenses-to-users), and [create new subscriptions](/partner-center/create-a-new-subscription). [!INCLUDE[prodshort](../developer/includes/prodshort.md)] is one of the subscriptions that you can create, and there are [!INCLUDE[prodshort](../developer/includes/prodshort.md)]-specific license types that you can assign to users.  

For more information about reseller readiness for [!INCLUDE[prodshort](../developer/includes/prodshort.md)], see [Build Your Business on Dynamics 365 Business Central](../developer/readiness/readiness-welcome.md).  

### Managing [!INCLUDE [prodshort](../developer/includes/prodshort.md)] online

For more information about administering online tenants, see [Administration of Business Central Online](../administration/tenant-administration.md).  

## When to choose on-premises deployment

There can be many reasons to prefer to deploy [!INCLUDE[prodshort](../developer/includes/prodshort.md)] on-premises rather than using online deployments.  

### Key Features of Setup for On-Premises Deployments  

With [!INCLUDE[prodsetup](../developer/includes/prodsetup.md)], you can:  

- Install different components on different computers.  

- Choose from a selection of predefined installation options, or create your own custom list of components and options to install.  

- Preconfigure components before installation.  

- Create, save, or load Setup configuration files that capture your selection of components and configuration information.  

 You use Setup to install software and to create custom deployments that you can distribute to different users across a company.  

### Installation Notes  

- Before installing [!INCLUDE[prodshort](../developer/includes/prodshort.md)] components on a computer, you must remove \(uninstall\) any previous versions.  

- All components must be from the same version and build of [!INCLUDE[prodshort](../developer/includes/prodshort.md)] for the software to run correctly.  

- If you have either SQL Server 2000 or Microsoft SQL Server Desktop Engine \(MSDE\) installed on a computer where you want to install [!INCLUDE[prodshort](../developer/includes/prodshort.md)], then you must remove it before you begin installing. The presence of either of these database products causes a Setup error.  

### Managing [!INCLUDE [prodshort](../developer/includes/prodshort.md)] on-premises

For more information about administering on-premises deployments, see [Administration of Business Central On-Premises](../administration/Administration.md).  

## Configuring the Help Experience

Part of your configuration is to specify where to look up the Help for the solution. For on-premises deployments, you can choose to install the legacy Help Server, for example. For more information, see [Configuring the Help Experience](configure-help.md).  

## See Also  

[Upgrading to Business Central](../upgrade/upgrading-to-business-central.md)
[Product and Architecture Overview](product-and-architecture-overview.md)  
[System Requirements 2019 release wave 2](system-requirement-business-central-v15.md)  
[System Requirements April '19](system-requirement-business-central.md)  
