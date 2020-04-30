---
title: 製品の一覧を取得する (国別)
description: 製品リソースを使用して、顧客の国別に製品のコレクションを取得することができます。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7427c3b3f28ac3cd6a2694fe90ac9024f913c749
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156904"
---
# <a name="get-a-list-of-products-by-country"></a>製品の一覧を取得する (国別)

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

次の方法を使用して、特定の国で利用可能な製品のコレクションを取得できます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 国。

## <a name="c"></a>C\#

製品の一覧を取得するには:

1. **Iaggregatepartner.customers**コレクションを使用して、 **bycountry ()** メソッドを使用して国を選択します。

2. **Bytargetview ()** メソッドを使用してカタログビューを選択します。

3. Optional**ByReservationScope ()** メソッドを使用して予約スコープを選択します。

4. Optional**Bytargetsegment ()** メソッドを使用してターゲットセグメントを選択します。

5. **Get ()** または**GetAsync ()** メソッドを呼び出して、コレクションを返します。

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

製品の一覧を取得するには:

1. **Bycountry ()** 関数を使用して国を選択するには、 **iaggregatepartner.customers**関数を使用します。

2. **Bytargetview ()** 関数を使用してカタログビューを選択します。
3. Optional**Bytargetsegment ()** 関数を使用してターゲットセグメントを選択します。

4. コレクションを返すには、 **get ()** 関数を呼び出します。

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

製品の一覧を取得するには:

1. [**Get PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)コマンドを実行します。

2. **カタログパラメーターを**指定してカタログを選択します。
3. Optional**セグメント**パラメーターを指定して、ターゲットセグメントを選択します。

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products? country = {country} &targetview = {targetview} &targetview = {TARGETVIEW} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

製品の一覧を取得するには、次のパスとクエリパラメーターを使用します。

| 名前                   | Type     | 必須 | Description                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | string   | はい      | 国/地域 ID。                                                  |
| targetView             | string   | はい      | カタログのターゲットビューを識別します。 サポートされる値は <ul><li>**Azure (すべて**の azure 項目を含む)</li><li>**AzureReservations**(すべての Azure 予約項目を含む)</li><li>**AzureReservationsVM**(すべての仮想マシン (VM) 予約項目を含む)</li><li>**AzureReservationsSQL**(すべての SQL 予約項目を含む)</li><li>**AzureReservationsCosmosDb**。すべての Cosmos データベース予約項目が含まれます。</li><li>**Microsoftazure.mobileengagement**: Microsoft Azure サブスクリプション (**0145p**) と Azure プランの項目が含まれています</li><li>すべてのオンラインサービス項目 (商用 marketplace 製品を含む) を含む**Onlineservices**</li><li>**ソフトウェア**。すべてのソフトウェア項目が含まれます。</li><li>**SoftwareSUSELinux**(すべてのソフトウェア SUSE Linux 項目を含む)</li><li>すべての永続ソフトウェア項目を含む、**永続的**なソフトウェア</li><li>すべて**のソフトウェアサブスクリプション項目**を含む software subscription</li></ul> |
| targetSegment          | string   | いいえ       | ターゲットセグメントを識別します。 さまざまな対象ユーザーのビュー。 サポートされる値は <ul><li>**迷惑**</li><li>**知識**</li><li>**官公庁**</li><li>**非営利**</li></ul> |
| reservationScope | string   | いいえ | Azure Reservations の製品の一覧を照会するときに、 `reservationScope=AzurePlan` Azure プランに適用可能な製品の一覧を取得するには、を指定します。 このパラメーターを除外すると、Microsoft Azure (**0145P**) サブスクリプションに適用される Azure 予約の製品の一覧を取得できます。  |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-examples"></a>要求の例

#### <a name="products-by-country"></a>国別の製品

次の例に従って、Microsoft Azure (MS AZR-0145P) サブスクリプションと Azure プランの国別製品の一覧を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Azure VM の予約 (Azure プラン)

次の例に従って、azure プランに適用可能な Azure VM 予約の国別製品の一覧を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure (MS-AZR-0145P) サブスクリプションの Azure VM 予約

次の例に従って、Microsoft Azure (0145P) サブスクリプションに適用される Azure VM 予約の国別製品の一覧を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[**製品**](product-resources.md#product)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード     | エラー コード   | 説明                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | 要求された targetSegment へのアクセスは許可されていません。                                                     |
| 403                  | 400036       | 要求された targetView へのアクセスは許可されていません。                                                        |

### <a name="response-example"></a>応答の例

```http
{
    "totalCount": 19,
    "items": [
        {
            "id": "DZH318Z0BQ3Q",
            "title": "Virtual Machines DSv2 Series",
            "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
            "productType": {
                "id": "Azure",
                "displayName": "Azure",
                "subType": {
                "id": "VirtualMachines",
                "displayName": "VirtualMachines"
                }
            },
            "isMicrosoftProduct": true,
            "publisherName": "Microsoft",
            "links": {
                "skus": {
                    "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
