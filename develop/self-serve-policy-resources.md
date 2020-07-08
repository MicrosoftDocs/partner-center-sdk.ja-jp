---
title: セルフサービスポリシーリソース
description: パートナーは、顧客のセルフサービスポリシーを設定します。
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095842"
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


## <a name="permission"></a>アクセス許可

セルフサービスポリシーの権限を表します。

| プロパティ             | Type|説明|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| リソース             | string                           | リソースへのアクセスも許可されています: AzureReservedInstances。                          |
| アクション               | string                           | アクションへのアクセスが許可されています: 購入                                           |
