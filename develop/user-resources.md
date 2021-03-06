---
title: ユーザーリソース
description: 個々のパートナーセンターのユーザー、個人とアカウントの情報、およびパートナーセンター内のアクセス許可について説明します。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c88b9b65dfb925712ff85fb42d34251cca6e0b5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093540"
---
# <a name="user-resources"></a>ユーザーリソース

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

個々のパートナーセンターのユーザー、個人とアカウントの情報、およびパートナーセンター内のアクセス許可について説明します。

## <a name="user"></a>ユーザー

個々のユーザーについて説明します。

| プロパティ              | Type                                                           | 説明                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | string                                                         | ユーザー識別子。                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | ユーザープリンシパル識別子。                                                                                                                                                                                             |
| firstName             | string                                                         | ユーザーの名。                                                                                                                                                                                                |
| lastName              | string                                                         | ユーザーの姓。                                                                                                                                                                                                 |
| displayName           | string                                                         | 表示されるユーザーの名前。                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | ユーザーのパスワードプロファイル。                                                                                                                                                                                               |
| phoneNumber           | string                                                         | ユーザーの電話番号。                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC 日時形式の文字列                                 | このユーザーの情報が Azure Active Directory とオンプレミス Active Directory の間で同期された最後の時刻。 日付と時刻の値は Azure AD Connect 同期が有効になっている場合にのみ表示されます。 それ以外の場合、値は null になります。 |
| userDomainType        | string                                                         | ユーザードメインの種類: "none"、"managed"、または "フェデレーション"。                                                                                                                                                                   |
| state                 | string                                                         | ユーザーの状態: "アクティブ"、"非アクティブ" (削除されたユーザーの場合)。                                                                                                                                                          |
| softDeletionTime      | UTC 日時形式の文字列                                 | 削除されたユーザーに関連付けられたデータが完全に削除され、回復できなくなる30日間の期間の開始を表します。                                                                          |
| リンク                 | [ResourceLinks](utility-resources.md#resourcelinks)           | リソースリンク。                                                                                                                                                                                                        |
| 属性            | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

顧客ユーザーを説明します。

| プロパティ              | Type                                                           | 説明                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | string                                                         | ユーザーがライセンスを使用する場所。                                                                                                                                                                    |
| id                    | string                                                         | ユーザー識別子。                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | ユーザープリンシパル識別子。                                                                                                                                                                                             |
| firstName             | string                                                         | ユーザーの名。                                                                                                                                                                                                |
| lastName              | string                                                         | ユーザーの姓。                                                                                                                                                                                                 |
| displayName           | string                                                         | 表示されるユーザーの名前。                                                                                                                                                                                            |
| immutableId           | string                                                         | ユーザーの不変 id。                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | ユーザーのパスワードプロファイル。                                                                                                                                                                                               |
| phoneNumber           | string                                                         | ユーザーの電話番号。                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC 日時形式の文字列                                 | このユーザーの情報が Azure Active Directory とオンプレミス Active Directory の間で同期された最後の時刻。 日付と時刻の値は Azure AD Connect 同期が有効になっている場合にのみ表示されます。 それ以外の場合、値は null になります。 |
| userDomainType        | string                                                         | ユーザードメインの種類: "none"、"managed"、または "フェデレーション"。                                                                                                                                                                   |
| state                 | string                                                         | ユーザーの状態: "アクティブ"、"非アクティブ" (削除されたユーザーの場合)。                                                                                                                                                          |
| softDeletionTime      | UTC 日時形式の文字列                                 | 削除されたユーザーに関連付けられたデータが完全に削除され、回復できなくなる30日間の期間の開始を表します。                                                                          |
| リンク                 | [ResourceLinks](utility-resources.md#resourcelinks)           | リソースリンク。                                                                                                                                                                                                        |
| 属性            | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                                                                                                                                                                                   |

## <a name="usercredentials"></a>ユーザー

ユーザーのログイン資格情報を記述します。

| プロパティ | Type                                               | 説明                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | string                                             | ユーザーの名前です。                |
| password | [SecureString](utility-resources.md#securestring) | ユーザーの安全に保存されたパスワード。 |

## <a name="usermember"></a>UserMember

ユーザーのメンバー情報を記述します。

| プロパティ          | Type                                                           | 説明                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | string                                                         | ユーザーの表示名。   |
| userPrincipalName | string                                                         | ユーザー プリンシパル名。    |
| roleId            | string                                                         | ユーザーのロールの識別子。 |
| id                | string                                                         | メンバーの識別子。      |
| 属性        | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。           |

