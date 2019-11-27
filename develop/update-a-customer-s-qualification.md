---
title: 顧客の資格を更新する
description: プロファイルに関連付けられているアドレスを含めて、顧客の資格を更新します。
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: f1faf509f67fa5dbb370acb9e0985a36810ed439
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486442"
---
# <a name="update-a-customers-qualification"></a>顧客の資格を更新する


**適用対象**

- パートナー センター

顧客の資格を更新します。

パートナーは、顧客の認定を "教育" または "GovernmentCommunityCloud" に更新できます。 その他の値 "None" と "非営利" は設定できません。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 顧客 ID (顧客-テナント id)。


## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#

顧客の認定を "教育" に更新するには、既存の[**顧客**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer?view=partnercenter-dotnet-latest)に対して **[update](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** を呼び出します。

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnersdk. FeatureSamples**クラス**: CustomerQualificationOperations.cs

お客様の資格を更新して、既存の顧客に限定なしで**GovernmentCommunityCloud**します。  パートナーには、顧客の[**Validationcode**](utility-resources.md#validationcode)を含める必要もあります。 
``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```


## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求

**要求の構文**

| メソッド  | 要求 URI                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **投入** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer_id}/修飾? code = {VALIDATIONCODE} HTTP/1.1 |


**URI パラメーター**

次のクエリパラメーターを使用して、修飾を更新します。

| 名前                   | 種類 | 必須 | 説明                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **顧客-テナント id** | GUID | 〇      | この値は、リセラーがリセラーに属する特定の顧客の結果をフィルター処理できるようにする GUID 形式の**顧客テナント id**です。 |
| **validationCode**     | int  | X       | 政府コミュニティクラウドにのみ必要です。                                                                                                            |


**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

[**顧客限定**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)列挙型からの整数値。

**要求の例**

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

3
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST 応答

成功した場合、このメソッドは応答本文で更新された[**修飾**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification)プロパティを返します。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-topics"></a>関連トピック

- [顧客の資格情報を取得する](get-a-customer-s-qualification.md)
- [パートナーの検証コードを取得する](get-a-partner-s-validation-codes.md)