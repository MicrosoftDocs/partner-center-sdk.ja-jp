---
title: 製品の一覧を取得する (国別)
description: 製品リソースを使用して、顧客の国別に製品のコレクションを取得することができます。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 4f3f00db59fa06769a581fca6ea028bc94f61883
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487322"
---
# <a name="get-a-list-of-products-by-country"></a>製品の一覧を取得する (国別)

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

次の方法を使用して、特定の国で利用可能な製品のコレクションを取得できます。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 国。

## <a name="c"></a>C\#

製品の一覧を取得するには:

1. **Iaggregatepartner.customers**コレクションを使用して、 **bycountry ()** メソッドを使用して国を選択します。
2. **Bytargetview ()** メソッドを使用してカタログビューを選択します。
3. Optional**ByReservationScope ()** メソッドを使用して予約スコープを選択します。
3. Optional**Bytargetsegment ()** メソッドを使用してターゲットセグメントを選択します。
4. **Get ()** または**GetAsync ()** メソッドを呼び出して、コレクションを返します。

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

### <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

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

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

製品の一覧を取得するには:

1. [**Get PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)コマンドを実行します。
2. **カタログパラメーターを**指定してカタログを選択します。
3. Optional**セグメント**パラメーターを指定して、ターゲットセグメントを選択します。

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest"></a>休息

### <a name="rest-request"></a>Rest 要求

#### <a name="request-syntax"></a>要求の構文

| メソッド  | 要求 URI                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/products? country = {country} & targetview = {targetview} & targetview = {TARGETVIEW} HTTP/1.1 |

##### <a name="uri-parameters"></a>URI パラメーター

製品の一覧を取得するには、次のパスとクエリパラメーターを使用します。

| 名前                   | 種類     | 必須 | 説明                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | string   | 〇      | 国/地域 ID。                                                  |
| targetView             | string   | 〇      | カタログのターゲットビューを識別します。 サポートされている値は次のとおりです。 <ul><li>**Azure (すべて**の azure 項目を含む)</li><li>**AzureReservations**(すべての Azure 予約項目を含む)</li><li>**AzureReservationsVM**(すべての仮想マシン (VM) 予約項目を含む)</li><li>**AzureReservationsSQL**(すべての SQL 予約項目を含む)</li><li>**AzureReservationsCosmosDb**。すべての Cosmos データベース予約項目が含まれます。</li><li>**Microsoftazure.mobileengagement**: Microsoft Azure サブスクリプション (**0145p**) と Azure プランの項目が含まれています</li><li>すべてのオンラインサービス項目 (商用 marketplace 製品を含む) を含む**Onlineservices**</li><li>**ソフトウェア**。すべてのソフトウェア項目が含まれます。</li><li>**SoftwareSUSELinux**(すべてのソフトウェア SUSE Linux 項目を含む)</li><li>すべての永続ソフトウェア項目を含む、**永続的**なソフトウェア</li><li>すべて**のソフトウェアサブスクリプション項目**を含む software subscription</li></ul> |
| targetSegment          | string   | X       | ターゲットセグメントを識別します。 さまざまな対象ユーザーのビュー。 サポートされている値は次のとおりです。 <ul><li>**迷惑**</li><li>**知識**</li><li>**官公庁**</li><li>**非営利**</li></ul> |
| reservationScope | string   | X | Azure Reservations の製品の一覧を照会する場合は、`reservationScope=AzurePlan` を指定して、Azure プランに適用可能な製品の一覧を取得します。 このパラメーターを除外すると、Microsoft Azure (**0145P**) サブスクリプションに適用される Azure 予約の製品の一覧を取得できます。  |

#### <a name="request-headers"></a>要求ヘッダー

詳細については、「[ヘッダー](headers.md)」を参照してください。

#### <a name="request-body"></a>要求本文

なし。

#### <a name="request-examples"></a>要求の例

##### <a name="products-by-country"></a>国別の製品

次の例に従って、Microsoft Azure (MS AZR-0145P) サブスクリプションと Azure プランの国別製品の一覧を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

##### <a name="azure-vm-reservations-azure-plan"></a>Azure VM の予約 (Azure プラン)

次の例に従って、azure プランに適用可能な Azure VM 予約の国別製品の一覧を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

##### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure (MS-AZR-0145P) サブスクリプションの Azure VM 予約

次の例に従って、Microsoft Azure (0145P) サブスクリプションに適用される Azure VM 予約の国別製品の一覧を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

### <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[**製品**](product-resources.md#product)リソースのコレクションが含まれます。

#### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード     | エラー コード   | 説明                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | 要求された targetSegment へのアクセスは許可されていません。                                                     |
| 403                  | 400036       | 要求された targetView へのアクセスは許可されていません。                                                        |

#### <a name="response-example"></a>応答の例

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
