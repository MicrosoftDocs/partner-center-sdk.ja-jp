---
title: 顧客の資格情報を更新する
description: プロファイルに関連付けられているアドレスを含めて、顧客の資格を更新します。
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 3cc486cc2f81f5708bf4b5d876bfd9bb74800365
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925592"
---
# <a name="update-a-customers-qualification"></a>顧客の資格情報を更新する

**適用対象**

- パートナー センター

顧客の資格を更新します。

パートナーは、顧客の認定を "教育" または "GovernmentCommunityCloud" に更新できます。 その他の値 "None" と "非営利" は設定できません。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウントページで、[**お客様のアカウント情報**] セクションで**Microsoft ID**を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="c"></a>C\#

顧客の認定を "教育" に更新するには、既存の [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer (**顧客**) に対して **[update/dotnet/api/icustomerqualification** ] を呼び出します。

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnersdk. FeatureSamples **クラス**: CustomerQualificationOperations.cs

お客様の資格を更新して、既存の顧客に限定なしで **GovernmentCommunityCloud** します。  パートナーには、顧客の [**Validationcode**](utility-resources.md#validationcode)を含める必要もあります。

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/修飾? code = {VALIDATIONCODE} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、修飾を更新します。

| 名前                   | 種類 | 必須 | 説明                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | GUID | はい      | この値は、リセラーがリセラーに属する特定の顧客の結果をフィルター処理できるようにする GUID 形式の **顧客テナント id** です。 |
| **validationCode**     | INT  | いいえ       | 政府コミュニティクラウドにのみ必要です。                                                                                                            |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[**顧客限定**/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) 列挙型の整数値。

### <a name="request-example"></a>要求の例

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で更新された [**修飾**/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification] プロパティを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a>関連記事

- [顧客の資格情報を取得する](get-a-customer-s-qualification.md)
- [パートナーの確認コードを取得する](get-a-partner-s-validation-codes.md)
