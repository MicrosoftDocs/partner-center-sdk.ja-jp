---
title: ライセンスリソース
description: ライセンスに関連するリソースについて説明します。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1c8cfd1b6edd5b15db72afd7241f2c3d8ad38879
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095107"
---
# <a name="license-resources"></a>ライセンスリソース

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

ライセンスに関連するリソースについて説明します。

## <a name="license"></a>ライセンス

ユーザーライセンスについて説明します。

>[!NOTE]
>21Vianet が運用するパートナーセンターではサポートされていません。

| プロパティ     | Type                                                           | 説明                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | ServicePlan リソースの配列                                 | ライセンスに対応するサービスプランのコレクション |
| productSKU   | ProductSku                                                     | ライセンスに対応する製品の sku。        |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes) | ライセンスに対応するメタデータ属性。          |

## <a name="licenseupdate"></a>LicenseUpdate

ユーザーにライセンスを割り当てる、または削除するために使用する情報を提供します。

| プロパティ         | Type                                                           | 説明                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | オブジェクトの配列                                               | [Licenseassignment](#licenseassignment)オブジェクトの配列。 |
| licensesToRemove すべてのものを | 文字列の配列                                               | 削除するライセンスの製品 SKU 識別子。    |
| licenseWarnings  | オブジェクトの配列                                               | [Licensewarning](#licensewarning)オブジェクトの配列。       |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                  |

## <a name="licenseassignment"></a>LicenseAssignment

ライセンスの更新操作に必要な情報を提供します。

| プロパティ      | Type             | 説明                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | 文字列の配列 | ユーザーが可用性から除外するサービスプラン識別子。 |
| skuId         | string           | ライセンスの製品 SKU 識別子。                                |

## <a name="licensewarning"></a>LicenseWarning

ライセンスの更新操作中に発生した警告情報が含まれます。

| プロパティ     | Type             | 説明                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | string           | 警告コード。                                   |
| message      | string           | 警告メッセージ。                                |
| servicePlans | 文字列の配列 | 警告に関連付けられているサービスプラン名。 |

## <a name="productsku"></a>ProductSku

製品の詳細について説明します。

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>Type</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>id</td>
<td>string</td>
<td>製品識別子。</td>
</tr>
<tr class="even">
<td>name</td>
<td>string</td>
<td>ユーザープリンシパル識別子。</td>
</tr>
<tr class="odd">
<td>skuPartNumber</td>
<td>string</td>
<td>製品の SKU 部品番号名。 たとえば、Office 365 Plan E3 の場合、この値はに <code>EnterprisePack</code> なります。 Id が使用できない場合は、このプロパティを id の代わりに使用できます。</td>
</tr>
<tr class="even">
<td>targetType</td>
<td>string</td>
<td>製品のターゲットの種類。 このプロパティは、製品がまたはに適用可能かどうかを識別 <code>User</code> <code>Tenant</code> します。</td>
</tr>
<tr class="odd">
<td>licenseGroupId</td>
<td>string</td>
<td>ProductSku ライセンスを管理する機関またはサービスをグループ識別子で識別します。 管理しやすいように、製品はライセンスグループの下に分離されています。
<p><code>group1</code>-Azure Active Directory (AAD) で管理できるライセンスを持つすべての製品。</p>
<p><code>group2</code>-Minecraft 製品ライセンス。</p></td>
</tr>
</tbody>
</table>

## <a name="serviceplan"></a>ServicePlan

製品 SKU 内の展開可能なサービスを識別します。 製品には、多くのサービスプランを含めることができます。

| プロパティ         | Type   | 説明                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | string | サービスプランの識別子。                                                                                      |
| displayName      | string | サービスプランのローカライズされた表示名。                                                                  |
| serviceName      | string | サービス名。                                                                                                 |
| capabilityStatus | string | サービスプランのサービスプランの状態。                                                                      |
| targetType       | string | サービスプランのターゲットの種類。 このプロパティは、製品が "ユーザー" または "テナント" に適用可能かどうかを識別します。 |

## <a name="subscribedsku"></a>SubscribedSku

テナントが所有するサブスクライブ済みの製品について説明します。

| プロパティ         | Type                                                           | 説明                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| ご自身のユニット   | integer                                                        | 割り当てに使用できる単位の数。 この値は、合計ユニット消費単位として計算されます。 |
| activeUnits      | integer                                                        | 割り当てに対してアクティブな単位の数。                                                        |
| consumedUnits    | integer                                                        | 消費された単位の数。                                                                     |
| suspendedUnits   | integer                                                        | 中断されたユニットの数。                                                                    |
| totalUnits       | integer                                                        | ユニットの合計数。 この値は、アクティブおよび警告単位の合計として計算されます。         |
| 警告ユニット     | integer                                                        | 警告ユニットの数です。                                                                      |
| productSku       | ProductSku                                                     | 製品 sku。                                                                                  |
| servicePlans     | ServicePlan リソースの配列                                 | 製品のサービスプランのコレクション。                                                     |
| capabilityStatus | string                                                         | 製品の sku の状態。                                                                      |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | リソースに対応するメタデータ属性。                                            |
