---
title: License resources
description: Describes resources related to licenses.
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
# <a name="license-resources"></a>License resources


**Applies To**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Describes resources related to licenses.

## <a name="span-idlicensespan-idlicensespan-idlicenselicense"></a><span id="License"/><span id="license"/><span id="LICENSE"/>License


Describes a user license.

>[!NOTE]
>Unsupported on Partner Center operated by 21Vianet.

 

| プロパティ     | タスクバーの検索ボックスに                                                           | 説明                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | array of ServicePlan resources                                 | The collection of service plans that correspond to the license |
| productSKU   | ProductSku                                                     | The sku of the product that corresponds to the license.        |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the license.          |

 

## <a name="span-idlicenseupdatespan-idlicenseupdatespan-idlicenseupdatelicenseupdate"></a><span id="LicenseUpdate"/><span id="licenseupdate"/><span id="LICENSEUPDATE"/>LicenseUpdate


Provides information used to assign or remove licenses from a user.

| プロパティ         | タスクバーの検索ボックスに                                                           | 説明                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | オブジェクトの配列                                               | Array of [LicenseAssignment](#licenseassignment) objects. |
| licensesToRemove | 文字列の配列                                               | The product SKU identifiers of the licenses to remove.    |
| licenseWarnings  | オブジェクトの配列                                               | Array of [LicenseWarning](#licensewarning) objects.       |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                  |

 

## <a name="span-idlicenseassignmentspan-idlicenseassignmentspan-idlicenseassignmentlicenseassignment"></a><span id="LicenseAssignment"/><span id="licenseassignment"/><span id="LICENSEASSIGNMENT"/>LicenseAssignment


Provides information needed for a license update operation.

| プロパティ      | タスクバーの検索ボックスに             | 説明                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | 文字列の配列 | The service plan identifiers to be excluded from availability to the user. |
| skuId         | string           | The product SKU identifier for the license.                                |

 

## <a name="span-idlicensewarningspan-idlicensewarningspan-idlicensewarninglicensewarning"></a><span id="LicenseWarning"/><span id="licensewarning"/><span id="LICENSEWARNING"/>LicenseWarning


Contains warning information that occurred during a license update operation.

| プロパティ     | タスクバーの検索ボックスに             | 説明                                         |
|--------------|------------------|-----------------------------------------------------|
| コード         | string           | The warning code.                                   |
| メッセージ      | string           | The warning message.                                |
| servicePlans | 文字列の配列 | The service plan names associated with the warning. |

 

## <a name="span-idproductskuspan-idproductskuspan-idproductskuproductsku"></a><span id="ProductSku"/><span id="productsku"/><span id="PRODUCTSKU"/>ProductSku


Describes product details.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>タスクバーの検索ボックスに</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>id</td>
<td>string</td>
<td>The product identifier.</td>
</tr>
<tr class="even">
<td>名前</td>
<td>string</td>
<td>The user principal identifier.</td>
</tr>
<tr class="odd">
<td>skuPartNumber</td>
<td>string</td>
<td>The SKU part number name for the product. For example, for Office 365 Plan E3 , this value is &quot;EnterprisePack&quot;. This can be used in place of id if the id is not available.</td>
</tr>
<tr class="even">
<td>targetType</td>
<td>string</td>
<td>The target type of the product. This identifies whether the product is applicable to a &quot;User&quot; or a &quot;Tenant&quot;.</td>
</tr>
<tr class="odd">
<td>licenseGroupId</td>
<td>string</td>
<td>Identifies via a group identifier the authority or service that manages the productSku license. Products are segregated under license groups for better manageability.
<p>&quot;group1&quot; - All products whose licenses can be managed by Azure Active Directory (AAD).</p>
<p>&quot;group2&quot; - Minecraft product licenses.</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idserviceplanspan-idserviceplanspan-idserviceplanserviceplan"></a><span id="ServicePlan"/><span id="serviceplan"/><span id="SERVICEPLAN"/>ServicePlan


Identifies a deployable service within a product SKU. A product can have many service plans.

| プロパティ         | タスクバーの検索ボックスに   | 説明                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | string | The service plan identifier.                                                                                      |
| displayName      | string | The localized display name for the service plan.                                                                  |
| serviceName      | string | The service name.                                                                                                 |
| capabilityStatus | string | The service plan status of the service plan.                                                                      |
| targetType       | string | The target type of the service plan. This identifies whether the product is applicable to a "User" or a "Tenant". |

 

## <a name="span-idsubscribedskuspan-idsubscribedskuspan-idsubscribedskusubscribedsku"></a><span id="SubscribedSku"/><span id="subscribedsku"/><span id="SUBSCRIBEDSKU"/>SubscribedSku


Describes a subscribed product owned by a tenant.

| プロパティ         | タスクバーの検索ボックスに                                                           | 説明                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | 整数                                                        | The number of units available for assignment. This is calculated as total units - consumed units. |
| activeUnits      | 整数                                                        | The number of units active for assignment.                                                        |
| consumedUnits    | 整数                                                        | The number of units consumed.                                                                     |
| suspendedUnits   | 整数                                                        | The number of units suspended.                                                                    |
| totalUnits       | 整数                                                        | The total number of units. This is calculated as the sum of the active and warning units.         |
| warningUnits     | 整数                                                        | The number of warning units.                                                                      |
| productSku       | ProductSku                                                     | The product sku.                                                                                  |
| servicePlans     | array of ServicePlan resources                                 | The collection of service plans of a product.                                                     |
| capabilityStatus | string                                                         | The sku status of a product.                                                                      |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the resource.                                            |

 

 

 




