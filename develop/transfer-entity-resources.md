---
title: TransferEntity リソース
description: パートナーは、顧客がパートナーとのサブスクリプションを別のパートナーに譲渡する必要がある場合に、転送を作成します。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0a9a357d9f2fd90069df0b39427e32fe25dc16af
ms.sourcegitcommit: e39e8dccf25020cccda8bcea83b72e7ef8a6a7c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84489169"
---
# <a name="transferentity-resources"></a>TransferEntity リソース

**適用対象:**

- パートナー センター

パートナーは、顧客がパートナーとのサブスクリプションを別のパートナーに譲渡する必要がある場合に、転送を作成します。

## <a name="transferentity"></a>TransferEntity

TransferEntity について説明します。

| プロパティ              | Type             | 説明                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | string           | TransferEntity が正常に作成されたときに提供される transferEntity 識別子。                               |
| createdTime           | DateTime         | TransferEntity が作成された日付 (日付/時刻形式)。 TransferEntity の作成が正常に完了したときに適用されます。      |
| lastModifiedTime      | DateTime         | TransferEntity が最後に更新された日付 (日付/時刻形式)。 TransferEntity の作成が正常に完了したときに適用されます。 |
| lastModifiedUser      | string           | TransferEntity を最後に更新したユーザー。 TransferEntity の作成が正常に完了したときに適用されます。                          |
| customerName          | string           | 省略可能。 サブスクリプションを転送する顧客の名前。                                              |
| 顧客 Tenantid      | string           | 顧客を識別する GUID 形式の顧客 id。 TransferEntity の作成が正常に完了したときに適用されます。         |
| partnertenantid       | string           | パートナーを識別する GUID 形式のパートナー id。                                                                   |
| sourcePartnerName     | string           | 省略可能。 譲渡を開始するパートナー組織の名前。                                           |
| sourcePartnerTenantId | string           | 転送を開始するパートナーを識別する GUID 形式のパートナー id。                                           |
| targetPartnerName     | string           | 省略可能。 譲渡の対象となるパートナーの組織の名前。                                         |
| targetPartnerTenantId | string           | 転送の対象となるパートナーを識別する GUID 形式のパートナー id。                                  |
| lineItems             | オブジェクトの配列 | [Transferlineitem](#transferlineitem)リソースの配列。                                                   |
| status                | string           | TransferEntity の状態。 有効な値は、"アクティブ" (削除/送信可能) および "完了" (既に完了している) です。 TransferEntity の作成が正常に完了したときに適用されます。|

## <a name="transferlineitem"></a>TransferLineItem

TransferEntity に含まれる1つの項目を表します。

| プロパティ             | Type                             | 説明                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | string                           | 転送明細項目の一意の識別子。 TransferEntity の作成が正常に完了したときに適用されます。   |
| subscriptionId       | string                           | サブスクリプションの識別子です。                                                                            |
| 数量             | INT                              | ライセンスまたはインスタンスの数。                                                                    |
| billingCycle         | Object                           | 現在の期間に設定されている請求サイクルの種類。                                                   |
| friendlyName         | string                           | 省略可能。 明確に区別できるように、パートナーによって定義された項目のフレンドリ名。                   |
| partnerIdOnRecord    | string                           | 転送が受け入れられたときに発生する、購入時の PartnerId (MPNID)。                 |
| offerId              | string                           | プラン ID。    |
| addonItems           | **Transferlineitem**オブジェクトの一覧 | 転送されるベースサブスクリプションと共に転送されるアドオンの transferEntity 行項目のコレクション。 TransferEntity の作成が正常に完了したときに適用されます。|
| transferError        | string                           | エラーが発生した場合に transferEntity が受け入れられた後に適用されます。                |
| status               | string           | TransferEntity 内の lineitem の状態。|

## <a name="transfersubmitresult"></a>TransferSubmitResult

転送の受け入れの結果を表します。

| プロパティ          | Type                                                  | Description                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| 注文            | [Order](order-resources.md#order)オブジェクトのリスト。    | 注文のコレクションです。          |
| transferErrors    | [Transfererror](#transfererror)オブジェクトの一覧。      | 転送エラーのコレクションです。 |

## <a name="transfererror"></a>TransferError

転送が受け入れられたときに発生するエラーを表します。

| プロパティ          | Type   | Description                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | string | 注文の注文グループ ID をエラーと共に使用します。 |
| code              | INT    | エラー コード。                                 |
| description       | string | エラーの説明。                   |
| lineItems         | **Transferlineitem**オブジェクトの一覧 | 転送エラーの一部である transferEntity の品目のコレクション。|

## <a name="transfererrorcode"></a>TransferErrorCode

注文エラーの種類を示す値を持つ[列挙](https://docs.microsoft.com/dotnet/api/system.enum)です。

| 値 | 位置 | Description |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | 要求コンテキストにパートナートークンがありません。 |
| InvalidInput | 800002 | 要求の入力が無効です。 |
| ServiceException | 800003 | 予期しないサービスエラーです。 |
| InvalidOfferId | 800004 | オファー ID が無効です。 |
| CreateOrderError | 800005 | 注文の作成に失敗しました。 |
| MpnIdNotFound | 800015 | MPN Id が見つかりません。 |
| NotValidIndirectResellerMpnId | 800016 | MPN Id は、有効な間接リセラーではありません。 |
| TransferIdNotFound | 900100   | 転送要求が見つかりませんでした。   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | 転送要求は既に進行中です。|
| TransferNotAllowedIfStatusIsCompleted | 900102 | 転送要求は既に完了しています。|
| TransferCreateOrderError | 900103 | 転送順序が正しくありません。|
| TransferProcessedByAnotherRequest | 900104 | 転送は別の要求によって処理されています。|