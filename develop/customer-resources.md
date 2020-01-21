---
title: お客様のリソース
description: 顧客または再販業者を表す顧客リソース。
ms.assetid: C7EC2657-62F2-43B3-B171-2F74498D45E0
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 5afcf2a9bd673a903f7cc75072ec0c3f35cae5c5
ms.sourcegitcommit: 80f8292f1b31649c59fd292d36023aa4d1877031
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75923532"
---
# <a name="customer-resources"></a>お客様のリソース

適用対象

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

## <a name="customer"></a>顧客

**顧客**リソースは、顧客または再販業者を表します。 多くの場合、お客様のリソースには、Microsoft と Microsoft のリセラーとの取引を行う人材、従業員、または組織を指定できます。 また、お客様には会社プロファイルと請求プロファイルもあります。

>[!NOTE]
>**お客様**のリソースには、テナント識別子ごとに1分あたり500の要求のレート制限があります。

| プロパティ              | 種類                                                             | 説明                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | string                                                           | 顧客 ID。                                                                                                                             |
| commerceId            | string                                                           | コマース ID。                                                                                                                             |
| 会社のプロファイル        | [顧客企業プロファイル](#customercompanyprofile)                | 会社または組織に関する追加情報。                                                                                    |
| billingProfile        | [顧客のプロファイル](#customerbillingprofile)                | 課金に使用される追加情報。                                                                                                     |
| relationshipToPartner | string                                                           | パートナーがこの顧客に使用するライセンスプログラムを定義します。 "none"、"再販業者"、"advisor"、"シンジケーション"、"microsoft\_support" などです。 |
| allowDelegatedAccess  | boolean                                                          | この顧客によって代理管理者特権がパートナーに付与されているかどうか。 このプロパティは、リストではなく ID で顧客を取得する場合にのみ使用できます。                                                         |
| ユーザー       | [ユーザー](user-resources.md#usercredentials) | ユーザー資格情報。                                                                                                                        |
| customDomains         | 文字列の配列                                                 | 顧客のカスタムドメインの一覧。                                                                                                        |
| associatedPartnerId   | string                                                           | この顧客アカウントに関連付けられている間接リセラー。 この値は、間接 CSP パートナーによってのみ設定できます。                              |
| リンク                 | [ResourceLinks](utility-resources.md#resourcelinks)             | プロファイル内に含まれるリソースリンク。                                                                                             |
| 属性            | [ResourceAttributes](utility-resources.md#resourceattributes)   | プロファイルに対応するメタデータ属性。                                                                                        |

## <a name="customercompanyprofile"></a>顧客企業プロファイル

**顧客企業プロファイル**リソースは、会社または組織に関する追加情報です。

| プロパティ    | 種類                                                           | 説明                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| テナント    | string                                                         | Azure AD の顧客のテナント識別子。 これは、MicrosoftID とも呼ばれます。 |
| domain      | string                                                         | 顧客の名前 (contoso.onmicrosoft.com など)。                             |
| 仕入 | string                                                         | 会社または組織の名前。                                          |
| リンク       | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイル内に含まれるリソースリンク。                                  |
| 属性  | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。                             |

## <a name="customerbillingprofile"></a>顧客のプロファイル

顧客ごとの**プロファイル**リソースは、顧客の請求に使用される追加情報です。

| プロパティ       | 種類                                                           | 説明                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | string                                                         | プロファイル識別子。                                                                                                                                |
| firstName      | string                                                         | 顧客の会社の請求先の連絡先の名。 これは、請求書とその他の課金情報の送信先になります。 |
| lastName       | string                                                         | 請求先の連絡先の姓。                                                                                                                  |
| 電子メール          | string                                                         | 請求先の連絡先の電子メールアドレス                                                                                                                    |
| カルチャ        | string                                                         | "En-us" など、コミュニケーションおよび通貨に適したカルチャ。                                                                               |
| language       | string                                                         | 通信に使用する優先言語。                                                                                                            |
| 仕入    | string                                                         | 会社または組織の名前。                                                                                                               |
| defaultAddress | [Address](utility-resources.md#address)                       | 請求先となる請求先の住所。                                                                                   |
| リンク          | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイル内に含まれるリソースリンク。                                                                                                       |
| 属性     | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。                                                                                                  |

## <a name="customerrelationshiprequest"></a>顧客の Relationshiprequest

カスタマー **Relationshiprequest**リソースには、パートナーとの再販業者関係を確立するために顧客が使用する URL が含まれています。

| プロパティ   | 種類                                                           | 説明                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | string                                                         | パートナーとの関係を確立するために顧客が使用する URL。 |
| 属性 | [ResourceAttributes](utility-resources.md#resourceattributes) | リレーションシップ要求に対応するメタデータ属性。       |