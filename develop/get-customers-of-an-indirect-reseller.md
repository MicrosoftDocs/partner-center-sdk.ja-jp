---
title: 間接リセラーの顧客を取得する
description: 間接リセラーの顧客の一覧を取得する方法。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: caf8a4ce707624672215e5b2a0c46659e0f9564b
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927083"
---
# <a name="get-customers-of-an-indirect-reseller"></a>間接リセラーの顧客を取得する

**適用対象**

- パートナー センター

間接リセラーの顧客の一覧を取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 間接リセラーのテナント識別子。

## <a name="c"></a>C\#

指定された間接リセラーとのリレーションシップを持つ顧客のコレクションを取得するには、まず、[**Simplefieldfilter**/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) オブジェクトをインスタンス化してフィルターを作成します。 文字列に変換された [/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield **]** 列挙型のメンバーを渡し、フィルター操作の種類として [**Fieldfilteroperation. StartsWith**/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation] を指定する必要があります。 また、間接リセラーのテナント id を指定してフィルター処理する必要もあります。

次に、[**Iquery**/dotnet/api/microsoft.store.partnercenter.models.query.iquery) オブジェクトをインスタンス化して、[**buildsimplequery**/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) メソッドを呼び出し、それにフィルターを渡してクエリに渡します。 BuildSimplyQuery は、[**Queryfactory**/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) クラスでサポートされているクエリの種類の1つにすぎません。

フィルターを実行して結果を取得するには、最初に [**iaggregatepartner.customers**/dotnet/api/microsoft.store.partnercenter.ipartner.customers) を使用して、パートナーの顧客の操作へのインターフェイスを取得します。 次に、[**Query**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) または [**QueryAsync**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) メソッドを呼び出します。

ページングされた結果を走査するための列挙子を作成するには、次のコードに示されているように、[**iaggregatepartner.customers**/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers] プロパティから customer collection enumerator factory インターフェイスを取得し、[**create**/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create] を呼び出します。次のコードに示すように、顧客のコレクションを保持する変数を渡します。

``` csharp
IAggregatePartner partnerOperations;
string indirectResellerId;

// Create a filter.
var filter = new SimpleFieldFilter(
    CustomerSearchField.IndirectReseller.ToString(),
    FieldFilterOperation.StartsWith,
    indirectResellerId);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(filter);

// Get the collection of matching customers.
var customersPage = partnerOperations.Customers.Query(myQuery);

// Create a customer enumerator for traversing the customer pages.
var customersEnumerator = partnerOperations.Enumerators.Customers.Create(customersPage);
int pageNumber = 1;

while (customersEnumerator.HasValue)
{
    // Work with the current page.
     foreach (var c in customersEnumerator.Current.Items)
    {
        // Display customer tenant identifier and company name.
        Console.WriteLine(string.Format("{0} - {1}.",c.Id,c.CompanyProfile.CompanyName));
    }
    // Get the next page of customers.
    customersEnumerator.Next();
}
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)**プロジェクト**: パートナーセンター SDK サンプル **クラス**: GetCustomersOfIndirectReseller.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers? size = {size}? filter = {FILTER} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

要求を作成するには、次のクエリパラメーターを使用します。

| 名前   | 種類   | 必須 | 説明                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| サイズ   | INT    | いいえ       | 一度に表示される結果の数。 このパラメーターは省略できます。                                                                                                                                                                                                                |
| filter | filter | Yes      | 検索をフィルター処理するクエリ。 指定された間接リセラーの顧客を取得するには、間接リセラー識別子を挿入し、次の文字列を含めてエンコードする必要があります: {"Field": "IndirectReseller 業者"、"Value": "{間接リセラー識別子}"、"Operator": " \_ で始まる"}。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example-encoded"></a>要求の例 (エンコード済み)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a>要求の例 (デコード済み)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文にはリセラーの顧客に関する情報が含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「 [パートナーセンターのエラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 2273
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: XI2/vIHmIEGVlGL9.0
MS-ServerId: 101112012
Date: Tue, 11 Apr 2017 23:31:28 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
            "companyProfile": {
                "tenantId": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                "domain": "FourthCoffee137.onmicrosoft.com",
                "companyName": "FourthCoffee137",
                "links": {
                    "self": {
                        "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
            "companyProfile": {
                "tenantId": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                "domain": "WingtipToys1254789149.onmicrosoft.com",
                "companyName": "Wingtip Toys1254789149",
                "links": {
                    "self": {
                        "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        },
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
