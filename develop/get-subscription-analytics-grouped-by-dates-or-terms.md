---
title: サブスクリプション分析を日付または使用条件でグループ化して取得する
description: サブスクリプション分析情報を日付または使用条件でグループ化して取得する方法。
ms.assetid: 5D0C0649-F64D-40A9-ACCC-2077E2D2BA4E
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 15387d0cbf00917628a4f401094c23458e59064c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487162"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>サブスクリプション分析を日付または使用条件でグループ化して取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


顧客のサブスクリプション分析情報を日付または使用条件でグループ化して取得する方法。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。


## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求の構文**

| メソッド | 要求 URI |
|--------|-------------|
| **取得** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions? groupby = {groupby_queries} |

 
**URI パラメーター**

組織を識別し、結果をグループ化するには、次の必須のパスパラメーターを使用します。

| 名前 | 種類 | 必須 | 説明 |
|------|------|----------|-------------|
| groupby_queries | 文字列と dateTime のペア | 〇 | 結果をフィルター処理するための用語と日付。 |

 

**GroupBy 構文**

Group by パラメーターは、一連のコンマ区切りのフィールド値として構成する必要があります。

エンコード前の例は次のようになります。  

```http
?groupby=termField1,dateField1,termField2
```

次の表に、group by でサポートされているフィールドの一覧を示します。

| フィールド | 種類 | 説明 |
|-------|------|-------------|
| 顧客 Tenantid | string | 顧客のテナントを識別する GUID 形式の文字列。 |  
| おける | string | 顧客の名前。 |  
| 顧客市場 | string | 顧客が事業を行っている国/地域。 |  
| id | string | サブスクリプションを識別する GUID 形式の文字列。 |  
| status | string | サブスクリプションの状態。 サポートされている値は、"ACTIVE"、"中断"、または "プロビジョニング解除" です。 |  
| productName | string | 製品の名前。 |  
| subscriptionType | string | サブスクリプションの種類。 注: このフィールドでは大文字と小文字が区別されます。 サポートされている値は、"Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS" です。 |  
| autoRenewEnabled | ブール値 | サブスクリプションが自動的に更新されるかどうかを示す値です。 |  
| パートナー  | string | MPN ID です。 ダイレクトリセラーの場合、これはパートナーの MPN ID になります。 間接リセラーの場合、これは間接リセラーの MPN ID になります。 |  
| friendlyName | string | サブスクリプションの名前。 |  
| partnerName | string | サブスクリプションが購入されたパートナーの名前 |  
| プロバイダー | string | 間接リセラーのサブスクリプショントランザクションの場合、プロバイダー名はサブスクリプションを購入した間接プロバイダーになります。
| creationDate | UTC 日時形式の文字列 | サブスクリプションが作成された日付。 |  
| And rateplancharge.effectivestartdate | UTC 日時形式の文字列 | サブスクリプションが開始された日付。 |  
| Commitの Enddate | UTC 日時形式の文字列 | サブスクリプションが終了する日付。 |  
| currentStateEndDate | UTC 日時形式の文字列 | サブスクリプションの現在の状態が変更される日付。 |  
| trialToPaidConversionDate | UTC 日時形式の文字列 | サブスクリプションが試用から有料に変換される日付。 既定値は null です。 |  
| trialStartDate | UTC 日時形式の文字列 | サブスクリプションの試用期間が開始された日付。 既定値は null です。 |  
| Lastの終了日 | UTC 日時形式の文字列 | サブスクリプションが最後に使用された日付。 既定値は null です。 |  
| deprovisionedDate | UTC 日時形式の文字列 | サブスクリプションがプロビジョニング解除された日付。 既定値は null です。 |  
| lastRenewalDate | UTC 日時形式の文字列 | サブスクリプションが最後に更新された日付。 既定値は null です。 |  

**フィールドのフィルター**

次の表に、オプションのフィルターフィールドとその説明を示します。

| フィールド | 種類 |  説明 |
|-------|------|--------------|
| top | int | 要求で返すデータの行数です。 値が指定されていない場合、最大値と既定値は1万です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |
| skip | int | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、top = 10000 および skip = 0 はデータの最初の1万行を取得し、top = 10000、skip = 10000 は、次の1万行のデータを取得します。 |
| filter | string | 応答内の行をフィルター処理する 1 つまたは複数のステートメントです。 各フィルターステートメントには、応答本文のフィールド名と、 **eq**、 **ne**、特定のフィールドに関連付けられている値が含まれています、 **contains**演算子です。 **and** または **or** を使ってステートメントを組み合わせることができます。 文字列値は、フィルターパラメーターで単一引用符で囲む必要があります。 フィルター処理できるフィールドと、それらのフィールドでサポートされている演算子の一覧については、次のセクションを参照してください。 |
| aggregationLevel | string | 集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。**day**、**week**、または **month**。 値が指定されていない場合、既定値は**dateRange**です。 **注**: このパラメーターは、日付フィールドが groupBy パラメーターの一部として渡された場合にのみ適用されます。 |
| groupBy | string | 指定したフィールドのみにデータ集計を適用するステートメントです。 |


**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType  
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST 応答

成功した場合、応答本文には、指定した用語と日付でグループ化された[サブスクリプション](partner-center-analytics-resources.md#subscription)リソースのコレクションが含まれます。

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

## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>関連項目

 - [パートナーセンター分析-リソース](partner-center-analytics-resources.md)