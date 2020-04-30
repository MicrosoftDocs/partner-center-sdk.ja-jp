---
title: サブスクリプション分析を日付または使用条件でグループ化して取得する
description: サブスクリプション分析情報を日付または使用条件でグループ化して取得する方法。
ms.assetid: 5D0C0649-F64D-40A9-ACCC-2077E2D2BA4E
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 713dceb4c037918f2dfd7793659b70ae8ef3148b
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157224"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>サブスクリプション分析を日付または使用条件でグループ化して取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

顧客のサブスクリプション分析情報を日付または使用条件でグループ化して取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI |
|--------|-------------|
| **GET** | baseURL/partner/v1/analytics/subscriptions? groupby = {groupby_queries} [* \{\}*](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>URI パラメーター

組織を識別し、結果をグループ化するには、次の必須のパスパラメーターを使用します。

| 名前 | Type | 必須 | 説明 |
|------|------|----------|-------------|
| groupby_queries | 文字列と dateTime のペア | はい | 結果をフィルター処理するための用語と日付。 |

### <a name="groupby-syntax"></a>GroupBy 構文

Group by パラメーターは、一連のコンマ区切りのフィールド値として構成する必要があります。

エンコードされていない場合、 のようになります。

```http
?groupby=termField1,dateField1,termField2
```

次の表に、group by でサポートされているフィールドの一覧を示します。

| フィールド | Type | 説明 |
|-------|------|-------------|
| 顧客 Tenantid | string | 顧客のテナントを識別する GUID 形式の文字列。 |
| customerName | string | 顧客の名前。 |
| 顧客市場 | string | 顧客が事業を行っている国/地域。 |
| id | string | サブスクリプションを識別する GUID 形式の文字列。 |
| status | string | サブスクリプションのステータス。 サポートされている値は、"ACTIVE"、"中断"、または "プロビジョニング解除" です。 |
| productName | string | 製品の名前です。 |
| subscriptionType | string | サブスクリプションの種類。 注: このフィールドでは大文字と小文字が区別されます。 サポートされている値は、"Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS" です。 |
| autoRenewEnabled | Boolean | サブスクリプションが自動的に更新されるかどうかを示す値です。 |
| パートナー  | string | MPN ID です。 ダイレクトリセラーの場合、このパラメーターはパートナーの MPN ID になります。 間接リセラーの場合、このパラメーターは間接リセラーの MPN ID になります。 |
| friendlyName | string | サブスクリプションの名前です。 |
| partnerName | string | サブスクリプションが購入されたパートナーの名前 |
| providerName | string | 間接リセラーのサブスクリプショントランザクションの場合、プロバイダー名はサブスクリプションを購入した間接プロバイダーになります。
| creationDate | UTC 日時形式の文字列 | サブスクリプションが作成された日付。 |
| effectiveStartDate | UTC 日時形式の文字列 | サブスクリプションが開始された日付。 |
| Commitの Enddate | UTC 日時形式の文字列 | サブスクリプションが終了する日付。 |
| currentStateEndDate | UTC 日時形式の文字列 | サブスクリプションの現在の状態が変更される日付。 |
| trialToPaidConversionDate | UTC 日時形式の文字列 | サブスクリプションが試用から有料に変換される日付。 既定値は、null です。 |
| trialStartDate | UTC 日時形式の文字列 | サブスクリプションの試用期間が開始された日付。 既定値は、null です。 |
| Lastの終了日 | UTC 日時形式の文字列 | サブスクリプションが最後に使用された日付。 既定値は、null です。 |
| deprovisionedDate | UTC 日時形式の文字列 | サブスクリプションがプロビジョニング解除された日付。 既定値は、null です。 |
| lastRenewalDate | UTC 日時形式の文字列 | サブスクリプションが最後に更新された日付。 既定値は、null です。 |

### <a name="filter-fields"></a>フィルター フィールド

次の表に、オプションのフィルターフィールドとその説明を示します。

| フィールド | Type |  説明 |
|-------|------|--------------|
| top | INT | 要求で返すデータの行数です。 値が指定されていない場合、最大値と既定値は1万です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |
| skip | int | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、top = 10000 および skip = 0 はデータの最初の1万行を取得し、top = 10000、skip = 10000 は、次の1万行のデータを取得します。 |
| filter | string | 応答内の行をフィルター処理する 1 つまたは複数のステートメントです。 各フィルターステートメントには**`eq`**、 **`ne`** 応答本文からのフィールド名と、特定のフィールド ( **`contains`** 演算子) の、、またはに関連付けられている値が含まれています。 ステートメントは、または**`and`** **`or`** を使用して組み合わせることができます。 filter パラメーターでは、文字列値を単一引用符で囲む必要があります。 フィルター処理できるフィールドと、それらのフィールドでサポートされている演算子の一覧については、次のセクションを参照してください。 |
| aggregationLevel | string | 集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。**day**、**week**、または **month**。 値が指定されていない場合、既定値は**dateRange**です。 **注**: このパラメーターは、日付フィールドが groupBy パラメーターの一部として渡された場合にのみ適用されます。 |
| groupBy | string | 指定したフィールドのみにデータ集計を適用するステートメントです。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には、指定した用語と日付でグループ化された[サブスクリプション](partner-center-analytics-resources.md#subscription-resource)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a>関連項目

[パートナー センターの分析 - リソース](partner-center-analytics-resources.md)
