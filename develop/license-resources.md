---
title: ライセンスリソース
description: ライセンスに関連するリソースについて説明します。
ms.assetid: 20592E06-8A87-41F4-B8B0-6F9200556FDA
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 625209f834a7d89fbf288b7a1430624cb99485b1
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486932"
---
# <a name="license-resources"></a>ライセンスリソース


**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

ライセンスに関連するリソースについて説明します。

## <a name="span-idlicensespan-idlicensespan-idlicenselicense"></a><span id="License"/><span id="license"/><span id="LICENSE"/>ライセンス


ユーザーライセンスについて説明します。

>[!NOTE]
>21Vianet が運用するパートナーセンターではサポートされていません。

 

| プロパティ     | 種類                                                           | 説明                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | ServicePlan リソースの配列                                 | ライセンスに対応するサービスプランのコレクション |
| productSKU   | ProductSku                                                     | ライセンスに対応する製品の sku。        |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes) | ライセンスに対応するメタデータ属性。          |

 

## <a name="span-idlicenseupdatespan-idlicenseupdatespan-idlicenseupdatelicenseupdate"></a><span id="LicenseUpdate"/><span id="licenseupdate"/><span id="LICENSEUPDATE"/>LicenseUpdate


ユーザーにライセンスを割り当てる、または削除するために使用する情報を提供します。

| プロパティ         | 種類                                                           | 説明                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | オブジェクトの配列                                               | [Licenseassignment](#licenseassignment)オブジェクトの配列。 |
| licensesToRemove すべてのものを | 文字列の配列                                               | 削除するライセンスの製品 SKU 識別子。    |
| licenseWarnings  | オブジェクトの配列                                               | [Licensewarning](#licensewarning)オブジェクトの配列。       |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                  |

 

## <a name="span-idlicenseassignmentspan-idlicenseassignmentspan-idlicenseassignmentlicenseassignment"></a><span id="LicenseAssignment"/><span id="licenseassignment"/><span id="LICENSEASSIGNMENT"/>LicenseAssignment


ライセンスの更新操作に必要な情報を提供します。

| プロパティ      | 種類             | 説明                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | 文字列の配列 | ユーザーが可用性から除外するサービスプラン識別子。 |
| skuId         | string           | ライセンスの製品 SKU 識別子。                                |

 

## <a name="span-idlicensewarningspan-idlicensewarningspan-idlicensewarninglicensewarning"></a><span id="LicenseWarning"/><span id="licensewarning"/><span id="LICENSEWARNING"/>LicenseWarning


ライセンスの更新操作中に発生した警告情報が含まれます。

| プロパティ     | 種類             | 説明                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | string           | 警告コード。                                   |
| メッセージ      | string           | 警告メッセージ。                                |
| servicePlans | 文字列の配列 | 警告に関連付けられているサービスプラン名。 |

 

## <a name="span-idproductskuspan-idproductskuspan-idproductskuproductsku"></a><span id="ProductSku"/><span id="productsku"/><span id="PRODUCTSKU"/>ProductSku


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
<th>種類</th>
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
<td>製品の SKU 部品番号名。 たとえば、Office 365 Plan E3 の場合、この値は EnterprisePack&quot;&quot;ます。 Id が使用できない場合は、id の代わりにこれを使用できます。</td>
</tr>
<tr class="even">
<td>targetType</td>
<td>string</td>
<td>製品のターゲットの種類。 これにより、製品が &quot;ユーザー&quot; または &quot;テナント&quot;に適用可能かどうかが識別されます。</td>
</tr>
<tr class="odd">
<td>licenseGroupId</td>
<td>string</td>
<td>ProductSku ライセンスを管理する機関またはサービスをグループ識別子で識別します。 管理しやすいように、製品はライセンスグループの下に分離されています。
<p>&quot;group1&quot;-Azure Active Directory (AAD) で管理できるライセンスを持つすべての製品。</p>
<p>&quot;group2&quot; 製品ライセンスです。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idserviceplanspan-idserviceplanspan-idserviceplanserviceplan"></a><span id="ServicePlan"/><span id="serviceplan"/><span id="SERVICEPLAN"/>ServicePlan


製品 SKU 内の展開可能なサービスを識別します。 製品には、多くのサービスプランを含めることができます。

| プロパティ         | 種類   | 説明                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | string | サービスプランの識別子。                                                                                      |
| displayName      | string | サービスプランのローカライズされた表示名。                                                                  |
| serviceName      | string | サービス名。                                                                                                 |
| capabilityStatus | string | サービスプランのサービスプランの状態。                                                                      |
| targetType       | string | サービスプランのターゲットの種類。 これにより、製品が "ユーザー" または "テナント" に適用可能かどうかが識別されます。 |

 

## <a name="span-idsubscribedskuspan-idsubscribedskuspan-idsubscribedskusubscribedsku"></a><span id="SubscribedSku"/><span id="subscribedsku"/><span id="SUBSCRIBEDSKU"/>SubscribedSku


テナントが所有するサブスクライブ済みの製品について説明します。

| プロパティ         | 種類                                                           | 説明                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| ご自身のユニット   | 整数                                                        | 割り当てに使用できる単位の数。 これは、合計ユニット消費ユニット数として計算されます。 |
| activeUnits      | 整数                                                        | 割り当てに対してアクティブな単位の数。                                                        |
| consumedUnits    | 整数                                                        | 消費された単位の数。                                                                     |
| suspendedUnits   | 整数                                                        | 中断されたユニットの数。                                                                    |
| totalUnits       | 整数                                                        | ユニットの合計数。 これは、アクティブおよび警告単位の合計として計算されます。         |
| 警告ユニット     | 整数                                                        | 警告単位の数。                                                                      |
| ProductSku       | ProductSku                                                     | 製品 sku。                                                                                  |
| servicePlans     | ServicePlan リソースの配列                                 | 製品のサービスプランのコレクション。                                                     |
| capabilityStatus | string                                                         | 製品の sku の状態。                                                                      |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | リソースに対応するメタデータ属性。                                            |

 

 

 




