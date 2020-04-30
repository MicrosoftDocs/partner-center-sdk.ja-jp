---
title: 製品リソース
description: 購入可能な商品またはサービスを表すリソース。 製品の種類と形状 (SKU) を説明し、在庫内の製品の可用性を確認するためのリソースが含まれています。
ms.assetid: 80C1F9B5-35FB-4DD8-B501-03467E1D75AD
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d733c956f4742a7299e847e7ff48130a6b268df6
ms.sourcegitcommit: 45094b6fb1437bca51f97e193ac2957747dbea27
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82124647"
---
# <a name="products-resources"></a>製品リソース

**適用対象**

- パートナー センター

購入可能な商品またはサービスを表すリソース。 製品の種類と形状 (SKU) を説明し、在庫内の製品の可用性を確認するためのリソースが含まれています。

## <a name="product"></a>Product

購入可能な good または service を表します。 製品自体は購入可能なの項目ではありません。

| プロパティ           | Type                          | 説明                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | string                        | この製品の ID。                                                 |
| title              | string                        | 製品タイトル。                                                       |
| description        | string                        | 製品の説明。                                                 |
| productType        | [ItemType](#itemtype)         | この製品の種類の分類を記述するオブジェクト。     |
| Ismicrosoft 製品 | [bool]                          | これが Microsoft 製品であるかどうかを示します。                          |
| publisherName      | string                        | 使用可能な場合は、製品の発行元の名前。                          |
| リンク              | [ProductLinks](#productlinks) | 製品内に含まれるリソースリンク。                         |

## <a name="itemtype"></a>ItemType

製品の種類を表します。

| プロパティ        | Type                          | 説明                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | string                        | 型識別子。                                                                 |
| displayName     | string                        | この型の表示名。                                                      |
| subType         | [ItemType](#itemtype)         | 省略可能。 この項目の種類のサブ型の分類を記述するオブジェクト。     |

## <a name="productlinks"></a>ProductLinks

[製品](#product)のリンクの一覧が含まれています。

| プロパティ        | Type                                                          | 説明                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| sku            | [リンク](utility-resources.md#link)                             | 基になる Sku にアクセスするためのリンク。          |
| リンク           | [ResourceLinks](utility-resources.md#resourcelinks)           | このリソース内に含まれるリソースリンク。   |

## <a name="sku"></a>Sku

製品の購入可能な在庫維持単位 (SKU) を表します。 これらは、製品のさまざまな形状を表します。

| プロパティ               | Type             | 説明                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | string           | この SKU の ID。 この ID は、その親製品のコンテキスト内でのみ一意です。 |
| title                  | string           | SKU のタイトル。                                                                 |
| description            | string           | SKU の説明。                                                           |
| productId              | string           | この SKU を含む親[製品](#product)の ID。                      |
| minimumQuantity        | INT              | 購入に許容される最小数量。                                            |
| maximumQuantity        | INT              | 購入に許可される最大数量。                                            |
| isTrial                | [bool]             | この SKU が試用版の項目であるかどうかを示します。                                           |
| supportedBillingCycles | 文字列の配列 | この SKU でサポートされている請求サイクルの一覧。 サポートされる値は、[BillingCycleType](#billingcycletype) で検出されたメンバー名です。 |
| purchasePrerequisites  | 文字列の配列 | この項目を購入する前に必要な前提条件の手順またはアクションの一覧です。 サポートされる値は<br/>  "InventoryCheck"-この項目の購入を試行する前に、項目の在庫を評価する必要があることを示します。<br/> "AzureSubscriptionRegistration"-Azure サブスクリプションが必要であり、この項目の購入を試行する前に登録する必要があることを示します。  |
| inventoryVariables     | 文字列の配列 | この項目の在庫チェックを実行するために必要な変数の一覧。 サポートされる値は<br/> "CustomerId"-購入の対象となる顧客の ID。<br/> "AzureSubscriptionId"-Azure 予約購入に使用される Azure サブスクリプションの ID。</br> "ArmRegionName"-インベントリを確認するリージョン。 この値は、SKU の DynamicAttributes の "ArmRegionName" と一致している必要があります。 |
| プロビジョニング変数  | 文字列の配列 | この項目を購入するときに[カート](cart-resources.md#cartlineitem)の品目のプロビジョニングコンテキストに提供する必要がある変数の一覧。 サポートされる値は<br/> スコープ-Azure 予約購入のスコープ。 "Single"、"Shared"。<br/> "SubscriptionId"-Azure 予約購入に使用される Azure サブスクリプションの ID。<br/> "Duration"-Azure 予約の期間 ("1Year"、"3Year")。  |
| dynamicAttributes      | キーと値のペア  | この項目に適用される動的プロパティのディクショナリ。 このディクショナリのプロパティは動的であり、予告なしに変更される可能性があることに注意してください。 このプロパティの値に存在する特定のキーに対しては、厳密な依存関係を作成しないでください。    |
| リンク                  | [ResourceLinks](utility-resources.md#resourcelinks) | SKU 内に含まれるリソースリンク。                   |

## <a name="availability"></a>可用性

SKU を購入できる構成 (国、通貨、業界セグメントなど) を表します。

| プロパティ        | Type                        | 説明                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | string                        | この可用性の ID。 この ID は、その親[製品](#product)および[SKU](#sku)のコンテキスト内でのみ一意です。 **メモ**この ID は、時間の経過と共に変化することがあります。 この値は、取得後の短い期間内でのみ使用してください。  |
| productId       | string                        | この可用性を含む[製品](#product)の ID。           |
| skuId           | string                        | この可用性を含む[SKU](#sku)の ID。                   |
| catalogItemId   | string                        | カタログ内のこのアイテムの一意の識別子です。 これは、親[SKU](#sku)を購入するときに、 [Orderlineitem. offerid](order-resources.md#orderlineitem)プロパティまたは[CartLineItem](cart-resources.md#cartlineitem)プロパティに値を設定する必要がある ID です。 **メモ**この ID は、時間の経過と共に変化することがあります。 この値は、取得後の短時間でのみ使用してください。 このファイルには、購入時にのみアクセスして使用する必要があります。  |
| defaultCurrency | string                        | この可用性に対してサポートされている既定の通貨です。                               |
| segment         | string                        | この可用性の業界セグメント。 サポートされている値は、商用、教育、政府、非営利です。 |
| country         | string                                              | この可用性が適用される国または地域 (ISO 国コード形式)。 |
| isPurchasable   | [bool]                                                | この可用性が購入可能なかどうかを示します。 |
| isRenewable 可能     | [bool]                                                | この可用性が更新可能かどうかを示します。 |
| product      | [梱包](#product)               | この可用性が対応する製品。 |
| sku          | [SKU](#sku)            | この可用性が対応する SKU。 |
| terms           | [用語](#term)リソースの配列  | この可用性に適用される用語のコレクション。 |
| リンク           | [ResourceLinks](utility-resources.md#resourcelinks) | 可用性に含まれるリソースリンク。 |

## <a name="term"></a>期間

可用性を購入できる用語を表します。

| プロパティ              | Type                                        | 説明                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| duration              | string                                      | 用語の期間の ISO 8601 表現。 現在サポートされている値は、P1M (1 か月)、P1Y (1 年)、および P3Y (3 年) です。 |
| description           | string                                      | 用語の説明。           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

特定のカタログアイテムに対して在庫を確認する要求を表します。

| プロパティ         | Type                                                | 説明                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | [InventoryItem](#inventoryitem)の配列            | インベントリチェックで評価されるカタログアイテムの一覧です。                           |
| inventoryContext | キーと値のペア                                     | 在庫チェックを実行するために必要なコンテキスト値のディクショナリ。 製品の各[SKU](#sku)は、この操作を実行するために必要な値 (存在する場合) を定義します。  |
| リンク            | [ResourceLinks](utility-resources.md#resourcelinks) | インベントリチェック要求内に含まれるリソースリンク。                            |

## <a name="inventoryitem"></a>InventoryItem

在庫確認操作の1つの項目を表します。 このリソースは、入力要求でターゲット項目を指定するために使用され、在庫確認操作の出力結果を表すためにも使用されます。

| プロパティ         | Type                                                              | 説明                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | string                                                            | 必要[製品](#product)の ID。                            |
| skuId            | string                                                            | [SKU](#sku)の ID。 このリソースを在庫要求への入力として使用する場合、この値は省略可能です。 この値が指定されていない場合、製品のすべての Sku が在庫確認操作のターゲット項目と見なされます。      |
| isRestricted     | [bool]                                                              | この項目が制限付きの在庫を持っていることが検出されたかどうかを示します。            |
| restrictions     | [InventoryRestriction](#inventoryrestriction)の配列            | この項目に対して検出された制限の詳細。 このプロパティは、 **Isrestricted** = "true" の場合にのみ設定されます。 |

## <a name="inventoryrestriction"></a>InventoryRestriction

在庫制限の詳細を表します。 これは、入力要求ではなく、在庫チェックの出力結果にのみ適用されます。

| プロパティ         | Type                  | 説明                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| 理由コード       | string                | 制限の理由を示すコード。                                    |
| description      | string                | 在庫制限の説明。                                               |
| properties       | キーと値のペア       | 制限の詳細を提供する可能性のあるプロパティのディクショナリ。           |

## <a name="billingcycletype"></a>BillingCycleType

請求サイクルの種類を示す値を持つ[列挙](https://docs.microsoft.com/dotnet/api/system.enum)型。

| 値              | [位置]     | [説明]                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Unknown            | 0            | 列挙型の初期化子です。                                                                          |
| 月 1 回            | 1            | パートナーが月単位で課金されることを示します。                                        |
| 年単位             | 2            | パートナーが毎年課金されることを示します。                                       |
| なし               | 3            | パートナーが課金されないことを示します。 この値は、試用版の項目に使用できます。    |
| OneTime            | 4            | パートナーに1回だけ課金されることを示します。                                       |
