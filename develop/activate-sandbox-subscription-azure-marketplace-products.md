---
title: 商用マーケットプレース製品のサンドボックス サブスクリプションをアクティブ化する
description: 商用 marketplace 製品のサンドボックスサブスクリプションをアクティブ化します。
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f7b6edef3984b64f04bdbec1f02218a4a84ca04e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095245"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-products"></a>商用マーケットプレース製品のサンドボックス サブスクリプションをアクティブ化する

**適用対象:**

- パートナー センター

統合サンドボックスアカウントから、商用 marketplace のサービスとしてのソフトウェア (SaaS) 製品のサブスクリプションをアクティブ化して課金を有効にする方法について説明します。

> [!NOTE]
> 統合サンドボックスアカウントから、商用 marketplace の SaaS 製品のサブスクリプションをアクティブ化することのみが可能です。 運用環境のサブスクリプションがある場合は、発行元のサイトにアクセスしてセットアッププロセスを完了する必要があります。 サブスクリプションの課金は、セットアップの完了後にのみ開始されます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 統合サンドボックスパートナーアカウント。お客様は、商用 marketplace SaaS 製品のアクティブなサブスクリプションを持っています。

- パートナーセンター .NET SDK を使用しているパートナーの場合、この機能にアクセスするには、SDK バージョン1.14.0 以上を使用する必要があります。

## <a name="c"></a>C\#

次の手順を使用して、商用 marketplace SaaS 製品のサブスクリプションをアクティブ化します。

1. 使用可能なサブスクリプション操作へのインターフェイスを作成します。 顧客を特定し、試用版サブスクリプションのサブスクリプション識別子を指定する必要があります。

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. **アクティブ化**操作を使用してサブスクリプションをアクティブ化します。

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法     | 要求 URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

| 名前                   | Type     | 必須 | 説明                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y | 値は、GUID 形式の顧客テナント識別子 (**顧客テナント id**) です。これにより、顧客を指定できます。 |
| **サブスクリプション id** | **guid** | Y | 値は、GUID 形式のサブスクリプション識別子 (**サブスクリプション id**) で、サブスクリプションを指定できます。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>REST 応答

このメソッドは、**サブスクリプション id**と**ステータス**プロパティを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
