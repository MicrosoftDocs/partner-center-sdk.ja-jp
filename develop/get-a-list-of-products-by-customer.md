---
title: 製品の一覧を取得する (顧客別)
description: 顧客識別子を使用して、顧客別に製品のコレクションを取得することができます。
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 2141de3cd52f4e270b6668321d7736f33b578b3c
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412292"
---
# <a name="get-a-list-of-products-by-customer"></a>製品の一覧を取得する (顧客別)

適用対象

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

次の方法を使用して、既存の顧客の製品のコレクションを取得できます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客 ID (**customer-tenant-id**)。

## <a name="rest"></a>REST

### <a name="rest-request"></a>Rest 要求

#### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/V1/customers/{customer-tenant-id}/products? targetview = {targetview} HTTP/1.1 |

#### <a name="request-uri-parameters"></a>要求 URI パラメーター

| Name               | 種類 | 必須 | 説明                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **顧客-テナント id** | GUID | はい | この値は、顧客を指定できるようにする識別子である、GUID 形式の **customer-tenant-id** です。 |
| **targetView** | string | はい | カタログのターゲットビューを識別します。 サポートされている値は次のとおりです。 <ul><li>**Azure (すべて**の azure 項目を含む)</li><li>**AzureReservations**(すべての Azure 予約項目を含む)</li><li>**AzureReservationsVM**(すべての仮想マシン (VM) 予約項目を含む)</li><li>**AzureReservationsSQL**(すべての SQL 予約項目を含む)</li><li>**AzureReservationsCosmosDb**。すべての Cosmos データベース予約項目が含まれます。</li><li>**Microsoftazure.mobileengagement**: Microsoft Azure サブスクリプション (**0145p**) と Azure プランの項目が含まれています</li><li>オンラインサービスのすべての項目 (商用 marketplace 製品を含む) を含む**Onlineservices**</li><li>**ソフトウェア**。すべてのソフトウェア項目が含まれます。</li><li>**SoftwareSUSELinux**(すべてのソフトウェア SUSE Linux 項目を含む)</li><li>すべての永続ソフトウェア項目を含む、**永続的**なソフトウェア</li><li>すべて**のソフトウェアサブスクリプション項目**を含む software subscription </ul> |

#### <a name="request-header"></a>要求ヘッダー

詳細については、「[ヘッダー](headers.md)」を参照してください。

#### <a name="request-body"></a>[要求本文]

[なし]。

#### <a name="request-example"></a>要求の例

特定の顧客が使用できる Azure 使用量ベースの製品の一覧を要求します。 パブリッククラウドのお客様については、Microsoft Azure (0145P) と Azure プランの両方の製品が返されます。

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

### <a name="rest-response"></a>Rest 応答

#### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード | エラー コード   | 説明                     |
|------------------|--------------|---------------------------------|
| 403 | 400036 | 要求された targetView へのアクセスは許可されていません。 | 

#### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
 
{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0001",
            "productId": "DZH318Z0BPS6",
            "title": "Microsoft Azure plan",
            "description": "Microsoft Azure plan (MS-AZR-0017G)",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "MicrosoftCustomerAgreement"
            ],
            "inventoryVariables": [],
            "provisioningVariables": [],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "pilotProgram": "modernazurepilot"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
