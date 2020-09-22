---
title: プロファイルリソース
description: クラウドソリューションプロバイダーのプロファイルの動作について説明します。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef14eb0307dae0d58dc9903a867ec3bee4ebb323
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925822"
---
# <a name="profile-resources"></a>プロファイルリソース

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

クラウドソリューションプロバイダーのプロファイルの動作について説明します。

## <a name="billingprofile"></a>BillingProfile

パートナーの請求プロファイルを説明します。

| プロパティ            | 種類                                                           | 説明                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | string                                                         | 請求先の会社名。                                   |
| address             | [アドレス](utility-resources.md#address)                       | 会社または組織の請求先住所。 |
| primaryContact      | [Contact](utility-resources.md#contact)                       | 会社または組織の主要連絡先。        |
| Dbo.accountnumber | string                                                         | 会社または組織の発注番号。        |
| taxId               | string                                                         | 会社または組織の税 Id。                       |
| billingCurrency     | string                                                         | 会社または組織によって使用される通貨。           |
| profileType         | string                                                         | パートナーのプロファイルの種類。                                   |
| リンク               | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイルに対応するリソースリンク。            |
| 属性          | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

パートナーの法的ビジネスプロファイルについて説明します。

| プロパティ               | 種類                                                           | 説明                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | string                                                         | 法的企業名。                                                                                                                                              |
| address                | [アドレス](utility-resources.md#address)                       | 会社または組織の住所。                                                                                                                          |
| primaryContact         | [Contact](utility-resources.md#contact)                       | 会社または組織の主要連絡先。                                                                                                                 |
| 会社の承認 Veraddress | [アドレス](utility-resources.md#address)                       | 会社の承認者のアドレス。                                                                                                                                        |
| 会社の承認 Veremail   | string                                                         | 会社の承認者の電子メール。                                                                                                                                          |
| vettingStatus          | string                                                         | 審査の状態。 この値は、[**VettingStatus**/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus) で見つかったメンバー名のいずれかの文字列表現です。           |
| vettingSubStatus       | string                                                         | 審査サブステータス。 この値は、[**VettingSubStatus**/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus) で見つかったメンバー名のいずれかの文字列表現です。 |
| profileType            | string                                                         | パートナーのプロファイルの種類。                                                                                                                                            |
| リンク                  | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイルに対応するリソースリンク。                                                                                                                     |
| 属性             | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

パートナーの Microsoft Partner Network プロファイルを記述します。

| プロパティ    | 種類                                                           | 説明                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | string                                                         | 会社名または組織名。                     |
| mpnId       | string                                                         | Microsoft Partner Network Id。                     |
| profileType | string                                                         | パートナーのプロファイルの種類。                             |
| リンク       | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイルに対応するリソースリンク。      |
| 属性  | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。 |

## <a name="organizationprofile"></a>組織のプロファイル

パートナーの組織のプロファイルについて説明します。

| プロパティ       | 種類                                                           | 説明                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | string                                                         | 組織の Id。                                                 |
| companyName    | string                                                         | 会社または組織の名前。                               |
| defaultAddress | [アドレス](utility-resources.md#address)                       | 会社または組織の既定のアドレス。                    |
| tenantId       | string                                                         | テナント識別子。                                                 |
| domain         | string                                                         | 会社または組織のドメイン。                                  |
| email          | string                                                         | 親サブスクリプションを取得します。値の設定もできます。                                  |
| language       | string                                                         | 通信に使用する言語です。                              |
| カルチャ        | string                                                         | 通信と通貨に使用する優先カルチャ ("en-us" など)。 |
| profileType    | string                                                         | パートナーのプロファイルの種類。                                              |
| リンク          | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイルに対応するリソースリンク。                       |
| 属性     | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。                  |

## <a name="supportprofile"></a>SupportProfile

パートナーのサポートプロファイルについて説明します。

| プロパティ    | 種類                                                           | 説明                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| email       | string                                                         | プロファイルに関連付けられている電子メールアドレス。        |
| telephone   | string                                                         | プロファイルに関連付けられている電話番号。         |
| Web サイト (website)     | string                                                         | サポート web サイト。                                  |
| profileType | string                                                         | パートナーのプロファイルの種類。                             |
| リンク       | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイルに対応するリソースリンク。      |
| 属性  | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。 |

