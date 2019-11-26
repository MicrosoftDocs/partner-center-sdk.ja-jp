---
title: Azure rate card resources
description: The Azure Rate Card provides real-time prices for Azure offers.
ms.assetid: A42B4FFA-278E-41FF-B51E-E48C2CA70EEF
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e81debb15c30ba024d897a00075bffe28be3acaf
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489142"
---
# <a name="azure-rate-card-resources"></a>Azure rate card resources

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

The Azure Rate Card provides real-time prices for Azure offers. Azure pricing is quite dynamic and changes frequently. Microsoft publishes updates on Partner Center, but the REST API provides the fastest way for Cloud Solution Provider partners to get current prices.

To track usage and help predict your monthly bill and the bills for individual customers, you can combine a Rate Card query to [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md) with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).

Prices differ by market and currency, and this API takes location into consideration. By default, it uses your partner profile settings in Partner Center and your browser language, but those are customizable. This is especially relevant if you manage sales in multiple markets from a single, centralized office.

## <a name="azureratecard"></a>AzureRateCard

Describes the properties of an Azure Rate Card resource.

| プロパティ      | タスクバーの検索ボックスに                                      | 説明                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | string                                    | The currency in which the rates are provided.                     |
| isTaxIncluded | boolean                                   | All rates are pretax, so this will always be returned as "false". |
| locale        | string                                    | The culture in which the resource information is localized.       |
| meters        | オブジェクトの配列                          | Array of [AzureMeter](#azuremeter) objects.                       |
| offerTerms    | オブジェクトの配列                          | Array of [AzureOfferTerm](#azureofferterm) objects.               |
| 属性    | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Contains "objectType": "AzureRateCard"   |


### <a name="operations-on-the-azureratecard-resource"></a>Operations on the AzureRateCard resource

- [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| プロパティ         | タスクバーの検索ボックスに             | 説明                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | string           | Meter's unique identifier.                                                                    |
| 名前             | string           | Friendly name of the meter.                                                                   |
| rates            | オブジェクト           | Meter rates. The key is the meter quantity (string) and the value is the meter rate (number). |
| tags             | 文字列の配列 | Optional meter tags. This array can be empty.                                                 |
| category         | string           | Category of the resource.                                                                     |
| subcategory      | string           | Sub-category of the resource.                                                                 |
| region           | string           | Region of the id.                                                                             |
| ユニット             | string           | The type of quantity (hours, bytes, etc.)                                                     |
| includedQuantity | number           | Meter quantity that is included free of charge.                                               |
| effectiveDate    | string           | The date this meter is in effect.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| プロパティ         | タスクバーの検索ボックスに             | 説明                             |
|------------------|------------------|-----------------------------------------|
| 名前             | string           | Friendly name of the offer term.        |
| discount         | number           | The discount applied, if any.           |
| excludedMeterIds | 文字列の配列 | Meters excluded from the offer, if any. |
| effectiveDate    | string           | The date the offer is in effect.        |