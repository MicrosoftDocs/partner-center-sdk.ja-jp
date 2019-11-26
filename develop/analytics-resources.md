---
title: Analytics resources
description: Partner Center resources for data used to report on usage, deployment, and consumption.
ms.assetid: 1FEB08D6-AD0C-4B01-B7A8-AE05C914912B
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 8098de53c3fc4632d17ef6cdba7fe983d9fffbbe
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489202"
---
# <a name="analytics-resources"></a>Analytics resources

適用対象:

- パートナー センター

The resources defined here contain data used to report on usage, deployment, and consumption.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

The **PartnerLicensesDeploymentInsights** resource contains partner-level insights about license deployment.

| プロパティ                  | タスクバーの検索ボックスに                                                           | 説明                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | number                                                         | The percentage of licenses deployed.                                                |
| licensesSold              | number                                                         | The number of licenses sold.                                                        |
| processedDateTime         | string in UTC date-time format                                 | The date and time when the data was aggregated.                                     |
| serviceName               | string                                                         | The service name (e.g. o365, crm).                                                  |
| channel                   | string                                                         | The channel name of the service (e.g. reseller).                                    |
| 属性                | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

The **PartnerLicensesUsageInsights** resource contains partner-level insights about license usage.

| プロパティ                     | タスクバーの検索ボックスに                                                           | 説明                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | number                                                         | The percentage of licenses deployed.                                           |
| workloadName                 | string                                                         | The workload name (e.g. exchange).                                             |
| processedDateTime            | string in UTC date-time format                                 | The date and time when the data was aggregated.                                |
| serviceName                  | string                                                         | The service name (e.g. o365, crm).                                             |
| channel                      | string                                                         | The channel name of the service (e.g. reseller).                               |
| 属性                   | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

The **CustomerLicensesDeploymentInsights** resource contains customer-level insights about license deployment.

| プロパティ          | タスクバーの検索ボックスに                                                           | 説明                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | number                                                         | The number of licenses deployed.                                                     |
| licensesSold      | number                                                         | The number of licenses sold.                                                         |
| deploymentPercent | number                                                         | The adjusted percentage of licenses deployed.                                        |
| customerId        | string                                                         | The customer identifier.                                                             |
| customerName      | string                                                         | The customer name.                                                                   |
| productName       | string                                                         | The product name.                                                                    |
| serviceCode       | string                                                         | The service code of the license.                                                     |
| processedDateTime | string in UTC date-time format                                 | The date and time when the data was aggregated.                                      |
| serviceName       | string                                                         | The service name (e.g. o365, crm).                                                   |
| channel           | string                                                         | The channel name of the service (e.g. reseller).                                     |
| 属性        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

The **CustomerLicensesUsageInsights** resource contains customer-level insights about license usage.

| プロパティ          | タスクバーの検索ボックスに                                                           | 説明                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | string                                                         | The workload code.                                                              |
| workloadName      | number                                                         | The workload name (e.g. Exchange).                                              |
| usagePercent      | number                                                         | The adjusted percentage of licenses used.                                       |
| licensesActive    | number                                                         | The number of active licenses.                                                  |
| licensesQualified | number                                                         | The number of qualified licenses.                                               |
| customerId        | string                                                         | The customer identifier.                                                        |
| customerName      | string                                                         | The customer name.                                                              |
| productName       | string                                                         | The product name.                                                               |
| serviceCode       | string                                                         | The service code of the license.                                                |
| processedDateTime | string in UTC date-time format                                 | The date and time when the data was aggregated.                                 |
| serviceName       | string                                                         | The service name (e.g. o365, crm).                                              |
| channel           | string                                                         | The channel name of the service (e.g. reseller).                                |
| 属性        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "CustomerLicensesUsageInsights" |