---
title: リソースの注文
description: パートナーは、顧客がプランの一覧からサブスクリプションを購入することを希望する場合に注文を行います。
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 587333504742a303f7bf02b41b58e45c855d2c2d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094732"
---
# <a name="order-resources"></a>リソースの注文

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーは、顧客がプランの一覧からサブスクリプションを購入することを希望する場合に注文を行います。

>[!NOTE]
>注文リソースには、テナント識別子ごとに1分あたり500の要求のレート制限があります。

## <a name="order"></a>順番

パートナーの注文について説明します。

| プロパティ           | Type                                               | 説明                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | string                                             | 注文が正常に作成されたときに提供される注文 id。                                   |
| alternateId        | string                                             | 注文のわかりやすい識別子。                                                                          |
|referenceCustomerId | string                                             | 顧客 ID。 |
| billingCycle       | string                                             | パートナーがこの注文に対して課金される頻度を示します。 サポートされる値は、[BillingCycleType](product-resources.md#billingcycletype) で検出されたメンバー名です。 既定値は、注文の作成時に "毎月" または "OneTime" です。 このフィールドは、注文が正常に作成されたときに適用されます。 |
| transactionType    | string                                             | 読み取り専用です。 注文のトランザクションの種類。 サポートされている値は、' UserPurchase '、' SystemPurchase '、または ' SystemBilling ' です。 |
| lineItems          | [Orderlineitem](#orderlineitem)リソースの配列 | 顧客が購入しているプランの一覧 (数量を含む)。        |
| currencyCode       | string                                             | 読み取り専用です。 注文を配置するときに使用する通貨。 注文が正常に作成されたときに適用されます。           |
| currencySymbol     | string                                             | 読み取り専用です。 通貨コードに関連付けられている通貨記号。 |
| creationDate       | DATETIME                                           | 読み取り専用です。 注文が作成された日付 (日付/時刻形式)。 注文が正常に作成されたときに適用されます。                                   |
| 状態             | string                                             | 読み取り専用です。 注文の状態。  サポートされる値は、 [**Orderstatus**](#orderstatus)で見つかったメンバー名です。        |
| リンク              | [OrderLinks](utility-resources.md#resourcelinks)           | 注文に対応するリソースリンク。            |
| 属性         | [ResourceAttributes](utility-resources.md#resourceattributes) | 順序に対応するメタデータ属性。       |

## <a name="orderlineitem"></a>OrderLineItem

注文にはオファーの一覧が含まれ、各項目は OrderLineItem として表されます。

| プロパティ             | Type                                      | 説明                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | INT                                       | コレクション内の各品目には、0 からカウント -1 までカウントする、一意の品目番号が与えられます。                                                                                                                                                 |
| offerId              | string                                    | オファーの ID。                                                                                                                                                                                                                       |
| subscriptionId       | string                                    | サブスクリプションの ID です。                                                                                                                                                                                                                |
| parentSubscriptionId | string                                    | 省略可能。 アドオン オファーの親サブスクリプションの ID。 PATCH にのみ適用されます。                                                                                                                                                     |
| friendlyName         | string                                    | 省略可能。 明確に区別するためにパートナーによって定義されたサブスクリプションのフレンドリ名。                                                                                                                                              |
| 数量             | INT                                       | ライセンスまたはインスタンスの数。                                                                                                                                                                                |
| termDuration         | string                                    | 用語の期間の ISO 8601 表現。 現在サポートされている値は、 **P1M** (1 か月)、 **P1Y** (1 年)、および**P3Y** (3 年) です。                               |
| transactionType      | string                                    | 読み取り専用です。 品目のトランザクションの種類。 サポートされている値は、' new '、' 書き換え '、' addQuantity '、' Remov-アンチ Ty '、' cancel '、' convert '、または ' 顧客クレジット ' です。 |
| partnerIdOnRecord    | string                                    | 間接プロバイダーが間接リセラーの代わりに注文を行う場合は、このフィールドに**間接リセラー**の MPN id のみを入力します (間接プロバイダーの id は使用しないでください)。 これにより、インセンティブを正しく計算できます。 |
| provisioningContext  | Dictionary<string、string>            | カタログ内の一部の項目のプロビジョニングに必要な情報。 SKU の "プロビジョニング変数" プロパティは、カタログ内の特定のアイテムに必要なプロパティを示します。                                                                                                                                               |
| リンク                | [OrderLineItemLinks](#orderlineitemlinks) | 読み取り専用です。 注文明細項目に対応するリソースリンク。                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |更新期間の詳細。                                                                           |

## <a name="renewsto"></a>RenewsTo

更新期間の詳細を表します。

| プロパティ              | Type             | 必須        | 説明 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | string           | いいえ              | 更新用語の期間の ISO 8601 表現。 現在サポートされている値は、 **P1M** (1 か月) と**P1Y** (1 年) です。 |

## <a name="orderlinks"></a>OrderLinks

注文に対応するリソースリンクを表します。

| プロパティ           | Type                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [リンク](utility-resources.md#link)            | 設定されている場合は、注文のプロビジョニングステータスを取得するためのリンクが表示されます。       |
| self               | [リンク](utility-resources.md#link)            | 注文リソースを取得するためのリンク。                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

注文に関連付けられた完全なサブスクリプションを表します。

| プロパティ           | Type                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [リンク](utility-resources.md#link)            | 値が設定されている場合は、行項目の[プロビジョニング状態](#orderlineitemprovisioningstatus)を取得するためのリンクが表示されます。       |
| sku                | [リンク](utility-resources.md#link)            | 購入したカタログアイテムの SKU 情報を取得するためのリンク。                    |
| subscription       | [リンク](utility-resources.md#link)            | 設定されている場合は、サブスクリプションの完全な情報へのリンク。                       |
| activationLinks    | [リンク](utility-resources.md#link)            | 値が設定されている場合は、サブスクリプションをアクティブにするためのリンクのリソースを取得します。             |

## <a name="orderstatus"></a>OrderStatus

順序の状態を示す値を持つ[列挙型](https://docs.microsoft.com/dotnet/api/system.enum)。

| 値              | 位置     | 説明                                     |
|--------------------|--------------|-------------------------------------------------|
| unknown            | 0            | 列挙型の初期化子です。                               |
| 完了          | 1            | 注文が完了したことを示します。          |
| pending            | 2            | 順序がまだ保留中であることを示します。      |
| た          | 3            | 注文がキャンセルされたことを示します。    |

## <a name="orderlineitemprovisioningstatus"></a>Orderlineitemプロビジョニングステータス

[Orderlineitem](#orderlineitem)のプロビジョニングの状態を表します。

| プロパティ                        | Type                                | Description                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | INT                                 | 注文明細項目の一意の行番号。 値の範囲は0からカウント-1 です。             |
| 状態                          | string                              | 注文明細項目のプロビジョニングの状態。 次の値が含まれます。</br>"フルフィルメント済み": 注文のフルフィルメントが正常に完了し、ユーザーが予約を使用できるようになります。</br>"満たされ": キャンセルにより満たされていません</br>"PrefulfillmentPending": 要求はまだ処理中ですが、フルフィルメントはまだ完了していません |
| quantityProvisioningInformation | リスト<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | 注文品目の数量のプロビジョニング状態情報の一覧。 |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

数量別のプロビジョニングの状態を表します。

| プロパティ                           | Type                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| 数量                           | INT                                          | 項目数。                                 |
| 状態                             | string                                       | 項目数の状態。                   |
