---
title: 検索フィールドによってフィルター処理された顧客の一覧を取得する
description: フィルターに一致する顧客リソースのコレクションを取得します。 必要に応じてページサイズを設定することもできます。 フィルターを適用するには、会社名、ドメイン、間接リセラー、または間接クラウドソリューションプロバイダー (CSP) を使用します。
ms.assetid: 7D5D8C83-1DBD-4C54-8CDA-FE0CAC911D14
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: cd050514f49fbb867df117d2220d4f60f94e32b8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490122"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>検索フィールドによってフィルター処理された顧客の一覧を取得する


**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

フィルターに一致する[顧客](customer-resources.md#customer)リソースのコレクションを取得します。 必要に応じてページサイズを設定することもできます。 フィルターを適用するには、会社名、ドメイン、間接リセラー、または間接クラウドソリューションプロバイダー (CSP) を使用します。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- ユーザーが作成したフィルター。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


フィルターに一致する顧客のコレクションを取得するには、まず[**Simplefieldfilter**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter)オブジェクトをインスタンス化してフィルターを作成します。 [**顧客 Searchfield**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)を含む文字列を渡し、フィルター操作の種類を[**Fieldfilteroperation. StartsWith**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation)として指定する必要があります。 これは、顧客のエンドポイントでサポートされている唯一のフィールドフィルター操作です。 また、フィルター処理に使用する文字列も指定する必要があります。

次に、 [**Buildsimplequery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)メソッドを呼び出し、それにフィルターを渡すことによって、クエリに渡す[**iquery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.iquery)オブジェクトをインスタンス化します。 BuildSimplyQuery は、 [**Queryfactory**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)クラスでサポートされているクエリの種類の1つにすぎません。

最後に、フィルターを実行して結果を取得するには、最初に Iaggregatepartner.customers を使用して、パートナーの顧客の操作へのインターフェイスを取得し[**ます。** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) その後、 [**Query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query)または[**QueryAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)メソッドを呼び出します。

``` csharp
IAggregatePartner partnerOperations;

// Specify the partial string to filter by (to match Contoso).
string searchPrefix = "cont"  

// Create a simple field filter.
var fieldFilter = new SimpleFieldFilter(
    CustomerSearchField.CompanyName.ToString(),
    FieldFilterOperation.StartsWith,
    searchPrefix);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(fieldFilter);

// Get the collection of matching customers.
var customers = partnerOperations.Customers.Query(myQuery);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: FilterCustomers.cs

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求


**要求の構文**

| メソッド  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers? size = {size} & フィルター = {FILTER} HTTP/1.1 |

 

**URI パラメーター**

次のクエリパラメーターを使用します。

| 名前   | 種類   | 必須 | 説明                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| size   | int    | X       | 一度に表示される結果の数。 このパラメーターは省略可能です。 |
| filter | filter | 〇      | 顧客に適用するフィルター。 これは、エンコードされた文字列である必要があります。              |

 

**フィルター構文**

フィルターパラメーターは、コンマ区切りの一連のキーと値のペアとして構成する必要があります。 各キーと値は、個別に引用符で囲み、コロンで区切る必要があります。 フィルター全体をエンコードする必要があります。

エンコード前の例は次のようになります。

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```  
  
次の表では、必要なキーと値のペアについて説明します。

| Key      | Value                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| フィールド    | フィルター処理するフィールド。 有効な値は、 [ **"顧客の searchfield"** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)にあります。 |
| Value    | フィルター処理の対象となる値。 値の大文字と小文字の区別は無視されます。                                                                |
| 演算子 | 適用する演算子。 このお客様のシナリオでサポートされている唯一の値は、"開始\_" です。                            |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22CompanyName%22%2C%22Value%22%3A%22Cont%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5ce66de5-eea9-486f-a11c-c852aa3d1502
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST 応答


成功した場合、このメソッドは応答本文で一致する[顧客](customer-resources.md#customer)リソースのコレクションを返します。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 1839
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
MS-RequestId: dfeda56c-1af5-43fc-a9c0-346b9e85dc96
MS-CV: n0lMNyJtaUC802pO.0
MS-ServerId: 202010223
Date: Fri, 24 Feb 2017 22:08:20 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "c5757d70-06f3-4f23-8367-5a9e55019f94",
            "companyProfile": {
                "tenantId": "c5757d70-06f3-4f23-8367-5a9e55019f94",
                "domain": "contoso190.onmicrosoft.com",
                "companyName": "Contoso190",
                "links": {
                    "self": {
                        "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94/profiles/company",
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
                    "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
            "companyProfile": {
                "tenantId": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                "domain": "ContosoCorpCo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d/profiles/company",
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
                    "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
            "companyProfile": {
                "tenantId": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                "domain": "contosocorpdemo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b/profiles/company",
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
                    "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers?size=0&filter=%7B%22Field%22%3A%22Domain%22%2C%22Value%22%3A%22cont%22%2C%22Operator%22%3A%22starts_with%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




