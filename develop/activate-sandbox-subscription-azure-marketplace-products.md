---
title: 商用 marketplace 製品のサンドボックスサブスクリプションをアクティブ化する
description: 商用 marketplace 製品のサンドボックスサブスクリプションをアクティブ化します。
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ec5046131369b68eb958b8143982abb65addbd09
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488752"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-products"></a>商用 marketplace 製品のサンドボックスサブスクリプションをアクティブ化する

適用対象:

- パートナー センター

統合サンドボックスアカウントから、商用 marketplace のサービスとしてのソフトウェア (SaaS) 製品のサブスクリプションをアクティブ化して課金を有効にする方法について説明します。

>[!NOTE]
>統合サンドボックスアカウントから、商用 marketplace の SaaS 製品のサブスクリプションをアクティブ化することのみが可能です。 運用環境のサブスクリプションがある場合は、発行元のサイトにアクセスしてセットアッププロセスを完了する必要があります。 サブスクリプションの課金は、セットアップの完了後にのみ開始されます。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 統合サンドボックスパートナーアカウント。お客様は、商用 marketplace SaaS 製品のアクティブなサブスクリプションを持っています。
- パートナーセンター .NET SDK を使用しているパートナーの場合、この機能にアクセスするには、SDK バージョン1.14.0 以上を使用する必要があります。

## <a name="c"></a>C#

次の手順を使用して、商用 marketplace SaaS 製品のサブスクリプションをアクティブ化します。

1. 使用可能なサブスクリプション操作へのインターフェイスを作成します。 顧客を特定し、試用版サブスクリプションのサブスクリプション識別子を指定する必要があります。

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

2. Activate the subscription using the **Activate** operation.

    ``` csharp
    var subscriptionActivationResult = subscriptionOperations.Activate();
## REST request

### Request syntax

| Method     | Request URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1 |

### URI parameter

| Name                   | Type     | Required | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y | The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer. |
| **subscription-id** | **guid** | Y | The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription. |

### Request headers

See [Partner Center REST headers](headers.md) for more information.

### Request body

None.

### Request example

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>REST 応答

このメソッドは、**サブスクリプション id**と**ステータス**プロパティを返します。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

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
