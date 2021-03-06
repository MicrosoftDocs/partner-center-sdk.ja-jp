---
title: サブスクリプション リソース
description: サブスクリプションリソースでは、サポート、返金、Azure 権利など、ライフサイクル全体にわたってサブスクリプションに関する詳細情報を提供できます。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd835e46e99b1fcb1e0b0e694ad73b1dca1240c9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095990"
---
# <a name="subscription-resources"></a>サブスクリプション リソース

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

サブスクリプションにより、顧客は一定期間、サービスを使用できます。 すべてのフィールドがすべてのサブスクリプションに適用されるわけではありません。 多くのフィールドは、サブスクリプションが中断されたり取り消されたりした場合など、ライフサイクルの特定の時点でのみ適用されます。

## <a name="subscription"></a>サブスクリプション

>[!NOTE]
>**サブスクリプション**リソースには、テナント識別子ごとに1分あたり500の要求のレート制限があります。

サブスクリプション**リソースは**、サブスクリプションのライフサイクルを表します。サブスクリプションのライフサイクル全体にわたって状態を定義するプロパティが含まれています。

| プロパティ             | Type                                                          | 説明                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string                                                        | サブスクリプションの識別子です。                                                                                                                                                  |
| offerId              | string                                                        | プラン ID。                                                                                                                                                         |
| entitlementId        | string                                                        | 権利識別子 (Azure サブスクリプション ID)。                                                                                                                        |
| offerName            | string                                                        | プラン名。                                                                                                                                                               |
| friendlyName         | string                                                        | 明確に区別するためにパートナーによって定義されたサブスクリプションのフレンドリ名。                                                                                           |
| 数量             | number                                                        | 数量。 たとえば、ライセンスベースの課金の場合、このプロパティはライセンス数に設定されます。                                                            |
| unitType             | string                                                        | サブスクリプションの数量を定義する単位です。                                                                                                                             |
| parentSubscriptionId | string                                                        | 親サブスクリプションの識別子を取得します。値の設定もできます。                                                                                                                              |
| creationDate         | string                                                        | 日付/時刻形式で作成日を取得または設定します。                                                                                                                          |
| effectiveStartDate   | UTC 日時形式の文字列                                | このサブスクリプションの有効な開始日を日付/時刻形式で取得または設定します。 移行されたサブスクリプションの日付をバックアップする場合、または別のサブスクリプションに合わせる場合に使用します。                |
| Commitの Enddate    | UTC 日時形式の文字列                                | このサブスクリプションのコミットメント終了日 (日付/時刻形式)。 自動更新できないサブスクリプションの場合、これはそれまでの日付を表します。       |
| 状態               | string                                                        | サブスクリプションの状態: "なし"、"アクティブ"、"保留中"、"中断"、または "削除済み"。                                                                                                         |
| autoRenewEnabled     | boolean                                                       | サブスクリプションが自動的に更新されるかどうかを示す値を取得します。                                                                                                    |
| 種類          | string                                                        | サブスクリプションの課金方法を指定します。 "none"、"usage"、"license" です。                                                                                                      |
| billingCycle         | string                                                        | パートナーがこの注文に対して課金される頻度を示します。 サポートされている値は、 [**BillingCycleType**](product-resources.md#billingcycletype)で見つかったメンバー名です。 |
| hasPurchasableAddons | boolean                                                       | サブスクリプションに購入可能なアドオンがあるかどうかを示す値を取得または設定します。                                                                                             |
| isTrial              | boolean                                                       | 評価版サブスクリプションであるかどうかを示す値です。                                                                                                                      |
| Ismicrosoft 製品   | boolean                                                       | このが Microsoft 製品であるかどうかを示す値。                                                                                                                       |
| publisherName        | string                                                        | 発行元の名前。                                                                                                                                                           |
| actions              | 文字列の配列                                              | 許可されるアクションを取得または設定します。 有効な値: "edit"、"cancel"                                                                                                  |
| パートナー            | string                                                        | 間接パートナーモデルで使用される、レコードの再販業者の MPN ID。                                                                                                     |
| suspensionReasons    | 文字列の配列                                              | 読み取り専用です。 サブスクリプションが中断された場合は、その理由を示します。                                                                                                                  |
| contractType         | string                                                        | 読み取り専用です。 コントラクトの種類: "subscription"、"productKey"、または "redemptionCode"。                                                                                           |
| refundOptions        | [RefundOption](#refundoption)リソースの配列   | 読み取り専用。 このサブスクリプションで使用できる返金オプションのセット。                                                                                              |
| リンク                | [SubscriptionLinks](#subscriptionlinks)                       | サブスクリプションリンクを取得または設定します。                                                                                                                                          |
| orderId              | string                                                        | サブスクリプションを開始するために配置された注文の ID。                                                                                                                |
| termDuration         | string                                                        | 用語の期間の ISO 8601 表現。 現在サポートされている値は、 **P1M** (1 か月)、 **P1Y** (1 年)、および**P3Y** (3 年) です。                                                        |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | サブスクリプションに対応するメタデータ属性。                                                                                                                    |
| renewalTermDuration  | string                                                        | 用語の期間の ISO 8601 表現。 現在サポートされている値は、 **P1M** (1 か月) と**P1Y** (1 年) です。                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

**Subscriptionlinks**リソースには、サブスクリプションリソースにアタッチされたリンクのコレクションが記述されています。

| プロパティ           | Type                               | 説明                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [リンク](utility-resources.md#link) | オファーを取得または設定します。               |
| parentSubscription | [リンク](utility-resources.md#link) | 親サブスクリプションを取得します。値の設定もできます。 |
| product            | [リンク](utility-resources.md#link) | サブスクリプションに関連付けられている製品を取得します。 |
| sku                | [リンク](utility-resources.md#link) | サブスクリプションに関連付けられている製品 sku を取得します。 |
| availability       | [リンク](utility-resources.md#link) | サブスクリプションに関連付けられている製品 sku の可用性を取得します。 |
| activationLinks    | [リンク](utility-resources.md#link) | サブスクリプションに関連付けられているアクティベーションリンクの一覧を取得します。 |
| self               | [リンク](utility-resources.md#link) | 自己 URI。                         |
| [次へ]               | [リンク](utility-resources.md#link) | 項目の次のページ。               |
| previous           | [リンク](utility-resources.md#link) | 項目の前のページ。           |

## <a name="subscriptionprovisioningstatus"></a>Subscriptionのプロビジョニングステータス

**Subscriptionprovisioning status**リソースは、サブスクリプションのプロビジョニング状態に関する情報を提供します。

| プロパティ   | Type                                                           | 説明                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | string                                                         | 製品 SKU を識別する GUID 形式の文字列。             |
| 状態     | string                                                         | プロビジョニングの状態を示します。 "成功"、"保留中"、または "失敗" です。 |
| 数量   | number                                                         | プロビジョニング後のサブスクリプション数を提供します。               |
| endDate    | UTC 日時形式の文字列                                 | サブスクリプションの終了日。                                    |
| 属性 | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

**Subscriptionregistrationstatus**リソースには、サブスクリプションリソースにアタッチされたリンクのコレクションが記述されています。

| プロパティ           | Type                               | 説明                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | string                             | サブスクリプションの識別子です。                                                          |
| 状態             | string                             | 登録状態を示します。 "登録済み"、"登録中"、または "notregistered" です。    |

## <a name="supportcontact"></a>サポート連絡先

**Supportcontact**リソースは、お客様のサブスクリプションのサポート連絡先を表します。

| プロパティ        | Type                                                           | 説明                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | string                                                         | サポート連絡先のテナント識別子を示す GUID 形式の文字列。 |
| supportMpnId    | string                                                         | 連絡先の Microsoft Partner Network (MPN) 識別子。                       |
| name            | string                                                         | サポート連絡先の名前。                                                |
| リンク           | [ResourceLinks](utility-resources.md#resourcelinks)            | サポート連絡先関連のリンク。                                              |
| 属性      | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。 "ObjectType": "SupportContact" が含まれています。              |

## <a name="registersubscription"></a>RegisterSubscription

**Registersubscription**リソースは、サブスクリプションの登録状態を照会するために使用できるリンクを返します。 登録状態は、Azure サブスクリプションを登録するために正常に受け入れられた要求の応答本文で返されます。

| プロパティ                | 種類                               | 説明                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | HTTP 状態コード 202 "accept" を返します。場所ヘッダーには、登録ステータスをクエリするためのリンクが含まれています。 たとえば、`"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>RefundOption

**RefundOption**リソースは、サブスクリプションの返金オプションを表します。

| プロパティ          | 種類 | [説明]                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| type | string | 返金の種類。 サポートされている値は、"Partial" と "Full" です。 |
| expiresAfter      | UTC 日時形式の文字列 | このオプションが有効期限切れになったときのタイムスタンプ。 Null の場合は、有効期限がないことを意味します。 |

## <a name="azureentitlement"></a>AzureEntitlement

**Azureentitlement**リソースは、サブスクリプションの Azure の権利を表します。

| プロパティ          | 種類 | 説明                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | string | 権利識別子 |
| friendlyName      | string | 権利のフレンドリ名。 |
| 状態 | string | 権利の状態。 |
| subscriptionId | string | 権利が属しているサブスクリプション識別子。 |
