---
title: カートのリソース
description: パートナーは、顧客がプランの一覧からサブスクリプションを購入することを希望する場合に注文を行います。
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 561bffb905becd1bfc699eb13fe4dc6e10e8e07a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096496"
---
# <a name="cart-resources"></a>カートのリソース

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーは、顧客がプランの一覧からサブスクリプションを購入することを希望する場合に注文を行います。

## <a name="cart"></a>カート

カートについて説明します。

| プロパティ              | Type             | 説明                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | string           | カートが正常に作成されたときに提供されるカート識別子。                               |
| 前のタイムスタンプ     | DateTime         | カートが作成された日付 (日付/時刻形式)。 カートが正常に作成されたときに適用されます。      |
| lastModifiedTimeStamp | DateTime         | カートが最後に更新された日付 (日付/時刻形式)。 カートが正常に作成されたときに適用されます。 |
| expirationTimeStamp   | DateTime         | カートの有効期限が切れる日付 (日付と時刻の形式)。 カートの作成が成功したときに適用されます。          |
| lastModifiedUser      | string           | カートを最後に更新したユーザー。 カートの作成が成功したときに適用されます。                          |
| lineItems             | オブジェクトの配列 | [CartLineItem](#cartlineitem)リソースの配列。                                                   |
| 状態                | string           | カートの状態。 有効な値は、"Active" (更新/送信可能) と "Ordered" (既に送信済み) です。 |

## <a name="cartlineitem"></a>CartLineItem

カートに含まれる1つのアイテムを表します。

| プロパティ             | Type                             | 説明                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string                           | カートの品目の一意の識別子。 カートの作成が成功したときに適用されます。                                                                   |
| catalogItemId        | string                           | カタログ項目の識別子。                                                                                                                          |
| friendlyName         | string                           | 省略可能。 明確に区別できるように、パートナーによって定義された項目のフレンドリ名。                                                                 |
| 数量             | INT                              | ライセンスまたはインスタンスの数。                                                                                                                  |
| currencyCode         | string                           | 通貨コード。                                                                                                                                    |
| billingCycle         | Object                           | 現在の期間に設定されている請求サイクルの種類。                                                                                                 |
| termDuration         | string                           | 用語の期間の ISO 8601 表現。 現在サポートされている値は、P1M (1 か月)、P1Y (1 年)、および P3Y (3 年) です。                                |
| participants         | オブジェクトの文字列ペアの一覧      | 購入時のレコードの PartnerId (MPNID) のコレクション。                                                                                          |
| provisioningContext  | Dictionary<string、string>       | 購入した項目をプロビジョニングするときに使用される追加のコンテキスト。 特定の項目に必要な値を確認するには、SKU の "プロビジョニング変数" プロパティを参照してください。 |
| orderGroup           | string                           | 同じ順序で一緒に送信できる項目を示すグループ。                                                                          |
| addonItems           | **CartLineItem**オブジェクトの一覧 | アドオンのカート行項目のコレクション。 これらの項目は、ルートカートの品目の購入から得られる基本サブスクリプションに対して購入されます。 |
| エラー                | Object                           | エラーが発生した場合にカートが作成された後に適用されます。                                                                                                    |
| renewsTo             | オブジェクトの配列                 | [Renewsto](#renewsto)の配列。                                                                            |

## <a name="renewsto"></a>RenewsTo

カートの品目に含まれる1つのアイテムを表します。

| プロパティ              | Type             | 必須        | 説明 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | 文字列           | いいえ              | 更新用語の期間の ISO 8601 表現。 現在サポートされている値は、 **P1M** (1 か月) と**P1Y** (1 年) です。 |

## <a name="carterror"></a>CartError

カートが作成された後に発生するエラーを表します。

| プロパティ         | Type                                   | 説明                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [CartErrorCode](#carterrorcode) | カートエラーの種類。                                                                       |
| errorDescription | string                                 | エラーの説明。サポートされる値、既定値、または制限に関する注意事項が含まれます。 |

## <a name="carterrorcode"></a>CartErrorCode

カートエラーの種類を示す値を持つ[列挙](https://docs.microsoft.com/dotnet/api/system.enum)です。

| 値                                | 位置 | 説明                                             |
|--------------------------------------|----------|---------------------------------------------------------|
| Unknown                              | 0        | 既定値です。                                          |
| CurrencyIsNotSupported               | 10000    | 指定された市場では、通貨はサポートされていません。 |
| CatalogItemIdIsNotValid              | 10001    | カタログ項目 ID が無効です。                       |
| QuotaNotAvailable                    | 10002    | 使用可能なクォータが不足しています。                    |
| InventoryNotAvailable                | 10003    | 選択されたプランでは、インベントリを利用できません。  |
| ParticipantsIsNotSupportedForPartner | 10004    | 参加者の設定は、このパートナーではサポートされていません。 |
| UnableToProcessCartLineItem          | 10006    | カートの品目を処理できません。                   |
| SubscriptionIsNotValid               | 10007    | サブスクリプションが無効です。                          |
| SubscriptionIsNotEnabledForRI        | 10008    | サブスクリプションで Azure 予約が有効になっていません。 |
| SandboxLimitExceeded                 | 10009    | サンドボックスの制限を超えました。                    |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

カートのチェックアウトの結果を表します。

| プロパティ    | Type                                              | 説明                     |
|-------------|---------------------------------------------------|---------------------------------|
| 注文      | [Order](order-resources.md#order)オブジェクトのリスト。         | 注文のコレクションです。       |
| orderErrors | [Ordererror](#ordererror)オブジェクトの一覧。 | 注文エラーのコレクションです。 |

## <a name="ordererror"></a>OrderError

注文が作成されたときにカートのチェックアウト中に発生するエラーを表します。

| プロパティ     | Type   | 説明                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | string | 注文の注文グループ ID をエラーと共に使用します。 |
| code         | INT    | エラー コード。                                 |
| description  | string | エラーの説明。                   |

## <a name="ordererrorcode"></a>OrderErrorCode

注文エラーの種類を示す値を持つ[列挙](https://docs.microsoft.com/dotnet/api/system.enum)です。

| 値 | 位置 | 説明 |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | 要求コンテキストにパートナートークンがありません。 |
| InvalidInput | 800002 | 要求の入力が無効です。 |
| ServiceException | 800003 | 予期しないサービスエラーです。 |
| InvalidOfferId | 800004 | オファー ID が無効です。 |
| CreateOrderError | 800005 | 注文の作成に失敗しました。 |
| ProvisioningStatusNotFound | 800007 | プロビジョニング情報を取得できません。 |
| CartIdNotFound | 800008 | カート ID を取得できません。 |
| CartItemErrorInCreateOrder | 800009 | カート項目でエラーが発生しました。 |
| InventoryNotAvailable | 800010 | このカタログ項目では、インベントリを利用できません。 |
| AzureSubscriptionNotValid | 800011 | このサブスクリプションは有効な Azure サブスクリプションではありません。 |
| SubscriptionIsNotActive | 800012 | このサブスクリプションはアクティブなサブスクリプションではありません。 |
| SubscriptionIsNotEnabledForRI | 800013 | このサブスクリプションでは、RI の購入が有効になっていません。 |
| PendingAdjustment | 800014 | この注文に対して保留中の調整が要求されています。 |
| MpnIdNotFound | 800015 | MPN Id が見つかりません。 |
| NotValidIndirectResellerMpnId | 800016 | MPN Id は、有効な間接リセラーではありません。 |
| InvalidQuantity | 800017 | このカタログ項目の数量は使用できません。 |
| SandboxLimitExceeded | 800018 | サンドボックスの制限に達しました。 |
| SandboxTenantOnly | 800019 | この操作は、サンドボックステナントに対してのみ有効です。 |
| CatalogItemNotEligibleForPurchase | 800020 | カタログ項目は購入に適合していません。 |
| SubscriptionIsNotValid | 800021 | このサブスクリプションは有効なサブスクリプションではありません。 |
| ManualReviewRequired | 800022 | このトランザクションの対象となる可能性があります。 サポートにお問い合わせください。|
| InsufficientFunds | 800023 | クレジットラインがこの購入の最小しきい値に達していないため、このトランザクションの対象になりません。注文を更新してください (または、サポートに連絡してください)。 |
| ReviewCancelled | 800024 | このトランザクションの対象ではありません。 |
| LineOfCreditNotDefined | 800025 | クレジットラインがこの購入の最小しきい値に達していないため、このトランザクションの対象になりません。 注文を更新してください (または、サポートに連絡してください)。 |
| RiskError | 800026 | このトランザクションの対象ではありません。 |
| SubscriptionNotRegistered | 800030 | このサブスクリプションは登録されていません。 |
| PurchaseSystemNotSupported | 800031 | 購入システムはサポートされていません。 |
| ConditionFailed | 800036 | 事前条件が失敗しました。 |
| AssetIdNotFound | 800037 | 資産 ID が見つかりません。 |
| AssetFutureBillingInfoNotFound | 800038 | Asset FutureBillingInfo が見つかりません。 |
| ResellerProgramStatusNotActive | 800039 | リセラープログラムの状態がアクティブではありません。 |
| AssetStatusChangeNotValid | 800040 | 資産の状態をからに変更することはできません **{0}** **{1}** 。 |
| 項目がアクティブになりました | 800041 | この項目は既にアクティブ化されています。 |
| NotSupported | 800042 | サポートされていません。 |
| PricingAccessForbidden | 800043 | 価格情報へのアクセス権は付与されません。 |
| OrderInProgress | 800060 | 注文が進行中です。 数分で最近の注文の注文履歴を確認してください。 |
| OrderCannotBeCancelled | 800061 | 注文を取り消すことはできません。 |
| ReviewRejected | 800062 | このトランザクションの対象ではありません。 |
| CancelLegacyOrder | 800063 | この順序 **{0}** を取り消すことはできません。 `PATCH /customers/{1}/subscriptions/<subscriptionId>`サブスクリプションを中断するには、を使用します。 |
| CartProcessedByAnotherRequest | 800064 | カート **{0}** は別の要求によって処理されています。 |
| CartCheckOutNotAllowedWhenStatusIsOrdered | 800065 | 既に送信されたカートをチェックアウトすることはできません **{0}** 。 |
