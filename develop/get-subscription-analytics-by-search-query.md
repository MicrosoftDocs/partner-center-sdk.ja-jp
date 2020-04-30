---
title: 検索クエリでサブスクリプション分析を取得する
description: 検索クエリでフィルター処理されたサブスクリプション分析情報を取得する方法。
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e93582b004429f1e15fb00e29e4e80e898c8846c
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157234"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>検索クエリでフィルター処理されたサブスクリプションの分析情報を取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

検索クエリでフィルター処理された顧客のサブスクリプション分析情報を取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI |
|--------|-------------|
| **GET** | baseURL/partner/v1/analytics/subscriptions? filter = {filter_string} [* \{\}*](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>URI パラメーター

組織を識別し、検索をフィルター処理するには、次の必須パスパラメーターを使用します。

| 名前 | Type | 必須 | 説明 |
|------|------|----------|-------------|
| filter_string | string | はい | サブスクリプション分析に適用するフィルター。 このパラメーターで使用する構文、フィールド、および演算子については、フィルター構文とフィルターフィールドに関するセクションを参照してください。 |

### <a name="filter-syntax"></a>フィルターの構文

Filter パラメーターは、一連のフィールド、値、および演算子の組み合わせとして構成する必要があります。 または演算子を使用し**`and`** て**`or`** 、複数の組み合わせを組み合わせることができます。

エンコードされていない場合、 のようになります。

- String: `?filter=Field operator 'Value'`
- ブール値: `?filter=Field operator Value`
- は`?filter=contains(field,'value')`

### <a name="filter-fields"></a>フィルター フィールド

要求の filter パラメーターには、応答内の行をフィルター処理する 1 つまたは複数のステートメントが含まれます。 各ステートメントに**`eq`** は、または**`ne`** 演算子に関連付けられているフィールドと値が含まれています。 **`contains`** 一部のフィールドでは、 **`gt`**、 **`lt`**、 **`ge`**、、 **`le`** および演算子もサポートされています。 ステートメントは、または**`and`** **`or`** 演算子を使用して組み合わせることができます。

フィルター文字列の例を次に示します。

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

次の表に、フィルターパラメーターでサポートされているフィールドとサポートされる操作の一覧を示します。 文字列値は、単一引用符で囲む必要があります。

| パラメーター | サポートされている演算子 | 説明 |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | サブスクリプションが自動的に更新されるかどうかを示す値です。 |
| Commitの Enddate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | サブスクリプションが終了する日付。 |
| creationDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | サブスクリプションが作成された日付。 |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | サブスクリプションの現在の状態が変更される日付。 |
| 顧客市場 | `eq`, `ne` | 顧客が事業を行っている国/地域。 |
| customerName | `contains` | 顧客の名前。 |
| 顧客 Tenantid | `eq`, `ne` | 顧客のテナントを識別する GUID 形式の文字列。 |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | サブスクリプションがプロビジョニング解除された日付。 既定値は、null です。 |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | サブスクリプションが開始された日付。 |
| friendlyName | `contains` | サブスクリプションの名前です。 |
| id | `eq`, `ne` | サブスクリプションを識別する GUID 形式の文字列。 |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | サブスクリプションが最後に更新された日付。 既定値は、null です。 |
| Lastの終了日 | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | サブスクリプションが最後に使用された日付。 既定値は、null です。 |
| パートナー | `eq`, `ne` | MPN ID です。 ダイレクトリセラーの場合、この値はパートナーの MPN ID になります。 間接リセラーの場合、この値は間接リセラーの MPN ID になります。 |
| partnerName | string | サブスクリプションが購入されたパートナーの名前 |
| productName | `contains`, `eq`, `ne` | 製品の名前です。 |
| providerName | string | 間接リセラーのサブスクリプショントランザクションの場合、プロバイダー名はサブスクリプションを購入した間接プロバイダーになります。|
| status | `eq`, `ne` | サブスクリプションのステータス。 サポートされている値は、"ACTIVE"、"中断"、または "プロビジョニング解除" です。 |
| subscriptionType | `eq`, `ne` | サブスクリプションの種類。 **注**: このフィールドでは大文字と小文字が区別されます。 サポートされている値は、"Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS" です。 |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | サブスクリプションの試用期間が開始された日付。 既定値は、null です。 |
| trialToPaidConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | サブスクリプションが試用から有料に変換される日付。 既定値は、null です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には、フィルター条件を満たす[サブスクリプション](partner-center-analytics-resources.md#subscription-resource)リソースのコレクションが含まれます。

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
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a>関連項目

- [パートナー センターの分析 - リソース](partner-center-analytics-resources.md)
