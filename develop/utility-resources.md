---
title: ユーティリティ リソース
description: パートナーセンター REST API には、SDK 全体で使用される汎用データモデルについて説明する多くのリソースが含まれています。
ms.assetid: C77219B9-FFDD-4779-AE15-5B15BA7BA863
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0451caae82ec29423ca8c40691d68c9eb2233cc8
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82119288"
---
# <a name="utility-resources"></a>ユーティリティ リソース

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーセンター REST API には、SDK 全体で使用される汎用データモデルについて説明する多くのリソースが含まれています。

## <a name="address"></a>Address

顧客またはパートナープロファイルに使用するアドレス。 さまざまな国/地域でサポートされている形式とプロパティの詳細については、「[市場別の住所書式規則の取得](get-market-specific-validation-data.md)」を参照してください。

| プロパティ     | Type   | 長さ (最小、最大) | 説明                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | string | (1, 200)          | 住所の 1 行目。                                                                   |
| AddressLine2 | string | (0, 200)          | 所在地の 2 行目。 このプロパティは省略可能です。                                       |
| City         | string | 該当なし               | 市区町村。                                                                                        |
| State        | string | (0, 2)            | 都道府県。                                                                                       |
| PostalCode   | string | 該当なし               | 郵便番号。                                                                     |
| Country      | string | (2, 2)            | ISO 国コード形式の国/地域。                                                   |
| リージョン       | string | 該当なし               | 地域。                                                                                      |
| FirstName    | string | (1, 50)           | 顧客の会社/組織の連絡先の名。                              |
| LastName     | string | (1, 50)           | 顧客の会社/組織の連絡先の姓。                               |
| PhoneNumber  | string | 該当なし               | 顧客の会社/組織の連絡先の電話番号。 このプロパティは省略可能です。 |

## <a name="contact"></a>Contact

特定の個人の連絡先情報の説明。

| プロパティ    | Type   | 説明                  |
|-------------|--------|------------------------------|
| FirstName   | string | 連絡先の名前。    |
| LastName    | string | 連絡先の姓。     |
| Email       | string | 連絡先のメール アドレス。 |
| PhoneNumber | string | 連絡先の電話番号。  |

## <a name="fieldfilter"></a>FieldFilter

検索結果に適用できるフィルターについて説明します。

| プロパティ | Type   | 説明                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 演算子 | string | フィルター演算子:\_"equals"、"not equals"、"より大きい\_"、"大\_なり\_or\_等しい"、"より小さい\_"、"\_\_\_次の値より小さい"、"または"\_、"で始まる"、"で始まる\_\_" はいません。 |

## <a name="fileinfo"></a>FileInfo

パートナーセンターにアップロードされた外部ファイルを表します。

| プロパティ                 | Type   | 説明                                   |
|--------------------------|--------|-----------------------------------------------|
| 解説                  | string | ファイルのアップロードに関連付けられているコメント。    |
| FileExtension            | string | ファイル拡張子。                           |
| FileNameWithoutExtension | string | 拡張子が含まれていないファイルの名前。 |
| FileSize                 | long   | ファイルのサイズ。                         |
| Id                       | string | ファイルをアップロードするための一意の ID。            |

## <a name="link"></a>Link

URI リンクと関連情報が含まれています。

| プロパティ | Type                   | 説明                        |
|----------|------------------------|------------------------------------|
| URI      | string                 | URI。                           |
| Method   | string                 | URI によって表されるメソッド。 |
| ヘッダー  | Keyvaluepair の配列 | リンクのヘッダー。          |

## <a name="passwordprofile"></a>PasswordProfile

特定のパスワードを指定し、そのパスワードを変更する必要がある場合はを示します。

>[!NOTE]
>21Vianet が運用するパートナーセンターではサポートされていません。

| プロパティ            | Type                          | 説明                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| パスワード            | [SecureString](#securestring) | パスワード。                                                          |
| ForceChangePassword | boolean                       | 次回ログイン時にパスワードを強制的に変更する必要があるかどうかを決定します。 |

## <a name="resourcelinks"></a>ResourceLinks

リソースのリンクの一覧が含まれています。

| プロパティ   | Type                                      | 説明                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| セルフ       | [リンク](#link)                             | 自己 URI。                                      |
| Next       | [リンク](#link)                             | 項目の次のページ。                            |
| Previous   | [リンク](#link)                             | 項目の前のページ。                        |
| 属性 | [ResourceAttributes](#resourceattributes) | ユーザーに対応するメタデータ属性。 |

## <a name="resourceattributes"></a>ResourceAttributes

リソースの属性メタデータを格納します。

| プロパティ   | Type   | 説明                                 |
|------------|--------|---------------------------------------------|
| ETag       | string | Etag。オブジェクトバージョンとも呼ばれます。 |
| ObjectType | string | 基本リソースのオブジェクトの型。    |

## <a name="securestring"></a>SecureString

パスワードなどのセキュリティで保護された情報を格納します。

| プロパティ | Type | 説明                       |
|----------|------|-----------------------------------|
| 長さ   | INT  | セキュリティで保護された文字列の長さ。 |

## <a name="validationcode"></a>ValidationCode

パートナーの政府機関向けコミュニティクラウド検証コードを表します。

| プロパティ         | Type         | 説明                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | パートナー id                                                       |
| OrganizationName | string       | 検証プロセス中に指定された組織名             |
| ValidationId     | INT          | 検証の一意の識別子                                       |
| MaxCreates       | null 許容の int | この検証コードを使用して作成できる最大顧客数    |
| RemainingCreates | null 許容の int | 残りの顧客はこの検証 ID で作成します                      |
| ETag             | string       | このリソースの特定のバージョン。 リソースが変更されると変更されます。 |
