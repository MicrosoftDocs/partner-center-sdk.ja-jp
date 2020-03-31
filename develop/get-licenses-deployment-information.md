---
title: ライセンスの取得の展開情報
description: Office と Dynamics のライセンスのデプロイ情報を取得する方法について説明します。
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: ad91b8082315e5c35ae43e70b44b94f5a948938b
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415764"
---
# <a name="get-licenses-deployment-information"></a>ライセンスの取得の展開情報

**適用対象**

- Partner Center

Office と Dynamics のライセンスのデプロイ情報を取得する方法について説明します。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


[パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証がサポートされます。


## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求

**要求の構文**

| メソッド  | 要求 URI                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/HTTP/1.1 |

 
**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。  

**URI パラメーター**

| パラメーター         | 種類     | 説明 | 必須 |  
|-------------------|----------|-------------|----------|  
| [top]               | string   | 要求で返すデータの行数です。 最大値および指定しない場合の既定値は 10000 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 | いいえ | 
| skip              | int      | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、top=10000 と skip=0 を指定すると、データの最初の 10,000 行が取得され、top=10000 と skip=10000 を指定すると、データの次の 10,000 行が取得されます。 | いいえ | 
| フィルター            | string   | <p>要求の <em>filter</em> パラメーターには、応答内の行をフィルター処理する 1 つまたは複数のステートメントが含まれます。 各ステートメントには **eq** 演算子または **ne** 演算子と関連付けられるフィールドと値が含まれ、**and** または **or** を使ってステートメントを組み合わせることができます。 <em>filter</em> パラメーターの例を次に示します。</p><ul><li><em>filter = serviceCode eq ' O365 '</em></li><li><em>filter = serviceCode eq ' O365 '</em>または (<em>Channel eq ' リセラー '</em>)</li></ul><p>次のフィールドを指定できます。</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>チャンネル</strong></li><li><strong>顧客 Tenantid</strong></li><li><strong>おける</strong></li><li><strong>Id</strong></li><li><strong>同様</strong></li></ul> | いいえ | 
| groupby           | string   | <p>指定したフィールドのみにデータ集計を適用するステートメントです。 次のフィールドを指定できます。</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>チャンネル</strong></li><li><strong>顧客 Tenantid</strong></li><li><strong>おける</strong></li><li><strong>Id</strong></li><li><strong>同様</strong></li></ul><p>返されるデータ行には、<em>groupby</em> パラメーターに指定したフィールドと次の値が含まれます。</p><ul><li><strong>licensesDeployed</strong></li><li><strong>licensesSold</strong></li></ul> | いいえ | 
| processedDateTime | DateTime | 使用状況データが処理された日付を指定できます。 データが処理された最新の日付を既定値に設定します。 | いいえ | 


**要求の例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```


## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答

成功した場合、応答本文には、デプロイされたライセンスに関するデータを含む次のフィールドが含まれます。

| フィールド             | 種類     | 説明                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | string   | サービスコード                          |
| serviceName       | string   | [サービス名]                          |
| channel           | string   | チャネル名、リセラー                |
| 顧客 Tenantid  | string   | 顧客の一意の識別子    |
| customerName      | string   | Customer name                         |
| productId         | string   | 製品の一意識別子     |
| productName       | string   | 製品名                          |
| licensesDeployed  | long     | 展開されたライセンスの数           |
| licensesSold      | long     | 販売済みライセンス数               |
| processedDateTime | DateTime | データが最後に処理された日付 |



**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK 
Content-Length: 487 
Content-Type: application/json; charset=utf-8 
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9 
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da 
MS-CV: f0trvmq8mEScHcFS.0 
MS-ServerId: 4 
Date: Wed, 24 Oct 2018 22:37:18 GMT
{
  "Value": [
   
{
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```