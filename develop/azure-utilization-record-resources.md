---
title: Azure utilization record resources
description: The Azure utilization record contains details about the utilization of an Azure subscription resource.
ms.assetid: 4C1EEEB3-DB25-4D61-BFED-C4AB5D3BB5CF
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 8874ce3a9dd3c6f8b0745baafd0f6a09fdbeb842
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489132"
---
# <a name="azure-utilization-record-resources"></a>Azure utilization record resources

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

The Azure utilization record contains details about the utilization of an Azure subscription resource. If you are a cloud service provider partner who owns the billing relationship for your customers' Azure subscriptions, you can use this REST API to provide a scalable way to track usage incurred on the subscriptions in order to send an invoice to your customers at the end of every billing cycle.

To track usage and help predict your monthly bill and the bills for individual customers, you can combine a Rate Card query to [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md) with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).

Prices differ by market and currency, and this API takes location into consideration. By default, it uses your partner profile settings in Partner Center and your browser language, but those are customizable. This is especially relevant if you manage sales in multiple markets from a single, centralized office.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Describes the properties of an Azure utilization record resource.

| プロパティ       | タスクバーの検索ボックスに                                      | 必須かどうか | 説明                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | string                                    | [はい]      | The start of the usage aggregation time range. The response is grouped by the time of consumption (when the resource was actually used vs. when was it reported to the billing system). |
| usageEndTime   | string                                    | [はい]      | The end of the usage aggregation time range. The response is grouped by the time of consumption (when the resource was actually used vs. when was it reported to the billing system).   |
| resource       | オブジェクト                                    | [はい]      | Contains an [AzureResource](#azureresource) object.                                                                                                                                     |
| quantity       | number                                    | [はい]      | The quantity consumed of the [AzureResource.](#azureresource)                                                                                                                           |
| ユニット           | string                                    | 必須ではない       | The type of quantity (hours, bytes, etc.) This property is optional                                                                                                                     |
| infoFields     | オブジェクト                                    | [はい]      | Key-value pairs of instance level details. This object may be empty.                                                                                                                    |
| instanceData   | オブジェクト                                    | 必須ではない       | Contains an [AzureInstanceData](#azureinstancedata) object that contains key-value pairs of instance level details. This property is optional and may not be included.                  |
| 属性     | [ResourceAttributes](utility-resources.md#resourceattributes) | [はい]      | The metadata attributes. Contains "objectType": "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Operations on the AzureUtilizationRecord resource

- [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Describes the properties of an Azure Resource.

| プロパティ    | タスクバーの検索ボックスに   | 必須かどうか | 説明                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | string | [はい]      | Unique identifier of the Azure resource. Also known as resourceID or resource GUID. |
| 名前        | string | 必須ではない       | Friendly name of the resource being consumed. このプロパティは省略可能です。            |
| category    | string | 必須ではない       | The category of the consumed resource. このプロパティは省略可能です。                   |
| subcategory | string | 必須ではない       | The sub-category of the consumed resource. このプロパティは省略可能です。               |
| region      | string | 必須ではない       | The region of the consumed resource. このプロパティは省略可能です。                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Describes the properties of an Azure Instance Data resource.

| プロパティ       | タスクバーの検索ボックスに             | 必須かどうか | 説明                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | string           | [はい]      | The fully qualified Azure resource ID, which includes the resource groups and the instance name.                   |
| location       | string           | [はい]      | Region in which the service was run.                                                                               |
| partNumber     | オブジェクト           | [はい]      | Unique namespace used to identify the resource for commercial marketplace 3rd party usage. This may be an empty string. |
| orderNumber    | number           | [はい]      | Unique namespace used to identify the 3rd party order for commercial marketplace. This may be an empty string.          |
| tags           | 文字列の配列 | 必須ではない       | Resource tags specified by the user. This property is optional and may not be included.                            |
| additionalInfo | 文字列の配列 | 必須ではない       | Additional data for an Azure resource. This property is optional and may not be included.                          |