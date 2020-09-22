---
title: パートナーセンターの webhook イベント
description: パートナーセンターでサポートされているすべての Webhook イベントに関するドキュメント。
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 5358aab8efdd68ad52c583936304f99ffae12708
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926852"
---
# <a name="partner-center-webhook-events"></a>パートナーセンターの webhook イベント

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーセンターの webhook イベントは、登録された URL に HTTP Post の形式で配信されるリソース変更イベントです。 パートナーセンターからイベントを受信するには、パートナーセンターがイベントを投稿できるコールバックをホストします。 イベントはデジタル署名されているため、パートナーセンターから送信されたことを検証できます。

イベントを受信する方法、コールバックを認証する方法、およびパートナーセンターの webhook Api を使用してイベント登録を作成、表示、更新する方法については、「 [パートナーセンター](partner-center-webhooks.md)の webhook」を参照してください。

## <a name="supported-events"></a>サポートされるイベント

パートナーセンターでは、次の webhook イベントがサポートされています。

### <a name="test-event"></a>テストイベント

このイベントを使用すると、テストイベントを要求し、その進行状況を追跡することによって、登録を自己オンボードしてテストできます。 イベントの配信を試みている間に、Microsoft から受信されているエラーメッセージを確認することができます。 これは "テスト作成済み" イベントにのみ適用され、7日を経過したデータは消去されます。

>[!NOTE]
>テスト作成イベントを投稿する場合、1分あたり2要求のスロットル制限があります。

#### <a name="properties"></a>Properties

| プロパティ                  | 種類                               | 説明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | イベントの名前です。 {Resource}-{action} の形式で。 このイベントでは、値は "テスト作成済み" です。                                          |
| ResourceUri               | URI                                | リソースを取得する URI。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" を使用します。 |
| ResourceName              | string                             | イベントを発生させるリソースの名前。 このイベントでは、値は "test" です。                                  |
| AuditUri                  | URI                                | Optional監査レコードを取得する URI (存在する場合)。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" を使用します。 |
| ResourceChangeUtcDate     | UTC 日時形式の文字列 | リソースが変更された日付と時刻。                                                         |

#### <a name="example"></a>例

```json
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="subscription-updated-event"></a>サブスクリプションの更新イベント

このイベントは、指定されたサブスクリプションが変更されたときに発生します。 パートナーセンター API を使用して変更が行われた場合に加えて、サブスクリプションの更新イベントが生成されます。  このイベントは、たとえば、ライセンスの数が変更されたときや、サブスクリプションの状態が変化したときなど、コマースレベルの変更がある場合にのみ生成されます。 サブスクリプション内でリソースが作成されるときには生成されません。

>[!NOTE]
>サブスクリプションが変更されてからサブスクリプションの更新イベントがトリガーされるまでに、最大48時間の遅延が発生します。

#### <a name="properties"></a>Properties

| プロパティ                  | 種類                               | 説明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | イベントの名前です。 {Resource}-{action} の形式で。 このイベントでは、値は "subscription-updated" です。                                  |
| ResourceUri               | URI                                | リソースを取得する URI。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" を使用します。 |
| ResourceName              | string                             | イベントを発生させるリソースの名前。 このイベントでは、値は "subscription" です。                          |
| AuditUri                  | URI                                | Optional監査レコードを取得する URI (存在する場合)。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" を使用します。 |
| ResourceChangeUtcDate     | UTC 日時形式の文字列 | リソースが変更された日付と時刻。                                                         |

#### <a name="example"></a>例

```json
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}",
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="threshold-exceeded-event"></a>しきい値を超えたイベント

いずれかの顧客による Microsoft Azure の使用量が、使用量の支出予算 (しきい値) を超えると、このイベントが発生します。 詳細については、「顧客/パートナーの Azure 支出予算を設定する」を参照してください。または、お客様に対して設定します。

#### <a name="properties"></a>Properties

| プロパティ                  | 種類                               | 説明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | イベントの名前です。 {Resource}-{action} の形式で。 このイベントでは、値は "usagerecords-thresholdExceeded" です。                                  |
| ResourceUri               | URI                                | リソースを取得する URI。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords" を使用します。 |
| ResourceName              | string                             | イベントを発生させるリソースの名前。 このイベントでは、値は "usagerecords" です。                          |
| AuditUri                  | URI                                | Optional監査レコードを取得する URI (存在する場合)。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" を使用します。 |
| ResourceChangeUtcDate     | UTC 日時形式の文字列 | リソースが変更された日付と時刻。                                                         |

#### <a name="example"></a>例

```json
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-created-event"></a>紹介作成イベント

このイベントは、参照が作成されるときに発生します。

#### <a name="properties"></a>Properties

| プロパティ                  | 種類                               | 説明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | イベントの名前です。 {Resource}-{action} の形式で。 このイベントでは、値は "参照作成" です。                                  |
| ResourceUri               | URI                                | リソースを取得する URI。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" を使用します。 |
| ResourceName              | string                             | イベントを発生させるリソースの名前。 このイベントでは、値は "参照" です。                          |
| AuditUri                  | URI                                | Optional監査レコードを取得する URI (存在する場合)。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" を使用します。 |
| ResourceChangeUtcDate     | UTC 日時形式の文字列 | リソースが変更された日付と時刻。                                                         |

#### <a name="example"></a>例

```json
{
    "EventName": "referral-created",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-updated-event"></a>参照の更新イベント

このイベントは、参照が更新されたときに発生します。

#### <a name="properties"></a>Properties

| プロパティ                  | 種類                               | 説明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | イベントの名前です。 {Resource}-{action} の形式で。 このイベントでは、値は "参照-更新" です。                                  |
| ResourceUri               | URI                                | リソースを取得する URI。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" を使用します。 |
| ResourceName              | string                             | イベントを発生させるリソースの名前。 このイベントでは、値は "参照" です。                          |
| AuditUri                  | URI                                | Optional監査レコードを取得する URI (存在する場合)。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" を使用します。 |
| ResourceChangeUtcDate     | UTC 日時形式の文字列 | リソースが変更された日付と時刻。                                                         |

#### <a name="example"></a>例

```json
{
    "EventName": "referral-updated",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="invoice-ready-event"></a>請求書の準備完了イベント

このイベントは、新しい請求書の準備が整ったときに発生します。

| プロパティ                  | 種類                               | 説明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | string | イベントの名前です。 {Resource}-{action} の形式で。 このイベントの場合、値は "invoice ready" です。 |
| ResourceUri | URI | リソースを取得する URI。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{{InvoiceId}}" を使用します。 |
| ResourceName | string | イベントを発生させるリソースの名前。 このイベントでは、値は "invoice" です。 |
| AuditUri |  URI | Optional監査レコードを取得する URI (存在する場合)。 構文 "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}") を使用します。 |
| ResourceChangeUtcDate | UTC 日時形式の文字列 | リソースが変更された日付と時刻。 |

#### <a name="example"></a>例

```json
{
    "EventName": "invoice-ready",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/invoices/{{InvoiceId}}",
    "ResourceName": "invoice",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}

```
