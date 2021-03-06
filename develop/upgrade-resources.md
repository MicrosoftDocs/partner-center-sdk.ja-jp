---
title: リソースのアップグレード
description: ソースサブスクリプションからターゲットサブスクリプションへのユーザーのアップグレードに使用されるリソースについて説明します。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bdbef383370761a01eb462f90284ad826a38ddaa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096555"
---
# <a name="upgrade-resources"></a>リソースのアップグレード

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

ソースサブスクリプションからターゲットサブスクリプションへのユーザーのアップグレードに使用されるリソースについて説明します。

## <a name="upgrade"></a>アップグレード

個々のアップグレードリソースの動作について説明します。

| プロパティ      | Type                   | 説明                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | プラン                  | ターゲットサブスクリプションのプラン。                                                        |
| UpgradeType   | string                 | アップグレードの種類は、"なし"、"アップグレード \_ のみ"、または " \_ ライセンス転送によるアップグレード \_ \_ " です。         |
| IsEligible    | boolean                | アップグレードを実行できるかどうかを識別します。                                                  |
| Quantity      | integer                | 購入する新しいプランの定量化。 既定値は、ソースサブスクリプションの数量です。 |
| UpgradeErrors | UpgradeErrors の配列 | 必要に応じて、アップグレードを実行できない理由。                                      |
| 属性    | ResourceAttributes     | アップグレードに対応するメタデータ属性。                                        |

## <a name="upgradeerror"></a>UpgradeError

アップグレードを実行できない理由について説明します。

| プロパティ          | Type               | 説明                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| コード              | string             | 問題に関連付けられているエラーコードは、"その他"、"委任 \_ された管理者の \_ アクセス許可 \_ が無効"、"サブスクリプションの状態がアクティブではありません"、"サービスの種類が競合しています"、"サブスクリプションのアドオンが存在しません"、"サブスクリプション \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ に \_ \_ \_ \_ \_ アップグレード \_ パス \_ \_ \_ \_ \_ \_ がありません |
| Description       | 文字列             | エラーを説明するわかりやすいテキスト。                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | string             | エラーに関する追加情報。                                                                                                                                                                                                                                                                                                                                                         |
| 属性        | ResourceAttributes | エラーに対応するメタデータ属性。                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>UpgradeResult

サブスクリプションのアップグレードプロセスの結果について説明します。

| プロパティ             | Type                        | 説明                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | string                      | ソースサブスクリプションの識別子です。                                           |
| TargetSubscriptionID | string                      | ターゲットサブスクリプションの識別子です。                                           |
| UpgradeType          | string                      | アップグレードの種類は、"なし"、"アップグレード \_ のみ"、または " \_ ライセンス転送によるアップグレード \_ \_ " です。 |
| UpgradeErrors        | UpgradeErrors の配列      | 必要に応じて、アップグレードの実行中に attemption 中にエラーが発生しました。           |
| LicenseErrors        | UserLicenseErrrors の配列 | ユーザーライセンスを移行しようとしたときにエラーが発生しました (該当する場合)。          |
| 属性           | ResourceAttributes          | ライセンスに対応するメタデータ属性。                                |

## <a name="userlicenseerror"></a>UserLicenseError

失敗したユーザーライセンスの譲渡に起因するエラーについて説明します。

| プロパティ     | Type                   | 説明                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | string                 | ユーザーオブジェクトを識別する一意の。                                 |
| 名前         | string                 | ユーザーの名前です。                                                     |
| 電子メール        | string                 | ユーザーの電子メール。                                                    |
| エラー       | ServiceFaults の配列 | ユーザーライセンスの転送を実行しようとしたときにスローされた例外の一覧。 |
| 属性   | ResourceAttributes     | ライセンスに対応するメタデータ属性。                     |

