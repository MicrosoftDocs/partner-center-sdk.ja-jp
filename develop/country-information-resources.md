---
title: Country information resources
description: Descriptive metadata for a country/region.
ms.assetid: 19460437-5611-49A1-A7E7-704420C1DE8F
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 321e05ff2f65746ae2e555bf35b4aa8d298c20af
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488812"
---
# <a name="country-information-resources"></a>Country information resources

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

The following resources are descriptive metadata for a country/region.

## <a name="countryinformation"></a>CountryInformation

| プロパティ                      | タスクバーの検索ボックスに               | 説明                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | string             | The extension data.                                                                                |
| Iso2Code                      | string             | An ISO-2 code.                                                                                     |
| Iso3Code                      | string             | An ISO-3 code.                                                                                     |
| DefaultCulture                | string             | The default culture.                                                                               |
| IsStateRequired               | boolean            | Indicates whether a state/province is required or not.                                             |
| SupportedStatesList           | 文字列の配列   | If a state/province is required, returns the full list for that country/region.                    |
| SupportedLanguagesList        | 文字列の配列   | A list of supported languages.                                                                     |
| SupportedCulturesList         | 文字列の配列   | A list of supported cultures.                                                                      |
| IsPostalCodeRequired          | boolean            | Indicates whether a ZIP code or postal code is required or not.                                    |
| PostalCodeRegex               | string             | The regular expression that defines the ZIP/postal code .                                          |
| IsCityRequired                | boolean            | Indicates whether a city is required or not.                                                       |
| IsVatIdSupported              | boolean            | Indicates whether a VAT ID is required or not.                                                     |
| TaxIdFormat                   | string             | The tax ID format.                                                                                 |
| TaxIdSample                   | string             | The tax ID sample.                                                                                 |
| VatIdRegex                    | string             | The tax ID regular expression.                                                                     |
| PhoneNumberRegex              | string             | The phone number regular expression.                                                               |
| IsRegistrationNumberSupported | boolean            | Indicates whether a registration number is supported or not.                                       |
| IsTaxIdSupported              | boolean            | Indicates whether a tax ID is supported or not. Note that this is different than IsVatIdSupported. |
| ResellerAgreementRegion       | string             | The reseller agreement region.                                                                     |
| GeographicRegion              | string             | The geographic region.                                                                             |
| CountryCallingCodesList       | 文字列の配列   | The calling codes supported in the country/region.                                                 |
| 属性                    | ResourceAttributes | The metadata attributes corresponding to the CountryInformation resource.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Describes the address formatting rules for a country/region.

| プロパティ                | タスクバーの検索ボックスに               | 説明                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | string             | An ISO-2 code.                                                                                     |
| DefaultCulture          | string             | The default culture.                                                                               |
| IsStateRequired         | boolean            | Indicates whether a state/province is required or not.                                             |
| SupportedStatesList     | 文字列の配列   | If a state/province is required, returns the full list for that country/region.                    |
| SupportedLanguagesList  | 文字列の配列   | A list of supported languages.                                                                     |
| SupportedCulturesList   | 文字列の配列   | A list of supported cultures.                                                                      |
| IsPostalCodeRequired    | boolean            | Indicates whether a ZIP code or postal code is required or not.                                    |
| PostalCodeRegex         | string             | The regular expression that defines the ZIP/postal code .                                          |
| IsCityRequired          | boolean            | Indicates whether a city is required or not.                                                       |
| IsVatIdSupported        | boolean            | Indicates whether a VAT ID is required or not.                                                     |
| TaxIdFormat             | string             | The tax ID format.                                                                                 |
| TaxIdSample             | string             | The tax ID sample.                                                                                 |
| VatIdRegex              | string             | The tax ID regular expression.                                                                     |
| PhoneNumberRegex        | string             | The phone number regular expression.                                                               |
| IsTaxIdSupported        | boolean            | Indicates whether a tax ID is supported or not. Note that this is different than IsVatIdSupported. |
| IsTaxIdOptional         | boolean            | Indicates whether a tax ID is optional or not.                                                     |
| CountryCallingCodesList | 文字列の配列   | The calling codes supported in the country/region.                                                 |
| 属性              | ResourceAttributes | The metadata attributes corresponding to the CountryInformation resource.                          |