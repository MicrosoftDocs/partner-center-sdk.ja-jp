---
title: アドレスを検証する
description: アドレス検証 API を使用してアドレスを検証する方法。
ms.assetid: 38A136CD-5E42-46D2-85A4-ED08E30444B8
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: aaa7e7ecb10b73a27ce6e406df95f1fe073d8f28
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487752"
---
# <a name="validate-an-address"></a>アドレスを検証する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

アドレス検証 API を使用してアドレスを検証する方法。

Address validation API は、顧客プロファイルの更新の事前検証にのみ使用してください。 国が米国、カナダ、中国、またはメキシコの場合、州フィールドはそれぞれの国の有効な州の一覧に対して検証されることを理解するために使用します。 他のすべての国では、このテストは行われず、API は状態が有効な文字列であることだけをチェックします。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件

「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

## <a name="span-idexamplesspan-idexamplesspan-idexamplesexamples"></a><span id="Examples"/><span id="examples"><span id="EXAMPLES"/>の例

### <a name="c"></a>C#

アドレスを検証するには、まず新しい**アドレス**オブジェクトをインスタンス化し、検証するアドレスをそのオブジェクトに設定します。 次に、 **iaggregatepartner.customers**プロパティから**検証**操作のためのインターフェイスを取得し、address オブジェクトを使用して**isaddressvalid**メソッドを呼び出します。

```csharp
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address()
{
    AddressLine1 = "One Microsoft Way",
    City = "Redmond",
    State = "WA",
    PostalCode = "98052",    
    Country = "US"
};

// Validate the address.
bool result = partnerOperations.Validations.IsAddressValid(address);

// If the address is valid, the result should equal true.
Console.WriteLine("Result: " + result.ToString());

// The following is an example that causes address validation to fail.
try
{
    // Change to an invalid postal code for this address.
    address.PostalCode = "98007";
             
    // Validate the address.
    result = partnerOperations.Validations.IsAddressValid(address);
    
    Console.WriteLine("ERROR: The code should have thrown an exception - BadRequest(400).");
}
catch (PartnerException exception)
{
    if (exception.ErrorCategory == PartnerErrorCategory.BadInput)
    {
        Console.WriteLine(exception.ErrorCategory.ToString());
        Console.WriteLine("Exception:");
        Console.WriteLine("Message: {0}", exception.Message);
    }
    else
    {
        throw;
    }
}
```

### <a name="java"></a>Java

アドレスを検証するには、まず新しい**アドレス**オブジェクトをインスタンス化し、検証するアドレスをそのオブジェクトに設定します。 次に、 **iaggregatepartner.customers**関数から**検証**操作のためのインターフェイスを取得し、address オブジェクトを使用して**isaddressvalid**メソッドを呼び出します。

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

```java
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address();

address.setAddressLine1("One Microsoft Way");
address.setCity("Redmond");
address.setState("WA");
address.setCountry("US");
address.setPostalCode("98052");

try
{
    // Validate the address
    Boolean validationResult = partnerOperations.getValidations().isAddressValid(address);

    System.out.println(validationResult ? "The address is valid." : "Invalid address");
}
catch (Exception exception)
{
    System.out.println("Address is invalid");
    
    if (! StringHelper.isNullOrWhiteSpace(exception.getMessage()))
    {
        System.out.println(exception.getMessage());
    }
}
```

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

アドレスを検証するには、アドレスパラメーターが設定された[**テストパートナーアドレス**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md)を実行します。

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求

**要求の構文**

| メソッド   | 要求 URI                                                                 |
|----------|-----------------------------------------------------------------------------|
| **投稿** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1 |

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

次の表では、要求本文に必要なプロパティについて説明します。

| 名前         | 種類   | 必須 | 説明                                                |
|--------------|--------|----------|------------------------------------------------------------|
| addressline1 | string | Y        | 住所の1行目。                             |
| addressline2 | string | N        | アドレスの2番目の行。 このプロパティは省略可能です。 |
| city         | string | Y        | 市区町村。                                                  |
| state        | string | Y        | 状態。                                                 |
| postalcode   | string | Y        | 郵便番号。                                           |
| country      | string | Y        | 2文字の ISO alpha 2 国コード。                |

**要求の例**

```http
POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Content-Type: application/json
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 129

{
    AddressLine1: "One Microsoft Way",
    City: "Redmond",
    State: "WA",
    PostalCode: "98052",
    Country: "US"
}
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答

成功した場合、メソッドは、次に示す応答検証成功の例に示すように、状態コード200を返します。

要求が失敗した場合、メソッドは、次に示す応答検証失敗の例に示すように状態コード400を返します。 応答本文には、エラーに関する追加情報を含む JSON ペイロードが含まれています。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

**応答-検証成功の例**

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

**応答-検証に失敗した例**

```http
HTTP/1.1 400 Bad Request
Content-Length: 418
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: pdlItMyvtkmGHDWt.0
MS-ServerId: 101112012
Date: Tue, 14 Mar 2017 01:57:55 GMT

{
    "code": 2007,
    "description": "{\"code\":\"60071\",\"reason\":\"ZipCityInvalid - Details: Field - &#39;City&#39; is corrected from OldValue: &#39;Redmond&#39; to NewValue: &#39;BELLEVUE&#39;.\",\"corrected_address\":{\"country\":\"US\",\"region\":\"WA\",\"city\":\"BELLEVUE\",\"address_line1\":\"One Microsoft Way\",\"postal_code\":\"98007\"},\"object_type\":\"AddressValidation\",\"resource_status\":\"Active\"}",
    "data": [],
    "source": "PartnerFD"
}
```