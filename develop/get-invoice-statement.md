---
title: 請求書明細書の取得
description: 請求書 ID を使用して請求書明細書を取得します。
ms.assetid: 60EAA1F1-AFE2-4FC3-A475-4DBEA58583D1
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 754db08297e7a3205441705ff24a23fc0de3e240
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489372"
---
# <a name="get-invoice-statement"></a>請求書明細書の取得

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

請求書 ID を使用して請求書明細書を取得します。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 有効な請求書 ID。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


ID で請求書明細書を取得するには、 **ById ()** メソッドを使用**して請求**書 id を使用し、**ドキュメント ()** および**ステートメント ()** メソッドを呼び出して、invoice ステートメントにアクセスします。 最後に、 **Get ()** メソッドまたは**GetAsync ()** メソッドを呼び出します。

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnersdk. FeatureSample**クラス**: GetInvoiceStatement.cs 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求の構文**

| メソッド  | 要求 URI                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1  |


**URI パラメーター**

次のクエリパラメーターを使用して、invoice ステートメントを取得します。

| 名前       | 種類       | 必須 | 説明                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| 請求書-id | string     | 〇      | 値は請求書 id で、リセラーは特定の請求書の結果をフィルター処理できます。 |

 

**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST 応答


成功した場合、このメソッドは応答本文で[InvoiceStatement](invoice-resources.md#invoicestatement)リソースを返します。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}  System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}  byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```