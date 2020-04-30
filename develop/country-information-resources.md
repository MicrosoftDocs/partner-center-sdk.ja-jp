---
title: 国情報リソース
description: 国/地域の記述メタデータ。
ms.assetid: 19460437-5611-49A1-A7E7-704420C1DE8F
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 4ff89cccf9c3605887b89f35b6505ae809d0ac9f
ms.sourcegitcommit: e5a29552fe24fbb87faab9f25afa47738e94c1a3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82092989"
---
# <a name="country-information-resources"></a>国情報リソース

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

次のリソースは、国/地域の記述メタデータです。

## <a name="countryinformation"></a>CountryInformation

| プロパティ                      | Type               | 説明                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | string             | 拡張データ。                                                                                |
| Iso2Code                      | string             | ISO 2 のコード。                                                                                     |
| Iso3Code                      | string             | ISO 3 コード。                                                                                     |
| DefaultCulture                | string             | 既定のカルチャ。                                                                               |
| IsStateRequired               | boolean            | 都道府県が必須かどうかを示します。                                             |
| SupportedStatesList           | 文字列の配列   | 都道府県が必要な場合は、その国/地域の完全な一覧を返します。                    |
| SupportedLanguagesList        | 文字列の配列   | サポートされている言語の一覧。                                                                     |
| SupportedCulturesList         | 文字列の配列   | サポートされているカルチャの一覧。                                                                      |
| IsPostalCodeRequired          | boolean            | 郵便番号が必要かどうかを示します。                                    |
| PostalCodeRegex               | string             | 郵便番号を定義する正規表現。                                          |
| IsCityRequired                | boolean            | 市区町村が必須かどうかを示します。                                                       |
| サポートされているもの              | boolean            | VAT ID が必須かどうかを示します。                                                     |
| TaxIdFormat                   | string             | 税 ID 形式。                                                                                 |
| TaxIdSample                   | string             | 税 ID のサンプルです。                                                                                 |
| V・ Dregex                    | string             | 税 ID の正規表現。                                                                     |
| PhoneNumberRegex              | string             | 電話番号の正規表現。                                                               |
| サポートされている Isregistrationnumber | boolean            | 登録番号がサポートされているかどうかを示します。                                       |
| IsTaxIdSupported              | boolean            | 税 ID がサポートされているかどうかを示します。 これは、Isvがサポートされているものとは異なります。 |
| ResellerAgreementRegion       | string             | リセラー契約リージョン。                                                                     |
| GeographicRegion              | string             | 地理的領域。                                                                             |
| CountryCallingCodesList       | 文字列の配列   | 国/地域でサポートされている呼び出しコード。                                                 |
| 属性                    | ResourceAttributes | CountryInformation リソースに対応するメタデータ属性。                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

国/地域の住所の書式規則について説明します。

| プロパティ                | Type               | 説明                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | string             | ISO 2 のコード。                                                                                     |
| DefaultCulture          | string             | 既定のカルチャ。                                                                               |
| IsStateRequired         | boolean            | 都道府県が必須かどうかを示します。                                             |
| SupportedStatesList     | 文字列の配列   | 都道府県が必要な場合は、その国/地域の完全な一覧を返します。                    |
| SupportedLanguagesList  | 文字列の配列   | サポートされている言語の一覧。                                                                     |
| SupportedCulturesList   | 文字列の配列   | サポートされているカルチャの一覧。                                                                      |
| IsPostalCodeRequired    | boolean            | 郵便番号が必要かどうかを示します。                                    |
| PostalCodeRegex         | string             | 郵便番号を定義する正規表現。                                          |
| IsCityRequired          | boolean            | 市区町村が必須かどうかを示します。                                                       |
| サポートされているもの        | boolean            | VAT ID が必須かどうかを示します。                                                     |
| TaxIdFormat             | string             | 税 ID 形式。                                                                                 |
| TaxIdSample             | string             | 税 ID のサンプルです。                                                                                 |
| V・ Dregex              | string             | 税 ID の正規表現。                                                                     |
| PhoneNumberRegex        | string             | 電話番号の正規表現。                                                               |
| IsTaxIdSupported        | boolean            | 税 ID がサポートされているかどうかを示します。 このプロパティは、Isvがサポートされているものとは異なります。 |
| Ist軸のその他の条件         | boolean            | 税 ID が省略可能かどうかを示します。                                                     |
| CountryCallingCodesList | 文字列の配列   | 国/地域でサポートされている呼び出しコード。                                                 |
| 属性              | ResourceAttributes | CountryInformation リソースに対応するメタデータ属性。                          |
