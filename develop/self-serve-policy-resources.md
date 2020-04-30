---
title: セルフサービスポリシーリソース
description: パートナーは、顧客のセルフサービスポリシーを設定します。
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dc0da58debb7ea0c32272bf180f26d535110d4a5
ms.sourcegitcommit: f71c7fb2fef51ac7ca0a28717d5f7276bd20ec56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82564320"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy リソース

**適用対象:**

- パートナー センター

パートナーは、顧客のセルフサービスポリシーを設定します。

## <a name="selfservepolicy"></a>SelfServePolicy

カートについて説明します。

| プロパティ              | Type             | 説明                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | string           | セルフサービスポリシーが正常に作成されたときに提供される、セルフサービスポリシー識別子。     |
| SelfServeEntity       | SelfServeEntity  | アクセスが許可されているセルフサービスエンティティ。                                                     |
| Grantor               | Grantor          | アクセスを許可している権限の許可。                                                                    |
| アクセス許可           | アクセス許可の配列| [アクセス許可](#permission)リソースの配列。                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

権限を許可されているエンティティを表します。

| プロパティ             | Type|説明|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | string                           | アクセスが許可されているエンティティ。許容値: Customer。                                 |
| TenantId             | string                           | アクセスが許可されているエンティティのテナント識別子。                                   |

## <a name="grantor"></a>Grantor

権限を付与する権限の許可を表します。

| プロパティ             | Type|説明|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | string                           | アクセスを許可する権限の許可、値: BillToPartner。                               |
| TenantId             | string                           | アクセス権を付与するエンティティのテナント識別子。                                       |


## <a name="permission"></a>権限

セルフサービスポリシーの権限を表します。

| プロパティ             | Type|説明|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| リソース             | string                           | リソースへのアクセスも許可されています: AzureReservedInstances。                          |
| アクション               | string                           | アクションへのアクセスが許可されています: 購入                                           |
