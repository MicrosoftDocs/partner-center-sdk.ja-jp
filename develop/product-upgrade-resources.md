---
title: 製品のアップグレードに関するリソース
description: Azure プランへのパートナーセンター製品のアップグレードに関連する複数のリソースを使用できます。 これには、ProductUpgradeRequest ProductUpgradesEligibility、Productupgradeesstatus、アップグレード Eslineitem、UpgradeProduct、および ErrorDetails が含まれます。
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3f891c3e7d25dfc6ec47ef861fa79345c32c1f9f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488202"
---
# <a name="product-upgrade-resources"></a>製品のアップグレードに関するリソース

適用対象:

- パートナー センター

Microsoft Azure (0145P) サブスクリプションから Azure プランへのパートナーセンター製品のアップグレードに関する情報については、次のリソースを参照してください。

## <a name="productupgraderequest"></a>Productアップグレード

**Productの**アップグレード要求のリソースには、製品アップグレード要求オブジェクトに関する情報が記載されています。

| プロパティ | 種類 | 説明 |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| 顧客           | string                                       | 顧客を識別する GUID 形式の文字列。 |
| productFamily        | string                                       | アップグレードが要求されている製品ファミリ。 |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

**ProductUpgradesEligibility**リソースは、顧客が製品をアップグレードするための資格に関する情報を提供します。

| プロパティ | 種類 | 説明 |
|----------------------|--------------------------------------------- |----------------------------------------------------------------|
| 顧客           | string                                       | 顧客を識別する GUID 形式の文字列。 |          | productFamily        | string                                       | アップグレードが要求されている製品ファミリ。 |
| IsEligible           | bool                                         | ブール値は、顧客が要求されたアップグレードの条件を満たしているかどうかを示します。 |
| upgradeId            | string                                       | 指定されたファミリの製品のアップグレードが既に配置されている場合のアップグレード ID。 |
| reason               | string                                       | 顧客が製品のアップグレードに適合していない理由。 |
| productFamily        | string                                       | アップグレードが要求されている製品ファミリ。 |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。  

## <a name="productupgradesstatus"></a>Productアップグレード Esstatus

**Productupgrade esstatus**リソースは、製品のアップグレードの状態に関する情報を提供します。

| プロパティ | 種類 | 説明 |
|---------------------|----------------------------------------------------------------|-----------------------------------------------|
| ID                  | string                                                         | アップグレードを識別する GUID 形式の文字列。 |
| productFamily       | string                                                         | アップグレードが要求されている製品ファミリ。
| status              | string                                                         | 製品のアップグレードの状態。
| lineItems           | アップグレード時の[lineitem](#upgradeslineitem)リソースの配列       | 要求本文の一部であった各品目のアップグレードの詳細情報を提供するオブジェクトの配列。
| errorDetails        | [Errordetails](#errordetails)リソース                         | アップグレードが要求された場合のエラーの詳細。
| 属性          | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。 |

## <a name="upgradeslineitem"></a>アップグレード Eslineitem

アップグレード**Eslineitem**リソースは、要求の各品目の製品アップグレードの詳細の状態を示します。

| プロパティ | 種類 | 説明 |
|-----------------|-----------------------------------------------------|--------------------------------------------------------------|
| sourceProduct   | [Upgradeproduct](#upgradeproduct)オブジェクト            | アップグレードされるソース製品の情報。 |
| targetProduct   | [Upgradeproduct](#upgradeproduct)オブジェクト            | ターゲット製品のアップグレード後の情報。 |
| upgradedDate    | UTC 日時形式の文字列                      | サブスクリプションがアップグレードされた日付。 |
| status          | string                                              | 製品のアップグレードの状態。 |
| errorDetails    | [Errordetails](#errordetails)リソース              | アップグレードが要求された場合のエラーの詳細。 |
| 属性      | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。  |

## <a name="upgradeproduct"></a>UpgradeProduct

**Upgradeproduct**リソースは、アップグレードされている製品に関する情報を提供します。

| プロパティ | 種類 |説明 |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| id                   | string                                       | 製品を識別する GUID 形式の文字列。 |
| name                 | string                                       | アップグレードされる製品のフレンドリ名。 |  
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 |

## <a name="errordetails"></a>ErrorDetails

**Errordetails**リソースは、アップグレード処理中のエラーに関する詳細を提供します。

| プロパティ | 種類 | 説明 |
|-------------------------|----------------------------------------------|-------------------------------------------------------------|
| code                    | string                                       | 製品のアップグレードに失敗した場合のエラーコード。 |
| メッセージ                 | string                                       | 製品のアップグレードに失敗した場合のエラーメッセージ。 |
| 属性              | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 |
