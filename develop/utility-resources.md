---
title: ユーティリティのリソース
description: パートナーセンター REST API には、SDK 全体で使用される汎用データモデルについて説明する多くのリソースが含まれています。
ms.assetid: C77219B9-FFDD-4779-AE15-5B15BA7BA863
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b19eb80c5be2cc07bd325681f9870a1af7fed481
ms.sourcegitcommit: 07153b06dae146418ca5213c7e6fe1c869ba164d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083079"
---
# <a name="utility-resources"></a>ユーティリティのリソース


**適用対象**

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーセンター REST API には、SDK 全体で使用される汎用データモデルについて説明する多くのリソースが含まれています。


## <a name="span-idaddressspan-idaddressaddress"></a><span id="address"/><span id="ADDRESS"/>アドレス

顧客またはパートナープロファイルに使用するアドレス。 さまざまな国/地域でサポートされている形式とプロパティの詳細については、「[市場別の住所書式規則の取得](get-market-specific-validation-data.md)」を参照してください。

| プロパティ     | 種類   | 長さ (最小、最大) | 説明                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | string | (1, 200)          | 所在地の 1 行目。                                                                   |
| AddressLine2 | string | (0, 200)          | 所在地の 2 行目。 このプロパティは省略可能です。                                       |
| 市         | string | なし               | 市区町村。                                                                                        |
| 状態        | string | (0, 2)            | 都道府県。                                                                                       |
| PostalCode   | string | なし               | 郵便番号。                                                                     |
| 国      | string | (2, 2)            | ISO 国コード形式の国/地域。                                                   |
| Region       | string | なし               | 地域。                                                                                      |
| FirstName    | string | (1, 50)           | 顧客の会社/組織の連絡先の名。                              |
| LastName     | string | (1, 50)           | 顧客の会社/組織の連絡先の姓。                               |
| PhoneNumber  | string | なし               | 顧客の会社/組織の連絡先の電話番号。 このプロパティは省略可能です。 |
 

## <a name="span-idcontactspan-idcontactspan-idcontactcontact"></a><span id="Contact"/><span id="contact"/><span id="CONTACT"/>連絡先

特定の個人の連絡先情報の説明。

| プロパティ    | 種類   | 説明                  |
|-------------|--------|------------------------------|
| FirstName   | string | 連絡先の名前。    |
| LastName    | string | 連絡先の姓。     |
| Email       | string | 連絡先の電子メール アドレス。 |
| PhoneNumber | string | 連絡先の電話番号。  |
 

## <a name="span-idfieldfilterspan-idfieldfilterspan-idfieldfilterfieldfilter"></a><span id="FieldFilter"/><span id="fieldfilter"/><span id="FIELDFILTER"/>FieldFilter

検索結果に適用できるフィルターについて説明します。

| プロパティ | 種類   | 説明                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 演算子 | string | フィルター演算子: "equals"、"not\_equals"、"より大きい\_より大きい"、"より大きい\_"、"\_または\_と等しい"、"より小さい"、"部分文字列"、"and"、"or"、"", "を使用して開始\_"、"ではなく\_"\_\_\_\_\_ |
 

## <a name="span-idfileinfospan-idfileinfospan-idfileinfofileinfo"></a><span id="FileInfo"/><span id="fileinfo"/><span id="FILEINFO"/>FileInfo

パートナーセンターにアップロードされた外部ファイルを表します。

| プロパティ                 | 種類   | 説明                                   |
|--------------------------|--------|-----------------------------------------------|
| コメント                  | string | ファイルのアップロードに関連付けられているコメント。    |
| FileExtension            | string | ファイル拡張子。                           |
| FileNameWithoutExtension | string | 拡張子が含まれていないファイルの名前。 |
| FileSize                 | long   | ファイルのサイズ。                         |
| Id                       | string | ファイルをアップロードするための一意の ID。            |
 

## <a name="span-idlinkspan-idlinkspan-idlinklink"></a><span id="Link"/><span id="link"/><span id="LINK"/>リンク

URI リンクと関連情報が含まれています。

| プロパティ | 種類                   | 説明                        |
|----------|------------------------|------------------------------------|
| URI      | string                 | URI。                           |
| メソッド   | string                 | URI によって表されるメソッド。 |
| ヘッダー  | Keyvaluepair の配列 | リンクのヘッダー。          |
 

## <a name="span-idpasswordprofilespan-idpasswordprofilespan-idpasswordprofilepasswordprofile"></a><span id="PasswordProfile"/><span id="passwordprofile"/><span id="PASSWORDPROFILE"/>PasswordProfile

特定のパスワードを指定し、そのパスワードを変更する必要がある場合はを示します。

>[!NOTE]
>21Vianet が運用するパートナーセンターではサポートされていません。

| プロパティ            | 種類                          | 説明                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Password            | [SecureString](#securestring) | パスワード。                                                          |
| ForceChangePassword | boolean                       | 次回ログイン時にパスワードを強制的に変更する必要があるかどうかを決定します。 |
 

## <a name="span-idresourcelinksspan-idresourcelinksspan-idresourcelinksresourcelinks"></a><span id="ResourceLinks"/><span id="resourcelinks"/><span id="RESOURCELINKS"/>ResourceLinks

リソースのリンクの一覧が含まれています。

| プロパティ   | 種類                                      | 説明                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self (自己)       | [Link](#link)                             | 自己 URI。                                      |
| 次へ       | [Link](#link)                             | 項目の次のページ。                            |
| 前へ   | [Link](#link)                             | 項目の前のページ。                        |
| 属性 | [ResourceAttributes](#resourceattributes) | ユーザーに対応するメタデータ属性。 |
 

## <a name="span-idresourceattributesspan-idresourceattributesspan-idresourceattributesresourceattributes"></a><span id="ResourceAttributes"/><span id="resourceattributes"/><span id="RESOURCEATTRIBUTES"/>ResourceAttributes

リソースの属性メタデータを格納します。

| プロパティ   | 種類   | 説明                                 |
|------------|--------|---------------------------------------------|
| Etag       | string | Etag。オブジェクトバージョンとも呼ばれます。 |
| ObjectType | string | 基本リソースのオブジェクトの型。    |
 

## <a name="span-idsecurestringspan-idsecurestringspan-idsecurestringsecurestring"></a><span id="SecureString"/><span id="securestring"/><span id="SECURESTRING"/>SecureString

パスワードなどのセキュリティで保護された情報を格納します。

| プロパティ | 種類 | 説明                       |
|----------|------|-----------------------------------|
| 長さ   | int  | セキュリティで保護された文字列の長さ。 |


## <a name="span-idvalidationcodespan-idvalidationcodespan-idvalidationcodevalidationcode"></a>ValidationCode <span id="VALIDATIONCODE"/><span id="validationcode"/><span id="ValidationCode"/>

パートナーの政府機関向けコミュニティクラウド検証コードを表します。

| プロパティ         | 種類         | 説明                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | パートナー id                                                       |
| OrganizationName | string       | 検証プロセス中に指定された組織名             |
| ValidationId     | int          | 検証の一意の識別子                                       |
| MaxCreates       | null 許容の int | この検証コードを使用して作成できる最大顧客数    |
| RemainingCreates | null 許容の int | 残りの顧客はこの検証 ID で作成します                      |
| ETag             | string       | このリソースの特定のバージョン。 リソースが変更されると変更されます。 |
