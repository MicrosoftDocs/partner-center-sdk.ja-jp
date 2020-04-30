---
title: サブスクリプションの分析情報をすべて取得する
description: すべてのサブスクリプション分析情報を取得する方法。
ms.assetid: 243E54BD-EA34-400E-B9AB-D735EB46B9F6
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b0afac55646980fb59f9cc42051a5532f45bf223
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156444"
---
# <a name="get-all-subscription-analytics-information"></a>サブスクリプションの分析情報をすべて取得する

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

この記事では、お客様のすべてのサブスクリプション分析情報を取得する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI |
|--------|-------------|
| **GET** | baseURL/partner/v1/analytics/subscriptions HTTP/1.1 [* \{\}*](partner-center-rest-urls.md) |

#### <a name="uri-parameters"></a>URI パラメーター

次の表に、省略可能なパラメーターとその説明を示します。

| パラメーター | Type |  説明 |
|-----------|------|--------------|
| top | INT | 要求で返すデータの行数です。 値が指定されていない場合、最大値と既定`10000`値はになります。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |
| skip | int | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、と`top=10000` `skip=0`は、データの最初の1万行を`top=10000`取得`skip=10000`し、次の1万行のデータを取得します。 |
| filter | string | 応答内の行をフィルター処理する 1 つまたは複数のステートメントです。 各フィルターステートメントには**`eq`**、 **`ne`** 応答本文からのフィールド名と、特定のフィールド ( **`contains`** 演算子) の、、またはに関連付けられている値が含まれています。 ステートメントは、または**`and`** **`or`** を使用して組み合わせることができます。 **filter** パラメーターでは、文字列値を単一引用符で囲む必要があります。 フィルター処理できるフィールドと、それらのフィールドでサポートされている演算子の一覧については、次のセクションを参照してください。 |
| aggregationLevel | string | 集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。**day**、**week**、または **month**。 値が指定されていない場合、既定値は**dateRange**です。 このパラメーターは、日付フィールドが**groupBy**パラメーターの一部として渡された場合にのみ適用されます。 |
| groupBy | string | 指定したフィールドのみにデータ集計を適用するステートメントです。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[**サブスクリプション**](partner-center-analytics-resources.md#subscription-resource)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a>関連項目

- [パートナー センターの分析 - リソース](partner-center-analytics-resources.md)
