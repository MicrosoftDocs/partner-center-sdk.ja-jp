---
title: すべてのサブスクリプション分析情報を取得する
description: すべてのサブスクリプション分析情報を取得する方法。
ms.assetid: 243E54BD-EA34-400E-B9AB-D735EB46B9F6
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a6b3d77dc23a0246d168979f754a3c1be5a2a02d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485852"
---
# <a name="get-all-subscription-analytics-information"></a>すべてのサブスクリプション分析情報を取得する

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

このトピックでは、顧客のすべてのサブスクリプション分析情報を取得する方法について説明します。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI |
|--------|-------------|
| **取得** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

次の表に、省略可能なパラメーターとその説明を示します。

| パラメーター | 種類 |  説明 |
|-----------|------|--------------|
| top | int | 要求で返すデータの行数です。 値が指定されていない場合、最大値と既定値は `10000`です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |
| skip | int | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、`top=10000` と `skip=0` では、最初の1万行のデータが取得され、`top=10000` と `skip=10000` データの次の1万行が取得されます。 |
| filter | string | 応答内の行をフィルター処理する 1 つまたは複数のステートメントです。 各フィルターステートメントには、応答本文のフィールド名と、 **eq**、 **ne**、特定のフィールドに関連付けられている値が含まれています、 **contains**演算子です。 **and** または **or** を使ってステートメントを組み合わせることができます。 **filter** パラメーターでは、文字列値を単一引用符で囲む必要があります。 フィルター処理できるフィールドと、それらのフィールドでサポートされている演算子の一覧については、次のセクションを参照してください。 |
| aggregationLevel | string | 集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。**day**、**week**、または **month**。 値が指定されていない場合、既定値は**dateRange**です。 このパラメーターは、日付フィールドが**groupBy**パラメーターの一部として渡された場合にのみ適用されます。 |
| groupBy | string | 指定したフィールドのみにデータ集計を適用するステートメントです。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

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

成功した場合、応答本文には[**サブスクリプション**](partner-center-analytics-resources.md#subscription)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

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

- [パートナーセンター分析-リソース](partner-center-analytics-resources.md)
