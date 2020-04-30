---
title: リソースの監査
description: パートナーセンターの監査操作で使用されるリソース。
ms.assetid: FEF0BED4-2CEB-46D2-9365-D7D3C50AF0E3
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: bfd70c213cfca961d1a793540fb0477a0bb7e396
ms.sourcegitcommit: 685137f5dd204912efcb4c406a1bf02278ce5dae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81785151"
---
# <a name="auditing-resources"></a>リソースの監査

**適用対象:**

- パートナー センター

監査操作には、次のリソースを使用できます。

## <a name="auditrecord"></a>AuditRecord

パートナーのユーザーまたはアプリケーションによって実行される操作のレコードを表します。

| プロパティ | Type | 説明 |
| --- | --- | ---|
| customerId | string | 顧客を識別する GUID 形式の文字列。 |
| customerName | string | 顧客名。 |
| userPrincipalName | string | ユーザープリンシパル名またはユーザー識別子。 通常、このプロパティは、インターネット標準の RFC 822 に基づく電子メールアドレス形式のユーザーのインターネットスタイルのログイン名です。 |
| applicationId | string | 操作を実行したアプリケーションを識別する文字列。 |
| resourceType | string | 操作によって処理されたリソースの種類。 使用可能な`customer`値`customer_user`: `order`、 `subscription`、 `license`、 `third_party_add_on` `mpn_association` `transfer` `application` `application_credential`、、、、、、、、 `partner_relationship` `partner_user`。 |
| resourceOldValue | string | リソースの古い値。 |
| resourceNewValue | string | リソースの新しい値。 |
| operationType | string | 実行された操作の種類。 使用可能な`update_customer_qualification`値`update_subscription`: `upgrade_subscription`、 `convert_trial_subscription`、 `add_customer`、 `update_customer_billing_profile` `update_customer_partner_contract_company_name`、、 `update_customer_spending_budget`、 `delete_customer` 、、(サンドボックス統合アカウント`remove_partner_customer_relationship`のみ`create_order`) `update_order`、 `create_customer_user`、 `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `remove_partner_user`、、 `unregister_application`、、、、、、、、、、、、、、、、、、、、、、、、、です。 `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` |
| operationDate | UTC 日時形式の文字列 | 操作が実行された日付と時刻。 |
| operationStatus | string | 監査されている操作の状態。 指定できる値`succeeded`は`failed`、、 `progress`、またはです。これは、操作がまだ進行中であることを意味します。 |
| customizedData  | オブジェクトの配列 | 追加情報。 各オブジェクトには、2つの JSON キーと値の`key`ペアが含まれています。 `value` 1 つ目は文字列値、もう1つは文字列値です。 配列内のオブジェクトの数は、実行された操作の種類によって異なります。 |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 |
