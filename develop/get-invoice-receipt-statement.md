---
title: 請求書の領収書の取得
description: 請求書 ID と受信確認 ID を使用して、請求書の領収書を取得します。
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 11549ad4de66d45f8375a6afb9956b2928c8045f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489522"
---
# <a name="get-invoice-receipt-statement"></a>請求書の領収書の取得

**適用対象**

- パートナー センター

請求書 ID と受信確認 ID を使用して、請求書の領収書を取得します。 

> [!IMPORTANT]
> この機能は、台湾の税金の領収書にのみ適用されます。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 有効な請求書 ID と対応する受信 ID。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#

ID で請求書の領収書を取得するには、Partner Center SDK v 1.12.0 以降を**使用して、** **ById ()** メソッドを請求書 ID を使用して呼び出してから、**領収**書のコレクションを呼び出し、 **ById (** ) メソッドを呼び出して、Invoice 受領書にアクセスするために**Documents ()** メソッドと**statement (** ) メソッドを呼び出します。 最後に、 **Get ()** メソッドまたは**GetAsync ()** メソッドを呼び出します。

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnersdk. FeatureSample**クラス**: GetInvoiceReceiptStatement.cs 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求

**要求の構文**

| メソッド  | 要求 URI                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1 |

**URI パラメーター**

次のクエリパラメーターを使用して、請求書の受領書を取得します。

| 名前       | 種類   | 必須 | 説明                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| 請求書-id | string | 〇      | 値は請求書 id で、リセラーは特定の請求書の結果をフィルター処理できます。 |
| 受領-id | string | 〇      | 値は、再販業者が特定の請求書の領収書をフィルター処理できるようにするための、受信確認 id です。 |
 
**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST 応答

成功した場合、このメソッドは応答本文で pdf ストリームを返します。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}  System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}  byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```
