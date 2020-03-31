---
title: リソースの監査
description: パートナーセンターの監査操作で使用されるリソース。
ms.assetid: FEF0BED4-2CEB-46D2-9365-D7D3C50AF0E3
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 719ddd1b2e5003842ea85e0f4710c2cf01970564
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413649"
---
# <a name="auditing-resources"></a>リソースの監査

適用対象

- Partner Center

監査操作には、次のリソースを使用できます。

## <a name="auditrecord"></a>AuditRecord

パートナーのユーザーまたはアプリケーションによって実行される操作のレコードを表します。

| プロパティ | 種類 | 説明 |
| --- | --- | ---|
| 顧客 | string | 顧客を識別する GUID 形式の文字列。 |
| customerName | string | 顧客名。 |
| userPrincipalName | string | ユーザープリンシパル名またはユーザー識別子。 通常、これはインターネット標準 RFC 822 に基づく電子メールアドレス形式のユーザーのインターネットスタイルのログイン名です。 |
| applicationId | string | 操作を実行したアプリケーションを識別する文字列。 |
| リソース | string | 操作によって処理されたリソースの種類。 使用可能な値: &quot;カスタマー&quot;、&quot;customer_user&quot;、&quot;順序&quot;、&quot;サブスクリプション&quot;、&quot;ライセンス&quot;、&quot;third_party_add_on&quot;、&quot;mpn_association&quot;、&quot;転送&quot;、&quot;アプリケーション&quot;、&quot;application_credential&quot;、&quot;partner_user&quot;、&quot;partner_relationship&quot;。 |
| resourceOldValue | string | リソースの古い値。 |
| resourceNewValue | string | リソースの新しい値。 |
| operationType | string | 実行された操作の種類。 使用可能な値: &quot;update_customer_qualification&quot;、&quot;update_subscription&quot;、&quot;upgrade_subscription&quot;、&quot;convert_trial_subscription&quot;、&quot;add_customer&quot;、&quot;update_customer_billing_profile&quot;、&quot;update_customer_partner_contract_company_name&quot;、&quot;update_customer_spending_budget&quot;、&quot;delete_customer&quot; (サンドボックス統合アカウント)のみ)、&quot;remove_partner_customer_relationship&quot;、&quot;create_order&quot;、&quot;update_order&quot;、&quot;create_customer_user&quot;、&quot;delete_customer_user&quot;、&quot;update_customer_user&quot;、&quot;update_customer_user_licenses&quot;、&quot;reset_customer_user_password&quot;、&quot;update_customer_user_principal_name&quot;、&quot;restore_customer_user&quot;、&quot;create_mpn_association&quot;、&quot;update_mpn_association&quot;、&quot;update_sfb_customer_user_licenses&quot;、&quot;update_transfer&quot;、&quot;create_partner_relationship&quot;、&quot;register_application&quot;、&quot;unregister_application&quot;、&quot;add_application_credential&quot;、&quot;remove_application_credential&quot;、&quot;create_partner_user&quot;、&quot;update_partner_user&quot;、&quot;remove_partner_user&quot;。 |
| operationDate | UTC 日時形式の文字列 | 操作が実行された日付と時刻。 |
| operationStatus | string | 監査されている操作の状態。 使用可能な値: &quot;succeeded&quot;、&quot;failed&quot;、または &quot;progress&quot;。これは、操作がまだ進行中であることを意味します。 |
| customizedData  | オブジェクトの配列 | 追加情報。 各オブジェクトには、2つの JSON キーと値のペアが含まれています。1つ目は &quot;キー&quot;、もう1つは文字列値、2番目は &quot;値&quot;、文字列値です。 配列内のオブジェクトの数は、実行された操作の種類によって異なります。 |
| 属性 | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 |