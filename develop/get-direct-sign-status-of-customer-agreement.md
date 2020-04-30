---
title: Microsoft カスタマーアグリーメントの顧客の直接署名の状態を取得します。
description: DirectSignedCustomerAgreementStatus リソースを使用して、Microsoft カスタマーアグリーメントの顧客の直接署名 (直接承諾) の状態を取得できます。
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f92e3d57438260af0b8e7beb12e9c7a4448eaf13
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157524"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Microsoft カスタマーアグリーメントの顧客の直接署名 (直接受け入れ) の状態を取得します。

**適用対象:**

- パートナー センター

**DirectSignedCustomerAgreementStatus**リソースは、現在、Microsoft パブリッククラウドのパートナーセンターでのみサポートされています。

このリソースは次のものには適用され*ません*。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

この記事では、お客様の Microsoft カスタマーアグリーメントの直接同意の状態を取得する方法について説明します。

## <a name="rest-request"></a>REST 要求

顧客の Microsoft カスタマーアグリーメントの直接同意の状態を取得するには、顧客の[DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md)を取得する REST 要求を作成します。

### <a name="request-syntax"></a>要求の構文

次の要求構文を使用します。

| Method | 要求 URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | baseURL/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1 [* \{\}*](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>URI パラメーター

要求では、次の URI パラメーターを使用できます。

| 名前             | Type | 必須 | 説明                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | はい | 値は、顧客のテナント ID を指定できるようにする GUID 形式の顧客**tenantid**です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で[ **DirectSignedCustomerAgreementStatus**リソース](./customer-agreement-direct-sign-status-resource.md)を返します。

リソースには、顧客の直接署名 (直接受け入れ) 状態を示す**Issigned**プロパティがあります。

- 値が**true**の場合は、アグリーメントが顧客によって直接署名 (承諾) されていることを示します。

- 値が**false**の場合は、アグリーメントが顧客によって直接署名 (受理) されて*いない*ことを示します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。

このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
