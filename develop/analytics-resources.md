---
title: 分析リソース
description: 使用状況、デプロイ、消費に関するレポートに使用されるデータのパートナーセンターリソース。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: 613f97cf36a3ecb978b7764fbf9fc5065bd74c30
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095415"
---
# <a name="analytics-resources"></a>分析リソース

**適用対象:**

- パートナー センター

ここで定義されているリソースには、使用状況、デプロイ、使用状況に関するレポートに使用されるデータが含まれています。

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

**PartnerLicensesDeploymentInsights**リソースには、ライセンスの展開に関するパートナーレベルの洞察が含まれています。

| プロパティ                  | Type                                                           | 説明                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | number                                                         | 展開されたライセンスの割合。                                                |
| licensesSold              | number                                                         | 販売されたライセンスの数。                                                        |
| processedDateTime         | UTC 日時形式の文字列                                 | データが集計された日付と時刻。                                     |
| serviceName               | string                                                         | サービス名 (例: o365、crm)。                                                  |
| channel                   | string                                                         | サービスのチャネル名 (例: リセラー)。                                    |
| 属性                | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 "ObjectType": "PartnerLicensesDeploymentInsights" が含まれます。 |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

**PartnerLicensesUsageInsights**リソースには、ライセンスの使用状況に関するパートナーレベルの洞察が含まれています。

| プロパティ                     | Type                                                           | 説明                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | number                                                         | 展開されたライセンスの割合。                                           |
| workloadName                 | string                                                         | ワークロード名 (例: exchange)。                                             |
| processedDateTime            | UTC 日時形式の文字列                                 | データが集計された日付と時刻。                                |
| serviceName                  | string                                                         | サービス名 (例: o365、crm)。                                             |
| channel                      | string                                                         | サービスのチャネル名 (例: リセラー)。                               |
| 属性                   | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 "ObjectType": "PartnerLicensesUsageInsights" が含まれます。 |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

**CustomerLicensesDeploymentInsights**リソースには、ライセンスの展開に関する顧客レベルの洞察が含まれています。

| プロパティ          | Type                                                           | 説明                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | number                                                         | 展開されたライセンスの数。                                                     |
| licensesSold      | number                                                         | 販売されたライセンスの数。                                                         |
| deploymentPercent | number                                                         | 配置されたライセンスの調整された割合。                                        |
| customerId        | string                                                         | 顧客 ID。                                                             |
| customerName      | string                                                         | 顧客名。                                                                   |
| productName       | string                                                         | 製品名。                                                                    |
| serviceCode       | string                                                         | ライセンスのサービスコード。                                                     |
| processedDateTime | UTC 日時形式の文字列                                 | データが集計された日付と時刻。                                      |
| serviceName       | string                                                         | サービス名 (例: o365、crm)。                                                   |
| channel           | string                                                         | サービスのチャネル名 (例: リセラー)。                                     |
| 属性        | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 "ObjectType": "CustomerLicensesDeploymentInsights" が含まれます。 |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

**CustomerLicensesUsageInsights**リソースには、ライセンスの使用状況に関する顧客レベルの洞察が含まれています。

| プロパティ          | Type                                                           | 説明                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | string                                                         | ワークロードコード。                                                              |
| workloadName      | number                                                         | ワークロード名 (例: Exchange)。                                              |
| パーセント      | number                                                         | 使用するライセンスの調整された割合。                                       |
| licensesActive    | number                                                         | アクティブ ライセンスの数です。                                                  |
| licensesQualified | number                                                         | 修飾されたライセンスの数。                                               |
| customerId        | string                                                         | 顧客 ID。                                                        |
| customerName      | string                                                         | 顧客名。                                                              |
| productName       | string                                                         | 製品名。                                                               |
| serviceCode       | string                                                         | ライセンスのサービスコード。                                                |
| processedDateTime | UTC 日時形式の文字列                                 | データが集計された日付と時刻。                                 |
| serviceName       | string                                                         | サービス名 (例: o365、crm)。                                              |
| channel           | string                                                         | サービスのチャネル名 (例: リセラー)。                                |
| 属性        | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 "ObjectType": "CustomerLicensesUsageInsights" が含まれます。 |