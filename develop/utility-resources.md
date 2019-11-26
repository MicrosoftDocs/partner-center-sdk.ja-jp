---
title: Utility resources
description: The Partner Center REST API contains many resources which describe general-purpose data models used throughout the SDK.
ms.assetid: C77219B9-FFDD-4779-AE15-5B15BA7BA863
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b19eb80c5be2cc07bd325681f9870a1af7fed481
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486252"
---
# <a name="utility-resources"></a>Utility resources


**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

The Partner Center REST API contains many resources which describe general-purpose data models used throughout the SDK.


## <a name="span-idaddressspan-idaddressaddress"></a><span id="address"/><span id="ADDRESS"/>Address

An address to use for the customer or for partner profiles. For more information about the supported formats and properties in different countries/regions, see [Get address formatting rules by market](get-market-specific-validation-data.md).

| プロパティ     | タスクバーの検索ボックスに   | Length (min, max) | 説明                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | string | (1, 200)          | The first line of the address.                                                                   |
| AddressLine2 | string | (0, 200)          | The second line of the address. このプロパティは省略可能です。                                       |
| 市区町村         | string | なし               | The city.                                                                                        |
| 都道府県        | string | (0, 2)            | The state.                                                                                       |
| PostalCode   | string | なし               | The ZIP code or postal code.                                                                     |
| Country      | string | (2, 2)            | The country/region in ISO country code format.                                                   |
| Region       | string | なし               | The region.                                                                                      |
| FirstName    | string | (1, 50)           | The first name of a contact at the customer's company/organization.                              |
| LastName     | string | (1, 50)           | The last name of a contact at the customer's company/organization.                               |
| PhoneNumber  | string | なし               | The phone number of a contact at the customer's company/organization. このプロパティは省略可能です。 |
 

## <a name="span-idcontactspan-idcontactspan-idcontactcontact"></a><span id="Contact"/><span id="contact"/><span id="CONTACT"/>Contact

Describes contact information for a specific individual.

| プロパティ    | タスクバーの検索ボックスに   | 説明                  |
|-------------|--------|------------------------------|
| FirstName   | string | The contact's first name.    |
| LastName    | string | The contact's last name.     |
| [メール]       | string | The contact's email address. |
| PhoneNumber | string | The contact's phone number.  |
 

## <a name="span-idfieldfilterspan-idfieldfilterspan-idfieldfilterfieldfilter"></a><span id="FieldFilter"/><span id="fieldfilter"/><span id="FIELDFILTER"/>FieldFilter

Describes a filter that can be applied to search results.

| プロパティ | タスクバーの検索ボックスに   | 説明                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 演算子 | string | The filter operator: "equals", "not\_equals", "greater\_than", "greater\_than\_or\_equals", "less\_than", "less\_than\_or\_equals", "substring", "and", "or", "starts\_with", "not\_starts\_with". |
 

## <a name="span-idfileinfospan-idfileinfospan-idfileinfofileinfo"></a><span id="FileInfo"/><span id="fileinfo"/><span id="FILEINFO"/>FileInfo

Represents an external file uploaded to Partner Center.

| プロパティ                 | タスクバーの検索ボックスに   | 説明                                   |
|--------------------------|--------|-----------------------------------------------|
| Comment                  | string | A comment associated with the file upload.    |
| FileExtension            | string | The file extension.                           |
| FileNameWithoutExtension | string | The name of the file, extension not included. |
| FileSize                 | long   | The size of the file.                         |
| Id                       | string | The unique ID for the file upload.            |
 

## <a name="span-idlinkspan-idlinkspan-idlinklink"></a><span id="Link"/><span id="link"/><span id="LINK"/>Link

Contains a URI link and associated information.

| プロパティ | タスクバーの検索ボックスに                   | 説明                        |
|----------|------------------------|------------------------------------|
| URI      | string                 | The URI.                           |
| メソッド   | string                 | The method represented by the URI. |
| ヘッダー  | Array of KeyValuePairs | The headers for the link.          |
 

## <a name="span-idpasswordprofilespan-idpasswordprofilespan-idpasswordprofilepasswordprofile"></a><span id="PasswordProfile"/><span id="passwordprofile"/><span id="PASSWORDPROFILE"/>PasswordProfile

Describes a specific password and if that password needs to be changed.

>[!NOTE]
>Unsupported on Partner Center operated by 21Vianet.

| プロパティ            | タスクバーの検索ボックスに                          | 説明                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| パスワード            | [SecureString](#securestring) | The password.                                                          |
| ForceChangePassword | boolean                       | Determines if the password needs to be forcibly changed on next login. |
 

## <a name="span-idresourcelinksspan-idresourcelinksspan-idresourcelinksresourcelinks"></a><span id="ResourceLinks"/><span id="resourcelinks"/><span id="RESOURCELINKS"/>ResourceLinks

Contains a list of links for a resource.

| プロパティ   | タスクバーの検索ボックスに                                      | 説明                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self (自己)       | [Link](#link)                             | The self URI.                                      |
| [次へ]       | [Link](#link)                             | The next page of items.                            |
| Previous   | [Link](#link)                             | The previous page of items.                        |
| 属性 | [ResourceAttributes](#resourceattributes) | The metadata attributes corresponding to the user. |
 

## <a name="span-idresourceattributesspan-idresourceattributesspan-idresourceattributesresourceattributes"></a><span id="ResourceAttributes"/><span id="resourceattributes"/><span id="RESOURCEATTRIBUTES"/>ResourceAttributes

Contains attribute metadata for a resource.

| プロパティ   | タスクバーの検索ボックスに   | 説明                                 |
|------------|--------|---------------------------------------------|
| Etag       | string | The etag, also known as the object version. |
| ObjectType | string | The type of object of the base resource.    |
 

## <a name="span-idsecurestringspan-idsecurestringspan-idsecurestringsecurestring"></a><span id="SecureString"/><span id="securestring"/><span id="SECURESTRING"/>SecureString

Stores secured information, such as a password.

| プロパティ | タスクバーの検索ボックスに | 説明                       |
|----------|------|-----------------------------------|
| 長さ   | 整数  | The length of the secured string. |


## <a name="span-idvalidationcodespan-idvalidationcodespan-idvalidationcodevalidationcode"></a><span id="ValidationCode"/><span id="validationcode"/><span id="VALIDATIONCODE"/>ValidationCode

Represents a partner's Government Community Cloud validation code.

| プロパティ         | タスクバーの検索ボックスに         | 説明                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | Partner identifier                                                       |
| OrganizationName | string       | The organization name provided during the validation process             |
| ValidationId     | 整数          | A unique identifier for validation                                       |
| MaxCreates       | nullable int | The maximum customers allowed to be created with this validation code    |
| RemainingCreates | nullable int | Remaining customer creates under this validation ID                      |
| ETag             | string       | The specific version of this resource. Changes when resource is changed. |
