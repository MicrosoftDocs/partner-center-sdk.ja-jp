---
title: ユーザーリソース
description: 個々のパートナーセンターのユーザー、個人とアカウントの情報、およびパートナーセンター内のアクセス許可について説明します。
ms.assetid: A2DEDDAB-C4DA-4ECA-931F-2054AB005973
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: bf338ea4eea57ff1164a72c95e86868c9320b970
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82119808"
---
# <a name="user-resources"></a>ユーザーリソース

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

個々のパートナーセンターのユーザー、個人とアカウントの情報、およびパートナーセンター内のアクセス許可について説明します。

## <a name="user"></a>User

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
| attributes            | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                                                                                                                                                                                   |

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
| attributes            | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                                                                                                                                                                                   |

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
| attributes        | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。           |

