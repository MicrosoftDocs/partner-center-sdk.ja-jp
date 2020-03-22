---
title: 請求書のリソース
description: 複数の請求書関連リソースは、パートナーセンター Api を通じて利用できます。 これらのリソースは、請求書と品目の詳細に関連しています。
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 6540af51e462974592ec18d7dd9ede8517ba1725
ms.sourcegitcommit: 07153b06dae146418ca5213c7e6fe1c869ba164d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083109"
---
# <a name="invoice-resources"></a>請求書のリソース

適用対象

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

次の請求関連リソースは、パートナーセンター Api を通じて入手できます。

## <a name="invoice"></a>請求書

| プロパティ | 種類 | 説明 |
| -------- | ---- | ----------- |
| id | string | 請求書の識別子。 |
| invoiceDate | UTC 日時形式の文字列 | 請求書が生成された日付。 |
| billingPeriodStartDate | UTC 日時形式の文字列 | 請求期間の開始日 (UTC)。 |
| billingPeriodEndDate | UTC 日時形式の文字列   | 請求期間の終了日 (UTC)。 |
| totalCharges | number | 合計料金。 トランザクションと調整の料金が含まれます。     |
| paidAmount | number  | パートナーが支払った金額。 支払いを受け取った場合は負の値です。  |
| currencyCode | string  | すべての請求書項目の金額と合計に使用される通貨を示すコード。 |
| currencySymbol  | string | すべての請求書項目の金額と合計に使用される通貨記号。 |
| pdfDownloadLink | string  | PDF 形式で請求書をダウンロードするためのリンク。 このリンクは検索結果の一部として返されず、ID で請求書にアクセスした場合にのみ設定されます。 このリンクは30分で自動有効期限が切れます。 |
| invoiceDetails  | [InvoiceDetail](#invoicedetail)オブジェクトの配列  | 請求書の詳細。  |
| 修正      | [Invoice](#invoice)オブジェクトの配列   | この請求書に対する修正。  |
| documentType    | string | 請求書のドキュメントの種類: "クレジットメモ"、"請求書"。 |
| amendsOf        | string | このドキュメントが適用されているドキュメントの参照番号。  |
| invoiceType     | string  | 請求書の種類。 "定期的に"、"1\_時間"。   |
| リンク           | [ResourceLinks](utility-resources.md#resourcelinks)  | リソースリンク。  |
| 属性      | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。  |

## <a name="invoicedetail"></a>InvoiceDetail

請求書には請求された項目のコレクションが含まれ、各項目は InvoiceDetail リソースによって表されます。

| プロパティ            | 種類                                                           | 説明                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | 請求書の詳細の種類は、"none"、"usage\_line\_items"、"billing\_line\_items" です。 |
| プロバイダ     | string                                                         | 課金プロバイダー: "none"、"office"、"azure"、または "azure\_data\_market"。         |
| リンク               | [ResourceLinks](utility-resources.md#resourcelinks)           | リソースリンク。                                                               |
| 属性          | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

請求書内の個々の料金は、InvoiceLineItem として表されます。

| プロパティ            | 種類                                                           | 説明                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | 請求書の品目の種類。 "none"、"usage\_line\_items"、"billing\_line\_items" と入力します。 |
| プロバイダ     | string                                                         | 課金プロバイダー: "none"、"office"、"azure"、または "azure\_data\_market"。            |
| 属性          | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

請求書の残高と合計料金の概要について説明します。

| プロパティ                 | 種類                                                           | 説明                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| 定率額            | number                                                         | 請求書の残高。 これは、未払いの請求額の合計です。 |
| currencyCode             | string                                                         | 残高の金額に使用する通貨を示すコード。       |
| currencySymbol           | string                                                         | 使用される通貨記号。                                             |
| アカウンティング日付           | UTC 日時形式の文字列                                 | 残高残量が最後に更新された日付。                         |
| firstInvoiceCreationDate | UTC 日時形式の文字列                                 | 顧客の最初の請求書が作成された日付。              |
| lastPaymentDate          | UTC 日時形式の文字列                                 | 前回の支払い日。                                         |
| lastPaymentAmount        | number                                                         | 前回の支払い額。                                       |
| latestInvoiceDate        | UTC 日時形式の文字列                                 | 顧客の最後の請求書が作成された日付。               |
| 詳細                  | [InvoiceSummaryDetail](#invoicesummarydetail)オブジェクトの配列 | 請求書の概要の詳細。                                           |
| リンク                    | [ResourceLinks](utility-resources.md#resourcelinks)            | リソースリンク。                                                   |
| 属性               | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

請求書の種類に関する個別の詳細の概要を表します (たとえば、定期的、1回の\_時間)。

| プロパティ            | 種類                                                           | 説明                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | string                                                         | 請求書の種類。 "定期的に"、"1\_時間"。                                       |
| summary             | [InvoiceSummary](#invoicesummary)オブジェクト                       | 請求書の種類ごとの請求書の概要。                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

通貨ごとの請求書の種類の個別の詳細を含む[InvoiceSummary](#invoicesummary)型のコレクションを表します。  

| プロパティ            | 種類                                                           | 説明                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | [InvoiceSummary](#invoicesummary)オブジェクトの配列             | 通貨ごとの請求書の種類ごとの請求書の概要。                            |

## <a name="licensebasedlineitem"></a>Licenseベースの Lineitem

ライセンスベースのサブスクリプションの請求書請求明細項目を表します。

| プロパティ                 | 種類                                                           | 説明                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| 時間                   | string                                                         | 合計金額を取得または設定します。 合計金額 = 単価 * 数量。  |
| 属性               | string                                                         | 属性を取得します。                                                  |
| billingCycleType         | string                                                         | 請求サイクルの種類を取得または設定します。                                  |
| プロバイダ          | string                                                         | 課金プロバイダーを取得します。                                            |
| chargeEndDate            | UTC 日時形式の文字列                                 | 料金の終了日を取得します。値の設定もできます。                             |
| chargeStartDate          | UTC 日時形式の文字列                                 | 料金の開始日を取得または設定します。                           |
| chargeType               | string                                                         | 課金の種類を取得します。値の設定もできます。                                      |
| 貨                 | string                                                         | この品目に使用する通貨を取得または設定します。                    |
| 顧客               | string                                                         | Microsoft 請求プラットフォームでの顧客の一意の識別子を取得または設定します。  |
| customerName             | UTC 日時形式の文字列                                 | 顧客名を取得または設定します。                                       |
| domainName               | string                                                         | ドメイン名を取得または設定します。                                             |
| durableOfferId           | string                                                         | 永続性オファーの一意の識別子を取得または設定します。                     |
| invoiceLineItemType      | string                                                         | 請求書の品目の種類を取得します。                                   |
| mpnId                    | number                                                         | この行項目に関連付けられている MPN ID を取得または設定します。 ダイレクトリセラーの場合、これはリセラーの MPN Id です。 間接リセラーの場合、これは付加価値再販業者 (VAR) の MPN ID です。                                   |
| offerId                  | string                                                         | オファーの一意の識別子を取得または設定します。                             |
| Context.offername                | string                                                         | プラン名を取得または設定します。                                          |
| orderId                  | string                                                         | 順序の一意識別子を取得または設定します。                             |
| パートナー                | string                                                         | パートナーの Azure active directory テナント ID を取得または設定します。            |
| quantity                 | number                                                         | この行項目に関連付けられている単位の数を取得または設定します。      |
| subscriptionDescription  | string                                                         | サブスクリプションの説明を取得します。値の設定もできます。                            |
| Subscription.subscriptionenddate      | UTC 日時形式の文字列                                 | サブスクリプションの有効期限が切れる日付を取得します。値の設定もできます。                      |
| subscriptionId           | string                                                         | サブスクリプションの一意の識別子を取得します。値の設定もできます。                      |
| subscriptionName         | string                                                         | サブスクリプション名を取得または設定します。                                   |
| And subscription.subscriptionstartdate    | UTC 日時形式の文字列                                 | サブスクリプションが開始される日付を取得します。値の設定もできます。                   |
| 小計                 | number                                                         | 割引後の金額を取得または設定します。                               |
| syndicationPartnerSubscriptionNumber | string                                             | 配信パートナーのサブスクリプション番号を取得します。値の設定もできます。             |
| 税金                      | number                                                         | 課金される税金を取得または設定します。                                       |
| tier2MpnId               | number                                                         | この品目に関連付けられている Tier 2 パートナーの MPN ID を取得します。値の設定もできます。 |
| totalForCustomer         | number                                                         | 割引と税金の後の合計金額を取得または設定します。                 |
| 割引率       | number                                                         | この購入に関連付けられている割引を取得または設定します。              |
| unitPrice                | number                                                         | 単価を取得または設定します。                                          |

## <a name="usagebasedlineitem"></a>その他の方法

使用状況に基づくサブスクリプションの請求書請求明細項目を表します。

| プロパティ                 | 種類                                                           | 説明                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| 属性               | string                                                         | 属性を取得します。                                                  |
| billingCycleType         | string                                                         | 請求サイクルの種類を取得または設定します。                                  |
| プロバイダ          | string                                                         | 課金プロバイダーを取得します。                                            |
| chargeEndDate            | UTC 日時形式の文字列                                 | 料金の終了日を取得します。値の設定もできます。                             |
| chargeStartDate          | UTC 日時形式の文字列                                 | 料金の開始日を取得または設定します。                           |
| chargeType               | string                                                         | 課金の種類を取得します。値の設定もできます。                                      |
| consumedQuantity         | number                                                         | 消費された合計単位を取得または設定します。                                |
| consumptionDiscount      | string                                                         | 使用量の割引を取得または設定します。                             |
| consumptionPrice         | string                                                         | 消費された数量の価格を取得または設定します。                          |
| 貨                 | string                                                         | 価格に関連付けられている通貨を取得または設定します。                 |
| customerName             | string                                                         | 顧客名を取得または設定します。                                       |
| 顧客               | string                                                         | 顧客の一意の識別子を取得または設定します。                          |
| すべての行の Itemid         | number                                                         | 詳細行項目 ID を取得または設定します。 使用された単位で計算が異なる場合に、行項目を一意に識別します。 例: 合計使用量 = 1338、1024は1つのレートで課金され、314は別のレートで課金されます。        |
| domainName               | string                                                         | ドメイン名を取得または設定します。                                             |
| includedQuantity         | number                                                         | 注文に含まれる単位を取得します。値の設定もできます。                         |
| invoiceLineItemType      | string                                                         | 請求書の品目の種類を取得します。                                   |
| invoiceNumber            | string                                                         | 請求書番号を取得または設定します。                                      |
| listPrice                | number                                                         | 各単位の価格を取得または設定します。                                  |
| mpnId                    | number                                                         | この行項目に関連付けられている MPN ID を取得または設定します。 ダイレクトリセラーの場合、これはリセラーの MPN ID です。 間接リセラーの場合、これは付加価値再販業者 (VAR) の MPN ID です。                                   |
| orderId                  | string                                                         | 順序の一意識別子を取得または設定します。                             |
| overageQuantity          | number                                                         | 許容される使用量を超えた場合に消費される数量を取得または設定します。               |
| Partnerの Lableaccountid | string                                                         | パートナーの課金対象アカウント ID を取得します。値の設定も可能です。                         |
| パートナー                | string                                                         | パートナーの Azure active directory テナント ID を取得または設定します。            |
| partnerName              | string                                                         | パートナーの名前を取得または設定します。                                      |
| postTaxEffectiveRate     | number                                                         | 税金後の有効価格を取得または設定します。                         |
| postTaxTotal             | number                                                         | 税金後の合計料金を取得または設定します。 税込みの料金と税金の金額 |
| preTaxCharges            | number                                                         | 税金の前に請求される価格を取得または設定します。                          |
| このように、      | number                                                         | 税金前の有効な価格を取得または設定します。                        |
| 領域 (region)                   | string                                                         | リソースインスタンスに関連付けられている領域を取得または設定します。        |
| resourceGuid             | string                                                         | リソース識別子を取得または設定します。                                 |
| resourceName             | string                                                         | リソース名を取得または設定します。 例: データベース (GB/月)。         |
| serviceName              | string                                                         | サービス名を取得または設定します。 例: Azure Data Service。           |
| serviceType              | string                                                         | サービスの種類を取得または設定します。 例: Azure SQL Azure DB。           |
| sku                      | string                                                         | サービス SKU を取得または設定します。                                         |
| subscriptionDescription  | string                                                         | サブスクリプションの説明を取得します。値の設定もできます。                            |
| subscriptionId           | string                                                         | サブスクリプションの一意の識別子を取得します。値の設定もできます。                      |
| subscriptionName         | string                                                         | サブスクリプション名を取得または設定します。                                   |
| taxAmount                | number                                                         | 課金される税金の量を取得または設定します。                               |
| tier2MpnId               | number                                                         | この品目に関連付けられている Tier 2 パートナーの MPN ID を取得します。値の設定もできます。 |
| unit                     | string                                                         | Azure の使用量の測定単位を取得または設定します。                     |

## <a name="invoicestatement"></a>InvoiceStatement

Application/pdf の invoice ステートメントで使用可能な操作を表します。

| プロパティ                 | 種類                                                           | 説明                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent と contentType = application/pdf。                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

ライセンスベースのサブスクリプションの請求書請求明細項目を表します。

| プロパティ | 種類 | 説明 |
| --- | --- | --- |
| PartnerId | string | パートナーのテナント ID を取得または設定します。 |
| CustomerId | string | 顧客のテナント ID を取得または設定します。 |
| CustomerName | string | 顧客名を取得または設定します。 |
| CustomerDomainName | string | 顧客のドメイン名を取得または設定します。 |
| CustomerCountry | string | 顧客の国を取得または設定します。 |
| InvoiceNumber | string | 請求書番号を取得または設定します。 |
| MpnId | string | この行項目に関連付けられている MPN ID を取得または設定します。 |
| ResellerMpnId | int | 順序の一意識別子を取得または設定します。 |
| OrderDate | DateTime | 注文が作成された日付を取得します。値の設定もできます。 |
| ProductId | string | 製品の一意識別子を取得します。値の設定もできます。 |
| SkuId | string | SKU の一意識別子を取得または設定します。 |
| AvailabilityId | string | 可用性の一意識別子を取得します。値の設定も可能です。 |
| ProductName | string | 製品名を取得または設定します。 |
| SkuName | string | SKU 名を取得または設定します。 |
| ChargeType | string | 課金の種類を取得します。値の設定もできます。 |
| UnitPrice | decimal | 単価を取得または設定します。 |
| EffectiveUnitPrice | decimal | 有効な単価を取得または設定します。 |
| Unittype.pixel 単位 | string | 単位の種類を取得または設定します。 |
| 数量 | int | この行項目に関連付けられている単位の数を取得または設定します。 |
| Subtotal | decimal | 割引後の金額を取得または設定します。 |
| TaxTotal | decimal | 課金される税金を取得または設定します。 |
| TotalForCustomer | decimal | 割引と税金の後の合計金額を取得または設定します。 |
| 通貨 | string | この品目に使用する通貨を取得または設定します。 |
| PublisherName | string | この購入に関連付けられている発行元の名前を取得または設定します。 |
| PublisherId | string | この購入に関連付けられている発行者 ID を取得または設定します。 |
| SubscriptionDescription | string | この購入に関連付けられているサブスクリプションの説明を取得または設定します。 |
| SubscriptionId | string | この購入に関連付けられているサブスクリプション ID を取得または設定します。 |
| ChargeStartDate | DateTime | この購入に関連付けられている料金の開始日を取得または設定します。 |
| ChargeEndDate | DateTime | この購入に関連付けられている料金の終了日を取得または設定します。 |
| Termandbilのサイクル | string | この購入に関連付けられている用語と請求サイクルを取得または設定します。 |
| 代替 id | string | 代替 ID (見積もり ID) を取得または設定します。 |
| PriceAdjustmentDescription | string | 価格調整の説明を取得または設定します。 |
| DiscountDetails | string |  **推奨されなくなった値**です。 この購入に関連付けられている割引の詳細を取得または設定します。 |
| PricingCurrency | string | 価格の通貨コードを取得または設定します。 |
| PCToBCExchangeRate | decimal | 請求通貨換算率の価格の通貨を取得または設定します。 |
| PCToBCExchangeRateDate | DateTime | 請求通貨換算レートの価格の通貨が決定された換算レートの日付を取得または設定します。 |
| 各販売数量 | decimal | 購入したユニットを取得します。値の設定もできます。 という名前の各デザイン列に対して、"/" という名前の列**があります**。 |
| MeterDescription | string | 消費明細項目のメーターの説明を取得または設定します。 |
| ReservationOrderId | string | Azure RI 購入の予約注文 id を取得します。値の設定もできます。 |
| Ic 周波数 | string | 請求頻度を取得または設定します。 |
| InvoiceLineItemType | InvoiceLineItemType | 請求書の品目の種類を返します。 |
| プロバイダ | プロバイダ | 課金プロバイダーを返します。 |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

日単位で評価された未請求を表します。

| プロパティ | 種類 | 説明 |
| --- | --- | --- |
| PartnerId | string | パートナーのテナント ID を取得または設定します。 |
| PartnerName | string | パートナー名を取得または設定します。 |
| CustomerId | string | 使用状況が属している顧客のテナント ID を取得または設定します。 |
| CustomerName | string | 使用状況が属している顧客会社の名前を取得または設定します。 |
| CustomerDomainName | string | 使用法が属している顧客のドメイン名を取得または設定します。 |
| InvoiceNumber | string | 使用法が属している請求書の ID を取得または設定します。 |
| ProductId | string | 製品の一意識別子を取得します。値の設定もできます。 |
| SkuId | string | SKU の一意識別子を取得または設定します。 |
| AvailabilityId | string | 可用性の一意識別子を取得します。値の設定も可能です。 |
| SkuName | string | サービスの SKU 名を取得または設定します。 |
| ProductName | string | 製品の名前を取得または設定します。 |
| PublisherName | string | パブリッシャーの名前を取得します。値の設定もできます。 |
| PublisherId | string | パブリッシャーの ID を取得します。値の設定もできます。 |
| SubscriptionId | string | サブスクリプション ID を取得または設定します。 |
| SubscriptionDescription | string | サブスクリプションの説明を取得します。値の設定もできます。 |
| ChargeStartDate | DateTime | 料金の開始日を取得または設定します。 |
| ChargeEndDate | DateTime | 料金の終了日を取得または設定します。 |
| UsageDate | DateTime | 使用日を取得または設定します。 |
| MeterType | string | メーターの種類を取得または設定します。 |
| MeterCategory | string | 測定カテゴリを取得または設定します。 |
| MeterId | string | メーター ID (GUID) を取得または設定します。 |
| MeterSubCategory カテゴリ | string | メーターサブカテゴリを取得または設定します。 |
| MeterName | string | メーターの名前を取得または設定します。 |
| MeterRegion | string | 測定領域を取得または設定します。 |
| UnitOfMeasure | string | 測定単位を取得または設定します。 |
| ResourceLocation | string | リソースの場所を取得または設定します。 |
| ConsumedService | string | 使用されたサービス名を取得または設定します。 |
| ResourceGroup | string | リソースグループの名前を取得または設定します。 |
| ResourceUri | string | 使用に関するリソースインスタンスの uri を取得または設定します。 |
| タグ | string | 顧客が追加したタグを取得または設定します。 |
| AdditionalInfo | string | サービス固有のメタデータを取得または設定します。 たとえば、仮想マシンのイメージの種類です。 |
| ServiceInfo1 | string | 内部の Azure サービスメタデータを取得または設定します。 |
| ServiceInfo2 | string | サービス情報を取得または設定します。たとえば、仮想マシンのイメージの種類と ExpressRoute の ISP 名を取得または設定します。 |
| CustomerCountry | string | 顧客の国を取得または設定します。 |
| MpnId | string | この行項目に関連付けられている MPN ID を取得または設定します。 |
| ResellerMpnId | string | この品目に関連付けられている Tier 2 パートナーの再販業者 MPN ID を取得します。値の設定もできます。 |
| ChargeType | string | 課金の種類を取得します。値の設定もできます。 |
| UnitPrice | decimal | ユニットの価格を取得します。値の設定もできます。 |
| 数量 | decimal | 使用量を取得または設定します。 |
| Unittype.pixel 単位 | string | 単位の種類 (1 時間など) を取得または設定します。 |
| すべての Lingpretaxtotal | decimal | 顧客または請求通貨の現地通貨での、税金前の延長コストまたは合計コストを取得または設定します。 |
| 通貨 | string | メートルが顧客または請求通貨の現地通貨で請求される ISO 通貨を取得または設定します。 |
| PricingPreTaxTotal | decimal | 評価に使用される米国ドルまたはカタログ通貨の税の前に、延長コストまたは合計コストを取得します。値の設定もできます。 |
| PricingCurrency | string | 測定に使用される米国ドルまたはカタログの通貨で測定される ISO 通貨を取得または設定します。 |
| entitlementId | string | 権利 (Azure サブスクリプション) ID を取得または設定します。 |
| EntitlementDescription | string | 権利 (Azure サブスクリプション) の説明を取得または設定します。 |
| PCToBCExchangeRate | string | 請求通貨換算率の価格の通貨を取得または設定します。 |
| PCToBCExchangeRateDate | DateTime | 請求通貨換算率の価格の通貨を取得または設定します。 |
| EffectiveUnitPrice | decimal | 有効な単価を取得または設定します。 |
| RateOfPartnerEarnedCredit | decimal | パートナー獲得クレジットの比率を取得または設定します。 |
| hasPartnerEarnedCredit | bool | パートナーの獲得クレジットが適用されることを取得または設定します。 |
| InvoiceLineItemType | InvoiceLineItemType | 請求書の品目の種類を返します。 |
| プロバイダ | プロバイダ | 課金プロバイダーを返します。 |
