---
title: 検索クエリでサブスクリプション分析を取得する
description: 検索クエリでフィルター処理されたサブスクリプション分析情報を取得する方法。
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: d742dce1d9f3cb24da4da70281ca04b0030d87b2
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487262"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>検索クエリでフィルター処理されたサブスクリプション分析情報を取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


検索クエリでフィルター処理された顧客のサブスクリプション分析情報を取得する方法。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。


## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求の構文**

| メソッド | 要求 URI |
|--------|-------------|
| **取得** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions? filter = {filter_string} |

 

**URI パラメーター**

組織を識別し、検索をフィルター処理するには、次の必須パスパラメーターを使用します。

| 名前 | 種類 | 必須 | 説明 |
|------|------|----------|-------------|
| filter_string | string | 〇 | サブスクリプション分析に適用するフィルター。 このパラメーターで使用する構文、フィールド、および演算子については、フィルター構文とフィルターフィールドに関するセクションを参照してください。 |
 

**フィルター構文**

Filter パラメーターは、一連のフィールド、値、および演算子の組み合わせとして構成する必要があります。 And また**は or**演算子を使用して **、** 複数の組み合わせを組み合わせることができます。  

エンコード前の例は次のようになります。
- 文字列:? filter = フィールド演算子 ' Value '
- ブール値:? filter = フィールド演算子値
- Contains? filter = contains (フィールド、' value ')


**フィールドのフィルター**

要求のフィルターパラメーターには、応答内の行をフィルター処理する1つ以上のステートメントが含まれています。 各ステートメントには **eq** または **ne** 演算子と関連付けられるフィールドと値が含まれ、一部のフィールドでは **contains**、**gt**、**lt**、**ge**、および **le** 演算子もサポートします。 ステートメントは **、and**また**は or**演算子を使用して組み合わせることができます。

フィルター文字列の例を次に示します。  
 
```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```  

次の表に、フィルターパラメーターでサポートされているフィールドとサポートされる操作の一覧を示します。 文字列値は、単一引用符で囲む必要があります。

| パラメーター | サポートされている演算子 | 説明 |
|-----------|---------------------|-------------|
| 顧客 Tenantid | eq、ne | 顧客のテナントを識別する GUID 形式の文字列。 |
| おける | は | 顧客の名前。 |
| 顧客市場 | eq、ne | 顧客が事業を行っている国/地域。 |
| id | eq、ne | サブスクリプションを識別する GUID 形式の文字列。 |
| status | eq、ne | サブスクリプションの状態。 サポートされている値は、"ACTIVE"、"中断"、または "プロビジョニング解除" です。 |
| productName | contains、eq、ne | 製品の名前。 |
| subscriptionType | eq、ne | サブスクリプションの種類。 **注**: このフィールドでは大文字と小文字が区別されます。 サポートされている値は、"Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS" です。 |
| autoRenewEnabled | eq、ne | サブスクリプションが自動的に更新されるかどうかを示す値です。 |
| パートナー | eq、ne | MPN ID です。 ダイレクトリセラーの場合、これはパートナーの MPN ID になります。 間接リセラーの場合、これは間接リセラーの MPN ID になります。 |
| friendlyName | は | サブスクリプションの名前。 |
| partnerName | string | サブスクリプションが購入されたパートナーの名前 |  
| プロバイダー | string | 間接リセラーのサブスクリプショントランザクションの場合、プロバイダー名はサブスクリプションを購入した間接プロバイダーになります。
| creationDate | eq、ne、gt、lt、ge、le  | サブスクリプションが作成された日付。 |
| And rateplancharge.effectivestartdate | eq、ne、gt、lt、ge、le | サブスクリプションが開始された日付。 |
| Commitの Enddate | eq、ne、gt、lt、ge、le  | サブスクリプションが終了する日付。 |
| currentStateEndDate | eq、ne、gt、lt、ge、le | サブスクリプションの現在の状態が変更される日付。 |
| trialToPaidConversionDate | eq、ne、gt、lt、ge、le  | サブスクリプションが試用から有料に変換される日付。 既定値は null です。 |
| trialStartDate | eq、ne、gt、lt、ge、le | サブスクリプションの試用期間が開始された日付。 既定値は null です。 |
| Lastの終了日 | eq、ne、gt、lt、ge、le | サブスクリプションが最後に使用された日付。 既定値は null です。 |
| deprovisionedDate | eq、ne、gt、lt、ge、le | サブスクリプションがプロビジョニング解除された日付。 既定値は null です。 |
| lastRenewalDate | eq、ne、gt、lt、ge、le | サブスクリプションが最後に更新された日付。 既定値は null です。 |


**要求ヘッダー** 

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST 応答


成功した場合、応答本文には、フィルター条件を満たす[サブスクリプション](partner-center-analytics-resources.md#subscription)リソースのコレクションが含まれます。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

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

## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>関連項目

 - [パートナーセンター分析-リソース](partner-center-analytics-resources.md)
