---
title: 権利リソース
description: 権利に関連するリソースについて説明します。
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: dc291e4d286e6eeeb1ce4ae6faeb965f59bb1c33
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490092"
---
# <a name="entitlement-resources"></a>権利リソース


**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


## <a name="span-identitlementspan-identitlementspan-identitlemententitlement"></a><span id="Entitlement"/><span id="entitlement"/><span id="ENTITLEMENT"/>権利


このリソースは、顧客がカタログから商品を購入した場合に使用する権利を持つ製品を表します。 

| プロパティ | 種類 | 説明 |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | 資格が得られた注文参照。 |
| productId | string | 製品の ID。 |
| skuID | string | SKU の ID。 |
| quantity | int | 権利の数量 (満たされ/転送される権利を除く)。 |
| quantityDetails | IEnumerable <[QuantityDetail](#quantitydetail)> | 権利の数量の詳細 (各数量の項目と状態の数) の一覧。 |
| entitlementType | string | 権利の種類。 (SDK 1.8 で[EntitlementType](#entitlementtype)から文字列に更新されました)。 |
| entitledArtifacts | IEnumerable <[成果物](#artifact)> | 権利に関連付けられている成果物の一覧。 |
| IncludedEntitlements | IEnumerable < の[権利](#artifact)> | カタログから ProductId/SkuId を購入した結果として暗黙的に含まれる権利の一覧。 |
| ExpiryDate | UTC 日時形式の文字列  | 権利の有効期限 (該当する場合)。 |


## <a name="span-idreferenceorderspan-idreferenceorderspan-idreferenceorderreferenceorder"></a><span id="ReferenceOrder"/><span id="referenceorder"/><span id="REFERENCEORDER"/>ReferenceOrder

権利の注文参照。 

| プロパティ | 種類 | 説明 |
|----------|------|-------------|
| id | string | 参照される順序の ID。 |
| lineItemId | string | 参照される注文品目の ID。 |
| 代替 id | string | 参照される注文品目の代替 ID。 |


## <a name="span-idquantitydetailspan-idquantitydetailspan-idquantitydetailquantitydetail"></a><span id="QuantityDetail"/><span id="quantitydetail"/><span id="QUANTITYDETAIL"/>QuantityDetail

権利の数量の詳細を表します。

| プロパティ | 種類 | 説明 |
|----------|------|-------------|
| quantity | int | 項目の数。 |
| status | string | 数量の状態。 |


## <a name="span-identitlementtypespan-identitlementtypespan-identitlementtypeentitlementtype"></a><span id="EntitlementType"/><span id="entitlementtype"/><span id="ENTITLEMENTTYPE"/>EntitlementType

> [!IMPORTANT]  
> SDK version 1.9 で非推奨

権利の種類を示す値を持つ[列挙](https://docs.microsoft.com/dotnet/api/system.enum)型。

| Value | 説明 |
|-------|-------------|
| ソフトウェア | ソフトウェアに関連する権利の種類を示します。 |
| VirtualMachineReservedInstance | Azure Reserved Virtual Machine Instances に関連する権利の種類を示します。 |


## <a name="span-idartifactspan-idartifactspan-idartifactartifact"></a><span id="Artifact"/><span id="artifact"/><span id="ARTIFACT"/>成果物

権利に関連付けられている成果物。  

| プロパティ | 種類 | 説明 |
|----------|------|-------------|
| ArtifactType | string | 成果物の種類。 (SDK Version 1.8 では[Artifacttype](#artifacttype)から文字列に更新) |
| dynamicAttributes | Dictionary&lt;string、object&gt; | Artifacttype 固有の値を含む動的属性。 たとえば、artifactType = "reservedinstance" の場合、これには "reservationType" = "virtualmachines" または "reservationType" = "sqldatabases" が含まれます。これは、仮想マシンの予約インスタンスまたは Azure SQL の予約済みインスタンスを示します。 (SDK v1.0 以降で利用可能) |


## <a name="span-idartifacttypespan-idartifacttypespan-idartifacttypeartifacttype"></a><span id="ArtifactType"/><span id="artifacttype"/><span id="ARTIFACTTYPE"/>ArtifactType

> [!IMPORTANT]  
> SDK version 1.9 で非推奨

権利の成果物の種類を示す値を持つ[列挙](https://docs.microsoft.com/dotnet/api/system.enum)です。

| Value                          | 説明                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | アーティファクトが Azure Reserved Virtual Machine Instances の取得に役立つことを示します。 |


## <a name="span-idreservedinstanceartifactspan-idreservedinstanceartifactspan-idreservedinstanceartifactreservedinstanceartifact"></a><span id="ReservedInstanceArtifact"/><span id="reservedinstanceartifact"/><span id="RESERVEDINSTANCEARTIFACT"/>ReservedInstanceArtifact

Azure 予約インスタンスに関連付けられている成果物。 [アーティファクト](#artifact)クラスから継承されます。 

| プロパティ   | 種類                           | 説明                                        |
|------------|--------------------------------|----------------------------------------------------|
| リンク       | [Link](./utility-resources.md#link) | 関連付けられているすべての成果物の詳細を取得するためのリンク。   |
| resourceID | string                         | Azure 予約注文またはリソースの ID。 |


## <a name="span-idreservedinstanceartifactdetailsspan-idreservedinstanceartifactdetailsspan-idreservedinstanceartifactdetailsreservedinstanceartifactdetails"></a><span id="ReservedInstanceArtifactDetails"/><span id="reservedinstanceartifactdetails"/><span id="RESERVEDINSTANCEARTIFACTDETAILS"/>ReservedInstanceArtifactDetails

Azure 予約インスタンス成果物リンクの呼び出し時に返されるエンティティを表します。 


|   プロパティ   |           種類           |                          説明                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     type     |          string          |                     成果物の種類。                     |
| 予約 | IEnumerable<Reservation> | Azure リソースまたは予約注文 id を示します。 |

## <a name="span-idreservationspan-idreservationspan-idreservationreservation"></a><span id="Reservation"/><span id="reservation"/><span id="RESERVATION"/>予約

個々の予約を表します。

| プロパティ          | 種類                           | 説明                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | string                         | 予約の ID。                                         |
| scopeType         | string                         | 仮想マシン予約に関連付けられているスコープの種類。 |
| displayName       | string                         | 予約の表示名。                               |
| appliedScopes     | IEnumerable                    | 予約に関連付けられている適用済みスコープの一覧。 (ScopeType が共有されていない場合にのみ使用できます。) |
| quantity          | int                            | 予約に含まれる仮想マシンの数。                 |
| expiryDateTime    | UTC 日時形式の文字列 | 予約の有効期限。                                |
| effectiveDateTime | UTC 日時形式の文字列 | 予約の有効日。                             |
| provisioningState | string                         | 予約のプロビジョニングの状態。                         |


## <a name="span-idvirtualmachinereservedinstanceartifactspan-idvirtualmachinereservedinstanceartifactspan-idvirtualmachinereservedartifactvirtualmachinereservedinstanceartifact"></a><span id="VirtualMachineReservedInstanceArtifact"/><span id="virtualmachinereservedinstanceartifact"/><span id="VIRTUALMACHINERESERVEDARTIFACT"/>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]  
> SDK version 1.9 で非推奨

Azure 予約仮想マシンインスタンスの権利に関連付けられている成果物。 [アーティファクト](#artifact)クラスから継承されます。  

| プロパティ   | 種類                              | 説明                                        |
|------------|-----------------------------------|----------------------------------------------------|
| リンク       | [Link](utility-resources.md#link) | 関連付けられているすべての成果物の詳細を取得するためのリンク。   |
| resourceID | string                            | Azure 予約注文またはリソースの ID。 |


## <a name="span-idvirtualmachinereservedinstanceartifactdetailsspan-idvirtualmachinereservedinstanceartifactdetailsspan-idvirtualmachinereservedartifactdetailsvirtualmachinereservedinstanceartifactdetails"></a><span id="VirtualMachineReservedInstanceArtifactDetails"/><span id="virtualmachinereservedinstanceartifactdetails"/><span id="VIRTUALMACHINERESERVEDARTIFACTDETAILS"/>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]  
> SDK version 1.9 で非推奨

Azure 予約仮想マシンインスタンス成果物リンクの呼び出し時に返されるエンティティを表します。  

| プロパティ                    | 種類                                                                 | 説明           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| type                        | [ArtifactType](#artifacttype)                                        | 成果物の種類。 |
| virtualMachineReservations  | IEnumerable <[VirtualMachineReservation](#virtualmachinereservation)> | Azure リソースまたは予約注文 id を示します。 |


## <a name="span-idvirtualmachinereservationspan-idvirtualmachinereservationspan-idvirtualmachinereservationvirtualmachinereservation"></a><span id="VirtualMachineReservation"/><span id="virtualmachinereservation"/><span id="VIRTUALMACHINERESERVATION"/>VirtualMachineReservation

> [!IMPORTANT]  
> SDK version 1.9 で非推奨

個々の仮想マシン予約を表します。


|     プロパティ      |              種類              |                                                説明                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             string             |                                         予約の ID。                                         |
|     scopeType     |             string             |                     仮想マシン予約に関連付けられているスコープの種類。                     |
|    displayName    |             string             |                                    予約の表示名。                                    |
|   appliedScopes   |      IEnumerable<string>       | 予約に関連付けられている適用済みスコープの一覧。 (ScopeType が共有されていない場合にのみ使用できます。) |
|     quantity      |              int               |                             予約に含まれる仮想マシンの数。                             |
|  expiryDateTime   | UTC 日時形式の文字列 |                                    予約の有効期限。                                     |
| effectiveDateTime | UTC 日時形式の文字列 |                                   予約の有効日。                                   |
| provisioningState |             string             |                                 予約のプロビジョニングの状態。                                 |

