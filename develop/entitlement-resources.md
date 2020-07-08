---
title: 権利リソース
description: 権利に関連するリソースについて説明します。
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d9dbba36fb8db8d040bd61d53483c56467987691
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094000"
---
# <a name="entitlement-resources"></a>権利リソース

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

## <a name="entitlement"></a>Entitlement

このリソースは、顧客がカタログから商品を購入した場合に使用する権利を持つ製品を表します。

| プロパティ | Type | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | 権利の原因となった注文参照。 |
| productId | string | 製品の ID。 |
| skuID | string | SKU の ID。 |
| 数量 | INT | 権利の数量 (満たされ/転送される権利を除く)。 |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | 権利の数量の詳細 (各数量の項目と状態の数) の一覧。 |
| entitlementType | string | 権利の種類。 (SDK 1.8 で[EntitlementType](#entitlementtype)から文字列に更新されました)。 |
| entitledArtifacts | IEnumerable<[成果物](#artifact)> | 権利に関連付けられている成果物の一覧。 |
| IncludedEntitlements | IEnumerable<の[権利](#artifact)> | 資格の一覧。カタログから ProductId/SkuId を購入した結果として暗黙的に含まれます。 |
| ExpiryDate | UTC 日時形式の文字列  | 権利の有効期限 (該当する場合)。 |

## <a name="referenceorder"></a>ReferenceOrder

権利の注文参照。

| プロパティ | Type | 説明 |
|----------|------|-------------|
| id | string | 参照される順序の ID。 |
| lineItemId | string | 参照される注文品目の ID。 |
| alternateId | string | 参照される注文品目の代替 ID。 |

## <a name="quantitydetail"></a>QuantityDetail

権利の数量の詳細を表します。

| プロパティ | Type | Description |
|----------|------|-------------|
| 数量 | INT | 項目数。 |
| 状態 | string | 数量の状態。 |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> SDK version 1.9 で非推奨

権利の種類を示す値を持つ[列挙](https://docs.microsoft.com/dotnet/api/system.enum)型。

| 値 | 説明 |
|-------|-------------|
| ソフトウェア | ソフトウェアに関連する権利の種類を示します。 |
| VirtualMachineReservedInstance | Azure Reserved Virtual Machine Instances に関連する権利の種類を示します。 |

## <a name="artifact"></a>アーティファクト

権利に関連付けられている成果物。

| プロパティ | Type | Description |
|----------|------|-------------|
| artifactType | string | 成果物の種類。 (SDK Version 1.8 では[Artifacttype](#artifacttype)から文字列に更新) |
| dynamicAttributes | ディクショナリ&lt;文字列、オブジェクト&gt; | Artifacttype 固有の値を含む動的属性。 たとえば、artifactType = "reservedinstance" の場合、このプロパティには、仮想マシンの予約インスタンスまたは Azure SQL 予約インスタンスを示す "reservationType" = "virtualmachines" または "reservationType" = "sqldatabases" が含まれます。 (SDK v1.0 以降で利用可能) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> SDK version 1.9 で非推奨

権利の成果物の種類を示す値を持つ[列挙](https://docs.microsoft.com/dotnet/api/system.enum)です。

| 値                          | 説明                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | アーティファクトが Azure Reserved Virtual Machine Instances の取得に役立つことを示します。 |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Azure 予約インスタンスに関連付けられている成果物。 [アーティファクト](#artifact)クラスから継承されます。

| プロパティ   | 種類                           | 説明                                        |
|------------|--------------------------------|----------------------------------------------------|
| link       | [リンク](./utility-resources.md#link) | 関連付けられているすべての成果物の詳細を取得するためのリンク。   |
| resourceID | string                         | Azure 予約注文またはリソースの ID。 |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Azure 予約インスタンス成果物リンクの呼び出し時に返されるエンティティを表します。

|   プロパティ   |           種類           |                          説明                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     type     |          string          |                     成果物の種類。                     |
| reservations | IEnumerable<Reservation> | Azure リソースまたは予約注文 id を示します。 |

## <a name="reservation"></a>予約

個々の予約を表します。

| プロパティ          | 種類                           | 説明                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | string                         | 予約の ID。                                         |
| scopeType         | string                         | 仮想マシン予約に関連付けられているスコープの種類。 |
| displayName       | string                         | 予約の表示名。                               |
| appliedScopes     | IEnumerable                    | 予約に関連付けられている適用済みスコープの一覧。 (ScopeType が共有でない場合にのみ使用できます)。 |
| 数量          | INT                            | 予約に含まれる仮想マシンの数。                 |
| expiryDateTime    | UTC 日時形式の文字列 | 予約の有効期限。                                |
| effectiveDateTime | UTC 日時形式の文字列 | 予約の有効日。                             |
| provisioningState | string                         | 予約のプロビジョニングの状態。                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> SDK version 1.9 で非推奨

Azure 予約仮想マシンインスタンスの権利に関連付けられている成果物。 [アーティファクト](#artifact)クラスから継承されます。

| プロパティ   | 種類                              | 説明                                        |
|------------|-----------------------------------|----------------------------------------------------|
| link       | [リンク](utility-resources.md#link) | 関連付けられているすべての成果物の詳細を取得するためのリンク。   |
| resourceID | string                            | Azure 予約注文またはリソースの ID。 |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> SDK version 1.9 で非推奨

Azure 予約仮想マシンインスタンス成果物リンクの呼び出し時に返されるエンティティを表します。

| プロパティ                    | 種類                                                                 | 説明           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| type                        | [ArtifactType](#artifacttype)                                        | 成果物の種類。 |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Azure リソースまたは予約注文 id を示します。 |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> SDK version 1.9 で非推奨

個々の仮想マシン予約を表します。

|     プロパティ      |              種類              |                                                説明                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             string             |                                         予約の ID。                                         |
|     scopeType     |             string             |                     仮想マシン予約に関連付けられているスコープの種類。                     |
|    displayName    |             string             |                                    予約の表示名。                                    |
|   appliedScopes   |      IEnumerable<string>       | 予約に関連付けられている適用済みスコープの一覧。 (ScopeType が共有でない場合にのみ使用できます)。 |
|     数量      |              INT               |                             予約に含まれる仮想マシンの数。                             |
|  expiryDateTime   | UTC 日時形式の文字列 |                                    予約の有効期限。                                     |
| effectiveDateTime | UTC 日時形式の文字列 |                                   予約の有効日。                                   |
| provisioningState |             string             |                                 予約のプロビジョニングの状態。                                 |
