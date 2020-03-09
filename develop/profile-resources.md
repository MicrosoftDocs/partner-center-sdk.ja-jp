---
title: プロファイルリソース
description: クラウドソリューションプロバイダーのプロファイルの動作について説明します。
ms.assetid: 42F2959B-D70D-41A7-9A50-E22A2356A339
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3449aeb3695a9f286f37668d3f0862dc7b5cfa9f
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78899819"
---
# <a name="profile-resources"></a>プロファイルリソース


**適用対象**

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

クラウドソリューションプロバイダーのプロファイルの動作について説明します。

## <a name="span-idbillingprofilespan-idbillingprofilespan-idbillingprofilebillingprofile"></a><span id="BillingProfile"/><span id="billingprofile"/><span id="BILLINGPROFILE"/>のプロファイル


パートナーの請求プロファイルを説明します。

| プロパティ            | 種類                                                           | 説明                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| 仕入         | string                                                         | 請求先の会社名。                                   |
| address             | [Address](utility-resources.md#address)                       | 会社または組織の請求先住所。 |
| primaryContact      | [Contact](utility-resources.md#contact)                       | 会社または組織の主要連絡先。        |
| Dbo.accountnumber | string                                                         | 会社または組織の発注番号。        |
| taxId               | string                                                         | 会社または組織の税 Id。                       |
| 通貨     | string                                                         | 会社または組織によって使用される通貨。           |
| profileType         | string                                                         | パートナーのプロファイルの種類。                                   |
| リンク               | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイルに対応するリソースリンク。            |
| 属性          | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。       |

 

## <a name="span-idlegalbusinessprofilespan-idlegalbusinessprofilespan-idlegalbusinessprofilelegalbusinessprofile"></a><span id="LegalBusinessProfile"/><span id="legalbusinessprofile"/><span id="LEGALBUSINESSPROFILE"/>LegalBusinessProfile


パートナーの法的ビジネスプロファイルについて説明します。

| プロパティ               | 種類                                                           | 説明                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 仕入            | string                                                         | 法的企業名。                                                                                                                                              |
| address                | [Address](utility-resources.md#address)                       | 会社または組織の住所。                                                                                                                          |
| primaryContact         | [Contact](utility-resources.md#contact)                       | 会社または組織の主要連絡先。                                                                                                                 |
| 会社の承認 Veraddress | [Address](utility-resources.md#address)                       | 会社の承認者のアドレス。                                                                                                                                        |
| 会社の承認 Veremail   | string                                                         | 会社の承認者の電子メール。                                                                                                                                          |
| vettingStatus          | string                                                         | 審査の状態。 この値は、 [**VettingStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus)で見つかったメンバー名のいずれかの文字列表現です。           |
| vettingSubStatus       | string                                                         | 審査サブステータス。 この値は、 [**VettingSubStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus)で見つかったメンバー名のいずれかの文字列表現です。 |
| profileType            | string                                                         | パートナーのプロファイルの種類。                                                                                                                                            |
| リンク                  | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイルに対応するリソースリンク。                                                                                                                     |
| 属性             | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。                                                                                                                |

 

## <a name="span-idmpnprofilespan-idmpnprofilespan-idmpnprofilempnprofile"></a><span id="MpnProfile"/><span id="mpnprofile"/><span id="MPNPROFILE"/>MpnProfile


パートナーの Microsoft Partner Network プロファイルを記述します。

| プロパティ    | 種類                                                           | 説明                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | string                                                         | 会社名または組織名。                     |
| mpnId       | string                                                         | Microsoft Partner Network Id。                     |
| profileType | string                                                         | パートナーのプロファイルの種類。                             |
| リンク       | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイルに対応するリソースリンク。      |
| 属性  | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。 |

 

## <a name="span-idorganizationprofilespan-idorganizationprofilespan-idorganizationprofileorganizationprofile"></a><span id="OrganizationProfile"/><span id="organizationprofile"/><span id="ORGANIZATIONPROFILE"/>組織プロファイル


パートナーの組織のプロファイルについて説明します。

| プロパティ       | 種類                                                           | 説明                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | string                                                         | 組織の Id。                                                 |
| 仕入    | string                                                         | 会社または組織の名前。                               |
| defaultAddress | [Address](utility-resources.md#address)                       | 会社または組織の既定のアドレス。                    |
| テナント       | string                                                         | テナント識別子。                                                 |
| domain         | string                                                         | 会社または組織のドメイン。                                  |
| 電子メール          | string                                                         | 親サブスクリプションを取得します。値の設定もできます。                                  |
| language       | string                                                         | 通信に使用する言語です。                              |
| カルチャ        | string                                                         | 通信と通貨に使用する優先カルチャ ("en-us" など)。 |
| profileType    | string                                                         | パートナーのプロファイルの種類。                                              |
| リンク          | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイルに対応するリソースリンク。                       |
| 属性     | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。                  |

 

## <a name="span-idsupportprofilespan-idsupportprofilespan-idsupportprofilesupportprofile"></a><span id="SupportProfile"/><span id="supportprofile"/><span id="SUPPORTPROFILE"/>SupportProfile


パートナーのサポートプロファイルについて説明します。

| プロパティ    | 種類                                                           | 説明                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| 電子メール       | string                                                         | プロファイルに関連付けられている電子メールアドレス。        |
| 電話   | string                                                         | プロファイルに関連付けられている電話番号。         |
| website     | string                                                         | サポート web サイト。                                  |
| profileType | string                                                         | パートナーのプロファイルの種類。                             |
| リンク       | [ResourceLinks](utility-resources.md#resourcelinks)           | プロファイルに対応するリソースリンク。      |
| 属性  | [ResourceAttributes](utility-resources.md#resourceattributes) | プロファイルに対応するメタデータ属性。 |

 

 

 




