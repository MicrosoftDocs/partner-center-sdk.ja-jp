---
title: リソースの監査
description: パートナーセンターの監査操作で使用されるリソース。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cef7ca8c86d8af92423e237a278c900c7a89002f
ms.sourcegitcommit: 6c71b5398445584bf6667f71723d06f5227c6302
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91102105"
---
# <a name="auditing-resources"></a>リソースの監査

**適用対象:**

- パートナー センター

監査操作には、次のリソースを使用できます。

## <a name="auditrecord"></a>AuditRecord

パートナーのユーザーまたはアプリケーションによって実行される操作のレコードを表します。

| プロパティ | 種類 | 説明 |
| --- | --- | ---|
| customerId | string | 顧客を識別する GUID 形式の文字列。 |
| customerName | string | 顧客名。 |
| userPrincipalName | string | ユーザープリンシパル名またはユーザー識別子。 通常、このプロパティは、インターネット標準の RFC 822 に基づく電子メールアドレス形式のユーザーのインターネットスタイルのログイン名です。 |
| applicationId | string | 操作を実行したアプリケーションを識別する文字列。 |
| resourceType | string | 操作によって処理されたリソースの種類。 使用可能な値:、、、、、、、、、、、 `customer` `customer_user` `order` `subscription` `license` `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` 。 |
| resourceOldValue | string | リソースの古い値。 |
| resourceNewValue | string | リソースの新しい値。 |
| operationType | string | 実行された操作の種類。 使用可能な値:、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、 `update_customer_qualification` `update_subscription` `upgrade_subscription` `convert_trial_subscription` `add_customer` `update_customer_billing_profile` `update_customer_partner_contract_company_name` `update_customer_spending_budget` `delete_customer` `remove_partner_customer_relationship` `create_order` `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` です。 |
| operationDate | UTC 日時形式の文字列 | 操作が実行された日付と時刻。 |
| operationStatus | string | 監査されている操作の状態。 指定できる値は `succeeded` 、、 `failed` 、またはです。これは、 `progress` 操作がまだ進行中であることを意味します。 |
| customizedData  | オブジェクトの配列 | 追加情報。 各オブジェクトには、2つの JSON キーと値のペアが含まれています。1つ目は文字列値、もう1つは文字列値 `key` `value` です。 配列内のオブジェクトの数は、実行された操作の種類によって異なります。 |
| 属性 | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 |
